---
title: 傳送參數 |將Target從at.js 2.x移轉至Web SDK
description: 了解如何使用Web SDK將mbox、設定檔和實體參數傳送至Adobe Target。
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 1%

---

# 使用Platform Web SDK將參數傳送至Target

Target實作因網站架構、業務需求和使用的功能而異。 大部分的Target實作包括傳遞各種參數以取得內容資訊、對象和內容建議。

讓我們使用簡單的產品詳細資料頁面和訂單確認頁面，來示範將參數傳遞至Target時程式庫之間的差異。

假設使用at.js的下列兩個範例頁面：

+++產品詳細資料頁面上的at.js :

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>
  <!--Target parameters -->
  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Mbox parameters
        "pageName": "product detail",
        // Profile parameters
        "profile.gender": "male",
        "user.categoryId": "clothing",
        // Entity parameters for Target Recomendations
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts",
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL",
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```

+++


+++訂單確認頁面上的at.js:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>-->
  <!--Target parameters -->
  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Order confirmation parameters
        "orderId": "ABC123",
        "productPurchasedId": "SKU-00002,SKU-00003",
        "orderTotal": 1337.89,
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```

+++


## 參數映射摘要

這些頁面的Target參數使用Platform Web SDK時的傳送方式不同。 使用at.js可透過多種方式將參數傳遞至Target:

- 設定為 `targetPageParams()` 函式（用於本頁的範例中）
- 設定為 `targetPageParamsAll()` 函式。
- 直接連同 `getOffer()` 函式
- 直接連同 `getOffers()` 功能


Platform Web SDK提供單一一致的方式，可傳送資料，而不需額外功能。 所有參數都必須在裝載中以 `sendEvent` 命令和屬於兩個類別：

- 自動從 `xdm` 物件
- 使用 `data.__adobe.target` 物件

下表概述如何使用Platform Web SDK重新對應範例參數：

| at.js參數範例 | 平台Web SDK選項 | 附註 |
| --- | --- | --- |
| `at_property` | 不適用 | 屬性代號可在 [資料流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) 和無法設定於 `sendEvent` 呼叫。 |
| `pageName` | `xdm.web.webPageDetails.name` | 所有Target mbox參數都必須在 `xdm` 物件，並遵循使用XDM ExperienceEvent類別的結構。 Mbox參數無法作為 `data` 物件。 |
| `profile.gender` | `data.__adobe.target.profile.gender` | 所有Target設定檔參數都必須在 `data` 物件和前置詞為 `profile.` 適當地對應。 |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | 用於Target的類別相關性功能的保留參數，此功能必須在 `data` 物件。 |
| `entity.id` | `data.__adobe.target.entity.id` <br>或<br> `xdm.productListItems[0].SKU` | 實體ID用於Target Recommendations行為計數器。 這些實體ID可在 `data` 物件或自動從 `xdm.productListItems` 陣列（如果您的實施使用該欄位群組）。 |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | 實體類別ID可在 `data` 物件。 |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | 自訂實體參數可用來更新Recommendations產品目錄。 這些自訂參數必須在 `data` 物件。 |
| `cartIds` | `data.__adobe.target.cartIds` | 用於Target的購物車型建議演算法。 |
| `excludedIds` | `data.__adobe.target.excludedIds` | 用於防止特定實體ID在建議設計中傳回。 |
| `mbox3rdPartyId` | 在 `xdm.identityMap` 物件 | 用於跨裝置和客戶屬性同步Target設定檔。 必須在 [資料流的目標配置](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID` | 用於識別Target轉換追蹤的唯一順序。 |
| `orderTotal` | `xdm.commerce.order.priceTotal` | 用於追蹤Target轉換和最佳化目標的訂單總計。 |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>或<br> `xdm.productListItems[0-n].SKU` | 用於Target轉換追蹤和建議演算法。 請參閱 [實體參數](#entity-parameters) 以取得詳細資訊。 |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | 用於 [自訂分數](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) 活動目標。 |

{style=&quot;table-layout:auto&quot;}

## 自訂參數

必須以XDM資料的形式，以 `sendEvent` 命令。 請務必確保XDM結構包含Target實作所需的所有欄位。

at.js範例使用 `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "pageName": "product detail"
  };
};
```

平台網頁SDK JavaScript範例，使用 `sendEvent` 命令：

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        // Other attributes included according to xdm schema
        "name": "product detail"
      }
    }
  }
});
```

>[!TAB 標記]

在標籤中，請先使用 [!UICONTROL XDM物件] 要對應至XDM欄位的資料元素：

![對應至XDM物件資料元素中的XDM欄位](assets/params-tags-pageName.png){zoomable=&quot;yes&quot;}

