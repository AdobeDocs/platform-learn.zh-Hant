---
title: 使用Platform Mobile SDK處理WebViews
description: 瞭解如何在行動應用程式中使用WebViews處理資料收集。
jira: KT-14632
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# 處理網頁檢視

瞭解如何在行動應用程式中使用WebViews處理資料收集。

## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。

## 學習目標

在本課程中，您將會：

* 瞭解應用程式中WebViews必須特別考量的原因。
* 瞭解避免追蹤問題所需的程式碼。

## 可能的追蹤問題

如果您從應用程式的原生部分和應用程式內的WebView傳送資料，每個部分都會產生自己的Experience CloudID (ECID)，導致中斷連線的點選和膨脹的造訪/訪客資料。 有關ECID的詳細資訊，請參閱[ECID概觀](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=zh-Hant)。

若要解決該不良情況，您必須將使用者的ECID從應用程式的原生部分傳遞至您可能會想要在應用程式中使用的WebView。

WebView中使用的AEP Edge身分擴充功能會收集目前的ECID並將其新增至URL，而非傳送要求給Adobe索取新ID。 實作接著會使用此ECID來要求URL。

## 實作

導覽至&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Info]** > **[!DNL TermsOfServiceSheet]**，並在`final class SwiftUIWebViewModel: ObservableObject`類別中找到`func loadUrl()`函式。 新增下列呼叫以處理Web檢視：

```swift
// Handle web view
AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
    if let error = error {
        print("Error with Webview", error)
        return;
    }
    
    if let urlVariables: String = urlVariables {
        urlString.append("?" + urlVariables)
        guard let url = URL(string: urlString) else {
            return
        }
        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: url))
        }
    }
    Logger.aepMobileSDK.info("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
}
```

[`AEPEdgeIdentity.Identity.getUrlVariables`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) API會設定URL的變數，以包含所有相關資訊，例如ECID等。 在此範例中，您使用的是本機檔案，但相同的概念適用於遠端頁面。

您可以在[Edge Network延伸模組API參考指南](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables)中進一步瞭解`Identity.getUrlVariables` API。

## 驗證

若要執行程式碼：

1. 檢閱[設定指示](assurance.md#connecting-to-a-session)區段，將您的模擬器或裝置連線到Assurance。
1. 前往應用程式中的&#x200B;**[!UICONTROL 設定]**
1. 點選&#x200B;**[!DNL View...]**&#x200B;按鈕以顯示&#x200B;**[!DNL Terms of Use]**。

   <img src="./assets/tou1.png" width="300" /> <img src="./assets/tou2.png" width="300" />

1. 在Assurance UI中，尋找&#x200B;**[!UICONTROL com.adobe.griffon.mobile]**&#x200B;廠商的&#x200B;**[!UICONTROL Edge身分識別回應URL變數]**&#x200B;事件。
1. 選取事件並檢閱&#x200B;**[!UICONTROL ACPExtensionEventData]**&#x200B;物件中的&#x200B;**[!UICONTROL urlvariable]**&#x200B;欄位，確認URL中存在下列引數： `adobe_mc`、`mcmid`和`mcorgid`。

   ![webview驗證](assets/webview-validation.png)

   範例`urvariables`欄位如下所示：

   * 原始（含逸出字元）

     ```html
     adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg
     ```

   * 美化

     ```html
     adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
     ```

很遺憾，對Web工作階段進行偵錯受到限制。 例如，您無法在瀏覽器中使用Adobe Experience Platform Debugger來繼續偵錯Webview工作階段。

>[!NOTE]
>
>Platform Web SDK （2.11.0版或更新版本）以及使用`VisitorAPI.js`時，支援透過這些URL引數連結訪客。


>[!SUCCESS]
>
>您現在已將應用程式設定為根據Webview中的URL顯示內容，使用與Adobe Experience Platform Mobile SDK已核發的ECID相同的ECID。
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享

下一個： **[身分](identity.md)**
