---
title: 傳送引數 — 將行動應用程式中的Adobe Target實作移轉至Adobe Journey Optimizer — 決策擴充功能
description: 瞭解如何使用Experience Platform Web SDK將mbox、設定檔和實體引數傳送至Adobe Target。
exl-id: 927d83f9-c019-4a6b-abef-21054ce0991b
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 1%

---

# 使用決策擴充功能將引數傳送至Target

由於應用程式架構、業務需求及所使用的功能，Target實施在行動應用程式間有所差異。 大部分的Target實作包括傳遞內容資訊、受眾和內容推薦的各種引數。

使用Target擴充功能時，所有的Target引數都是使用`TargetParameters`函式傳遞。

搭配決策擴充功能：

* 可在XDM物件中傳遞用於多個Adobe應用程式的引數
* 只能用於Target的引數可以在`data.__adobe.target`物件中傳遞


>[!IMPORTANT]
>
> 使用Decisioning擴充功能時，在要求中傳送的引數會套用至要求中的所有範圍。 如果您需要為不同的範圍設定不同的引數，則必須提出其他要求。

## 自訂引數

自訂mbox引數是傳遞資料至Target的最基本方式，可以在`xdm`或`data.__adobe.target`物件中傳遞。

## 輪廓參數

設定檔引數會將資料長時間儲存在使用者的Target設定檔中，且必須在`data.__adobe.target`物件中傳遞。

## 實體引數

[實體引數](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/entity-attributes)是用來傳遞Target Recommendations的行為資料和補充目錄資訊。 與設定檔引數類似，大部分實體引數應該在`data.__adobe.target`物件下傳遞。 唯一的例外是`xdm.productListItems`陣列存在，然後第一個`SKU`值會用作`entity.id`。

特定專案的實體引數必須以`entity.`為前置詞，才能正確擷取資料。 建議演演算法的保留`cartIds`和`excludedIds`引數不應加上前置詞，而且每個引數的值都必須包含以逗號分隔的實體ID清單。

## 購買引數

成功訂單後，購買引數會在訂單確認頁面上傳遞，並用於Target轉換和最佳化目標。 透過使用決策擴充功能的Platform Mobile SDK實作，這些引數和會自動從作為`commerce`欄位群組的一部分傳遞的XDM資料進行對應。

當`commerce`欄位群組將`purchases.value`設定為`1`時，購買資訊會傳遞至Target。 訂單識別碼與訂單總計會自動從`order`物件對應。 如果`productListItems`陣列存在，則`SKU`值會用於`productPurchasedId`。

如果您未在`xdm`物件中傳遞`commerce`欄位，您可以使用`data.__adobe.target.orderId`、`data.__adobe.target.orderTotal`和`data.__adobe.target.productPurchasedId`欄位將訂單詳細資料傳遞至目標。

## 客戶ID (mbox3rdPartyId)

Target允許使用單一客戶ID跨裝置和系統同步設定檔。 此客戶ID應在XDM物件的`identityMap`欄位中傳遞，並對應至資料流中的目標協力廠商ID欄位。

## 表格

