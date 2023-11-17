---
title: 活動
description: 瞭解如何收集行動應用程式中的事件資料。
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 1%

---

# 活動

瞭解如何追蹤行動應用程式中的事件。

>[!INFO]
>
> 在2023年11月下旬，此教學課程將由使用新範例行動應用程式的新教學課程取代

Edge Network擴充功能提供API，可將Experience事件傳送至Platform Edge Network。 體驗事件是包含符合XDM ExperienceEvent結構描述定義的資料的物件。 更簡單地說，這類功能可擷取使用者在您的行動應用程式中的動作。 Platform Edge Network收到資料後，即可將其轉送至資料流中設定的應用程式和服務，例如Adobe Analytics和Experience Platform。 進一步瞭解 [體驗事件](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) 產品檔案內。

## 先決條件

* 更新PodFile及必要的SDK。
* AppDelegate中註冊的擴充功能。
* 已將MobileCore設定為使用您的開發AppId。
* 匯入的SDK。
* 使用上述變更成功建置並執行應用程式。

## 學習目標

在本課程中，您將會：

* 瞭解如何根據結構描述來建構XDM資料。
* 根據標準欄位群組傳送XDM事件。
* 根據自訂欄位群組傳送XDM事件。
* 傳送XDM購買事件。
* 使用保證進行驗證。

## 建構體驗事件

Adobe Experience Platform Edge擴充功能可傳送遵循先前定義XDM結構描述的事件至Adobe Experience Platform Edge Network。

程式如下……

1. 識別您嘗試追蹤的行動應用程式互動。

1. 檢閱您的結構並識別適當的事件。

1. 檢閱您的結構描述，並識別應用於描述事件的任何其他欄位。

1. 建構並填入資料物件。

1. 建立並傳送事件。

1. 驗證.

讓我們來看看幾個範例。

### 範例#1 — 標準欄位群組

檢閱以下範例，而不嘗試在範例應用程式中實作：

1. 在您的結構描述中，識別您嘗試收集的事件，在此範例中，我們追蹤產品檢視。
   ![產品檢視結構描述](assets/mobile-datacollection-prodView-schema.png)

1. 開始建構物件：

   ```swift
   var xdmData: [String: Any] = [
       "eventType": "commerce.productViews",
       "commerce": [
           "productViews": [
           "value": 1
           ]
       ]
   ]
   ```

   * eventType：說明已發生的事件，請使用 [已知值](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) 可能的話。
   * commerce.productViews.value：提供事件的數值。 如果是布林值(或Adobe Analytics中的「計數器」)，此值一律為1。 如果是數值或貨幣事件，值可以是> 1。

1. 在您的結構描述中，識別與該事件相關聯的任何其他資料。 在此範例中，包括 `productListItems` 這是一組用於商務相關事件的標準欄位：
   ![產品清單專案結構描述](assets/mobile-datacollection-prodListItems-schema.png)
   * 請注意 `productListItems` 是一個陣列，因此可提供多個產品。

1. 展開您的xdmData物件以包含補充資料：

   ```swift
   var xdmData: [String: Any] = [
       "eventType": "commerce.productViews",
           "commerce": [
           "productViews": [
               "value": 1
           ]
       ],
       "productListItems": [
           [
               "name":  productName,
               "SKU": sku,
               "priceTotal": priceString,
               "quantity": 1
           ]
       ]
   ]
   ```

1. 使用資料結構來建立 `ExperienceEvent`：

   ```swift
   let productViewEvent = ExperienceEvent(xdm: xdmData)
   ```

1. 將事件和資料傳送至Platform Edge Network：

   ```swift
   Edge.sendEvent(experienceEvent: productViewEvent)
   ```

### 範例#2 — 自訂欄位群組

檢閱以下範例，而不嘗試在範例應用程式中實作：

1. 在您的結構描述中，識別您嘗試收集的事件。 在此範例中，追蹤包含應用程式動作事件和名稱的「應用程式互動」。
   ![應用程式互動結構描述](assets/mobile-datacollection-appInteraction-schema.png)

1. 開始建構物件。

   >[!NOTE]
   >
   >  標準欄位群組一律以物件根目錄開始。
   >
   >  自訂欄位群組一律以Experience Cloud組織專屬的物件開頭，在本範例中為「_techmarketingdemos」。

   ```swift
   var xdmData: [String: Any] = [
   "_techmarketingdemos": [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
                   ]
               ]
           ]
       ]
   ]
   ```

   或者……

   ```swift
   var xdmData: [String: Any] = [:]
   xdmData["_techmarketingdemos"] = [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
               ]
           ]
       ]
   ]
   ```

1. 使用資料結構來建立 `ExperienceEvent`.

   ```swift
   let appInteractionEvent = ExperienceEvent(xdm: xdmData)
   ```

1. 將事件和資料傳送至Platform Edge Network。

   ```swift
   Edge.sendEvent(experienceEvent: appInteractionEvent)
   ```

### 新增畫面檢視追蹤至Luma應用程式

以上範例有望說明建構XDM資料物件時的思維程式。 接下來，我們將在Luma應用程式中新增畫面檢視追蹤。

