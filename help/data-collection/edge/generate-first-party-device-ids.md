---
title: 產生第一方裝置識別碼
description: 學習如何產生第一方裝置識別碼
feature: Web SDK
kt: 9728
thumbnail: KT-9728.jpeg
exl-id: 2e3c1f71-e224-4631-b680-a05ecd4c01e7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 2%

---

# 產生第一方裝置識別碼

Adobe Experience Cloud應用程式傳統上會產生cookie，以使用不同技術儲存裝置id，包括：

1. 第三方 Cookie
1. Adobe伺服器使用網域名稱的CNAME設定所設定的第一方Cookie
1. 由JavaScript設定的第一方Cookie

最近的瀏覽器變更會限制這些類型Cookie的持續時間。 使用客戶擁有的伺服器設定第一方Cookie時，第一方Cookie最有效，此伺服器使用DNS A/AAAA記錄，而非DNS CNAME。 第一方裝置ID(FPID)功能可讓實作Adobe Experience Platform Web SDK的客戶使用DNS A/AAAA記錄之伺服器之Cookie中的裝置ID。 接著，這些ID可傳送至Adobe，並作為種子來產生Experience CloudID(ECID)，而ECID仍是Adobe Experience Cloud應用程式中的主要識別碼。

以下是功能運作方式的快速範例：

![第一方裝置ID(FPID)和Experience CloudID(ECID)](../assets/kt-9728.png)

1. 一般使用者的瀏覽器會向客戶的網頁伺服器或CDN要求網頁。
1. 客戶在其Web伺服器或CDN上產生裝置ID(FPID)（Web伺服器應系結至網域名稱的DNS A/AAAA記錄）。
1. 客戶設定第一方Cookie，將FPID儲存在使用者的瀏覽器中。
1. 客戶的Adobe Experience Platform Web SDK實作會向Platform Edge Network提出要求，包括身分對應中的FPID。
1. Experience Platform邊緣網路接收FPID，並使用它產生Experience CloudID(ECID)。
1. Platform Web SDK回應會將ECID傳回使用者的瀏覽器。
1. Platform Web SDK使用JavaScript將ECID儲存為 `AMCV_` cookie。
1. 若 `AMCV_` cookie過期時，程式會重複。 只要有相同的第一方裝置ID可用，就會有新的 `AMCV_` Cookie的ECID值與之前相同。

在本教程中，使用PHP指令碼語言的特定示例用於說明如何：

* 產生UUIDv4
* 將UUIDv4值寫入Cookie
* 在身分對應中加入Cookie值
* 驗證ECID產生

如需與第一方裝置ID相關的進一步檔案，請參閱產品檔案。

## 產生UUIDv4

PHP沒有用於產生UUID的原生程式庫，因此這些程式碼範例比使用其他程式設計語言時可能需要的更廣泛。 此示例選擇了PHP，因為它是受廣泛支援的伺服器端語言。


呼叫下列函式時，會產生隨機的UUID第4版：

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

下列程式碼會向上述函式提出要求，以產生UUID。 接著會設定貴組織決定的Cookie旗標。 如果已產生Cookie，則有效期會延長。

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
>包含第一方裝置ID的Cookie可以有任何名稱。

## 在身分對應中加入Cookie值

最後一步是使用PHP將Cookie值回顯至「身分對應」。


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
>必須呼叫身分對應中使用的身分命名空間符號 `FPID`.
>
> `FPID` 是保留的身分識別命名空間，不會顯示在身分識別命名空間的介面清單中。


## 驗證ECID產生

確認從第一方裝置ID產生的ECID相同，以驗證實作：

1. 產生FPID Cookie。
1. 使用Platform Web SDK傳送要求至Platform Edge Network。
1. 格式的Cookie `AMCV_<IMSORGID@AdobeOrg>` 的URL。 此Cookie包含ECID。
1. 記下產生的Cookie值，然後刪除您網站的所有Cookie, `FPID` cookie。
1. 傳送另一個要求至Platform Edge Network。
1. 確認 `AMCV_<IMSORGID@AdobeOrg>` cookie相同 `ECID` 值，如 `AMCV_` 已刪除的cookie。 如果指定FPID的Cookie值相同，ECID的種子設定程式會成功。

如需此功能的詳細資訊，請參閱 [檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html).
