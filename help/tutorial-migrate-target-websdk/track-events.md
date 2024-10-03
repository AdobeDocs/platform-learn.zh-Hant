---
title: 追蹤事件 — 將Target從at.js 2.x移轉至Web SDK
description: 瞭解如何使用Experience Platform Web SDK追蹤Adobe Target轉換事件。
exl-id: 5da772bc-de05-4ea9-afbd-3ef58bc7f025
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# 使用Platform Web SDK追蹤目標轉換事件

可使用Platform Web SDK （類似at.js）追蹤Target的轉換事件。 轉換事件通常分為下列類別：

* 自動追蹤不需要任何設定的事件
* 針對最佳實務Platform Web SDK實作而應調整的購買轉換事件
* 需要程式碼更新的非購買轉換事件

## 目標追蹤比較

下表比較at.js和Platform Web SDK追蹤轉換事件的方式

| 活動目標 | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| 轉換>已檢視頁面 | 已自動追蹤。 根據at.js要求裝載中的`context.address.url`值。 | 已自動追蹤。 根據`sendEvent`承載中`xdm.web.webPageDetails.URL`的值 |
| 「轉換>已檢視mbox」 | 已使用具有`type`值`display`的`trackEvent()`或`sendNotifications()`來追蹤顯示mbox位置或通知的要求。 | 已使用Platform Web SDK `sendEvent`呼叫和`decisioning.propositionDisplay`的`eventType`進行追蹤。 |
| 轉換>點選元素 | 已針對VEC型活動自動追蹤。 顯示為at.js網路呼叫，要求裝載中有`notifications`物件且`type`值為`click`。 | 已針對VEC型活動自動追蹤。 顯示為Platform Web SDK `sendEvent`呼叫，具有`decisioning.propositionInteract`的`eventType`。 |
| 參與度>頁面檢視 | 已自動追蹤 | 已自動追蹤 |
| 參與度>網站逗留時間 | 已自動追蹤 | 已自動追蹤 |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## 自動追蹤的事件

下列轉換目標不需要對實作作作作任何特定調整：

* 轉換>已檢視頁面
* 轉換>點選元素
* 參與度>頁面檢視
* 參與度>網站逗留時間

>[!NOTE]
>
>Platform Web SDK允許對請求承載中傳遞的值進行更全面的控制。 若要確保Target功能（例如QA URL和「已檢視頁面」轉換目標）正常運作，請檢查`xdm.web.webPageDetails.URL`值是否包含具有適當字元大小寫的完整頁面URL。

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

Target實施通常會使用自訂轉換事件來追蹤表單式活動的點按、表示流量中的轉換，或傳遞引數而不要求新內容。

下表概述幾個常見轉換追蹤使用案例的at.js方法和Platform Web SDK同等功能。

| 使用實例 | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| 追蹤mbox位置（範圍）的點選轉換事件 | 針對特定mbox位置以`type`值`click`執行`trackEvent()`或`sendNotifications()` | 執行事件型別為`decisioning.propositionInteract`的`sendEvent`命令 |
| 追蹤可能也會包含其他資料（例如Target設定檔引數）的自訂轉換事件 | 針對特定mbox位置以`type`值`display`執行`trackEvent()`或`sendNotifications()` | 執行事件型別為`decisioning.propositionDisplay`的`sendEvent`命令 |

>[!NOTE]
>
>雖然`decisioning.propositionDisplay`最常用於增加特定範圍的曝光數，但通常也應該用來直接取代at.js `trackEvent()`。 如果未指定，`trackEvent()`函式預設為`display`型別。 請檢查您的實作，確保您可能已定義的任何自訂轉換使用正確的事件型別。

請參閱專屬的at.js檔案，以取得有關如何使用[`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/)和[`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/)來追蹤Target事件的詳細資訊。

at.js範例使用`trackEvent()`追蹤mbox位置上的點選：

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

透過Platform Web SDK實作，您可以呼叫`sendEvent`命令、填入`_experience.decisioning.propositions` XDM欄位群組，並將`eventType`設定為下列兩個值之一，以追蹤事件和使用者動作：

* `decisioning.propositionDisplay`：代表Target活動的轉譯。
* `decisioning.propositionInteract`：代表使用者與活動的互動，例如滑鼠點按。

`_experience.decisioning.propositions` XDM欄位群組是物件陣列。 每個物件的屬性衍生自`sendEvent`命令中傳回的`result.propositions`： `{ id, scope, scopeDetails }`

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

接下來，瞭解如何[啟用跨網域ID共用](cross-domain.md)，以取得一致的訪客設定檔。

>[!NOTE]
>
>我們致力協助您成功將Target從at.js移轉至Web SDK。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
