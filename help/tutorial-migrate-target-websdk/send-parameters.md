---
title: 傳送引數 — 將Target從at.js 2.x移轉至Web SDK
description: 瞭解如何使用Experience PlatformWeb SDK將mbox、設定檔和實體引數傳送至Adobe Target。
exl-id: 7916497b-0078-4651-91b1-f53c86dd2100
source-git-commit: f30d6434be69e87406326955b3821d07bd2e66c1
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# 使用Platform Web SDK傳送引數至Target

由於網站架構、業務需求及使用的功能，Target實施在各網站間會有所不同。 大部分的Target實作包括傳遞內容資訊、受眾和內容推薦的各種引數。

讓我們使用簡單的產品詳細資訊頁面和訂單確認頁面，示範將引數傳遞至Target時程式庫之間的差異。

假設以下兩個使用at.js的範例頁面：

「產品詳細資料」頁面上的+++at.js：

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


+++「訂單確認」頁面上的at.js：

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


## 引數對應摘要

這些頁面的Target引數會使用Platform Web SDK以不同方式傳送。 有多種方式可使用at.js將引數傳遞至Target：

- 針對頁面載入事件使用`targetPageParams()`函式設定（用於此頁面的範例）
- 針對頁面上的所有Target要求使用`targetPageParamsAll()`函式設定
- 直接使用單一位置的`getOffer()`函式傳送引數
- 直接與一或多個位置的`getOffers()`函式一起傳送引數


Platform Web SDK提供單一一致的方式來傳送資料，而不需要額外的函式。 所有引數必須使用`sendEvent`命令在承載中傳遞，且屬於兩個類別：

- 自動從`xdm`物件對應
- 使用`data.__adobe.target`物件手動傳遞

下表概述範例引數如何使用Platform Web SDK重新對應：

