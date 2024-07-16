---
title: 透過標記在網站中實施 Experience Cloud
description: 前端程式開發人員或技術行銷人員若想瞭解如何在其網站上實施Adobe Experience Cloud解決方案，透過標籤在網站中實施Experience Cloud是最佳起點。
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: 2483409b52562e13a4f557fe5bdec75b5afb4716
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 36%

---

# 概觀

_使用標籤在網站中實作Experience Cloud_&#x200B;是想要瞭解如何在其網站上實作Adobe Experience Cloud解決方案的前端開發人員或技術行銷人員的最佳起點。

每個課程都包含操作練習和基礎資訊，協助您實施 Experience Cloud 並瞭解其價值。示範網站是供您完成本教學課程使用，讓您可以在安全的環境中瞭解基礎技術。完成本教學課程後，您應已準備好開始透過您自己的網站上的標籤實作所有行銷解決方案。

>[!INFO]
>
>本教學課程使用應用程式專用的擴充功能和程式庫(Adobe Analytics的AppMeasurement.js，Adobe Target的at.js)。 如果您想要實作Adobe Experience Platform Web SDK，請參閱[使用Web SDK實作Adobe Experience Cloud](/help/tutorial-web-sdk/overview.md)教學課程。


完成此教學課程之後，您應該能夠：

* 建立標籤屬性

* 在網站上安裝標籤屬性

* 新增下列 Adobe Experience Cloud 解決方案：
   * **[Adobe Experience Platform Identity服務](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* 建立規則和資料元素以將資料傳送至 Adobe 解決方案

* 使用 Adobe Experience Cloud Debugger 驗證實施

* Publish會透過開發、測試和生產環境進行變更

>[!NOTE]
>
>Adobe Experience Platform Launch正在以資料收集技術套裝的形式整合到Adobe Experience Platform中。 此介面已推出幾項術語變更，使用此內容時請務必注意：
>
> * platform launch（使用者端）現在是&#x200B;**[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)**
> * platform launch伺服器端現在是&#x200B;**[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Edge設定現在是&#x200B;**[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**

>[!NOTE]
>
>[Web SDK](../tutorial-web-sdk/overview.md)和[Mobile SDK](../tutorial-mobile-sdk/overview.md)也提供類似的多重解決方案教學課程。

## 必要條件

這些課程假設您擁有 Adobe ID 和完成練習所需的權限。如果不具備上述條件，您可能需要聯絡您的 Experience Cloud 管理員以請求存取權限。

* 針對標籤，您必須擁有開發、核准、Publish、管理擴充功能及管理環境的許可權。 如需有關標籤使用者許可權的詳細資訊，請參閱[檔案](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html)。
* 針對 Adobe Analytics，您必須知道您的追蹤伺服器，以及您將使用哪些報表套裝來完成本教學課程
* 若要Audience Manager，您必須知道您的Audience Manager子網域（也稱為「合作夥伴名稱」、「合作夥伴ID」或「合作夥伴子網域」）

此外，我們假設您已熟悉 HTML 和 JavaScript 等前端開發語言。您不需要這些語言的專家就能完成這些課程，但如果您熟悉且瞭解程式碼，將能從中學到更多。

## 關於標籤

Adobe Experience Platform的標籤功能是新一代Adobe的網站標籤與行動SDK管理功能。 標籤可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告解決方案功能，以便支援相關客戶體驗。 標籤不需額外付費。 可供所有 Adobe Experience Cloud 客戶使用。

網站的標籤可讓您集中管理與案頭和行動網站上使用的分析、行銷和廣告解決方案相關的所有JavaScript。 例如，如果您部署Adobe Analytics，標籤將管理AppMeasurementJavaScript程式庫、填入變數和引發請求。

容器的內容皆經過適當極簡化，包括自訂程式碼。一切模組化。如果您不需要某個項目，就不必將該項目納入程式庫。如此可使實施流程更加快速和精簡。

標籤也是一個平台，可讓協力廠商建立擴充功能，以便透過標籤輕鬆部署其解決方案。 擴充功能是指能擴充標籤介面和使用者端功能的程式碼(JavaScript、HTML和CSS)套件。 您可以將標籤視為作業系統，而擴充功能則是您用來完成工作的應用程式。

## 關於課程

在這些課程中，您會將 Adobe Experience Cloud 實施至名為 Luma 的虛擬零售網站中。[Luma 網站](https://luma.enablementadobe.com/content/luma/us/en.html)具有豐富的資料層和功能，可讓您建置逼真的實施。您將在自己的Experience Cloud組織中建置自己的標籤屬性，並使用Experience Cloud Debugger將其對應至我們託管的Luma網站。

[![Luma網站](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## 取得工具

1. 由於您將會用到一些瀏覽器專用擴充功能，建議您使用 [Chrome 網頁瀏覽器](https://www.google.com/chrome/)完成本教學課程
1. 將[Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)擴充功能新增至Chrome瀏覽器
1. 複製範例html頁面程式碼

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

1. 取得可用來變更範例 html 頁面的文字編輯器。(如果您沒有這類文字編輯器，建議您試用 [Brackets](https://brackets.io/))
1. 將 [Luma 網站](https://luma.enablementadobe.com/content/luma/us/en.html)加入書籤

>[!NOTE]
>
>您會發現，在Chrome中開啟Luma網站，同時在其他瀏覽器中閱讀本教學課程並完成資料收集介面步驟，可更輕鬆完成本教學課程。

我們開始吧！

[下堂課「建立標籤屬性」>](create-a-property.md)
