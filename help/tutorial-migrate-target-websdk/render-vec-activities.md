---
title: 轉譯VEC活動 — 將Target從at.js 2.x移轉至Web SDK
description: 瞭解如何透過Adobe Target的Web SDK實作擷取及套用視覺化體驗撰寫器活動。
exl-id: bbbbfada-e236-44de-a7bf-5c63ff840db4
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# 呈現Adobe Target視覺化體驗撰寫器(VEC)活動

使用視覺化體驗撰寫器(VEC)或表單式撰寫器來設定Target活動。 Platform Web SDK可以擷取以VEC為基礎的活動，並套用至頁面，就像at.js一樣。 對於移轉的這個部分，您將會：

* 安裝Visual Editing Helper瀏覽器擴充功能
* 使用Platform Web SDK執行`sendEvent`呼叫以要求活動。
* 更新您的at.js實作中任何使用`getOffers()`執行Target `pageLoad`要求的參考。

## Visual Editing Helper瀏覽器擴充功能

適用於Google Chrome的Adobe Experience Cloud Visual Editing Helper瀏覽器擴充功能可讓您可靠地在Adobe Target視覺化體驗撰寫器(VEC)內載入網站，以快速撰寫網站體驗及評估品質。

Visual Editing Helper瀏覽器擴充功能適用於使用at.js或Platform Web SDK的網站。

### 取得並安裝Visual Editing Helper

1. 瀏覽至Chrome網站商店中的[Adobe Experience Cloud Visual Editing Helper瀏覽器擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca)。
1. 按一下&lbrack;新增至&#x200B;**Chrome** > **新增擴充功能**。
1. 在Target中開啟VEC。
1. 若要使用擴充功能，請在VEC或QA模式中時，按一下Chrome瀏覽器工具列上的Visual Editing Helper瀏覽器擴充功能圖示![Visual Editing擴充功能圖示](assets/VEC-Helper.png){zoomable="yes"}。

Visual Editing Helper會在Target VEC中開啟網站時自動啟用，以支援撰寫。 擴充功能沒有任何條件設定。 此擴充功能會自動處理所有設定，包括SameSite Cookie設定。

請參閱專屬檔案，以取得有關[Visual Editing Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html?lang=zh-Hant)和[疑難排解Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html?lang=zh-Hant)的詳細資訊。

>[!IMPORTANT]
>
>新的[Visual Editing Helper擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca)會取代先前的[Target VEC Helper瀏覽器擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=zh-Hant)。 如果已安裝舊版VEC Helper擴充功能，應先移除或停用該擴充功能，再使用Visual Editing Helper擴充功能。

## 自動要求與套用內容

在頁面上設定Platform Web SDK後，您就可以從Target要求內容。 不同於at.js可設定為在程式庫載入時自動要求內容，Platform Web SDK需要您明確執行命令。

如果您的at.js實作將`pageLoadEnabled`設定設為`true`，這會啟用自動轉譯VEC型活動，則您將會使用Platform Web SDK執行下列`sendEvent`命令：

>[!BEGINTABS]

>[!TAB JavaScript]

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TAB 標記]

在標籤中，使用[!UICONTROL 傳送事件]動作型別並選取[!UICONTROL 呈現視覺個人化決定]選項：

![傳送事件，其中包含標籤中選取的轉譯器視覺個人化決定](assets/vec-sendEvent-renderTrue.png){zoomable="yes"}

>[!ENDTABS]

<!--
When the Platform Web SDK renders an activity to the page with `renderDecisions` set to `true`, an additional notification call fires automatically to increment an impression and attribute the visitor to the activity. This call uses an event type with the value `decisioning.propositionDisplay`.

![Platform Web SDK call incrementing a Target impression](assets/target-impression-call.png){zoomable="yes"}
-->

## 隨選要求並套用內容

有些Target實作需要先對VEC選件進行一些自訂處理，才能將其套用至頁面。 或者，他們會在單一呼叫中要求多個位置。 在at.js實作中，您可以將`pageLoadEnabled`設定為`false`並使用`getOffers()`函式來執行`pageLoad`要求來完成此操作。

+++ at.js範例使用`getOffers()`和`applyOffers()`手動轉譯VEC型活動

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

Platform Web SDK沒有特定的`pageLoad`事件。 目標內容的所有要求都是使用`decisionScopes`選項和`sendEvent`命令所控制。 `__view__`範圍符合`pageLoad`要求的用途。

+++ 同等的Platform Web SDK `sendEvent`方法：

1. 執行包含`__view__`決定範圍的`sendEvent`命令
1. 使用`applyPropositions`命令將傳回的內容套用至頁面
1. 執行具有`decisioning.propositionDisplay`事件型別和主張詳細資料的`sendEvent`命令，以增加曝光數

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
>可以[手動轉譯在視覺化體驗撰寫器中進行的修改](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=zh-Hant#manually-rendering-content)。 手動呈現VEC型修改並不常見。 檢查您的at.js實作是否使用`getOffers()`函式手動執行Target `pageLoad`要求，而不使用`applyOffers()`將內容套用至頁面。

Platform Web SDK為開發人員在請求和轉譯內容時提供極大的彈性。 如需其他選項和詳細資訊，請參閱[有關演算個人化內容](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=zh-Hant)的專屬檔案。

## 實作範例

基本的Platform Web SDK實作現已完成。

>[!BEGINTABS]

>[!TAB JavaScript]

具有自動Target內容轉譯的JavaScript範例：

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

具有自動Target內容呈現功能的標籤範例頁面：


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

在標籤中，新增Adobe Experience Platform Web SDK擴充功能：

![新增Adobe Experience Platform Web SDK擴充功能](assets/library-tags-addExtension.png){zoomable="yes"}

新增所需的設定：
![設定Web SDK標籤延伸移轉選項](assets/tags-config-migration.png){zoomable="yes"}

建立具有[!UICONTROL 傳送事件]動作和已選取[!UICONTROL 呈現視覺個人化決定]的規則：
![傳送包含標籤中選取之轉譯器個人化的事件](assets/vec-sendEvent-renderTrue.png){zoomable="yes"}

>[!ENDTABS]

接下來，瞭解如何請求和[轉譯表單式Target活動](render-form-based-activities.md)。

>[!NOTE]
>
>我們致力協助您成功將Target從at.js移轉至Web SDK。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=zh-Hant#M463)中張貼以告知我們。
