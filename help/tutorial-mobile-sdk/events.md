---
title: 使用Experience Platform Mobile SDK追蹤行動應用程式中的事件資料
description: 瞭解如何追蹤行動應用程式中的事件資料。
jira: KT-14631
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: 49d8c53d2ba2f9dcecf2470d855ad22f44763f6f
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 1%

---

# 追蹤事件資料

瞭解如何追蹤行動應用程式中的事件。

Edge Network擴充功能提供API，可將體驗事件傳送至Platform Edge Network。 體驗事件是包含符合XDM ExperienceEvent結構描述定義的資料的物件。 更簡單地說，這些事件會擷取使用者在您的行動應用程式中的動作。 Platform Edge Network收到資料後，即可將該資料轉送至資料流中設定的應用程式和服務，例如Adobe Analytics和Experience Platform。 在產品檔案中進一步瞭解[體驗事件](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/)。

## 先決條件

* 所有套件相依性都在您的Xcode專案中設定。
* 已在&#x200B;**[!UICONTROL AppDelegate]**&#x200B;中登入副檔名。
* 已設定MobileCore擴充功能使用您的開發`appId`。
* 匯入的SDK。
* 已順利建置並執行應用程式，包含上述變更。

## 學習目標

在本課程中，您將學習

* 瞭解如何根據結構描述來建構XDM資料。
* 根據標準欄位群組傳送XDM事件。
* 根據自訂欄位群組傳送XDM事件。
* 傳送XDM購買事件。
* 使用Assurance進行驗證。

## 建構體驗事件

Adobe Experience Platform Edge擴充功能可將遵循先前已定義XDM結構的事件傳送至Adobe Experience Platform Edge Network。

程式如下……

1. 識別您嘗試追蹤的行動應用程式互動。

1. 檢閱您的結構並識別適當的事件。

1. 檢閱您的結構描述，並識別應用於描述事件的任何其他欄位。

1. 建構並填入資料物件。

1. 建立並傳送事件。

1. 驗證。


### 標準欄位群組

對於標準欄位群組，程式看起來像這樣：

* 在您的結構描述中，識別您嘗試收集的事件。 在此範例中，您正在追蹤商務體驗事件，例如產品檢視(**[!UICONTROL productViews]**)事件。

  ![產品檢視結構描述](assets/datacollection-prodView-schema.png){zoomable="yes"}

* 若要在您的應用程式中建構包含體驗事件資料的物件，請使用如下的程式碼：

>[!BEGINTABS]

>[!TAB iOS]

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

在此程式碼中：

* `eventType`：說明已發生的事件，儘可能使用[已知值](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values)。

* `commerce.productViews.value`：事件的數值或布林值。 如果是布林值(或Adobe Analytics中的「計數器」)，此值一律設為1。 如果是數值或貨幣事件，值可以是> 1。

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "commerce.productViews",
    "commerce" to mapOf(
        "productViews" to mapOf(
        "value": 1
        )
    )
)
```

在此程式碼中：

* `eventType`：說明已發生的事件，儘可能使用[已知值](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values)。

* `commerce.productViews.value`：事件的數值或布林值。 如果是布林值(或Adobe Analytics中的「計數器」)，此值一律設為1。 如果是數值或貨幣事件，值可以是> 1。

>[!ENDTABS]


* 在您的結構描述中，識別與商務產品檢視事件相關聯的任何其他資料。 在此範例中，包含&#x200B;**[!UICONTROL productListItems]**，這是用於任何商務相關事件的標準欄位集：

  ![產品清單專案結構描述](assets/datacollection-prodListItems-schema.png){zoomable="yes"}
   * 請注意，**[!UICONTROL productListItems]**&#x200B;是一個陣列，因此可以提供多個產品。

* 若要新增此資料，請展開您的`xdmData`物件以包含補充資料：

>[!BEGINTABS]

>[!TAB iOS]

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

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "commerce.productViews",
    "commerce" to mapOf(
        "productViews" to mapOf(
        "value": 1
        )
    ),
    "productListItems" to mapOf(
        "name": productName,
        "SKU": sku,
        "priceTotal", priceString,
        "quantity", 1
    )
)
```

