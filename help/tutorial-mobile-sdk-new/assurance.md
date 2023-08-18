---
title: 設定保證
description: 瞭解如何在行動應用程式中實作Assurance擴充功能。
feature: Mobile SDK,Assurance
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 9%

---

# Assurance

瞭解如何在行動應用程式中設定Adobe Experience Platform保證。

Assurance （正式名稱為Project Griffon）可協助您檢查、證明、模擬及驗證如何在行動應用程式中收集資料或提供體驗。

Assurance 可協助您檢查 Adobe Experience Platform Mobile SDK 產生的原始 SDK 事件。SDK 收集的所有事件都可供檢查。SDK 事件會載入清單檢視，並依時間排序。每個事件都有一個可提供更多詳細資料的詳細檢視。此外，也提供瀏覽SDK設定、資料元素、共用狀態和SDK擴充功能版本的其他檢視。 進一步瞭解 [保證](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html) 產品檔案內。


## 先決條件

* 已成功安裝並設定SDK以設定應用程式。

## 學習目標

在本課程中，您將會：

* 確認您的組織擁有存取權（如果您沒有存取權，請提出要求）。
* 設定您的基底URL。
* 新增必要的iOS特定程式碼。
* 連線到工作階段.

## 確認存取

完成下列步驟，確認貴組織可以存取「保證」：

1. 造訪 [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance{target="_blank"}).
1. 使用您用於Experience Cloud的Adobe ID憑證登入。
1. 如果您看到 **[!UICONTROL 工作階段]** 熒幕，則表示您擁有存取權。 如果您看見（測試版）存取頁面，請選取 **[!UICONTROL 註冊]** 以註冊。

## 實作

除了一般 [SDK安裝](install-sdks.md)，您已完成先前的課程，iOS還需要下列新增專案，才能啟動應用程式的保證工作階段。 將下列程式碼新增至 **[!UICONTROL SceneDelegate]**：

```swift {highlight="5"}
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
        // Called when the app in background is opened with a deep link.
        if let deepLinkURL = URLContexts.first?.url {
            // Start the Assurance session
            Assurance.startSession(url: deepLinkURL)
        }
    }
```

可以找到更多資訊 [此處](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/{target="_blank"}).

## 簽署

在Xcode中首次執行應用程式之前，請務必更新簽署。

1. 在Xcode中開啟專案。
1. 選取 **[!UICONTROL Luma]** 在「導覽器」中。
1. 選取 **[!UICONTROL Luma]** 目標。
1. 選取 **簽署與功能** 標籤。
1. 設定 **[!UICONTROL 自動管理簽署]**， **[!UICONTROL 團隊]**、和 **[!UICONTROL 組合識別碼]**.

   ![Xcode簽署功能](assets/xcode-signing-capabilities.png)

## 設定基礎URL

1. 前往Xcode中的專案。
1. 選取 **[!UICONTROL Luma]** 在「導覽器」中。
1. 選取 **[!UICONTROL Luma]** 目標。
1. 選取 **資訊** 標籤。
1. 若要新增基本URL，請向下捲動至 **URL型別** 並選取 **+** 按鈕。
1. 設定 **識別碼** 至您在中設定的組合識別碼 [簽署](#signing) (例如 `com.adobe.luma.tutorial.swiftui`)和 **URL配置** 至 `lumatutorialswiftui`.

   ![保證url](assets/assurance-url-type.png)

若要進一步瞭解iOS中的URL配置，請檢閱 [Apple的檔案](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app{target="_blank"}).

Assurance的運作方式是透過瀏覽器或QR碼開啟URL。 該URL以基礎URL開頭，此URL會開啟應用程式並包含其他引數。 這些唯一引數用於連線工作階段。


## 連線到工作階段

1. 在模擬器或連線的實體裝置上執行應用程式。
1. 選取 **[!UICONTROL 保證]** 從資料收集UI的左側邊欄。
1. 選取 **[!UICONTROL 建立工作階段]**.
1. 選取 **[!UICONTROL 開始]**.
1. 提供 **[!UICONTROL 工作階段名稱]** 例如 `Luma Mobile App Session` 和 **[!UICONTROL 基礎URL]**，即您在Xcode中輸入的URL配置，後面接著 `://`. 例如: `lumatutorialswiftui://`.
1. 選取&#x200B;**[!UICONTROL 「下一步」]**。
   ![保證建立工作階段](assets/assurance-create-session.png)
1. 在「建立新作業階段」對話方塊中：

   如果您使用實體裝置：

   * 選取 **[!UICONTROL 掃描QR碼]**. 使用實體裝置上的相機掃描二維碼，然後點選連結以開啟應用程式。

     ![保證qa程式碼](assets/assurance-qr-code.png)

   如果您使用模擬器：

   1. 選取 **[!UICONTROL 複製連結]**.
   1. 使用複製功能複製深層連結 ![複製](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) 按鈕並使用深層連結，在模擬器中以Safari開啟應用程式。
      ![保證副本連結](assets/assurance-copy-link.png)

1. 應用程式載入時，畫面會顯示強制回應對話方塊，要求您輸入步驟7顯示的PIN。

   <img src="assets/assurance-enter-pin.png" width="300">

   輸入PIN並選取 **[!UICONTROL 連線]**.


1. 如果連線成功，您會看到：
   * 「保證」圖示會浮動在應用程式上方。

   <img src="assets/assurance-modal.png" width="300">

   * Experience Cloud更新會在保證網頁式UI中傳入，顯示：

      1. 來自應用程式的體驗事件。
      1. 所選事件的詳細資料。
      1. 裝置和時間表。

     ![保證事件](assets/assurance-events.png)

如果您遇到任何挑戰，請檢閱 [技術](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/{target="_blank"}) 和 [一般檔案](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html{target="_blank"}).

>[!SUCCESS]
>
>您現在已設定應用程式，以便在教學課程的其餘部分使用Assurance 。<br/>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)


下一步： **[同意](consent.md)**
