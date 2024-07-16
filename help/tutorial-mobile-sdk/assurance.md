---
title: 設定Platform Mobile SDK實施的保證
description: 瞭解如何在行動應用程式中實作Assurance擴充功能。
feature: Mobile SDK,Assurance
jira: KT-14628
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: 576f85eda6e5888b9eafa15a705a99c3a70fed07
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 5%

---

# 設定保證

瞭解如何在行動應用程式中設定Adobe Experience Platform保證。

Assurance （正式名稱為Project Griffon）可協助您檢查、證明、模擬及驗證如何在行動應用程式中收集資料或提供體驗。

Assurance 可協助您檢查 Adobe Experience Platform Mobile SDK 產生的原始 SDK 事件。SDK 收集的所有事件都可供檢查。SDK 事件會載入清單檢視，並依時間排序。每個事件都有一個可提供更多詳細資料的詳細檢視。此外，也提供瀏覽SDK設定、資料元素、共用狀態和SDK擴充功能版本的其他檢視。 在產品檔案中進一步瞭解[保證](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html)。


## 先決條件

* 已成功安裝並設定SDK以設定應用程式。

## 學習目標

在本課程中，您將會：

* 確認您的組織擁有存取權（如果您沒有存取權，請提出要求）。
* 設定您的基底URL。
* 新增必要的iOS特定程式碼。
* 連線到工作階段。

## 確認存取

確認您的組織有權存取Assurance。 您身為使用者，應已新增至Adobe Experience Platform的設定檔。 如需詳細資訊，請參閱保證指南中的[使用者存取權](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=en)。

## 實作

除了一般[SDK安裝](install-sdks.md)之外，您已在先前的課程中完成，iOS還需要下列附加專案，才能啟動您應用程式的保證工作階段。

1. 導覽至Xcode專案導覽器中的&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]**。

1. 將下列程式碼新增至 `func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>`:

   ```swift
   // Called when the app in background is opened with a deep link.
   if let deepLinkURL = URLContexts.first?.url {
       // Start the Assurance session
       Assurance.startSession(url: deepLinkURL)
   }
   ```

   當應用程式於背景並使用深層連結開啟時，此程式碼就會啟動保證工作階段。

在[這裡](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}可以找到更多資訊。



## 定義套件組合識別碼

您必須提供應用程式的唯一套件組合識別碼。

1. 在Xcode中開啟專案。
1. 在專案導覽器中選取&#x200B;**[!DNL Luma]**。
1. 選取&#x200B;**[!DNL Luma]**&#x200B;目標。
1. 選取「**簽署與功能**」標籤。
1. 定義&#x200B;**[!UICONTROL 組合識別碼]**。

   >[!IMPORTANT]
   >
   >請確定您使用&#x200B;_唯一_&#x200B;組合識別碼並取代`com.adobe.luma.tutorial.swiftui`組合識別碼，因為每個組合識別碼必須是唯一的。 一般而言，您會使用反向DNS格式作為套件組合ID字串，例如`com.organization.brand.uniqueidentifier`。 例如，此教學課程的完成版本使用`com.adobe.luma.tutorial.swiftui`。


   ![Xcode簽署功能](assets/xcode-signing-capabilities.png){zoomable="yes"}


## 設定基礎URL

1. 前往Xcode中的專案。
1. 在專案導覽器中選取&#x200B;**[!DNL Luma]**。
1. 選取&#x200B;**[!DNL Luma]**&#x200B;目標。
1. 選取&#x200B;**資訊**&#x200B;索引標籤。
1. 若要新增基底URL，請向下捲動至&#x200B;**URL型別**&#x200B;並選取&#x200B;**+**&#x200B;按鈕。
1. 將&#x200B;**識別碼**&#x200B;設定為您選擇的組合識別碼，並設定您選擇的&#x200B;**URL配置**。

   ![保證url](assets/assurance-url-type.png)

   >[!IMPORTANT]
   >
   >請確定您使用&#x200B;_唯一_&#x200B;組合識別碼並取代`com.adobe.luma.tutorial.swiftui`組合識別碼，因為每個組合識別碼必須是唯一的。 一般而言，您會使用反向DNS格式作為套件組合ID字串，例如`com.organization.brand.uniqueidentifier`。 您可以使用您在[定義組合識別碼](#define-bundle-identifier)中使用的相同組合識別碼。<br/>同樣地，使用唯一的URL配置，並以您唯一的URL配置取代已經提供的`lumatutorialswiftui`。

若要進一步瞭解iOS中的URL配置，請檢閱[Apple的檔案](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}。

Assurance的運作方式是透過瀏覽器或QR碼開啟URL。 該URL以基礎URL開頭，此URL會開啟應用程式並包含其他引數。 這些唯一引數用於連線工作階段。


## 連線到工作階段

在Xcode中：