| at.js引數範例 | Platform Web SDK選項 | 附註 |
| --- | --- | --- |
| `at_property` | 不適用 | 屬性Token是在[資料流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target)中設定，無法在`sendEvent`呼叫中設定。 |
| `pageName` | `xdm.web.webPageDetails.name` | 所有Target mbox引數都必須作為`xdm`物件的一部分傳遞，並符合使用XDM ExperienceEvent類別的結構描述。 Mbox引數無法當作`data`物件的一部分傳遞。 |
| `profile.gender` | `data.__adobe.target.profile.gender` | 所有Target設定檔引數都必須作為`data`物件的一部分傳遞，且前置詞為`profile.`才能正確對應。 |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | 用於目標類別相關性功能的保留引數，必須作為`data`物件的一部分傳遞。 |
| `entity.id` | `data.__adobe.target.entity.id` <br>或<br> `xdm.productListItems[0].SKU` | 實體ID可用於Target Recommendations行為計數器。 這些實體ID可以作為`data`物件的一部分傳遞，或者如果您的實作使用該欄位群組，則會自動從`xdm.productListItems`陣列中的第一個專案進行對應。 |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | 實體類別ID可作為`data`物件的一部分傳遞。 |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | 自訂實體引數可用來更新Recommendations產品目錄。 這些自訂引數必須作為`data`物件的一部分傳遞。 |
| `cartIds` | `data.__adobe.target.cartIds` | 用於Target的購物車型建議演演算法。 |
| `excludedIds` | `data.__adobe.target.excludedIds` | 用來防止特定實體ID在建議設計中傳回。 |
| `mbox3rdPartyId` | 在`xdm.identityMap`物件中設定 | 用於跨裝置和客戶屬性同步Target設定檔。 必須在資料流](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html)的[Target設定中指定用於客戶ID的名稱空間。 |
| `orderId` | `xdm.commerce.order.purchaseID` | 用於識別Target轉換追蹤的唯一訂單。 |
| `orderTotal` | `xdm.commerce.order.priceTotal` | 用於追蹤Target轉換和最佳化目標的訂單總計。 |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>或<br> `xdm.productListItems[0-n].SKU` | 用於Target轉換追蹤和建議演演算法。 如需詳細資訊，請參閱下方的[實體引數](#entity-parameters)區段。 |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | 用於[自訂評分](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html)活動目標。 |

{style="table-layout:auto"}

## 自訂引數

自訂mbox引數必須以XDM資料搭配`sendEvent`命令傳遞。 請務必確保XDM結構描述包含Target實作所需的所有欄位。

使用`targetPageParams()`的at.js範例：

```JavaScript
targetPageParams = function() {
  return {
    "pageName": "product detail"
  };
};
```

使用`sendEvent`命令的Platform Web SDK JavaScript範例：

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

在標籤中，請先使用[!UICONTROL XDM物件]資料元素來對應至XDM欄位：

![對應到XDM物件資料元素中的XDM欄位](assets/params-tags-pageName.png){zoomable="yes"}

然後將您的[!UICONTROL XDM物件]加入您的[!UICONTROL 傳送事件] [!UICONTROL 動作] （多個[!UICONTROL XDM物件]可以[合併](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)）：

![在傳送事件中包含XDM物件資料元素](assets/params-tags-sendEvent.png){zoomable="yes"}

>[!ENDTABS]


>[!NOTE]
>
>由於自訂mbox引數是`xdm`物件的一部分，因此您需要使用新的名稱更新任何參照這些mbox引數的對象、活動或設定檔指令碼。 如需詳細資訊，請參閱本教學課程的[更新Target對象和設定檔指令碼以瞭解Platform Web SDK相容性](update-audiences.md)頁面。


## 輪廓參數

目標設定檔引數必須傳遞到Platform Web SDK `sendEvent`命令承載中的`data.__adobe.target`物件下。

與at.js類似，所有設定檔引數也必須加上`profile.`前置詞，值才能正確儲存為永久Target設定檔屬性。 目標類別相關性功能的保留`user.categoryId`引數會加上前置詞`user.`。

使用`targetPageParams()`的at.js範例：

```JavaScript
targetPageParams = function() {
  return {
    "profile.gender": "male",
    "user.categoryId": "clothing"
  };
};
```

使用`sendEvent`命令的平台Web SDK範例：

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

在標籤中，請先建立資料元素以定義`data.__adobe.target`物件：

![在資料元素中定義您的資料物件](assets/params-tags-dataObject.png){zoomable="yes"}

然後將您的資料物件加入您的[!UICONTROL 傳送事件] [!UICONTROL 動作] （多個[!UICONTROL 物件]可以[合併](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)）：

![在傳送事件中包含資料物件](assets/params-tags-sendEvent-withData.png){zoomable="yes"}

>[!ENDTABS]

## 實體引數

實體引數可用來傳遞行為資料和Target Recommendations的補充目錄資訊。 at.js支援的所有[實體引數](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html)也受Platform Web SDK支援。 與設定檔引數類似，所有實體引數都應在Platform Web SDK `sendEvent`命令承載中的`data.__adobe.target`物件下傳遞。

特定專案的實體引數必須以`entity.`為前置詞，才能正確擷取資料。 建議演演算法的保留`cartIds`和`excludedIds`引數不應加上前置詞，而且每個引數的值都必須包含以逗號分隔的實體ID清單。

使用`targetPageParams()`的at.js範例：

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

使用`sendEvent`命令的平台Web SDK範例：

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

在標籤中，請先建立資料元素以定義`data.__adobe.target`物件：

![在資料元素中定義您的資料物件](assets/params-tags-dataObject-entities.png){zoomable="yes"}

然後將您的資料物件加入您的[!UICONTROL 傳送事件] [!UICONTROL 動作] （多個[!UICONTROL 物件]可以[合併](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)）：

![在傳送事件中包含資料物件](assets/params-tags-sendEvent-withData.png){zoomable="yes"}

>[!ENDTABS]

>[!NOTE]
>
>如果使用`commerce`欄位群組，且XDM裝載中包含`productListItems`陣列，則此陣列中的第一個`SKU`值對應至`entity.id`，以遞增產品檢視。


## 購買引數

成功訂單後，購買引數會在訂單確認頁面上傳遞，並用於Target轉換和最佳化目標。 透過Platform Web SDK實作，這些引數和會自動從作為`commerce`欄位群組的一部分傳遞的XDM資料進行對應。

使用`targetPageParams()`的at.js範例：

```JavaScript
targetPageParams = function() {
  return {
    "orderId": "ABC123",
    "productPurchasedId": "SKU-00002,SKU-00003"
    "orderTotal": 1337.89
  };
};
```

當`commerce`欄位群組將`purchases.value`設定為`1`時，購買資訊會傳遞至Target。 訂單識別碼與訂單總計會自動從`order`物件對應。 如果`productListItems`陣列存在，則`SKU`值會用於`productPurchasedId`。

使用`sendEvent`的平台Web SDK範例：

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
    }],
      "_experience": {
          "decisioning": {
              "propositions": [{
                  "scope": "<your_mbox>"
              }],
              "propositionEventType": {
                  "display": 1
              }
          }
      }
  }
});
```

>[!TAB 標記]

在標籤中，請先使用[!UICONTROL XDM物件]資料元素來對應到必要的XDM欄位(請參閱JavaScript範例)和選用的自訂範圍：

![對應到XDM物件資料元素中的XDM欄位](assets/params-tags-purchase.png){zoomable="yes"}

然後將您的[!UICONTROL XDM物件]加入您的[!UICONTROL 傳送事件] [!UICONTROL 動作] （多個[!UICONTROL XDM物件]可以[合併](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)）：

![在傳送事件中包含XDM物件資料元素](assets/params-tags-sendEvent-purchase.png){zoomable="yes"}

>[!ENDTABS]

>[!IMPORTANT]
>
> `_experience.decisioning.propositionEventType`必須設定為`display: 1`，才能使用呼叫來遞增Target量度。

>[!NOTE]
>
> 如果您想要在Target量度定義中使用自訂位置/mbox名稱（例如`orderConfirmPage`），請以如上範例中的自訂範圍填入`_experience.decisioning.propositions`陣列。

>[!NOTE]
>
>`productPurchasedId`值也可作為`data`物件下以逗號分隔的實體ID清單傳遞。


## 客戶ID (mbox3rdPartyId)

Target允許使用單一客戶ID跨裝置和系統同步設定檔。 使用at.js時，可將此值設定為Target請求中的`mbox3rdPartyId`，或設定為第一個傳送至Experience CloudIdentity Service的客戶ID。 不像at.js，Platform Web SDK實作可讓您指定在有多個`mbox3rdPartyId`時使用哪個客戶ID。 例如，如果您的企業擁有全域客戶ID，以及不同業務線的個別客戶ID，您可以設定Target應使用哪個ID。

針對Target跨裝置和客戶屬性使用案例設定ID同步的步驟如下：

1. 為Data Collection或Platform的&#x200B;**[!UICONTROL 身分]**&#x200B;畫面中的客戶ID建立&#x200B;**[!UICONTROL 身分名稱空間]**
1. 請確定客戶屬性中的&#x200B;**[!UICONTROL 別名]**&#x200B;符合您名稱空間中的&#x200B;**[!UICONTROL 身分符號]**
1. 在資料串流的Target設定中，將&#x200B;**[!UICONTROL 身分符號]**&#x200B;指定為&#x200B;**[!UICONTROL 目標第三方ID名稱空間]**
1. 使用`identityMap`欄位群組執行`sendEvent`命令

使用`targetPageParams()`的at.js範例：

```JavaScript
targetPageParams = function() {
  return {
    "mbox3rdPartyId": "TT8675309"
  };
};
```

使用`sendEvent`命令的平台Web SDK範例：

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "identityMap": {
      "GLOBAL_CUSTOMER_ID": [{
        "id": "TT8675309",
        "authenticatedState": "authenticated",
        "primary": true
      }]
    }
  }
});
```

