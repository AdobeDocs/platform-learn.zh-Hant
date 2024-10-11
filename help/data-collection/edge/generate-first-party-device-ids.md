---
title: 產生第一方裝置識別碼
description: 學習如何產生第一方裝置識別碼
feature: Web SDK
level: Experienced
jira: KT-9728
thumbnail: KT-9728.jpeg
exl-id: 2e3c1f71-e224-4631-b680-a05ecd4c01e7
source-git-commit: fd60f7ad338c81f5b32e7951d5a00b49c5aa1756
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# 產生第一方裝置識別碼

Adobe Experience Cloud應用程式傳統上會使用不同技術產生Cookie以儲存裝置id，包括：

1. 第三方Cookie
1. Adobe伺服器使用網域名稱的CNAME設定所設定的第一方Cookie
1. JavaScript設定的第一方Cookie

近期的瀏覽器變更會限制這些型別Cookie的持續時間。 第一方Cookie在使用客戶擁有的伺服器（使用DNS A/AAAA記錄，而不是DNS CNAME）設定時最有效。 [第一方裝置識別碼(FPID)功能](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/identity/first-party-device-ids)可讓實作Adobe Experience Platform Web SDK的客戶使用DNS A/AAAA記錄的伺服器，在Cookie中使用裝置ID。 接著，這些ID可以傳送至Adobe，並當作種子來產生Experience CloudID (ECID)，這仍是Adobe Experience Cloud應用程式中的主要識別碼。

以下是功能運作方式的快速範例：

![第一方裝置識別碼(FPID)和Experience Cloud識別碼(ECID)](../assets/kt-9728.png)

1. 一般使用者的瀏覽器會從客戶的網頁伺服器或CDN要求網頁。
1. 客戶在其網頁伺服器或CDN上產生裝置ID (FPID) （網頁伺服器應繫結至網域名稱的DNS A/AAAA-record）。
1. 客戶設定第一方Cookie，以將FPID儲存在使用者的瀏覽器中。
1. 客戶的Adobe Experience Platform Web SDK實作會向PlatformEdge Network提出要求，且：
   1. 包含身分對應中的FPID。
   1. 為其Web SDK請求設定CNAME，並使用其FPID Cookie名稱設定其資料流。
1. Experience PlatformEdge Network會接收FPID，並使用它來產生Experience CloudID (ECID)。
1. Platform Web SDK回應會將ECID傳送回使用者的瀏覽器。
1. 如果`idMigrationEnabled=true`，Platform Web SDK會使用JavaScript將ECID儲存為一般使用者瀏覽器中的`AMCV_` Cookie。
1. 如果`AMCV_` Cookie過期，程式會自我重複。 只要有相同的第一方裝置識別碼可用，就會使用與之前相同的ECID值建立新的`AMCV_` Cookie。

>[!NOTE]
>
>`idMigrationEnabled`不需要設定為`true`即可使用FPID。 但使用`idMigrationEnabled=false`時，您可能無法看到`AMCV_` Cookie，而且必須在網路回應中尋找ECID值。


在本教學課程中，會使用使用PHP指令碼語言的特定範例來說明如何：

* 產生UUIDv4
* 將UUIDv4值寫入Cookie
* 在身分對應中包含Cookie值
* 驗證ECID產生

有關第一方裝置ID的其他檔案可在產品檔案中找到。

## 產生UUIDv4

PHP沒有用於產生UUID的原生程式庫，因此這些程式碼範例比使用其他程式語言時可能需要的範例更廣泛。 PHP之所以被選作這個範例，是因為它是一種廣泛支援的伺服器端語言。


呼叫下列函式時，會產生隨機UUID版本4：

```
<?php
    
    function guidv4($data)
    {
        $data = $data ?? random_bytes(16);

        $data[6] = chr(ord($data[6]) & 0x0f | 0x40); // set version to 0100
        $data[8] = chr(ord($data[8]) & 0x3f | 0x80); // set bits 6-7 to 10

        return vsprintf('%s%s-%s-%s-%s-%s%s%s', str_split(bin2hex($data), 4));
    }

?>
```

## 將UUIDv4值寫入Cookie

下列程式碼會向上述函式提出要求，以產生UUID。 接著，系統會設定貴組織所決定的Cookie標幟。 如果已經產生Cookie，則會延長有效期。

```
<?php

    if(!isset($_COOKIE['FPID'])) {
        $cookie_value = guidv4(openssl_random_pseudo_bytes(16));        
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
        $_COOKIE[$cookie_name] = $cookie_value;
    }
    else {
        $cookie_value = $_COOKIE[$cookie_name];
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
    }

?>
```

>[!NOTE]
>
>包含第一方裝置識別碼的Cookie可以有任何名稱。

## 在身分對應中包含Cookie值

最後一個步驟是使用PHP將Cookie值回應至「身分對應」。


```
{
    "identityMap": {
        "FPID": [
                    {
                        "id": "<? echo $_COOKIE[$cookie_name] ?>",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
        }
}
```

>[!IMPORTANT]
>
>識別對應中使用的識別名稱空間符號，必須稱為`FPID`。
>
> `FPID`是保留的身分名稱空間，在身分名稱空間的介面清單中看不到。


## 驗證ECID產生

確認會從您的第一方裝置ID產生相同的ECID，以驗證實施：

1. 產生FPID Cookie。
1. 使用Platform Web SDK傳送要求給PlatformEdge Network。
1. 已產生格式為`AMCV_<IMSORGID@AdobeOrg>`的Cookie。 此Cookie包含ECID。
1. 將產生的Cookie值記入筆記，然後刪除您網站的所有Cookie （`FPID` Cookie除外）。
1. 傳送另一個要求給PlatformEdge Network。
1. 確認`AMCV_<IMSORGID@AdobeOrg>` Cookie中的值與已刪除的`AMCV_` Cookie中的值相同`ECID`。 如果指定FPID的Cookie值相同，表示ECID的植入程式成功。

如需有關此功能的詳細資訊，請參閱[檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html)。
