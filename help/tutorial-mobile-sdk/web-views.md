---
title: 處理WebViews
description: 了解如何使用行動應用程式中的WebViews處理資料收集。
kt: 6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 1%

---

# 處理WebViews

了解如何使用行動應用程式中的WebViews處理資料收集。

## 先決條件

* 已安裝並設定SDK，成功建立並執行應用程式。

## 學習目標

在本課程中，您將：

* 了解您為何必須對WebViews採取特殊考量。
* 了解防止追蹤問題所需的程式碼。

## 潛在的追蹤問題

如果您從應用程式的原生部分和WebView傳送資料，每個都會產生各自的Experience CloudID(ECID)。 這會導致中斷連結的點擊，以及膨脹的造訪/訪客資料。 如需ECID的詳細資訊，請參閱 [ECID概觀](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

為了解決這種不良情況，必須將使用者的ECID從原生部分傳遞至WebView。

WebView中的Experience CloudID服務JavaScript擴充功能會從URL中擷取ECID，而非傳送要求Adobe新ID。 ID服務會使用此ECID來追蹤訪客。

## 實作

在Luma範例應用程式中，尋找 `TermsOfService.swift` 檔案(在 `Intro-Login_SignUp` )，然後找到下列程式碼：

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

這是載入WebView的簡單方法。 在此情況下，它是本機檔案，但相同的概念適用於遠端頁面。

重新調整Web檢視程式碼，如下所示：

```swift
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
if var urlString = url?.absoluteString {
    // Adobe Experience Platform - Handle Web View
    AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
        if let error = error {
            self.simpleAlert("\(error.localizedDescription)")
            return;
        }

        if let urlVariables: String = urlVariables {
            urlString.append("?" + urlVariables)
        }

        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: URL(string: urlString)!))
        }
        print("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
    }
} else {
    self.simpleAlert("Failed to create URL for webView")
}
```

您可以進一步了解 `Identity.getUrlVariables` 中的API [Edge Network Extension API參考指南](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables).

## 驗證

檢閱 [安裝指示](assurance.md) 區段，並將您的模擬器或裝置連線至「保證」，載入WebView並尋找 `Edge Identity Response URL Variables` 來自 `com.adobe.griffon.mobile` 供應商。

若要載入WebView，請前往Luma應用程式的主畫面，選取「帳戶」圖示，然後在頁尾中選取「使用條款」。

載入WebView後，選取事件並檢閱 `urlvariables` 欄位 `ACPExtensionEventData` 物件，確認URL中有下列參數： `adobe_mc`, `mcmid`，和 `mcorgid`.

![網站檢視驗證](assets/mobile-webview-validation.png)

範例 `urvariables` 欄位如下：

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>Platform Web SDK(2.11.0版或更新版本)目前支援透過這些URL參數進行訪客拼接，且 `VisitorAPI.js`.


下一個： **[身分](identity.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)