>[!ENDTABS]

* 您現在可以使用此資料結構來建立`ExperienceEvent`：

>[!BEGINTABS]

>[!TAB iOS]

```swift
let productViewEvent = ExperienceEvent(xdm: xdmData)
```

>[!TAB Android]

```kotlin
val productViewEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
```

>[!ENDTABS]

* 並使用`sendEvent` API將事件和資料傳送至Platform Edge Network：

>[!BEGINTABS]

>[!TAB iOS]

```swift
Edge.sendEvent(experienceEvent: productViewEvent)
```

>[!TAB Android]

```kotlin
Edge.sendEvent(productViewEvent, null)
```

>[!ENDTABS]


[`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API是AEP Mobile SDK，相當於[`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction)和[`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate) API呼叫。 如需詳細資訊，請參閱[從Analytics行動擴充功能移轉至Adobe Experience Platform Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/)。

您現在即將在專案中實作此程式碼。
您的應用程式中有不同的商務產品相關動作，而您想要根據使用者執行的這些動作，傳送事件：

* 檢視：當使用者檢視特定產品時發生，
* 加入購物車：使用者點選時 產品詳細資料畫面中的<img src="assets/addtocart.png" width="20">，
* 儲存以供稍後使用：使用者點選時 <img src="assets/saveforlater.png" width="15" /> / 產品詳細資料畫面中的<img src="assets/heart.png" width="25">，
* 購買：使用者點選時 產品詳細資料畫面中的<img src="assets/purchase.png" width="20">。

若要以可重複使用的方式實作與商業相關的體驗事件的傳送，請使用專用函式：

>[!BEGINTABS]

>[!TAB iOS]

1. 導覽至Xcode專案導覽器中的&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**，並將下列專案新增至`func sendCommerceExperienceEvent(commerceEventType: String, product: Product)`函式。

   ```swift
   // Set up a data dictionary, create an experience event and send the event.
   let xdmData: [String: Any] = [
       "eventType": "commerce." + commerceEventType,
       "commerce": [
           commerceEventType: [
               "value": 1
           ]
       ],
       "productListItems": [
           [
               "name": product.name,
               "priceTotal": product.price,
               "SKU": product.sku
           ]
       ]
   ]
   
   let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   ```

   此函式將商務體驗事件型別和產品視為引數和

   * 使用函式的引數，將XDM裝載設定為字典。
   * 使用字典設定體驗事件，
   * 使用[`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API傳送體驗事件。

1. 導覽至Xcode專案導覽器中的&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!UICONTROL ProductView]**，並新增各種呼叫至`sendCommerceExperienceEvent`函式：

   1. 在`.task`結尾內的`ATTrackingManager.trackingAuthorizationStatus`修飾元。 當產品檢視初始化並顯示時，會呼叫此`.task`修飾元，因此您想要在該特定時刻傳送產品檢視事件。

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
      ```

   1. 針對每個按鈕(<img src="assets/saveforlater.png" width="15" />， <img src="assets/addtocart.png" width="20">和 <img src="assets/purchase.png" width="20">)在工具列中，在`ATTrackingManager.trackingAuthorizationStatus == .authorized`關閉內新增相關呼叫：

      1. 的 <img src="assets/saveforlater.png" width="15" />：

         ```swift
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. 的 <img src="assets/addtocart.png" width="20">：

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. 的 <img src="assets/purchase.png" width="20">：

         ```swift
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

>[!TAB Android]

1. 在Android Studio導覽器中導覽至&#x200B;**[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!UICONTROL 應用程式]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL 模型]** > **[!UICONTROL MobileSDK]**，並將下列專案新增至`func sendCommerceExperienceEvent(commerceEventType: String, product: Product)`函式。

   ```kotlin
   // Set up a data map, create an experience event and send the event.
   val xdmData = mapOf(
       "eventType" to "commerce.$commerceEventType",
       "commerce" to mapOf(commerceEventType to mapOf("value" to 1)),
       "productListItems" to listOf(
           mapOf(
               "name" to product.name,
               "priceTotal" to product.price,
               "SKU" to product.sku
           )
       )
   )
   val commerceExperienceEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
   Edge.sendEvent(commerceExperienceEvent, null)
   ```

   此函式將商務體驗事件型別和產品視為引數和

   * 使用函式中的引數將XDM裝載設定為對應，
   * 使用地圖設定體驗事件，
   * 使用[`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API傳送體驗事件。

