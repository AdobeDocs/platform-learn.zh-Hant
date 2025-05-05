---
title: 將Target從at.js 2.x移轉至Web SDK
description: 瞭解如何將Adobe Target實作從at.js 2.x移轉至Adobe Experience Platform Web SDK。 主題包括程式庫概述、實作差異和其他值得注意的圖說文字。
exl-id: 43b9ae91-4524-4071-9eb4-12a0a8aec242
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# 呈現使用表單式撰寫器的Target活動

有些Target實作可能會使用地區mbox （現在稱為「範圍」），從使用表單式體驗撰寫器的活動傳送內容。 如果您的at.js Target實作使用mbox，則您需要執行下列動作：

* 將使用`getOffer()`或`getOffers()`的at.js實作中的任何參考更新為同等的Platform Web SDK方法。
* 新增程式碼以觸發`propositionDisplay`事件，計算曝光次數。

## 隨選要求並套用內容

使用Target的表單式撰寫器建立並傳送至地區mbox的活動，無法由Platform Web SDK自動轉譯。 與at.js類似，傳遞至特定Target位置的選件需要隨選呈現。


+++使用`getOffer()`和`applyOffer()`的at.js範例：

1. 執行`getOffer()`以要求某個位置的選件
1. 執行`applyOffer()`將選件轉譯為指定的選取器
1. 活動曝光會在`getOffer()`要求時自動增加

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

+++

+++使用`applyPropositions`命令的Platform Web SDK對等專案：

1. 執行`sendEvent`命令以要求一或多個位置（範圍）的選件（主張）
1. 使用中繼資料物件執行`applyPropositions`命令，該物件提供如何為每個範圍的頁面套用內容的指示
1. 執行eventType為`decisioning.propositionDisplay`的`sendEvent`命令以追蹤印象

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

+++

Platform Web SDK提供更好的控制功能，可讓您使用指定了`actionType`的`applyPropositions`命令，將表單式活動套用至頁面：

| `actionType` | 說明 | at.js `applyOffer()` | Platform Web SDK `applyPropositions` |
| --- | --- | --- | --- |
| `setHtml` | 清除容器的內容，然後將選件新增至容器 | 是（永遠使用） | 是 |
| `replaceHtml` | 移除容器並以選件取代 | 無 | 是 |
| `appendHtml` | 在指定的選取器後附加選件 | 無 | 是 |

如需其他轉譯選項和範例，請參閱[有關使用Platform Web SDK轉譯內容的專屬檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html)。

## 實作範例

以下範例頁面以上一節中概述的實作為基礎，只是將其他範圍新增到`sendEvent`命令。

+++具有多個範圍的Platform Web SDK範例

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

接下來，瞭解如何使用Platform Web SDK[傳遞Target引數](send-parameters.md)。

>[!NOTE]
>
>我們致力協助您成功將Target從at.js移轉至Web SDK。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
