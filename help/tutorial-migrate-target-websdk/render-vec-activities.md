---
title: 呈現VEC活動 |將Target從at.js 2.x移轉至Web SDK
description: 了解如何透過Adobe Target的Web SDK實作來擷取和套用可視化體驗撰寫器活動。
source-git-commit: ca2fade972a2f7f84134ee4ef9c0f24c5ab1c5c6
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 6%

---

# 呈現Adobe Target可視化體驗撰寫器(VEC)活動

Target活動是使用可視化體驗撰寫器(VEC)或表單式撰寫器來設定。 Platform Web SDK可像at.js一樣，擷取VEC型活動並套用至頁面。 在移轉的這部分，您會：

* 安裝Visual Editing Helper瀏覽器擴充功能
* 執行 `sendEvent` 使用Platform Web SDK呼叫以要求活動。
* 更新來自您at.js實作的任何參考，這些實作會使用 `getOffers()` 執行目標 `pageLoad` 請求。

## Visual Editing Helper瀏覽器擴充功能

適用於Google Chrome的Adobe Experience Cloud Visual Editing Helper瀏覽器擴充功能可讓您在Adobe Target可視化體驗撰寫器(VEC)中以可靠的方式載入網站，以快速撰寫網頁體驗和保證體驗品質。

Visual Editing Helper瀏覽器擴充功能適用於使用at.js或Platform Web SDK的網站。

### 獲取並安裝Visual Editing Helper

1. 導覽至 [Adobe Experience Cloud Chrome線上應用程式商店中的Visual Editing Helper瀏覽器擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. 按一下「新增至」 **鉻黃** > **新增擴充功能**.
1. 在Target中開啟VEC。
1. 若要使用擴充功能，請按一下Visual Editing Helper瀏覽器擴充功能圖示 ![可視化編輯擴充功能圖示](assets/VEC-Helper.png)在VEC或QA模式時，在Chrome瀏覽器的工具列中出現{zoomable=&quot;yes&quot;}。

Visual Editing Helper 會在 Target VEC 中開啟網站時自動啟用，以支援撰寫。 此擴充功能沒有任何條件設定。 此擴充功能可自動處理所有設定，包括 SameSite Cookie 設定。

如需 [Visual Editing Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) 和 [疑難排解可視化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html).

>[!IMPORTANT]
>
>新 [Visual Editing Helper擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca) 取代上一個 [Target VEC Helper瀏覽器擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html). 如果已安裝舊版VEC Helper擴充功能，則應先移除或停用該擴充功能，再使用Visual Editing Helper擴充功能。

## 自動要求和套用內容

在頁面上設定Platform Web SDK後，您就可以向Target要求內容。 與at.js不同，at.js可在程式庫載入時設定為自動要求內容，Platform Web SDK會要求您明確執行命令。

如果您的at.js實作具有 `pageLoadEnabled` 設定為 `true` 可自動轉譯VEC型活動，則您會執行下列動作 `sendEvent` 命令（與Platform Web SDK搭配使用）:

>[!BEGINTABS]

>[!TAB JavaScript]

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TAB 標記]

在標籤中，使用 [!UICONTROL 傳送事件] 動作類型與 [!UICONTROL 轉譯視覺個人化決策] 選項：

![傳送在標籤中選取「呈現視覺個人化」決策的事件](assets/vec-sendEvent-renderTrue.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

<!--
When the Platform Web SDK renders an activity to the page with `renderDecisions` set to `true`, an additional notification call fires automatically to increment an impression and attribute the visitor to the activity. This call uses an event type with the value `decisioning.propositionDisplay`.

![Platform Web SDK call incrementing a Target impression](assets/target-impression-call.png){zoomable="yes"}
-->

## 隨選要求和套用內容

在將VEC選件套用至頁面之前，部分Target實作需要先對VEC選件進行一些自訂處理。 或者，他們在單一呼叫中要求多個位置。 在at.js實作中，您可以透過設定 `pageLoadEnabled` to `false` 和使用 `getOffers()` 執行函式 `pageLoad` 請求。

+++ at.js範例使用 `getOffers()` 和 `applyOffers()` 手動呈現VEC型活動的方式

```JavaScript
adobe.target.getOffers({
  request: {
    execute: {
      pageLoad: {}
    }
  }
}).
then(response => adobe.target.applyOffers({ response: response }));
```

+++

Platform Web SDK沒有特定 `pageLoad` 事件。 所有Target內容的請求都可透過 `decisionScopes` 選項 `sendEvent` 命令。 此 `__view__` 範圍符合 `pageLoad` 請求。

+++ 同等的Platform Web SDK `sendEvent` 方法：

1. 執行 `sendEvent` 包含 `__view__` 決策範圍
1. 將傳回的內容套用至具有 `applyPropositions` 命令
1. 執行 `sendEvent` 命令 `decisioning.propositionDisplay` 事件類型和主張詳細資料以增加曝光

```Javascript
alloy("sendEvent", {
  // Request the special "__view__" scope for target-global-mbox / pageLoad
  decisionScopes: ["__view__"]
}).then(function(result) {
  // Check if content (propositions) were returned
  if (result.propositions) {
    var retrievedPropositions = result.propositions;
    // Apply propositions to the page
    return alloy("applyPropositions", {
      propositions: retrievedPropositions
    }).then(function(applyPropositionsResult) {
      var renderedPropositions = applyPropositionsResult.propositions;
      // Send a display notification with the sendEvent command
      alloy("sendEvent", {
        "xdm": {
          "eventType": "decisioning.propositionDisplay",
          "_experience": {
            "decisioning": {
              "propositions": renderedPropositions
            }
          }
        }
      });
    });
  }
});
```

+++

>[!NOTE]
>
>可以 [手動呈現修改](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) 在可視化體驗撰寫器中建立。 手動轉譯VEC型修改不常見。 檢查您的at.js實作是否使用 `getOffers()` 函式來手動執行Target `pageLoad` 請求不使用 `applyOffers()` 來將內容套用至頁面。

Platform Web SDK為開發人員提供要求和轉譯內容的極大彈性。 請參閱 [轉譯個人化內容的專屬檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) 以取得其他選項和詳細資訊。

## 實作範例

基礎平台網頁SDK實作現已完成。

>[!BEGINTABS]

>[!TAB JavaScript]

自動轉譯Target內容的JavaScript範例：

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK then send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    
    // Send an event to the Adobe edge network and render Target content automatically 
    alloy("sendEvent", {
      "renderDecisions": true
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```


>[!TAB 標記]

自動呈現Target內容的標籤範例頁面：


```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

在標籤中新增Adobe Experience Platform Web SDK擴充功能：

![新增Adobe Experience Platform Web SDK擴充功能](assets/library-tags-addExtension.png){zoomable=&quot;yes&quot;}

新增所需的設定：
![設定Web SDK標籤擴充功能移轉選項](assets/tags-config-migration.png){zoomable=&quot;yes&quot;}

使用 [!UICONTROL 傳送事件] 行動與 [!UICONTROL 轉譯視覺個人化決策] 已選取：
![傳送在標籤中選取「呈現個人化」的事件](assets/vec-sendEvent-renderTrue.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

接下來，了解如何要求和 [呈現表單式Target活動](render-form-based-activities.md).

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