1. 使用![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg)，在模擬器中或在Xcode的實體裝置上建置或重建並執行應用程式。

   >[!TIP]
   >
   >您可選擇是否要「清除」組建，尤其是在看到非預期結果時。 若要這麼做，請從Xcode **[!UICONTROL 產品]**&#x200B;功能表選取&#x200B;**[!UICONTROL 清除組建資料夾……]**。


1. 在&#x200B;**[!UICONTROL 允許[Luma應用程式]使用您的位置]**&#x200B;對話方塊中，選取&#x200B;**[!UICONTROL 使用應用程式時允許]**。

   <img src="assets/geolocation-permissions.png" width="300">

1. 在&#x200B;**[!UICONTROL 「Luma應用程式」想要傳送通知]**&#x200B;對話方塊中，選取&#x200B;**[!UICONTROL 允許]**。

   <img src="assets/notification-permissions.png" width="300">

1. 選取&#x200B;**[!UICONTROL 繼續……]**&#x200B;以允許應用程式追蹤您的活動。

   <img src="assets/tracking-continue.png" width="300">

1. 在&#x200B;**[!UICONTROL 允許[Luma應用程式]追蹤其他公司應用程式和網站]**&#x200B;對話方塊中，選取&#x200B;**[!UICONTROL 允許]**。

   <img src="assets/tracking-allow.png" width="300">


在您的瀏覽器中：

1. 前往資料收集UI。
1. 從左側邊欄選取&#x200B;**[!UICONTROL 保證]**。
1. 選取&#x200B;**[!UICONTROL 建立工作階段]**。
1. 選取&#x200B;**[!UICONTROL 開始]**。
1. 提供&#x200B;**[!UICONTROL 工作階段名稱]**，例如`Luma Mobile App Session`和&#x200B;**[!UICONTROL 基底URL]**，這是您在Xcode中輸入的URL配置，後面接著`://`，例如： `lumatutorialswiftui://`
1. 選取&#x200B;**[!UICONTROL 下一步]**。
   ![保證建立工作階段](assets/assurance-create-session.png)
1. 在&#x200B;**[!UICONTROL 建立新工作階段]**&#x200B;模型對話方塊中：

   如果您使用實體裝置：

   * 選取&#x200B;**[!UICONTROL 掃描QR碼]**。 若要開啟應用程式，請使用實體裝置上的相機掃描二維碼並點選連結。

     ![保證qa代碼](assets/assurance-qr-code.png)

   如果您使用模擬器：

   1. 選取&#x200B;**[!UICONTROL 複製連結]**。
   1. 使用![Copy](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)複製深層連結，並使用深層連結在模擬器中使用Safari開啟應用程式。
      ![保證副本連結](assets/assurance-copy-link.png)

1. 應用程式載入時，畫面會顯示強制回應對話方塊，要求您輸入步驟7顯示的PIN。

   <img src="assets/assurance-enter-pin.png" width="300">

   輸入PIN並選取&#x200B;**[!UICONTROL 連線]**。


1. 如果連線成功，您會看到：
   * 「保證」圖示會浮動在應用程式上方。

     <img src="assets/assurance-modal.png" width="300">

   * Experience Cloud更新從Assurance UI傳入，顯示：

      1. 來自應用程式的體驗事件。
      1. 所選事件的詳細資料。
      1. 裝置和時間表。

         ![保證事件](assets/assurance-events.png)

如果您遇到任何挑戰，請檢閱[技術](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"}和[一般檔案](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html){target="_blank"}。


## 驗證擴充功能

若要確認您的應用程式是否使用最新的擴充功能：

1. 選取&#x200B;**[!UICONTROL 設定]**。

1. 選取![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL 延伸版本]**&#x200B;的![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg)。

1. 選取「**[!UICONTROL 儲存]**」。

   ![設定擴充功能版本](assets/assurance-configure-extension-versions.png)

1. 選取![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL 擴充功能版本]**，以檢視最新可用擴充功能的概觀，以及您應用程式版本中使用的擴充功能。

   ![延伸功能版本](assets/assurance-extension-versions.png)

1. 若要更新您的擴充功能版本（例如，**[!UICONTROL 傳訊]**&#x200B;與&#x200B;**[!UICONTROL 最佳化]**），請從&#x200B;**[!UICONTROL 封裝相依性]** （例如，**[!UICONTROL AEPMessaging]**）選取封裝（擴充功能），然後從內容功能表選取&#x200B;**[!UICONTROL 更新封裝]**。 Xcode將更新套件相依性。


>[!NOTE]
>
>更新您在Xcode中的擴充功能（套件）後，請關閉並刪除目前的工作階段，並重複從[連線到工作階段](#connecting-to-a-session)和[驗證擴充功能](#verify-extensions)的所有步驟，以確保保證在新的保證工作階段中正確報告正確的擴充功能。





>[!SUCCESS]
>
>您現在已設定應用程式，以便在教學課程的其餘部分使用Assurance 。
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享


下一個： **[實作同意](consent.md)**
