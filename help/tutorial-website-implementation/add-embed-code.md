---
title: 新增內嵌程式碼
description: 了解如何取得標籤屬性的內嵌程式碼，並在您的網站中實作。 本課程屬於「在網站中實作Experience Cloud」教學課程的一部分。
exl-id: a2959553-2d6a-4c94-a7df-f62b720fd230
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 46%

---

# 新增內嵌程式碼

在本課程中，您將實施標籤屬性之開發環境的非同步內嵌程式碼。 在過程中，您將了解標籤的兩個主要概念：環境和內嵌程式碼。

>[!NOTE]
>
>Adobe Experience Platform Launch已整合至Adobe Experience Platform，為資料收集技術的套件。 介面中已推出數個術語變更，在使用此內容時應注意：
>
> * platform launch（用戶端）現在為 **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)**
> * platform launch伺服器端現在是 **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * 現在提供邊緣設定 **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**


## 學習目標

在本課程結束時，您將能夠：

* 取得標籤屬性的內嵌程式碼
* 瞭解開發、測試和生產環境之間的差異
* 將標籤內嵌程式碼新增至html檔案
* 說明標籤內嵌程式碼相對於 `<head>` html文檔

## 複製內嵌程式碼

內嵌程式碼是 `<script>` 標籤，以載入並執行您在標籤中建置的邏輯。 如果您非同步載入程式庫，瀏覽器會繼續載入頁面、擷取標籤程式庫，並同時執行。 在這種情況下，只會有一個內嵌程式碼，您會將其放在 `<head>` 中。(同步部署標籤時，會有兩個內嵌程式碼，您會將一個放在 `<head>` 還有你放在前面的 `</body>`)。

在屬性概述畫面中，按一下 **[!UICONTROL 環境]** 在左側導覽中前往環境頁面。 請注意，系統已為您預先建立開發、測試和生產環境。

![按一下頂端導覽列中的「環境」](images/launch-environments.png)

開發、測試和生產環境對應至程式碼開發和發佈程序中的典型環境。程式碼是先由開發人員在開發環境中撰寫。當開發人員完成其工作時，就會將其傳送至測試環境，讓 QA 和其他團隊進行審查。QA 和其他團隊完成確認之後，就會將程式碼發佈到生產環境，這是訪客來到您的網站時所體驗的公開環境。

標籤可允許使用其他開發環境，這在有多位開發人員同時處理不同專案的大型組織中很有用。

完成本教學課程只需用到這些環境。環境可讓您擁有托管於不同URL的不同標籤程式庫有效版本，這樣您就能安全地新增功能，並提供給適當的使用者使用（例如開發人員、QA工程師、大眾等） 。

現在來複製內嵌程式碼：

1. 在&#x200B;**[!UICONTROL 開發]**&#x200B;列中，按一下「安裝」圖示 ![「安裝」圖示](images/launch-installIcon.png)，開啟強制回應視窗.

1. 請注意，標籤會預設為非同步內嵌程式碼

1. 按一下「複製」圖示 ![「複製」圖示](images/launch-copyIcon.png)，將內嵌程式碼複製到剪貼簿。

1. 按一下&#x200B;**[!UICONTROL 關閉]**&#x200B;以關閉強制回應視窗.

   ![「安裝」圖示](images/launch-copyInstallCode.png)

## 在範例 HTML 頁面的 `<head>` 中實施內嵌程式碼

內嵌程式碼應在將共用屬性之所有 HTML 頁面的 `<head>` 元素中實施。您可能有一或多個範本檔案可控制 `<head>` 全域，讓新增標籤的程式相當簡單明瞭。