>[!TAB 標記]

[!UICONTROL ID]值、[!UICONTROL 已驗證狀態]和[!UICONTROL 名稱空間]已擷取至[!UICONTROL 身分對應]資料元素：
![擷取客戶ID的身分對應資料元素](assets/params-tags-customerIdDataElement.png){zoomable="yes"}

然後會使用[!UICONTROL 身分對應]資料元素來設定[!UICONTROL XDM物件]資料元素中的[!UICONTROL identityMap]欄位：
![用於XDM物件資料元素中的身分對應資料元素](assets/params-tags-customerIdInXDMObject.png){zoomable="yes"}

然後[!UICONTROL XDM物件]會包含在規則的[!UICONTROL 傳送事件]動作中：

![在傳送事件中包含XDM物件資料元素](assets/params-tags-sendEvent-xdm.png){zoomable="yes"}

在您的資料串流的Adobe Target服務中，請務必將[!UICONTROL Target第三方ID名稱空間]設定為[!UICONTROL 身分對應]資料元素中使用的相同名稱空間：
![在資料流中設定目標第三方ID名稱空間](assets/params-tags-customerIdNamespaceInDatastream.png){zoomable="yes"}

>[!ENDTABS]

>[!NOTE]
>
> Adobe建議將代表個人的名稱空間（例如已驗證的身分）傳送為主要身分。



## 平台Web SDK範例

現在您已瞭解如何使用Platform Web SDK對應不同的Target引數，例如可以將兩個範例頁面從at.js移轉至Platform Web SDK，如下所示。 範例頁面包含下列專案：

- 非同步程式庫實作的Target預先隱藏程式碼片段
- Platform Web SDK基底程式碼
- Platform Web SDK JavaScript資料庫
- 初始化程式庫的`configure`命令
- 傳送資料並要求轉譯Target內容的`sendEvent`命令

+++產品詳細資料頁面上的Web SDK：

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
            "authenticatedState": "authenticated",
            "primary": true
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

+++訂單確認頁面上的Web SDK：

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
            "authenticatedState": "authenticated",
            "primary": true
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
        }],
        "_experience": {
            "decisioning": {
                "propositions": [{
                    "scope": "<your_mbox>"
                }],
                "propositionEventType": {
                    "display": 1
                }
            }
        }
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

接下來，瞭解如何使用Platform Web SDK [追蹤Target轉換事件](track-events.md)。

>[!NOTE]
>
>我們致力協助您成功將Target從at.js移轉至Web SDK。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