1. 導覽至Android Studio導覽器中的&#x200B;**[!UICONTROL 應用程式]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL 檢視]** > **[!UICONTROL ProductView.kt]**，並將各種呼叫新增至`sendCommerceExperienceEvent`函式：

   1. 在`LaunchedEffect(Unit)`可撰寫函式中，您要在檢視產品的特定時間傳送產品檢視事件。

      ```kotlin
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent("productViews", product)
      ```

   1. 針對每個按鈕(<img src="assets/heart.png" width="25">, <img src="assets/addtocart.png" width="20">和 <img src="assets/purchase.png" width="20">)在工具列中，新增在`scope.launch`的`if (MobileSDK.shared.trackingEnabled == TrackingStatus.AUTHORIZED)  statement`內的相關呼叫：

      1. 的 <img src="assets/heart.png" width="25">：

         ```kotlin
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("saveForLaters", product)
         ```

      1. 的 <img src="assets/addtocart.png" width="20">：

         ```kotlin
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("productListAdds", product)
         ```

      1. 的 <img src="assets/purchase.png" width="20">：

         ```kotlin
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("purchases", product)
         ```

>[!ENDTABS]

>[!TIP]
>
>如果您正在針對Android™開發，請使用Map (`java.util.Map`)作為建構XDM承載的基礎介面。


### 自訂欄位分組

想像您想要追蹤應用程式本身的熒幕檢視和互動情形。 請記住，您已為此型別事件定義自訂欄位群組。

* 在您的結構描述中，識別您嘗試收集的事件。
  ![應用程式互動結構描述](assets/datacollection-appInteraction-schema.png){zoomable="yes"}

* 開始建構物件。

  >[!NOTE]
  >
  >* 標準欄位群組一律以物件根目錄開始。
  >
  >* 自訂欄位群組一律以您的Experience Cloud組織`_techmarketingdemos`所獨有的物件開頭（在此範例中）。

* 針對應用程式互動事件，您可以建構如下的物件：

>[!BEGINTABS]

>[!TAB iOS]

```swift
let xdmData: [String: Any] = [
    "eventType": "application.interaction",
    "_techmarketingdemos": [
    "appInformation": [
        "appInteraction": [
            "name": "login",
            "appAction": [
                "value": 1
                ]
            ]
        ]
    ]
]
```

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "application.interaction",
    "_techmarketingdemos" to mapOf(
        "appInformation" to mapOf(
            "appInteraction" to mapOf(
                "name" to "login",
                "appAction" to mapOf("value" to 1)
            )
        )
    )
)
```

>[!ENDTABS]

* 對於熒幕追蹤事件，您可以建構如下的物件：

>[!BEGINTABS]

>[!TAB iOS]

```swift
var xdmData: [String: Any] = [
    "eventType": "application.scene",
    "_techmarketingdemos": [
        "appInformation": [
            "appStateDetails": [
                "screenType": "App",
                "screenName": "luma: content: ios: us: en: login",
                "screenView": [
                    "value": 1
                ]
            ]
        ] 
    ]
]
```

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "application.scene",
    tenant.value to mapOf(
        "appInformation" to mapOf(
            "appStateDetails" to mapOf(
                "screenType" to "App",
                "screenName" to stateName,
                "screenView" to mapOf("value" to 1)
            )
        )
    )
)
```

>[!ENDTABS]



* 您現在可以使用此資料結構來建立`ExperienceEvent`。

>[!BEGINTABS]