1. 導覽至 `Home.swift`。
1. 將下列程式碼新增至 `viewDidAppear(...)`.

   ```swift
           let stateName = "luma: content: ios: us: en: home"
           var xdmData: [String: Any] = [:]
           //Page View
           xdmData["_techmarketingdemos"] = [
               "appInformation": [
                   "appStateDetails": [
                       "screenType": "App",
                       "screenName": stateName,
                       "screenView": [
                           "value": 1
                       ]
                   ]
               ]
           ]
           let experienceEvent = ExperienceEvent(xdm: xdmData)
           Edge.sendEvent(experienceEvent: experienceEvent)
   ```

1. 對應用程式中的每個畫面重複執行，正在更新 `stateName` 隨時待命。



### 驗證

1. 檢閱 [設定指示](assurance.md) 區段並將模擬器或裝置連線至Assurance。
1. 執行動作並尋找 `hitReceived` 來自的事件 `com.adobe.edge.konductor` 廠商。
1. 選取事件並檢閱中的XDM資料 `messages` 物件。
   ![資料彙集驗證](assets/mobile-datacollection-validation.png)

### 範例#3 — 購買

在此範例中，假設使用者已成功進行下列購買：

* 產品#1 — 瑜伽墊。
   * $49.99 x1
   * SKU：5829
* 產品#2 — 水瓶。
   * $10.00 x3
   * SKU： 9841
* 訂單總計：$79.99
* 唯一訂單Id：298234720
* 付款型別：Visa信用卡
* 唯一付款交易識別碼： 847361

#### 綱要

以下是要使用的相關結構描述欄位：

* eventType： &quot;commerce.purchases&quot;
* commerce.purchases
* commerce.order
* productsListItems
* _techmarketingdemos.appStateDetails （自訂）

>[!TIP]
>
>自訂欄位群組一律放置在您的Experience Cloud組織識別碼下。
>
>「_techmarketingdemos」已取代為您組織的唯一值。

![購買結構描述](assets/mobile-datacollection-purchase-schema.png)


#### 程式碼

以下說明在應用程式中建構及傳送XDM物件的方式。

```swift
let stateName = "luma: content: ios: us: en: orderconfirmation"
let currencyCode = "USD"
let orderTotal = "79.99"
let paymentType = "Visa Credit Card"
let orderId = "298234720"
let paymentTransactionId = "847361"
var xdmData: [String: Any] = [
  "eventType": "commerce.purchases",
  "commerce": [
    "purchases": [
      "value": 1
    ],
    "order": [
      "currencyCode": currencyCode,
      "priceTotal": orderTotal,
      "purchaseID": orderId,
      "purchaseOrderNumber": orderId,
      "payments": [ //Assuming only 1 payment type is used
        [
          "currencyCode": currencyCode,
          "paymentAmount": orderTotal,
          "paymentType": paymentType,
          "transactionID": paymentTransactionId
        ]
      ]
    ]
  ],
  "productListItems": [
      [
          "name":  "Yoga Mat",
          "SKU": "5829",
          "priceTotal": "49.99",
          "quantity": 1
      ],
      [
        "name":  "Water Bottle",
        "SKU": "9841",
        "priceTotal": "30.00",
        "quantity": 3
      ]
  ]
]

//Custom field group
xdmData["_techmarketingdemos"] = [
  "appInformation": [
    "appStateDetails": [
      "screenType": "App",
      "screenName": stateName,
      "screenView": [
        "value": 1
      ]
    ]
  ]
]
let experienceEvent = ExperienceEvent(xdm: xdmData)
Edge.sendEvent(experienceEvent: experienceEvent)
```

>[!NOTE]
>
>為清楚起見，所有值皆為硬式編碼。 在真實世界情況中，值會以動態方式填入。


### Luma應用程式中的實作

您應該有所有的工具，以便開始將資料收集新增至Luma範例應用程式。 以下是您可以遵循的假設追蹤需求清單。

* 追蹤每個畫面檢視。
   * 結構描述欄位： screenType、screenName、screenView
* 追蹤非商業動作。
   * 結構描述欄位： appInteraction.name， appAction
* 商務動作：
   * 產品頁面：產品檢視
   * 加入購物車： productListAdds
   * 從購物車移除： productListRemovals
   * 開始結帳：結帳
   * 檢視購物車： productListViews
   * 新增至願望清單： saveForLaters
   * 購買：購買、訂購

>[!TIP]
>
>檢閱 [完整實施的應用程式](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) 以取得更多範例。

### 驗證

1. 檢閱 [設定指示](assurance.md) 區段並將模擬器或裝置連線至Assurance。

1. 執行動作並尋找 `hitReceived` 來自的事件 `com.adobe.edge.konductor` 廠商。

1. 選取事件並檢閱中的XDM資料 `messages` 物件。
   ![資料彙集驗證](assets/mobile-datacollection-validation.png)

## 將事件傳送至Analytics和Platform

現在您已收集事件並傳送至Platform Edge Network，系統會將它們傳送至中設定的應用程式和服務。 [資料流](create-datastream.md). 在稍後的課程中，您會將此資料對應至 [Adobe Analytics](analytics.md) 和 [Adobe Experience Platform](platform.md).

下一步： **[網頁檢視](web-views.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)