然後加入您的 [!UICONTROL XDM物件] 在 [!UICONTROL 傳送事件] [!UICONTROL 動作] (多個 [!UICONTROL XDM物件] 可以 [合併](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![在「傳送」事件中包含XDM物件資料元素](assets/params-tags-sendEvent.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]


>[!NOTE]
>
>因為自訂mbox參數是 `xdm` 物件您需要更新任何對象、活動或設定檔指令碼，這些指令碼會使用這些mbox參數的新名稱來參考這些mbox參數。 請參閱 [更新Target受眾和設定檔指令碼，以便與Platform Web SDK相容](update-audiences.md) 以取得詳細資訊。


## 設定檔參數

必須在 `data.__adobe.target` Platform Web SDK中的物件 `sendEvent` 命令裝載。

與at.js類似，所有設定檔參數也必須加上前置詞 `profile.` 以正確儲存為永久Target設定檔屬性的值。 保留 `user.categoryId` Target的類別相關性功能參數會加上前置詞 `user.`.

at.js範例使用 `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "profile.gender": "male",
    "user.categoryId": "clothing"
  };
};
```

平台網頁SDK範例，使用 `sendEvent` 命令：

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "male",
        "user.categoryId": "clothing"
      }
    }
  }
});
```

>[!TAB 標記]

在標籤中，先建立資料元素以定義 `data.__adobe.target` 物件：

![在資料元素中定義資料物件](assets/params-tags-dataObject.png){zoomable=&quot;yes&quot;}

然後將您的資料物件加入 [!UICONTROL 傳送事件] [!UICONTROL 動作] (多個 [!UICONTROL 物件] 可以 [合併](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![在傳送事件中包含資料物件](assets/params-tags-sendEvent-withData.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

## 實體參數

實體參數可用來傳遞Target Recommendations的行為資料和補充目錄資訊。 全部 [實體參數](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) 平台網頁SDK也支援at.js。 與設定檔參數類似，所有實體參數應傳遞至 `data.__adobe.target` Platform Web SDK中的物件 `sendEvent` 命令裝載。

特定項目的實體參數必須加上前置詞 `entity.` 以正確擷取資料。 保留 `cartIds` 和 `excludedIds` recommendations演算法的參數不應加上前置詞，且每個的值必須包含以逗號分隔的實體ID清單。

at.js範例使用 `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "entity.id": "SKU-00001-LARGE",
    "entity.categoryId": "clothing,shirts",
    "entity.customEntity": "some value",
    "cartIds": "SKU-00002,SKU-00003",
    "excludedIds": "SKU-00001-SMALL"
  };
};
```

平台網頁SDK範例，使用 `sendEvent` 命令：

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts",
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL"
      }
    }
  }
});
```

>[!TAB 標記]

在標籤中，先建立資料元素以定義 `data.__adobe.target` 物件：

![在資料元素中定義資料物件](assets/params-tags-dataObject-entities.png){zoomable=&quot;yes&quot;}

然後將您的資料物件加入 [!UICONTROL 傳送事件] [!UICONTROL 動作] (多個 [!UICONTROL 物件] 可以 [合併](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![在傳送事件中包含資料物件](assets/params-tags-sendEvent-withData.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

>[!NOTE]
>
>若 `commerce` 欄位群組已使用，且 `productListItems` 陣列會包含在XDM裝載中，然後是第一個 `SKU` 此陣列中的值對應至 `entity.id` 以增加產品檢視。


## 購買參數

成功訂單後，購買參數會傳遞至訂單確認頁面，並用於目標轉換和最佳化目標。 透過Platform Web SDK實作，這些參數和會自動從作為 `commerce` 欄位群組。

at.js範例使用 `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "orderId": "ABC123",
    "productPurchasedId": "SKU-00002,SKU-00003"
    "orderTotal": 1337.89
  };
};
```

購買資訊會傳遞至Target，當 `commerce` 欄位組具有 `purchases.value` 設為 `1`. 訂單ID和訂單總計會自動從 `order` 物件。 若 `productListItems` 陣列存在，則 `SKU` 值用於 `productPurchasedId`.

平台網頁SDK範例，使用 `sendEvent` 命令：

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "ABC123",
        "priceTotal": 1337.89
      },
      "purchases": {
        "value": 1
      }
    },
    "productListItems": [{
      "SKU": "SKU-00002"
    }, {
      "SKU": "SKU-00003"
    }]
  }
});
```

>[!TAB 標記]

在標籤中，請先使用 [!UICONTROL XDM物件] 要對應至XDM欄位的資料元素：

![對應至XDM物件資料元素中的XDM欄位](assets/params-tags-purchase.png){zoomable=&quot;yes&quot;}

然後加入您的 [!UICONTROL XDM物件] 在 [!UICONTROL 傳送事件] [!UICONTROL 動作] (多個 [!UICONTROL XDM物件] 可以 [合併](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![在「傳送」事件中包含XDM物件資料元素](assets/params-tags-sendEvent-purchase.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]


>[!NOTE]
>
>此 `productPurchasedId` 值也可以以逗號分隔的實體ID清單形式，在 `data` 物件。


## 客戶Id(mbox3rdPartyId)

Target允許使用單一客戶ID跨裝置和系統進行設定檔同步。 透過at.js，此值可設為 `mbox3rdPartyId` ，或做為傳送至Experience CloudIdentity Service的第一個客戶ID。 不同於at.js，平台Web SDK實作可讓您指定要使用哪個客戶ID作為 `mbox3rdPartyId` 如果有多個。 例如，如果您的企業有全域客戶ID，且不同業務的客戶ID不同，您可以設定Target應使用的ID。

為Target跨裝置和客戶屬性使用案例設定ID同步有幾個步驟：

1. 建立 **[!UICONTROL 身分命名空間]** (針對 **[!UICONTROL 身分]** 資料收集或平台畫面
1. 請確定 **[!UICONTROL 別名]** 在「客戶屬性」中， **[!UICONTROL 身分符號]** 您的命名空間
1. 指定 **[!UICONTROL 標識符號]** 作為 **[!UICONTROL Target第三方ID命名空間]** 在資料流的Target設定中
1. 執行 `sendEvent` 命令 `identityMap` 欄位群組

at.js範例使用 `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "mbox3rdPartyId": "TT8675309"
  };
};
```

平台網頁SDK範例，使用 `sendEvent` 命令：

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "identityMap": {
      "GLOBAL_CUSTOMER_ID": [{
        "id": "TT8675309",
        "authenticatedState": "authenticated"
      }]
    }
  }
});
```