| at.js引數範例 | Platform Web SDK選項 | 附註 |
| --- | --- | --- |
| `at_property` | 不適用 | 屬性Token是在[資料流](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure#target)中設定，無法在`sendEvent`呼叫中設定。 |
| `pageName` | `xdm.web.webPageDetails.name`或<br> `data.__adobe.target.pageName` | 目標mbox引數可以做為`xdm`物件的一部分或`data.__adobe.target`物件的一部分來傳遞。 |
| `profile.gender` | `data.__adobe.target.profile.gender` | 所有Target設定檔引數都必須作為`data`物件的一部分傳遞，且前置詞為`profile.`才能正確對應。 |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | 用於目標類別相關性功能的保留引數，必須作為`data`物件的一部分傳遞。 |
| `entity.id` | `data.__adobe.target.entity.id` <br>或<br> `xdm.productListItems[0].SKU` | 實體ID可用於Target Recommendations行為計數器。 這些實體ID可以作為`data`物件的一部分傳遞，或者如果您的實作使用該欄位群組，則會自動從`xdm.productListItems`陣列中的第一個專案進行對應。 |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | 實體類別ID可作為`data`物件的一部分傳遞。 |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | 自訂實體引數用於更新Recommendations產品目錄。 這些自訂引數必須作為`data`物件的一部分傳遞。 |
| `cartIds` | `data.__adobe.target.cartIds` | 用於Target的購物車型建議演演算法。 |
| `excludedIds` | `data.__adobe.target.excludedIds` | 用來防止特定實體ID在建議設計中傳回。 |
| `mbox3rdPartyId` | 在`xdm.identityMap`物件中設定 | 用於跨裝置和客戶屬性同步Target設定檔。 必須在資料流](https://experienceleague.adobe.com/en/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid)的[Target設定中指定用於客戶ID的名稱空間。 |
| `orderId` | `xdm.commerce.order.purchaseID`<br> （當`commerce.purchases.value`設定為`1`）<br>或<br> `data.__adobe.target.orderId` | 用於識別Target轉換追蹤的唯一訂單。 |
| `orderTotal` | `xdm.commerce.order.priceTotal`<br> （當`commerce.purchases.value`設定為`1`）<br>或<br> `data.__adobe.target.orderTotal` | 用於追蹤Target轉換和最佳化目標的訂單總計。 |
| `productPurchasedId` | `xdm.productListItems[0-n].SKU`<br> （當`commerce.purchases.value`設定為`1`時） <br>或<br> `data.__adobe.target.productPurchasedId` | 用於Target轉換追蹤和建議演演算法。 |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | 用於[自訂評分](https://experienceleague.adobe.com/en/docs/target/using/activities/success-metrics/capture-score)活動目標。 |

{style="table-layout:auto"}


## 傳遞引數的範例

以簡單範例說明將引數傳遞至Target時，擴充功能之間的差異。

### Android

>[!BEGINTABS]

>[!TAB 最佳化SDK]

```Java
final Map<String, Object> data = new HashMap<>();
final Map<String, String> targetParameters = new HashMap<>();
 
// Mbox parameters
targetParameters.put("status", "platinum");
 
// Profile parameters - prefix with profile.
targetParameters.put("profile.gender", "male");
 
// Product parameters
targetParameters.put("productId", "pId1");
targetParameters.put("categoryId", "cId1");
 
// Order parameters
targetParameters.put("orderId", "id1");
targetParameters.put("orderTotal", "1.0");
targetParameters.put("purchasedProductIds", "ppId1");
 
data.put("__adobe", new HashMap<String, Object>() {
  {
    put("target", targetParameters);
  }
});
 
// Target location (or mbox)
final DecisionScope decisionScope = DecisionScope("myTargetLocation")
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope);
 
Optimize.updatePropositions(decisionScopes, null, data);
```

>[!TAB 目標SDK]

```Java
Map<String, String> mboxParameters = new HashMap<String, String>();
mboxParameters1.put("status", "platinum");
 
Map<String, String> profileParameters = new HashMap<String, String>();
profileParameters1.put("gender", "male");
 
List<String> purchasedProductIds = new ArrayList<String>();
purchasedProductIds.add("ppId1");
TargetOrder targetOrder = new TargetOrder("id1", 1.0, purchasedProductIds);
 
TargetProduct targetProduct = new TargetProduct("pId1", "cId1");
 
TargetParameters targetParameters = new TargetParameters.Builder()
                                    .parameters(mboxParameters)
                                    .profileParameters(profileParameters)
                                    .product(targetProduct)
                                    .order(targetOrder)
                                    .build();
```

>[!ENDTABS]

### iOS

>[!BEGINTABS]

>[!TAB 最佳化SDK]

```Swift
var data: [String: Any] = [:]
var targetParameters: [String: String] = [:]
 
// Mbox parameters
targetParameters["status"] = "platinum"
 
// Profile parameters - prefix with profile.
targetParameters["profile.gender"] = "make"
 
// Product parameters
targetParameters["productId"] = "pId1"
targetParameters["categoryId"] = "cId1"
 
// Add order parameters
targetParameters["orderId"] = "id1"
targetParameters["orderTotal"] = "1.0"
targetParameters["purchasedProductIds"] = "ppId1"
 
data["__adobe"] = [
  "target": targetParameters
]
 
// Target location (or mbox)
let decisionScope = DecisionScope(name: "myTargetLocation")
Optimize.updatePropositions(for: [decisionScope] withXdm: nil andData: data)
```

>[!TAB 目標SDK]

```Swift
let mboxParameters = [
                        "status": "platinum"
                     ]
 
let profileParameters = [
                            "gender": "male"
                        ]
 
let order = TargetOrder(id: "id1", total: 1.0, purchasedProductIds: ["ppId1"])
 
let product = TargetProduct(productId: "pId1", categoryId: "cId1")
 
let targetParameters = TargetParameters(parameters: mboxParameters, profileParameters: profileParameters, order: order, product: product))
```


>[!ENDTABS]






接下來，瞭解如何使用Platform Web SDK [追蹤Target轉換事件](track-events.md)。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625)中張貼以告知我們。