>[!TAB iOS]

```swift
let event = ExperienceEvent(xdm: xdmData)
```

>[!TAB Android]

```kotlin
val event = ExperienceEvent(xdmData)
```

>[!ENDTABS]


* 將事件和資料傳送至Platform Edge Network。

>[!BEGINTABS]

>[!TAB iOS]

```swift
Edge.sendEvent(experienceEvent: event)
```

>[!TAB Android]

```kotlin
Edge.sendEvent(event, null)
```

>[!ENDTABS]

再次強調，請在專案中實作此程式碼。

>[!BEGINTABS]

>[!TAB iOS]

1. 為方便起見，您在&#x200B;**[!UICONTROL MobileSDK]**&#x200B;中定義了兩個函式。 導覽至Xcode專案導覽器中的&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**。

   * 一個用於應用程式互動。 將此程式碼新增至`func sendAppInteractionEvent(actionName: String)`函式：

     ```swift
     // Set up a data dictionary, create an experience event and send the event.
     let xdmData: [String: Any] = [
         "eventType": "application.interaction",
         tenant : [
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
     let appInteractionEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: appInteractionEvent)
     ```

     此函式使用動作名稱作為引數，且

      * 使用函式的引數，將XDM裝載設定為字典。
      * 使用字典設定體驗事件，
      * 使用[`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API傳送體驗事件。


   * 另一個用於熒幕追蹤。 將此程式碼新增至`func sendTrackScreenEvent(stateName: String) `函式：

     ```swift
     // Set up a data dictionary, create an experience event and send the event.
     let xdmData: [String: Any] = [
         "eventType": "application.scene",
         tenant : [
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
     ]
     let trackScreenEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: trackScreenEvent)
     ```

     此函式使用狀態名稱作為引數，而

      * 使用函式的引數，將XDM裝載設定為字典。
      * 使用字典設定體驗事件，
      * 使用[`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API傳送體驗事件。

1. 導覽至&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 登入工作表]**。

   1. 將下列醒目提示的程式碼新增至「登入」按鈕的關閉處：

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      ```

   1. 將下列醒目提示的程式碼新增至`onAppear`修飾元：

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

>[!TAB Android]

1. 為方便起見，您在&#x200B;**[!UICONTROL MobileSDK]**&#x200B;中定義了兩個函式。 導覽至Android Studio導覽器中的&#x200B;**[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL 模型]** > **[!UICONTROL MobileSDK]**。

   * 一個用於應用程式互動。 將此程式碼新增至`fun sendAppInteractionEvent(actionName: String)`函式：

     ```kotlin
     // Set up a data map, create an experience event and send the event.
     val xdmData = mapOf(
         "eventType" to "application.interaction",
         tenant.value to mapOf(
             "appInformation" to mapOf(
                 "appInteraction" to mapOf(
                     "name" to actionName,
                     "appAction" to mapOf("value" to 1)
                 )
             )
         )
     )
     val appInteractionEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
     Edge.sendEvent(appInteractionEvent, null)
     ```

     此函式使用動作名稱作為引數，且

      * 使用函式的引數，將XDM裝載設定為對應。
      * 使用地圖設定體驗事件，
      * 使用[`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API傳送體驗事件。


   * 另一個用於熒幕追蹤。 將此程式碼新增至`fun sendTrackScreenEvent(stateName: String)`函式：

     ```kotlin
     // Set up a data map, create an experience event and send the event.
     val xdmData = mapOf(
         "eventType" to "application.scene",
         tenant.value to mapOf(
             "appInformation" to mapOf(
                 "appStateDetails" to mapOf(
                     "screenType" to "App",
                     "screenName" to stateName,
                     "screenView" to mapOf("value" to 1)
                 )
             )
         )
     )
     val trackScreenEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
     Edge.sendEvent(trackScreenEvent, null)
     ```

     此函式使用狀態名稱作為引數，而

      * 使用函式的引數，將XDM裝載設定為對應。
      * 使用地圖設定體驗事件，
      * 使用[`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API傳送體驗事件。

1. 導覽至&#x200B;**[!UICONTROL Android]** ![ChevronDown ](/help/assets/icons/ChevronDown.svg)**[!DNL app]**>**[!DNL kotlin+java]**>**[!DNL com.adobe.luma.tutorial.android]**>**[!UICONTROL &#x200B;檢視&#x200B;]**>**[!UICONTROL &#x200B; LoginSheet.kt &#x200B;]**

   1. 將下列醒目提示的程式碼新增至&#x200B;**[!UICONTROL 按鈕]** **[!UICONTROL onClick]**&#x200B;事件：

      ```kotlin
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent("login")
      ```

   1. 將下列醒目提示的程式碼新增至`LaunchedEffect(Unit)`可撰寫函式：

      ```kotlin
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent("luma: content: android: us: en: login")
      ```

>[!ENDTABS]



## 驗證

1. 檢閱[設定指示](assurance.md#connecting-to-a-session)區段，將您的模擬器或裝置與Assurance連線。

   1. 將Assurance圖示向左移動。
   1. 在索引標籤列中選取「**[!UICONTROL 首頁]**」，並確認您在「首頁」畫面中看到&#x200B;**[!UICONTROL ECID]**、**[!UICONTROL 電子郵件]**&#x200B;和&#x200B;**[!UICONTROL CRM ID]**。
   1. 在索引標籤列中選取&#x200B;**[!DNL Products]**。
   1. 選取產品。
   1. 選擇 <img src="assets/saveforlater.png" width="15"> (iOS)或 <img src="assets/heart.png" width="25"> (Android)。
   1. 選擇 <img src="assets/addtocart.png" width="20">。
   1. 選擇 <img src="assets/purchase.png" width="15">。

>[!BEGINTABS]

>[!TAB iOS]

<img src="./assets/mobile-app-events-3.png" width="300">

>[!TAB Android]

<img src="./assets/mobile-app-events-3-android.png" width="278">

>[!ENDTABS]

1. 在Assurance UI中，尋找來自&#x200B;**[!UICONTROL com.adobe.edge.konductor]**&#x200B;廠商的&#x200B;**[!UICONTROL hitReceived]**&#x200B;事件。
1. 選取事件並檢閱&#x200B;**[!UICONTROL 訊息]**&#x200B;物件中的XDM資料。 或者，您可以使用![複製](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL 複製原始事件]**，並使用您喜好的文字或程式碼編輯器貼上並檢查該事件。

   ![資料彙集驗證](assets/datacollection-validation.png){zoomable="yes"}


## 後續步驟

您現在應該擁有所有工具，可開始將資料收集新增至應用程式。 您可以新增更多智慧來瞭解使用者如何與應用程式中的產品互動，也可以新增更多應用程式互動和熒幕追蹤呼叫至應用程式：

* 實施訂單、結帳、清空購物籃和其他功能至應用程式，並新增相關商務體驗事件至此功能。
* 使用適當的引數重複呼叫`sendAppInteractionEvent`，以追蹤使用者的其他應用程式互動。
* 使用適當的引數重複呼叫`sendTrackScreenEvent`，以追蹤使用者在應用程式中檢視的熒幕。

>[!TIP]
>
>如需更多範例，請檢閱[完成的應用程式](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App)。


## 將事件傳送至Analytics和Platform

現在您已收集事件並傳送至Platform Edge Network，它們會傳送至[資料流](create-datastream.md)中設定的應用程式和服務。 在稍後的課程中，您會將此資料對應至[Adobe Analytics](analytics.md)、[Adobe Experience Platform](platform.md)和其他Adobe Experience Cloud解決方案(如[Adobe Target](target.md)和Adobe Journey Optimizer)。

>[!SUCCESS]
>
>您現在已設定應用程式，以追蹤商務、應用程式互動和畫面追蹤事件至Adobe Experience Platform Edge Network。 以及您在資料流中定義的所有服務。
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享。

下一個： **[處理WebViews](web-views.md)**
