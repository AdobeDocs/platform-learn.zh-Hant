---
title: 新增內嵌程式碼
description: 瞭解如何取得標籤屬性的內嵌程式碼並在您的網站中實作。 本課程屬於「在網站中實作Experience Cloud」教學課程的一部分。
exl-id: a2959553-2d6a-4c94-a7df-f62b720fd230
source-git-commit: 277f5f2c07bb5818e8c5cc129bef1ec93411c90d
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 43%

---

# 新增內嵌程式碼

在本課程中，您將實作標籤屬性的開發環境非同步內嵌程式碼。 在此過程中，您將瞭解標籤的兩個主要概念：環境和內嵌程式碼。

>[!NOTE]
>
>Adobe Experience Platform Launch正在以資料收集技術套裝的形式整合到Adobe Experience Platform中。 此介面已推出幾項術語變更，使用此內容時請務必注意：
>
> * platform launch（使用者端）現在是&#x200B;**[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)**
> * platform launch伺服器端現在是&#x200B;**[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Edge設定現在是&#x200B;**[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**

## 學習目標

在本課程結束時，您將能夠：

* 取得標籤屬性的內嵌程式碼
* 瞭解開發、測試和生產環境之間的差異
* 將標籤內嵌程式碼新增至html檔案
* 說明標籤內嵌程式碼相對於html檔案`<head>`中其他程式碼的最佳位置

## 複製內嵌程式碼

內嵌程式碼是您放在網頁上的`<script>`標籤，可載入並執行您在標籤中建置的邏輯。 如果您非同步載入程式庫，瀏覽器會繼續載入頁面，擷取標籤程式庫，然後同時執行。 在這種情況下，只會有一個內嵌程式碼，您會將其放在 `<head>` 中。（以同步方式部署標籤時，會有兩個內嵌程式碼，一個放在`<head>`中，另一個放在`</body>`之前）。

在屬性Overview畫面中，按一下左側導覽中的&#x200B;**[!UICONTROL 環境]**&#x200B;以移至環境頁面。 請注意，系統已為您預先建立開發、測試和生產環境。

![按一下頂端導覽列中的「環境」](images/launch-environments.png)

開發、測試和生產環境對應至程式碼開發和發佈程序中的典型環境。程式碼是先由開發人員在開發環境中撰寫。當開發人員完成其工作時，就會將其傳送至測試環境，讓 QA 和其他團隊進行審查。QA 和其他團隊完成確認之後，就會將程式碼發佈到生產環境，這是訪客來到您的網站時所體驗的公開環境。

標籤允許使用其他開發環境，這在有多位開發人員同時處理不同專案的大型組織中很有用。

完成本教學課程只需用到這些環境。環境可讓您擁有位於不同URL託管的不同標籤程式庫有效版本，這樣您就能安全地新增功能，並在正確的時間提供給適當的使用者使用（例如開發人員、QA工程師、大眾等） 。

現在來複製內嵌程式碼：

1. 在&#x200B;**[!UICONTROL 開發]**&#x200B;列中，按一下「安裝」圖示![安裝圖示](images/launch-installIcon.png)以開啟強制回應視窗。

1. 請注意，標籤會預設為非同步內嵌程式碼

1. 按一下「複製」圖示 ![「複製」圖示](images/launch-copyIcon.png)，將內嵌程式碼複製到剪貼簿。

1. 按一下&#x200B;**[!UICONTROL 關閉]**&#x200B;以關閉強制回應視窗。

   ![「安裝」圖示](images/launch-copyInstallCode.png)

## 在範例 HTML 頁面的 `<head>` 中實施內嵌程式碼

內嵌程式碼應在將共用屬性之所有 HTML 頁面的 `<head>` 元素中實施。您可能有一或數個可跨網站全域控制`<head>`的範本檔案，能讓新增標籤的程式相當簡單明瞭。

如果沒有，請複製範例html頁面程式碼並將其貼到程式碼編輯器中。 如果您需要編輯器，可使用免費的開放原始碼編輯器 [Brackets](https://brackets.io/)。

+++範例html頁面程式碼

```html
<!doctype html>
<html lang="en">
<head>
    <title>Tags: Sample HTML Page</title>
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
    <!--Tags Header Embed Code: REPLACE THE NEXT LINE WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
    <h1>Tags: Sample HTML Page</h1>
    <p>This is a very simple page to demonstrate basic implementation concepts of Tags</p>
    <p>See <a href="https://docs.adobe.com/content/help/en/experience-cloud/implementing-in-websites-with-launch/index.html">Implementing the Experience Cloud in Websites with Tags</a> for the complete tutorial</p>
</body>
</html>
```

+++

將第 34 行或其附近的現有內嵌程式碼取代為您剪貼簿上的內容，然後儲存頁面。現在，請在網頁瀏覽器中開啟該頁面。如果您使用 `file://` 通訊協定載入頁面，必須在程式碼編輯器中的內嵌程式碼 URL 開頭新增「https:」。範例頁面的第 33 到 36 行看起來可能像這樣：

```html
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="https://assets.adobedtm.com/launch-ENa21cfed3f06f4ddf9690de8077b39e81-development.min.js" async></script>
    <!--/Tags Header Embed Code-->
```

開啟網頁瀏覽器的開發人員工具，然後前往「網路」標籤。此時，您應該會看到標籤環境URL的404錯誤：
![404錯誤](images/samplepage-404.png)

404錯誤是預期會出現的情況，因為您尚未在此標籤環境中建置程式庫。 您會在下一個課程中執行該操作。如果您看到「失敗」訊息 (而不是 404 錯誤)，表示您可能忘了將 `https://` 通訊協定加入內嵌程式碼中。同樣地，如果您使用 `file://` 通訊協定載入範例頁面，則只需指定 `https://` 通訊協定即可。進行該變更並重新載入頁面，直到 404 錯誤出現為止。

## 標籤實作最佳作法

讓我們花點時間檢閱範例頁面中示範的某些標籤實作最佳作法：

* **資料層**：

   * 我們&#x200B;*強烈*&#x200B;建議您在網站上建立資料層，包含在Analytics、Target和其他行銷解決方案中填入變數所需的所有屬性。 此範例頁面只包含非常簡單的資料層，但實際資料層可能包含有關頁面的更多詳細資料、訪客、其購物車詳細資料等內容。如需資料層的詳細資訊，請參閱[客戶體驗數位資料層 1.0](https://www.w3.org/2013/12/ceddl-201312.pdf)

   * 在標籤內嵌程式碼之前定義資料層，以發揮Experience Cloud解決方案的最大效用。

* **JavaScript協助程式庫**：如果您已在頁面的`<head>`中實作JQuery等程式庫，請在標籤之前將其載入，以便在標籤和Target中運用其語法

* **HTML5 doctype**：HTML5 doctype 在 Target 實施中是必要的

* **preconnect 和 dns-prefetch**: 使用 preconnect 和 dns-prefetch 來改善頁面載入時間。另請參閱：[https://w3c.github.io/resource-hints/](https://w3c.github.io/resource-hints/)

* **非同步Target實施的預先隱藏程式碼片段**：您將在Target課程中深入瞭解，但是若Target是透過非同步標籤內嵌程式碼部署，您應在頁面上於標籤內嵌程式碼之前新增預先隱藏的程式碼片段，以便管理內容閃爍問題

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
