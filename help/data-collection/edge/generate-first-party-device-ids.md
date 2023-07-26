---
title: 產生第一方裝置識別碼
description: 學習如何產生第一方裝置識別碼
feature: Web SDK
level: Experienced
jira: KT-9728
thumbnail: KT-9728.jpeg
exl-id: 2e3c1f71-e224-4631-b680-a05ecd4c01e7
source-git-commit: ac07d62cf4bfb6a9a8b383bbfae093304d008b5f
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 2%

---

# 產生第一方裝置識別碼

Adobe Experience Cloud應用程式傳統上會使用不同技術產生Cookie以儲存裝置id，包括：

1. 第三方 Cookie
1. Adobe伺服器使用網域名稱的CNAME設定所設定的第一方Cookie
1. JavaScript設定的第一方Cookie

近期的瀏覽器變更會限制這些型別Cookie的持續時間。 第一方Cookie在使用客戶擁有的伺服器（使用DNS A/AAAA記錄，而不是DNS CNAME）設定時最有效。 第一方裝置ID (FPID)功能允許實作Adobe Experience Platform Web SDK的客戶從使用DNS A/AAAA記錄的伺服器使用Cookie中的裝置ID。 接著，這些ID可以傳送至Adobe，並當作種子來產生Experience CloudID (ECID)，這仍是Adobe Experience Cloud應用程式中的主要識別碼。

以下是功能運作方式的快速範例：

![第一方裝置ID (FPID)和Experience CloudID (ECID)](../assets/kt-9728.png)

1. 一般使用者的瀏覽器會從客戶的網頁伺服器或CDN要求網頁。
1. 客戶在其網頁伺服器或CDN上產生裝置ID (FPID) （網頁伺服器應繫結至網域名稱的DNS A/AAAA-record）。
1. 客戶設定第一方Cookie，以將FPID儲存在使用者的瀏覽器中。
1. 客戶的Adobe Experience Platform Web SDK實作會向Platform Edge Network提出要求，包括身分對應中的FPID。
1. Experience Platform Edge Network會接收FPID，並使用它來產生Experience CloudID (ECID)。
1. Platform Web SDK回應會將ECID傳送回使用者的瀏覽器。
1. 如果 `idMigrationEnabled=true`，Platform Web SDK會使用JavaScript將ECID儲存為 `AMCV_` 一般使用者瀏覽器中的Cookie。
1. 如果事件中 `AMCV_` Cookie過期，程式會重複本身。 只要相同的第一方裝置ID可用，就會新增一個 `AMCV_` Cookie會以與之前相同的ECID值建立。

>[!NOTE]
>
>此 `idMigrationEnabled` 不需要設定為 `true` 以使用FPID。 替換為 `idMigrationEnabled=false` 您可能看不到 `AMCV_` 然而，和Cookie必須在網路回應中尋找ECID值。


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
>必須呼叫身分對應中使用的身分名稱空間符號 `FPID`.
>
> `FPID` 是保留的身分名稱空間，不會顯示在身分名稱空間的介面清單中。


## 驗證ECID產生

確認會從您的第一方裝置ID產生相同的ECID，以驗證實施：

1. 產生FPID Cookie。
1. 使用Platform Web SDK傳送要求給Platform Edge Network。
1. 格式為的Cookie `AMCV_<IMSORGID@AdobeOrg>` 「 」已產生。 此Cookie包含ECID。
1. 記下產生的Cookie值，然後刪除網站的所有Cookie，但 `FPID` Cookie。
1. 傳送另一個要求給Platform Edge Network。
1. 確認中的值 `AMCV_<IMSORGID@AdobeOrg>` Cookie相同 `ECID` 值，如下所示 `AMCV_` 已刪除的Cookie。 如果指定FPID的Cookie值相同，表示ECID的植入程式成功。

如需有關此功能的詳細資訊，請參閱 [說明檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html).