如果尚未下載，請下載 [範例html頁面](https://www.enablementadobe.com/multi/web/basic-sample.html) （以滑鼠右鍵按一下此連結，然後按一下「另存連結」），然後在程式碼編輯器中開啟它。 如果您需要編輯器，可使用免費的開放原始碼編輯器 [Brackets](https://brackets.io/)。

將第 34 行或其附近的現有內嵌程式碼取代為您剪貼簿上的內容，然後儲存頁面。現在，請在網頁瀏覽器中開啟該頁面。如果您使用 `file://` 通訊協定載入頁面，必須在程式碼編輯器中的內嵌程式碼 URL 開頭新增「https:」。範例頁面的第 33 到 36 行看起來可能像這樣：

```html
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="https://assets.adobedtm.com/launch-ENa21cfed3f06f4ddf9690de8077b39e81-development.min.js" async></script>
    <!--/Tags Header Embed Code-->
```

開啟網頁瀏覽器的開發人員工具，然後前往「網路」標籤。此時，標籤環境URL應該會出現404錯誤：
![404錯誤](images/samplepage-404.png)

404錯誤是預期會出現的情況，因為您尚未在此標籤環境中建立程式庫。 您會在下一個課程中執行該操作。如果您看到「失敗」訊息 (而不是 404 錯誤)，表示您可能忘了將 `https://` 通訊協定加入內嵌程式碼中。同樣地，如果您使用 `file://` 通訊協定載入範例頁面，則只需指定 `https://` 通訊協定即可。進行該變更並重新載入頁面，直到 404 錯誤出現為止。

## 標籤實作最佳作法

讓我們花點時間檢閱範例頁面中示範的某些標籤實施最佳實務：

* **資料層**：

   * 我們 *強烈* 建議您在網站上建立資料層，包含在Analytics、Target和其他行銷解決方案中填入變數所需的所有屬性。 此範例頁面只包含非常簡單的資料層，但實際資料層可能包含有關頁面的更多詳細資料、訪客、其購物車詳細資料等內容。如需資料層的詳細資訊，請參閱[客戶體驗數位資料層 1.0](https://www.w3.org/2013/12/ceddl-201312.pdf)

   * 在標籤內嵌程式碼之前定義資料層，以發揮Experience Cloud解決方案的最大效用。

* **JavaScript協助程式程式庫**:如果您已在中實作JQuery等程式庫， `<head>` ，請在標籤之前載入，以便在標籤和Target中運用其語法

* **HTML5 doctype**：HTML5 doctype 在 Target 實施中是必要的

* **preconnect 和 dns-prefetch**: 使用 preconnect 和 dns-prefetch 來改善頁面載入時間。另請參閱：[https://w3c.github.io/resource-hints/](https://w3c.github.io/resource-hints/)

* **非同步Target實作的預先隱藏程式碼片段**:您會在Target課程中深入了解，但透過非同步標籤內嵌程式碼部署Target時，您應在頁面上的標籤內嵌程式碼之前，以硬式編碼撰寫預先隱藏的程式碼片段，以管理內容忽隱忽現的情形

以下依建議順序呈現這些最佳做法的摘要。請注意，帳戶專屬詳細資訊有一些預留位置：

```html
<!doctype html>
<html lang="en">
<head>
    <title>Basic Demo</title>
    <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
    <link rel="preconnect" href="//dpm.demdex.net">
    <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//cm.everesttech.net">
    <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
    <link rel="dns-prefetch" href="//dpm.demdex.net">
    <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//cm.everesttech.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
    <!--/Preconnect and DNS-Prefetch-->
    <!--Data Layer to enable rich data collection and targeting-->
    <script>
    var digitalData = {
        "page": {
            "pageInfo" : {
                "pageName": "Home"
                }
            }
    };
    </script>
    <!--/Data Layer-->
    <!--jQuery or other helper libraries-->
    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    <!--/jQuery-->
    <!--prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <script>
        (function(g,b,d,f){(function(a,c,d){if(a){var e=b.createElement("style");e.id=c;e.innerHTML=d;a.appendChild(e)}})(b.getElementsByTagName("head")[0],"at-body-style",d);setTimeout(function(){var a=b.getElementsByTagName("head")[0];if(a){var c=b.getElementById("at-body-style");c&&a.removeChild(c)}},f)})(window,document,"body {opacity: 0 !important}",3E3);
    </script>
    <!--/prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE INSTALL CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
    <h1>Tags Basic Demo</h1>
    <p>This is a very simple page to demonstrate basic concepts of tags</p>
</body>
</html>
```

現在您知道如何將標籤內嵌程式碼新增至網站了！

[下堂課「新增資料元素、規則和程式庫」>](add-data-elements-rules.md)
