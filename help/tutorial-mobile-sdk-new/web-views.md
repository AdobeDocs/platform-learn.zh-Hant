---
title: 處理網頁檢視
description: 瞭解如何在行動應用程式中使用WebViews處理資料收集。
jira: KT-6987
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# 處理網頁檢視

瞭解如何在行動應用程式中使用WebViews處理資料收集。

## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。

## 學習目標

在本課程中，您將會：

* 瞭解為何您必須在應用程式中針對WebViews採取特殊考量。
* 瞭解避免追蹤問題所需的程式碼。

## 可能的追蹤問題

如果您從應用程式的原生部分和WebView傳送資料，每個部分都會產生自己的Experience CloudID (ECID)，導致中斷連線的點選和膨脹的造訪/訪客資料。 有關ECID的更多資訊可在以下連結中找到： [ECID概觀](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

若要解決該不良情況，您必須將使用者的ECID從應用程式的原生部分傳遞至您可能會想要在應用程式中使用的WebView。

WebView中的Experience CloudID服務JavaScript擴充功能會從URL提取ECID，而非傳送要求給Adobe索取新ID。 ID服務會使用此ECID追蹤訪客。

## 實作

在Luma範例應用程式中，找到 **[!UICONTROL 服務條款工作表]** 檔案(在 **[!UICONTROL 資訊]** 資料夾)，並在 `SwiftUIWebViewModel` 類別：

```swift {highlight="6-22"}
    func loadUrl() {
        let url = Bundle.main.url(forResource: "tou", withExtension: "html")
        if var urlString = url?.absoluteString {
            // Adobe Experience Platform - Handle Web View
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
        }
    }
```

此程式碼最重要的部分為 `AEPEdgeIdentity.Identity.getUrlVariables` 關閉（反白顯示）。 結尾會設定URL的變數，以包含所有相關資訊，例如ECID等。 在此範例中，您使用的是本機檔案，但相同的概念適用於遠端頁面。

您可以進一步瞭解 `Identity.getUrlVariables` 中的API [Edge Network身分擴充功能API參考指南](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## 驗證

若要執行程式碼：

1. 前往 **[!UICONTROL 設定]** 在應用程式中
1. 點選 **[!UICONTROL 檢視……]** 按鈕以顯示 **[!UICONTROL 使用條款]**.

   <img src="./assets/tou1.png" width="300" /> <img src="./assets/tou2.png" width="300" />

1. 在Assurance UI中，尋找 **[!UICONTROL 邊緣身分回應URL變數]** 來自的事件 **[!UICONTROL com.adobe.griffon.mobile]** 廠商。
1. 選取事件並檢閱 **[!UICONTROL urlvariable]** 中的欄位 **[!UICONTROL ACPExtensionEventData]** 物件，確認URL中存在下列引數： `adobe_mc`， `mcmid`、和 `mcorgid`.

   ![webview驗證](assets/webview-validation.png)

   範例 `urvariables` 欄位如下所示：

   * 原始（含逸出字元）

     ```html
     adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg
     ```

   * 美化

     ```html
     adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
     ```

>[!NOTE]
>
>Platform Web SDK （2.11.0版或更新版本）支援透過這些URL引數彙整訪客，且在使用時 `VisitorAPI.js`.


>[!SUCCESS]
>
>您現在已將應用程式設定為根據Webview中的URL顯示內容，使用與Adobe Experience Platform Mobile SDK已核發的ECID相同的ECID。<br/>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[身分](identity.md)**
