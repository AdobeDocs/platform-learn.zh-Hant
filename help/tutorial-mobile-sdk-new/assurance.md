---
title: 設定保證
description: 瞭解如何在行動應用程式中實作Assurance擴充功能。
feature: Mobile SDK,Assurance
hide: true
exl-id: 49d608e7-e9c4-4bc8-8a8a-5195f8e2ba42
source-git-commit: d1338390986a242c91051e94134f8d69e979c0b4
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 6%

---

# 設定保證

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

確認您的組織有權存取Assurance。 您身為使用者，應已新增至Adobe Experience Platform的設定檔。 另請參閱 [使用者存取權](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=en) 在保證指南中取得詳細資訊。

## 實作

除了一般 [SDK安裝](install-sdks.md)，您已完成先前的課程，iOS還需要下列新增專案，才能啟動應用程式的保證工作階段。

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** 在您的Xcode專案導覽器中。

1. 將下列程式碼新增至 `func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>`:

   ```swift
   // Called when the app in background is opened with a deep link.
   if let deepLinkURL = URLContexts.first?.url {
       // Start the Assurance session
       Assurance.startSession(url: deepLinkURL)
   }
   ```

   當應用程式於背景並使用深層連結開啟時，此程式碼就會啟動保證工作階段。

可以找到更多資訊 [此處](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.

<!-- not initially required

## Signing

Signing the application is only required for the [Create and send push notifications](journey-optimizer-push.md) and the [Create and send in-app messages](journey-optimizer-inapp.md) lessons in this tutorial. These lessons require an Apple provisioning profile which **requires a paid Apple developer account**.

To update the signing for the lessons that require that you sign the application:

1. Open the project in Xcode.
1. Select **[!DNL Luma]** in the Project navigator.
1. Select the **[!DNL Luma]** target.
1. Select the **Signing & Capabilities** tab.
1. Configure **[!UICONTROL Automatic manage signing]**, **[!UICONTROL Team]**, and **[!UICONTROL Bundle Identifier]**, or use your specific Apple development provisioning details. 
 
   >[!IMPORTANT]
   >
   >Ensure you use a _unique_ bundle identifier and replace the `com.adobe.luma.tutorial.swiftui` bundle identifier, as each bundle identifier needs to be unique. Typically, you use a reverse-DNS format for bundle ID strings, like `com.organization.brand.uniqueidentifier`. The Finished version of this tutorial, for example, uses `com.adobe.luma.tutorial.swiftui`.


    ![Xcode signing capabilities](assets/xcode-signing-capabilities.png){zoomable="yes"}

-->

## 設定基礎URL

1. 前往Xcode中的專案。
1. 選取 **[!DNL Luma]** 在「專案」導覽器中。
1. 選取 **[!DNL Luma]** 目標。
1. 選取 **資訊** 標籤。
1. 向下捲動至 **URL型別(1)** 若尚未開啟，則使用>形箭號開啟區段。
1. 設定 **識別碼** 至您選擇的組合識別碼，並設定 **URL配置** ，依您的選擇而定。

   ![保證url](assets/assurance-url-type.png)

   >[!IMPORTANT]
   >
   >確定您使用 _獨特_ 組合識別碼，因此請將 `com.adobe.luma.tutorial.swiftui` 組合識別碼，因為每個組合識別碼必須是唯一的。 通常，套件組合ID字串會使用反向DNS格式，例如 `com.organization.brand.uniqueidentifier`.<br/>同樣地，使用唯一的URL配置，因此請取代已經提供的 `lumatutorialswiftui` 使用您唯一的URL配置。

若要進一步瞭解iOS中的URL配置，請檢閱 [Apple的檔案](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

Assurance的運作方式是透過瀏覽器或QR碼開啟URL。 該URL以基礎URL開頭，此URL會開啟應用程式並包含其他引數。 這些唯一引數用於連線工作階段。


## 連線到工作階段

在Xcode中：

1. 在模擬器中或從Xcode在實體裝置上建置或重建及執行應用程式，使用 ![播放](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

   >[!TIP]
   >
   >您可選擇是否要「清除」組建，尤其是在看到非預期結果時。 要執行此操作，請選取 **[!UICONTROL 清除建置資料夾……]** 從Xcode **[!UICONTROL 產品]** 功能表。


1. 在 **[!UICONTROL 允許「Luma應用程式」使用您的位置]** 對話方塊，選取 **[!UICONTROL 使用應用程式時允許]**.

   <img src="assets/geolocation-permissions.png" width="300">

1. 在 **[!UICONTROL 「Luma應用程式」想要傳送通知給您]** 對話方塊，選取 **[!UICONTROL 允許]**.

   <img src="assets/notification-permissions.png" width="300">

1. 選取 **[!UICONTROL 繼續……]** 允許應用程式追蹤您的活動。

   <img src="assets/tracking-continue.png" width="300">

1. 在 **[!UICONTROL 允許「Luma應用程式」追蹤您在其他公司的應用程式和網站上的活動]** 對話方塊，選取 **[!UICONTROL 允許]**.

   <img src="assets/tracking-allow.png" width="300">


在您的瀏覽器中：

1. 前往資料收集UI。
1. 選取 **[!UICONTROL 保證]** 從左側邊欄。
1. 選取 **[!UICONTROL 建立工作階段]**.
1. 選取 **[!UICONTROL 開始]**.
1. 提供 **[!UICONTROL 工作階段名稱]** 例如 `Luma Mobile App Session` 和 **[!UICONTROL 基礎URL]**，即您在Xcode中輸入的URL配置，後面接著 `://` 例如： `lumatutorialswiftui://`
1. 選取&#x200B;**[!UICONTROL 「下一步」]**。
   ![保證建立工作階段](assets/assurance-create-session.png)
1. 在 **[!UICONTROL 建立新工作階段]** 模型對話方塊：

   如果您使用實體裝置：

   * 選取 **[!UICONTROL 掃描QR碼]**. 若要開啟應用程式，請使用實體裝置上的相機掃描二維碼並點選連結。

     ![保證qa程式碼](assets/assurance-qr-code.png)

   如果您使用模擬器：

   1. 選取 **[!UICONTROL 複製連結]**.
   1. 複製深層連結，使用 ![複製](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)  並使用深層連結，在模擬器中以Safari開啟應用程式。
      ![保證副本連結](assets/assurance-copy-link.png)

1. 應用程式載入時，畫面會顯示強制回應對話方塊，要求您輸入步驟7顯示的PIN。

   <img src="assets/assurance-enter-pin.png" width="300">

   輸入PIN並選取 **[!UICONTROL 連線]**.


1. 如果連線成功，您會看到：
   * 「保證」圖示會浮動在應用程式上方。

     <img src="assets/assurance-modal.png" width="300">

   * Experience Cloud更新從Assurance UI傳入，顯示：

      1. 來自應用程式的體驗事件。
      1. 所選事件的詳細資料。
      1. 裝置和時間表。

         ![保證事件](assets/assurance-events.png)

如果您遇到任何挑戰，請檢閱 [技術](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} and [general documentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html){target="_blank"}.


## 驗證擴充功能

若要確認您的應用程式是否使用最新的擴充功能：

1. 選取 **[!UICONTROL 設定]**.

1. 選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 的 ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL 擴充功能版本]**.

1. 選取「**[!UICONTROL 儲存]**」。

   ![設定擴充功能版本](assets/assurance-configure-extension-versions.png)

1. 選取 ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL 擴充功能版本]** 以檢視最新可用擴充功能的概觀，以及應用程式版本中使用的擴充功能。

   ![擴充功能版本](assets/assurance-extension-versions.png)

1. 若要更新擴充功能版本(例如 **[!UICONTROL 傳訊]** 和 **[!UICONTROL 最佳化]**)從中選擇套件（擴充功能） **[!UICONTROL 套件相依性]** (例如， **[!UICONTROL AEPMessaging]**)並從快顯選單中選取 **[!UICONTROL 更新封裝]**. Xcode將更新套件相依性。


>[!NOTE]
>
>在Xcode中更新擴充功能（套件）後，請關閉並刪除目前的工作階段，並重複的所有步驟，從 [連線到工作階段](#connecting-to-a-session) 和 [驗證擴充功能](#verify-extensions) 確保Assurance在新的Assurance工作階段中正確報告正確的延伸模組。





>[!SUCCESS]
>
>您現在已設定應用程式，以便在教學課程的其餘部分使用Assurance 。
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)


下一步： **[實作同意](consent.md)**
