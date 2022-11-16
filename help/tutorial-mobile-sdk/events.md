---
title: 活動
description: 了解如何在行動應用程式中收集事件資料。
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# 活動

了解如何在行動應用程式中追蹤事件。

Edge Network擴充功能提供API，可將體驗事件傳送至Platform Edge Network。 「體驗事件」是物件，其中包含符合XDM ExperienceEvent架構定義的資料。 更簡單地說，它們會擷取使用者在您行動應用程式中的行為。 Platform Edge Network收到資料後，即可將其轉送至您資料流中設定的應用程式和服務，例如Adobe Analytics和Experience Platform。 深入了解 [體驗事件](https://aep-sdks.gitbook.io/docs/getting-started/initialize-the-sdk) 在產品檔案中。

## 先決條件

* 以必要的SDK更新PodFile。
* 在AppDelegate中註冊的擴充功能。
* 已設定MobileCore以使用您的開發AppId。
* 匯入的SDK。
* 已成功建置並運行應用程式，並進行了上述更改。

## 學習目標

在本課程中，您將：

* 了解如何根據結構來建構XDM資料。
* 根據標準欄位群組傳送XDM事件。
* 根據自訂欄位群組傳送XDM事件。
* 傳送XDM購買事件。
* 有保證地驗證。

## 建構體驗事件

Adobe Experience Platform Edge擴充功能可將遵循先前定義之XDM架構的事件傳送至Adobe Experience Platform Edge Network。

過程是這樣……

1. 識別您嘗試追蹤的行動應用程式互動。

1. 檢閱您的結構並識別適當的事件。

1. 檢閱您的結構，並識別應用來說明事件的任何其他欄位。

1. 建構並填入資料物件。

1. 建立和傳送事件。

1. 驗證.

讓我們看幾個例子。

### 範例#1 — 標準欄位群組

檢閱下列範例，而不嘗試在範例應用程式中實施：

1. 在您的結構中，識別您嘗試收集的事件，在此範例中，我們會追蹤產品檢視。
   ![產品檢視綱要](assets/mobile-datacollection-prodView-schema.png)

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

   * eventType:說明發生的事件，請使用 [已知值](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) 當然。
   * commerce.productViews.value:提供事件的數值。 如果是布林值(或Adobe Analytics中的「計數器」)，則值一律為1。 如果是數值或貨幣事件，值可能大於1。

1. 在您的結構中，識別與事件相關聯的任何其他資料。 在此範例中，包括 `productListItems` 這是與商務相關事件搭配使用的標準欄位集：
   ![產品清單項目綱要](assets/mobile-datacollection-prodListItems-schema.png)
   * 請注意 `productListItems` 是陣列，因此可提供多個產品。

1. 展開xdmData物件以包含補充資料：

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

1. 使用資料結構來建立 `ExperienceEvent`:

   ```swift
   let productViewEvent = ExperienceEvent(xdm: xdmData)
   ```

1. 將事件和資料傳送至Platform Edge Network:

   ```swift
   Edge.sendEvent(experienceEvent: productViewEvent)
   ```

### 範例#2 — 自訂欄位群組

檢閱下列範例，而不嘗試在範例應用程式中實施：

1. 在您的結構中，識別您嘗試收集的事件。 在此範例中，追蹤「應用程式互動」，此互動包含應用程式動作事件和名稱。
   ![應用程式互動綱要](assets/mobile-datacollection-appInteraction-schema.png)

1. 開始建構物件。

   >[!NOTE]
   >
   >  標準欄位組始終在對象根中開始。
   >
   >  自訂欄位群組一律從您Experience Cloud組織「_techmarketingdemos」中唯一的物件開始。

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

### 將畫面檢視追蹤新增至Luma應用程式

上述例子有望說明構建XDM資料對象時的思路。 接下來，我們將在Luma應用程式中新增畫面檢視追蹤。

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

1. 對應用程式中的每個畫面重複，並更新 `stateName` 隨你。



### 驗證

1. 檢閱 [安裝指示](assurance.md) 區段，並將您的模擬器或裝置連線至「保證」。
1. 執行動作並尋找 `hitReceived` 來自 `com.adobe.edge.konductor` 供應商。
1. 選取事件並檢閱 `messages` 物件。
   ![資料收集驗證](assets/mobile-datacollection-validation.png)

### 範例#3 — 購買

在此範例中，假設使用者成功進行了下列購買：

* 產品#1 — 瑜伽墊。
   * $49.99 x1
   * SKU:5829
* 產品#2 — 水瓶。
   * $10.00 x3
   * SKU:9841
* 訂購總計：US$79.99
* 唯一訂單Id:298234720
* 付款類型：Visa信用卡
* 不重複付款交易標識：847361

#### 方案

以下是要使用的相關架構欄位：

* eventType:&quot;commerce.purchases&quot;
* commerce.purchases
* commerce.order
* productsListItems
* _techmarketingdemos.appStateDetails（自訂）

>[!TIP]
>
>自訂欄位群組一律放在您的Experience Cloud組織識別碼下。
>
>「_techmarketingdemos」會取代為您組織的唯一值。

![購買方案](assets/mobile-datacollection-purchase-schema.png)


#### 程式碼

以下說明如何在應用程式中建構和傳送XDM物件。

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
>為了清楚起見，所有值都以硬式編碼撰寫。 在現實情況中，值會動態填入。


### 在Luma應用程式中實作

您應該有所有工具可以開始將資料收集新增至Luma範例應用程式。 以下是您可遵循的假設追蹤需求清單。

* 追蹤每個畫面檢視。
   * 結構欄位：screenType, screenName, screenView
* 追蹤非商務動作。
   * 結構欄位：appInteraction.name, appAction
* 商務動作：
   * 產品頁面：productViews
   * 添加到購物車：productListAdds
   * 從購物車中移除：productListRemovements
   * 開始結帳：結帳
   * 查看購物車：productListViews
   * 添加到願望清單：saveForLaters
   * 購買：購買，訂購

>[!TIP]
>
>檢閱 [完整實作的應用程式](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) 以取得更多範例。

### 驗證

1. 檢閱 [安裝指示](assurance.md) 區段，並將您的模擬器或裝置連線至「保證」。

1. 執行動作並尋找 `hitReceived` 來自 `com.adobe.edge.konductor` 供應商。

1. 選取事件並檢閱 `messages` 物件。
   ![資料收集驗證](assets/mobile-datacollection-validation.png)

## 將事件傳送至Analytics和Platform

現在您已收集事件並將其傳送至Platform Edge Network，系統就會將它們傳送至您 [資料流](create-datastream.md). 在稍後的課程中，您會將此資料對應至 [Adobe Analytics](analytics.md) 和 [Adobe Experience Platform](platform.md).

下一個： **[WebViews](web-views.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)