---
title: 將使用Platform Mobile SDK收集的資料對應至Adobe Analytics
description: 瞭解如何在行動應用程式中收集並對映Adobe Analytics的資料。
solution: Data Collection,Experience Platform,Analytics
jira: KT-14636
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: 30dd0142f1f5220f30c45d58665b710a06c827a8
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 1%

---

# 收集與對應Analytics資料

瞭解如何將行動資料對應至Adobe Analytics。

您收集並在先前課程中傳送至PlatformEdge Network的[事件](events.md)資料會轉送至您在資料流中設定的服務，包括Adobe Analytics。 將資料對應至報表套裝中的正確變數。

![架構](assets/architecture-aa.png)

## 先決條件

* 瞭解ExperienceEvent追蹤。
* 已成功在您的範例應用程式中傳送XDM資料。
* 可用於本課程的Adobe Analytics報表套裝。

## 學習目標

在本課程中，您將會：

* 使用Adobe Analytics服務設定您的資料串流。
* 瞭解Analytics變數的自動對應。
* 設定處理規則，將XDM資料對應至Analytics變數。

## 新增Adobe Analytics資料流服務

若要將您的XDM資料從Edge Network傳送至Adobe Analytics，請將Adobe Analytics服務設定至您設定的資料流，作為[建立資料流](create-datastream.md)的一部分。

1. 在資料收集UI中，選取&#x200B;**[!UICONTROL 資料串流]**&#x200B;和您的資料串流。

1. 然後選取![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增服務]**。

1. 從[!UICONTROL 服務]清單新增&#x200B;**[!UICONTROL Adobe Analytics]**，

1. 輸入您要在&#x200B;**[!UICONTROL 報表套裝ID]**&#x200B;中使用的來自Adobe Analytics的報表套裝名稱。

1. 透過將&#x200B;**[!UICONTROL 已啟用]**&#x200B;切換為開啟來啟用服務。

1. 選取「**[!UICONTROL 儲存]**」。

   ![將Adobe Analytics新增為資料流服務](assets/datastream-service-aa.png)


## 自動對應

許多標準XDM欄位會自動對應至Analytics變數。 請參閱[這裡](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en)的完整清單。

### 範例#1 - s.products

無法使用處理規則填入的[產品變數](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)就是很好的範例。 透過XDM實作，您傳遞了`productListItems`中的所有必要資料，系統透過Analytics對應自動填入`s.products`。

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
s.products = ";5829;1;49.99,9841;3;30.00"
```

>[!NOTE]
>
>如果`productListItems[].SKU`和`productListItems[].name`都包含資料，則使用`productListItems[].SKU`中的值。 如需詳細資訊，請參閱AdobeExperience Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en)中的[Analytics變數對應。


### 範例#2 - scAdd

若您仔細檢視，所有事件都有兩個欄位`value` （必要）和`id` （選用）。 `value`欄位用於增加事件計數。 `id`欄位用於序列化。

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

使用[保證](assurance.md)，您可以確認您傳送的是體驗事件、XDM資料正確，且Analytics對應如預期發生。

1. 檢閱[設定指示](assurance.md#connecting-to-a-session)區段，將您的模擬器或裝置連線到Assurance。

1. 傳送&#x200B;**[!UICONTROL productListAdds]**&#x200B;活動（新增產品至購物籃）。

1. 檢視ExperienceEvent點選。

   ![分析xdm點選](assets/analytics-assurance-experiencevent.png)

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
       "value" : 1
     }
   }
   // ...
   ```

1. 檢閱&#x200B;**[!UICONTROL analytics.mapping]**&#x200B;事件。

   ![分析xdm點選](assets/analytics-assurance-mapping.png)

在Analytics對應中注意下列事項：

* **[!UICONTROL 個事件]**&#x200B;已根據`commerce.productListAdds`填入`scAdd`。
* **[!UICONTROL pl]** （產品變數）已填入以`productListItems`為基礎的串連值。
* 此事件還有其他有趣的資訊，包括所有內容資料。


## 與內容資料對應

轉送至Analytics的XDM資料會轉換為[內容資料](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en)，包含標準和自訂欄位。

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
>`_techmarketingdemos`已取代為您組織的唯一值。



