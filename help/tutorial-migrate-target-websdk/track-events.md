---
title: 追蹤事件 |將Target從at.js 2.x移轉至Web SDK
description: 了解如何使用Adobe Target Web SDK追蹤Experience Platform轉換事件。
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# 使用Platform Web SDK追蹤Target轉換事件

可以使用類似於at.js的平台Web SDK追蹤Target的轉換事件。 轉換事件通常分為下列類別：

* 不需要任何設定的自動追蹤事件
* 購買轉換事件，應因應最佳實務Platform Web SDK實作而調整
* 需要更新程式碼的非購買轉換事件

## 目標追蹤比較

下表比較at.js和Platform Web SDK追蹤轉換事件的方式

| 活動目標 | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 轉換>已檢視頁面 | 自動追蹤。 根據 `context.address.url` 在at.js要求裝載中。 | 自動追蹤。 根據 `xdm.web.webPageDetails.URL` 在 `sendEvent` 裝載 |
| 轉換>已檢視mbox | 以顯示mbox位置的請求或使用的通知來追蹤 `trackEvent()` 或 `sendNotifications()` 帶 `type` 值 `display`. | 使用Platform Web SDK追蹤 `sendEvent` 呼叫 `eventType` of `decisioning.propositionDisplay`. |
| 轉換>按一下元素 | 針對VEC型活動自動追蹤。 顯示為具有 `notifications` 中的物件，以及 `type` 值 `click`. | 針對VEC型活動自動追蹤。 以Platform Web SDK的形式顯示 `sendEvent` 呼叫 `eventType` of `decisioning.propositionInteract`. |
| 參與>頁面檢視 | 自動追蹤 | 自動追蹤 |
| 參與>網站逗留時間 | 自動追蹤 | 自動追蹤 |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## 自動追蹤的事件

下列轉換目標不需要對您的實作進行任何特定調整：

* 轉換>已檢視頁面
* 轉換>按一下元素
* 參與>頁面檢視
* 參與>網站逗留時間

>[!NOTE]
>
>Platform Web SDK可讓您進一步控制要求裝載中傳遞的值。 若要確保QA URL和「已檢視頁面」轉換目標等Target功能正常運作，請檢查 `xdm.web.webPageDetails.URL` 值包含整頁URL，且大小寫正確。

<!--
## Purchase conversion events

The following conversion goals are based on the order details information passed in the Platform Web SDK `sendEvent` payload:

* Revenue > Revenue per Visit (RPV)
* Revenue > Average Order Value (AOV)
* Revenue > Total Sales
* Revenue > Orders

Target at.js implementations typically use an order confirmation mbox with the `trackEvent()` or `sendNotifications()` functions to pass the order ID, order total, and a list of product IDs purchased. These methods are specific to Target.

The Platform Web SDK is a shared library for all Adobe applications and you may have other applications such as Adobe Analytics to consider. Because of this shared nature, its best send a single order confirmation call using the appropriate commerce XDM field group.

For more information and an example, refer to the tutorial section about [sending purchase parameters to Target](send-parameters.md#purchase-parameters). 
-->

## 自訂追蹤事件

Target實作通常使用自訂轉換事件來追蹤表單式活動的點按、表示流量中的轉換，或在不要求新內容的情況下傳遞參數。

下表概述at.js方法，以及針對一些常見的轉換追蹤使用案例的同等Platform Web SDK。

| 使用案例 | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 追蹤mbox位置（範圍）的點擊轉換事件 | 執行 `trackEvent()` 或 `sendNotifications()` 帶 `type` 值 `click` 特定mbox位置 | 執行 `sendEvent` 命令的事件類型為 `decisioning.propositionInteract` |
| 追蹤自訂轉換事件，該事件可能也包含其他資料，例如Target設定檔參數 | 執行 `trackEvent()` 或 `sendNotifications()` 帶 `type` 值 `display` 特定mbox位置 | 執行 `sendEvent` 命令的事件類型為 `decisioning.propositionDisplay` |

>[!NOTE]
>
>雖然 `decisioning.propositionDisplay` 最常用於增加特定範圍的曝光數，也應當用作at.js的直接取代 `trackEvent()` 通常。 此 `trackEvent()` 函式預設為 `display` 若未指定。 檢查您的實作，以確保您對可能定義的任何自訂轉換使用正確的事件類型。

如需如何使用的詳細資訊，請參閱專屬的at.js檔案 [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) 和 [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) 來追蹤Target事件。

at.js範例使用 `trackEvent()` 若要追蹤mbox位置上的點按：

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

透過Platform Web SDK實作，您可以呼叫 `sendEvent` 命令，填入 `_experience.decisioning.propositions` XDM欄位群組，並設定 `eventType` 至兩個值之一：

* `decisioning.propositionDisplay`:代表Target活動轉譯。
* `decisioning.propositionInteract`:代表使用者與活動的互動，例如滑鼠點按。

此 `_experience.decisioning.propositions` XDM欄位群組是物件的陣列。 每個物件的屬性衍生自 `result.propositions` 那些在 `sendEvent` 命令： `{ id, scope, scopeDetails }`

```JavaScript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

接下來，學習如何 [啟用跨網域ID共用](cross-domain.md) 以便一致的訪客設定檔。

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).