>[!TAB 標記]

此 [!UICONTROL ID] 值， [!UICONTROL 驗證狀態] 和 [!UICONTROL 命名空間] 擷取於 [!UICONTROL 身分對應] 資料元素：
![擷取客戶ID的「身分對應」資料元素](assets/params-tags-customerIdDataElement.png){zoomable=&quot;yes&quot;}

此 [!UICONTROL 身分對應] 之後，會使用資料元素來設定 [!UICONTROL identityMap] 欄位 [!UICONTROL XDM物件] 資料元素：
![XDM物件資料元素中使用的「身分對應」資料元素](assets/params-tags-customerIdInXDMObject.png){zoomable=&quot;yes&quot;}

此 [!UICONTROL XDM物件] 則會納入 [!UICONTROL 傳送事件] 規則的動作：

![在「傳送」事件中包含XDM物件資料元素](assets/params-tags-sendEvent-xdm.png){zoomable=&quot;yes&quot;}

在您資料流的Adobe Target服務中，請務必將 [!UICONTROL Target第三方ID命名空間] 至 [!UICONTROL 身分對應] 資料元素：
![在資料流中設定Target第三方ID命名空間](assets/params-tags-customerIdNamespaceInDatastream.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

## 平台Web SDK範例

現在您已了解使用Platform Web SDK對應不同Target參數的方式，我們的兩個範例頁面可從at.js移轉至Platform Web SDK，如下所示。 範例頁面包括：

- 非同步程式庫實作的Target預先隱藏程式碼片段
- Platform Web SDK基本程式碼
- Platform Web SDK JavaScript程式庫
- A `configure` 初始化庫的命令
- A `sendEvent` 命令來傳送資料並請求要呈現的Target內容

+++產品詳細資訊頁面上的Web SDK:

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>

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

  <!--Configure Platform Web SDK and send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "renderDecisions": true,
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated"
          }]
        },
        "web": {
          "webPageDetails": {
            // Other attributes included according to XDM schema
            "pageName": "product detail"
          }
        }
      },
      "data": {
        "__adobe": {
          "target": {
            "profile.gender": "male",
            "user.categoryId": "clothing",
            "entity.id": "SKU-00001-LARGE",
            "entity.categoryId": "clothing,shirts",
            "entity.customEntity": "some value",
            "cartIds": "SKU-00002,SKU-00003",
            "excludedIds": "SKU-00001-SMALL"
          }
        }
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```

+++

+++訂單確認頁面上的Web SDK:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>


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

  <!--Configure Platform Web SDK and send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated"
          }]
        },
        "commerce": {
          "order": {
            "purchaseID": "ABC123",
            "priceTotal": 1337.89
          },
          "purchases": {
            "value": 1
          }
        },
        "productListItems": [{
          "SKU": "SKU-00002"
        }, {
          "SKU": "SKU-00003"
        }]
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```

+++

接下來，學習如何 [追蹤Target轉換事件](track-events.md) 搭配Platform Web SDK。

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
