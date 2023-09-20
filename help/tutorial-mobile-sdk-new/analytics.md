---
title: 將資料對應至Analytics資料
description: 瞭解如何在行動應用程式中收集並對映Adobe Analytics的資料。
solution: Data Collection,Experience Platform,Analytics
hide: true
source-git-commit: 5f178f4bd30f78dff3243b3f5bd2f9d11c308045
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 4%

---

# 收集與對應Analytics資料

瞭解如何將行動資料對應至Adobe Analytics。

此 [事件](events.md) 您在先前的課程中收集並傳送至Platform Edge Network的資料，會轉送至您在資料流中設定的服務，包括Adobe Analytics。 將資料對應至報表套裝中的正確變數。

![架構](assets/architecture-aa.png)

## 先決條件

* 瞭解ExperienceEvent追蹤。
* 已成功在您的範例應用程式中傳送XDM資料。
* 資料流已設定為Adobe Analytics

## 學習目標

在本課程中，您將會：

* 使用Adobe Analytics服務設定您的資料串流。
* 瞭解Analytics變數的自動對應。
* 設定處理規則，將XDM資料對應至Analytics變數。

## 新增Adobe Analytics資料流服務

若要將您的XDM資料從Edge Network傳送到Adobe Analytics，請將Adobe Analytics服務設定為您設定的資料串流，做為的一部分 [建立資料串流](create-datastream.md).

1. 在資料收集UI中，選取 **[!UICONTROL 資料串流]** 和您的資料流。

1. 然後選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增服務]**.

1. 新增 **[!UICONTROL Adobe Analytics]** 從 [!UICONTROL 服務] 清單，

1. 輸入您要在Adobe Analytics中使用的報表套裝名稱 **[!UICONTROL 報告套裝ID]**.

1. 透過切換來啟用服務 **[!UICONTROL 已啟用]** 開啟。

1. 選取「**[!UICONTROL 儲存]**」。

   ![將Adobe Analytics新增為資料流服務](assets/datastream-service-aa.png)


## 自動對應

許多標準XDM欄位會自動對應至Analytics變數。 請參閱[這裡](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en)的完整清單。

### 範例#1 - s.products

一個很好的範例是 [products變數](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=zh-Hant) 無法使用處理規則填入的專案。 透過XDM實施，您可將所有必要資料傳入 `productListItems` 和 `s.products` 透過Analytics對應自動填入。

此物件：

```swift
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
```

結果為：

```
s.products = ";Yoga Mat;1;49.99,;Water Bottle,3,30.00"
```

>[!NOTE]
>
>目前 `productListItems[N].SKU` 被自動對應忽略。


### 範例#2 - scAdd

仔細檢視，所有事件都有兩個欄位 `value` （必要）和 `id` （選擇性）。 此 `value` 欄位用於增加事件計數。 此 `id` 欄位用於序列化。

此物件：

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

結果為：

```
s.events = "scAdd"
```

此物件：

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1,
    "id": "321435"
  }
}
```

結果為：

```
s.events = "scAdd:321435"
```

## 使用保證進行驗證

使用 [保證](assurance.md) 您可以確認自己正在傳送體驗事件、XDM資料正確且Analytics對應如預期般發生。 例如：

1. 傳送productListAdds事件

1. 檢視ExperienceEvent點選。

   ![analytics xdm點選](assets/analytics-assurance-experiencevent.png)

1. 檢閱JSON的XDM部分。

   ```json
   "xdm" : {
     "productListItems" : [ {
       "SKU" : "LLWS05.1-XS",
       "name" : "Desiree Fitness Tee",
       "priceTotal" : 24
     } ],
   "timestamp" : "2023-08-04T12:53:37.662Z",
   "eventType" : "commerce.productListAdds",
   "commerce" : {
     "productListAdds" : {
       "id" : "LLWS05.1-XS",
       "value" : 1
     }
   }
   // ...
   ```

1. 檢閱 **[!UICONTROL analytics.mapping]** 事件。

   ![analytics xdm點選](assets/analytics-assurance-mapping.png)

在Analytics對應中注意下列事項：

* **[!UICONTROL 事件]** 填入 `scAdd` 根據 `commerce.productListAdds`.
* **[!UICONTROL pl]** （產品變數）會填入一個串連值，根據 `productListItems`.
* 此事件還有其他有趣的資訊，包括所有內容資料。


## 與內容資料對應

轉送至Analytics的XDM資料會轉換為 [內容資料](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en) 包含標準和自訂欄位。

內容資料索引鍵的建構遵循下列語法：

```
a.x.[xdm path]
```

例如：

```
// Standard Field
a.x.commerce.saveforlaters.value

// Custom Field
a.x._techmarketingdemos.appinformation.appstatedetails.screenname
```

>[!NOTE]
>
>自訂欄位會放置在您的Experience Cloud組織識別碼下。
>
>`_techmarketingdemos` 會取代為您組織的唯一值。

若要將此XDM內容資料對應至報表套裝中的Analytics資料，您可以：

* 新增 **[!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能]** 欄位群組至您的結構描述。

  ![Analytics ExperienceEvent FullExtension欄位群組](assets/schema-analytics-extension.png)
* 在「標籤」屬性中建立規則，將內容資料對應至「Adobe Analytics ExperienceEvent完整擴充功能」欄位群組中的欄位。 例如，地圖 `_techmarketingdemo.appinformation.appstatedetails.screenname` 至 `_experience.analytics.customDimensions.eVars.eVar2`.

<!-- Old processing rules section
Here is what a processing rule using this data might look like:

* You **[!UICONTROL Overwrite value of]** (1) **[!UICONTROL App Screen Name (eVar2)]** (2) with the value of **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3) if **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (4) **[!UICONTROL is set]** (5).

* You **[!UICONTROL Set event]** (6) **[!UICONTROL Add to Wishlist (Event 3)]** (7) to **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) if **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL is set]** (10).

![analytics processing rules](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Some of the automatically mapped variables may not be available for use in processing rules.
>
>
>The first time you map to a processing rule, the interface does not show you the context data variables from the XDM object. To fix that select any value, Save, and come back to edit. All XDM variables should now appear.


Additional information about processing rules and context data can be found [here](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>Unlike previous mobile app implementations, there is no distinction between a page / screen views and other events. Instead you can increment the **[!UICONTROL Page View]** metric by setting the **[!UICONTROL Page Name]** dimension in a processing rule. Since you are collecting the custom `screenName` field in the tutorial, it is highly recommended to map screen name to **[!UICONTROL Page Name]** in a processing rule.

-->

>[!SUCCESS]
>
>您已設定應用程式，將您的Experience Edge XDM物件對應至Adobe Analytics變數，以在您的資料流中啟用Adobe Analytics服務，並在適用的情況下使用處理規則。<br/> 感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[傳送資料給Experience Platform](platform.md)**
