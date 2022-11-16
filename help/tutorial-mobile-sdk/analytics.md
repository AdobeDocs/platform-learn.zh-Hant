---
title: Analytics對應
description: 了解如何在行動應用程式中收集Adobe Analytics的資料。
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 4%

---

# Analytics對應

了解如何將行動資料對應至Adobe Analytics。

此 [事件](events.md) 您在先前的課程中收集並傳送至Platform Edge Network的資料會轉送至您資料流中設定的服務，包括Adobe Analytics。 您只需將資料對應至報表套裝中的正確變數即可。

## 先決條件

* 了解ExperienceEvent追蹤。
* 在範例應用程式中成功傳送XDM資料。
* 設定至Adobe Analytics的資料流

## 學習目標

在本課程中，您將：

* 了解Analytics變數的自動對應。
* 設定處理規則，將XDM資料對應至Analytics變數。

## 自動對應

許多標準XDM欄位會自動對應至Analytics變數。 請參閱[這裡](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en)的完整清單。

### 範例#1 - s.products

例如 [產品變數](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=zh-Hant) 無法使用處理規則填入。 在XDM實作中，您會傳遞productListItems和s.products中的所有必要資料，並透過Analytics對應自動填入。

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

會導致下列結果：

```
s.products = ";Yoga Mat;1;49.99,;Water Bottle,3,30.00"
```

>[!NOTE]
>
>目前 `productListItems[N].SKU` 被自動映射忽略。

### 範例#2 - scAdd

如果您仔細查看，所有事件都有兩個欄位 `value` （必要）和 `id` （可選）。 此 `value` 欄位可用來增加事件計數。 此 `id` 欄位用於序列化。

此物件：

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

會導致下列結果：

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

會導致下列結果：

```
s.events = "scAdd:321435"
```

## 驗證並保證

使用 [保證QA工具](assurance.md) 您可以確認傳送的是ExperienceEvent、XDM資料正確，且Analytics對應正如預期般發生。 例如：

1. 傳送productListAdds事件。

   ```swift
   var xdmData: [String: Any] = [
     "eventType": "commerce.productListAdds",
     "commerce": [
       "productListAdds": [
         "value": 1
       ]
     ],
     "productListItems": [
       [
         "name": "neve studio dance jacket - (blue)",
         "SKU": "test-sku",
         "priceTotal": 69
       ]
     ]
   ]
   let addToCartEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: addToCartEvent)
   ```

1. 檢視ExperienceEvent點擊。

   ![analytics xdm點擊](assets/mobile-analytics-assurance-xdm.png)

1. 檢閱JSON的XDM部分。

   ```json
     "xdm" : {
       "productListItems" : [ {
         "priceTotal" : 69,
         "SKU" : "test-sku",
         "name" : "neve studio dance jacket - (blue)"
       } ],
       "timestamp" : "2021-10-22T22:03:37Z",
       "commerce" : {
         "productListAdds" : {
           "value" : 1
         }
       },
       "eventType" : "commerce.productListAdds",
       //...
     }
   ```

1. 檢閱 `analytics.mapping` 事件。

   ![analytics xdm點擊](assets/mobile-analytics-assurance-mapping.png)

請在Analytics對應中注意下列事項：

* 根據 `commerce.productListAdds`.
* 「pl」（產品變數）會根據 `productListItems`.
* 此事件中還有其他有趣的資訊，包括所有內容資料。


## 與內容資料對應

轉送至Analytics的XDM資料會轉換為 [內容資料](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en) 包括標準和自訂欄位。

內容資料索引鍵是依照下列語法來建構：

```
a.x.[xdm path]
```

例如：

```
//Standard Field
a.x.commerce.saveforlaters.value

//Custom Field
a.x._techmarketingdemos.appinformationa.appstatedetails.screenname
```

>[!NOTE]
>
>自訂欄位會放在您的Experience Cloud組織識別碼下。
>
>「_techmarketingdemos」會取代為您組織的唯一值。

以下是使用此資料的處理規則看起來的樣子：

![analytics處理規則](assets/mobile-analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>某些自動對應的變數可能無法用於處理規則。
>
>
>第一次對應至處理規則時，UI不會顯示XDM物件的內容資料變數。 若要修正選取任何值的問題，請儲存，然後返回編輯。 所有XDM變數現在應會顯示。


可找到處理規則和內容資料的其他資訊 [此處](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>與先前的行動應用程式實作不同，頁面/畫面檢視與其他事件之間沒有區別。 反之，您可以遞增 **[!UICONTROL 頁面檢視]** 量度 **[!UICONTROL 頁面名稱]** 維度。 因為您正在收集自訂 `screenName` 教學課程中的欄位，強烈建議將此欄位對應至 **[!UICONTROL 頁面名稱]** 填入。


下一個： **[Experience Platform](platform.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)