若要將此XDM內容資料對應至報表套裝中的Analytics資料，您可以：

### 使用欄位群組

* 將&#x200B;**[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]**&#x200B;欄位群組新增至您的結構描述。

  ![Analytics ExperienceEvent FullExtension欄位群組](assets/schema-analytics-extension.png)

* 在您的應用程式中建置XDM裝載，符合Adobe Analytics ExperienceEvent Full Extension欄位群組，類似於您在[追蹤事件資料](events.md)課程中完成的工作，或者
* 在Tags屬性中建置規則，這些規則使用規則動作來附加或修改資料至Adobe Analytics ExperienceEvent Full Extension欄位群組。 檢視更多詳細資料[將資料附加至SDK事件](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/)或[修改SDK事件中的資料](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/)。


### 銷售eVar

如果您在Analytics設定中使用[銷售eVar](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/merchandising-evars.html?lang=en)，例如為了擷取產品（如`&&products = ...;evar1=red;event10=50,...;evar1=blue;event10=60`）的顏色，您必須擴充您在[追蹤事件資料](events.md)中定義的XDM裝載，才能擷取該銷售資訊。

* 在JSON中：

  ```json
  {
    "productListItems": [
        {
            "SKU": "LLWS05.1-XS",
            "name": "Desiree Fitness Tee",
            "priceTotal": 24,
            "_experience": {
                "analytics": {
                    "events1to100": {
                        "event10": {
                            "value": 50
                        }
                    },
                    "customDimensions": {
                        "eVars": {
                            "eVar1": "red",
                        }
                    }
                }
            }
        }
    ],
    "eventType": "commerce.productListAdds",
    "commerce": {
        "productListAdds": {
            "value": 1
        }
    }
  }
  ```

* 在程式碼中：

  ```swift
  var xdmData: [String: Any] = [
    "productListItems": [
      [
        "name":  productName,
        "SKU": sku,
        "priceTotal": priceString,
        "_experience" : [
          "analytics": [
            "events1to100": [
              "event10": [
                "value:": value
              ]
            ],
            "customDimensions": [
              "eVars": [
                "eVar1": color
              ]
            ]
          ]
        ]
      ]
    ],
    "eventType": "commerce.productViews",
    "commerce": [
      "productViews": [
        "value": 1
      ]
    ]
  ]
  ```


### 使用處理規則

以下是使用此資料的處理規則的外觀：

* 如果設定了&#x200B;**[!UICONTROL a.x._techmarketingdemo.appstatedetails.appstatedetails.screenname]** (4) **[!UICONTROL (5)，您**[!UICONTROL &#x200B;以&#x200B;**[!UICONTROL a.x._techmarketingdemo.appstatedetails.appstatedetails.screenname]**&#x200B;的值&#x200B;**[!UICONTROL 覆寫]** (1)應用程式畫面名稱(eVar2)]**(2)]** (5)。

* 如果&#x200B;**[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL 已設定]** (10)，則您&#x200B;**[!UICONTROL 將event]** (6) **[!UICONTROL Add to Wishlist (Event 3)]** (7)設為&#x200B;**[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8)。

![分析處理規則](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>有些自動對應的變數可能無法用於處理規則。
>
>
>第一次對應到處理規則時，介面不會顯示XDM物件的內容資料變數。 若要修正選取的任何值，請儲存並返回編輯。 所有XDM變數現在都會顯示。


您可以在[這裡](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en)找到有關處理規則和內容資料的其他資訊。

>[!TIP]
>
>和先前的行動應用程式實作不同，頁面/畫面檢視和其他事件沒有區別。 反之，您可以在處理規則中設定&#x200B;**[!UICONTROL 頁面名稱]**&#x200B;維度，以增加&#x200B;**[!UICONTROL 頁面檢視]**&#x200B;量度。 由於您正在教學課程中收集自訂`screenName`欄位，強烈建議在處理規則中將熒幕名稱對應至&#x200B;**[!UICONTROL 頁面名稱]**。


>[!SUCCESS]
>
>您已設定應用程式，將您的Experience Edge XDM物件對應至Adobe Analytics變數，以在您的資料流中啟用Adobe Analytics服務，並在適用的情況下使用處理規則。<br/>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享。

下一步： **[傳送資料給Experience Platform](platform.md)**
