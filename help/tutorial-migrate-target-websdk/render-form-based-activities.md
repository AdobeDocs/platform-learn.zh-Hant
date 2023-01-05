---
title: 將Target從at.js 2.x移轉至Web SDK
description: 了解如何將Adobe Target實作從at.js 2.x移轉至Adobe Experience Platform Web SDK。 主題包括程式庫概觀、實作差異和其他值得注意的圖說文字。
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 2%

---

# 呈現使用表單式撰寫器的Target活動

某些Target實作可能會使用地區mbox（現在稱為「範圍」），從使用表單式體驗撰寫器的活動傳送內容。 如果您的at.js Target實作使用mbox，則您需要執行下列動作：

* 更新來自您at.js實作的任何參考，這些實作會使用 `getOffer()` 或 `getOffers()` 至相同的Platform Web SDK方法。
* 新增程式碼以觸發 `propositionDisplay` 事件，以便計算曝光數。

## 隨選要求和套用內容

使用Target的表單式撰寫器建立並傳遞至地區mbox的活動，無法由Platform Web SDK自動轉譯。 與at.js類似，傳遞至特定Target位置的選件需要隨選呈現。

at.js範例使用 `getOffer()` 和 `applyOffer()`:

1. 執行 `getOffer()` 要求位置的優惠方案
1. 執行 `applyOffer()` 將選件呈現至指定的選取器
1. 活動曝光會在 `getOffer()` 請求

```JavaScript
// Retrieve an offer for the homepage-hero location
adobe.target.getOffer({
  "mbox": "homepage_hero",

  // Render offer to the #hero-banner selector
  "success": function(offers) {
    adobe.target.applyOffer({
      "mbox": "homepage_hero",
      "selector": "#hero-banner",
      "offer": offers
    });
  },
  "error": {
    console.log(error);
  },
  "timeout": 3000
});
```

平台Web SDK的對等方法，使用 `applyPropositions` 命令：

1. 執行 `sendEvent` 命令請求一個或多個位置（作用域）的選件（命令）
1. 執行 `applyPropositions` 帶有元資料對象的命令，該元資料對象提供如何將內容應用於每個範圍的頁面的說明
1. 執行 `sendEvent` 命令，其eventType為 `decisioning.propositionDisplay` 追蹤曝光數

```JavaScript
// Retrieve propositions for homepage_hero location (scope)
alloy("sendEvent", {
  "decisionScopes": ["homepage_hero"]
}).then(function(result) {
  var retrievedPropositions = result.propositions;
    
  // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
  return alloy("applyPropositions", {
    "propositions": retrievedPropositions,
    "metadata": {
      // Specify each regional mbox or scope name along with a selector and actionType
      "homepage_hero": {
        "selector": "#hero-banner",
        "actionType": "setHtml"
      }
    }
  }).then(function(applyPropositionsResult) {
    var renderedPropositions = applyPropositionsResult.propositions;

    // Send the display notifications via sendEvent command
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
});
```

Platform Web SDK可讓您進一步控制要使用，將表單式活動套用至頁面 `applyPropositions` 命令 `actionType` 指定：

| `actionType` | 說明 | at.js `applyOffer()` | 平台Web SDK `applyPropositions` |
| --- | --- | --- | --- |
| `setHtml` | 清除容器的內容，然後新增選件至容器 | 是（一律使用） | 是 |
| `replaceHtml` | 移除容器並以選件取代 | 無 | 是 |
| `appendHtml` | 在指定的選取器之後附加選件 | 無 | 是 |

請參閱 [專屬檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) 關於使用Platform Web SDK轉譯內容，以取得其他轉譯選項和範例。

## 實作範例

以下範例頁面以前一節中概述的實作為基礎，只會新增其他範圍至 `sendEvent` 命令。

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

  <!--Prehiding snippet for Target with asynchronous deployment-->
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
    alloy("sendEvent", {
      // Request and render VEC-based activities
      "renderDecisions": true,
      // Request content for form-based activities using the "homepage_hero" scope
      "decisionScopes": ["homepage_hero"]
    }).then(function(result) {
      var retrievedPropositions = result.propositions;
        
      // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
      return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
          // Specify each regional mbox or scope name along with a selector and actionType
          "homepage_hero": {
            "selector": "#hero-banner",
            "actionType": "setHtml"
          }
        }
      }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
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

接下來，學習如何 [使用Platform Web SDK傳遞Target參數](send-parameters.md).

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).