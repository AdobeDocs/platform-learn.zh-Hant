---
title: 安裝Adobe Experience Platform Mobile SDK
description: 瞭解如何在行動應用程式中實施Adobe Experience Platform Mobile SDK。
hide: true
source-git-commit: 1b09f81b364fe8cfa9d5d1ac801d7781d1786259
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 1%

---

# 安裝Adobe Experience Platform Mobile SDK

瞭解如何在行動應用程式中實施Adobe Experience Platform Mobile SDK。

## 先決條件

* 已成功使用「 」中所述的擴充功能建置標籤程式庫。 [上一課程](configure-tags.md).
* 來自的開發環境檔案ID [行動安裝指示](configure-tags.md#generate-sdk-install-instructions).
* 下載空白 [範例應用程式](https://git.corp.adobe.com/rmaur/Luma){target="_blank"}.
* 使用體驗 [XCode](https://developer.apple.com/xcode/){target="_blank"}.

## 學習目標

在本課程中，您將會：

* 使用Swift封裝管理程式，將必要的SDK新增至您的專案。
* 註冊擴充功能。

>[!NOTE]
>
>在行動應用程式實作中，「擴充功能」和「SDK」這兩個辭彙幾乎可以互換。

## Swift封裝管理程式

不要使用CocoaPods和Pod檔案（如行動安裝指示中所述），請參閱 [產生SDK安裝指示](./configure-tags.md#generate-sdk-install-instructions))，您可使用Xcode的原生Swift Package Manager新增個別套件。

在Xcode中，使用 **[!UICONTROL 檔案]** > **[!UICONTROL 新增封裝……]** 並安裝下表中列出的所有套件。 在表格中選取套裝程式的連結，以取得特定套裝程式的完整URL。

| 封裝 | 說明 |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios.git) | 此 `AEPCore`， `AEPServices`、和 `AEPIdentity` 擴充功能是Adobe Experience Platform SDK的基礎，每個使用SDK的應用程式都必須包含擴充功能。 這些模組包含所有SDK擴充功能所需的一組通用功能與服務。<br/>`AEPCore` 包含事件中樞的實作。 事件中心是用於在應用程式和SDK之間傳遞事件的機制。 事件中心也用於在擴充功能之間共用資料。<br/>`AEPServices` 提供平台支援所需的數個可重複使用的實作，包括網路、磁碟存取和資料庫管理。<br/>`AEPIdentity` 實作與Adobe Experience Platform Identity服務的整合。<br/>`AEPSignal` 代表Adobe Experience Platform SDK的Signal擴充功能，可讓行銷人員傳送「訊號」至其應用程式，以將資料傳送至外部目的地或開啟URL。<br/>`AEPLifecycle` 代表Adobe Experience Platform SDK的生命週期擴充功能，可協助收集應用程式生命週期量度，例如應用程式安裝或升級資訊、應用程式啟動和工作階段資訊、裝置資訊，以及應用程式開發人員提供的任何其他內容資料。 |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios.git) | Adobe Experience Platform Edge Network行動擴充功能可讓您從行動應用程式傳送資料至Adobe Edge Network。 此擴充功能可讓您以更強大的方式實施Adobe Experience Cloud功能、透過單一網路呼叫提供多個Adobe解決方案，並同時將此資訊轉送至Adobe Experience Platform。<br/>Edge Network行動擴充功能是Adobe Experience Platform SDK的擴充功能，需要 `AEPCore` 和 `AEPServices` 事件處理的擴充功能以及 `AEPEdgeIdentity` 用於擷取身分的擴充功能，例如ECID。 |
| [AEP Edge Identity](https://github.com/adobe/aepsdk-edgeidentity-ios.git) | AEP Edge Identity行動擴充功能可讓您在使用Adobe Experience Platform SDK和Edge Network擴充功能時，處理來自行動應用程式的使用者身分資料。 |
| [AEP Edge同意](https://github.com/adobe/aepsdk-edgeconsent-ios.git) | AEP同意收集行動擴充功能可在使用Adobe Experience Platform SDK和Edge Network擴充功能時，從行動應用程式收集同意偏好設定。 |
| [AEP使用者設定檔](https://github.com/adobe/aepsdk-userprofile-ios.git) | Adobe Experience Platform使用者設定檔行動擴充功能是管理Adobe Experience Platform SDK之使用者設定檔的擴充功能。 |
| [AEP地點](https://github.com/adobe/aepsdk-places-ios) | AEPPlaces擴充功能可讓您追蹤「Adobe地點」使用者介面和「Adobe資料收集標籤」規則中定義的地理位置事件。 |
| [AEP傳訊](https://github.com/adobe/aepsdk-messaging-ios.git) | AEP傳訊擴充功能可讓您將推播通知權杖和推播通知點進意見傳送至Adobe Experience Platform。 |
| [AEP最佳化](https://github.com/adobe/aepsdk-optimize-ios) | AEP Optimize擴充功能提供API，使用Adobe Target或Adobe Journey OptimizerOffer decisioning在Adobe Experience Platform Mobile SDK中啟用即時個人化工作流程。 它需要 `AEPCore` 和 `AEPEdge` 將個人化查詢事件傳送至Experience Edge網路的擴充功能。 |
| [AEP保證](https://github.com/adobe/aepsdk-assurance-ios.git) | Assurance （又稱為project Griffon）是全新創新產品，可協助您檢查、證明、模擬及驗證如何在行動應用程式中收集資料或提供體驗。 此擴充功能可讓您的應用程式提供保證。 |


安裝所有套件後，您的Xcode **[!UICONTROL 套件相依性]** 畫面應如下所示：

![Xcode套件相依性](assets/xcode-package-dependencies.png)


## 匯入擴充功能

在Xcode中，瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** 並確保下列匯入專案為此來源檔案的一部分。

```swift
// import AEP MobileSDK libraries
import AEPCore
import AEPServices
import AEPIdentity
import AEPSignal
import AEPLifecycle
import AEPEdge
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPUserProfile
import AEPPlaces
import AEPMessaging
import AEPOptimize
import AEPAssurance
```

對執行相同操作 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]**.

## 更新AppDelegate

瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **AppDelegate** 在「Xcode專案」導覽器中。

1. 設定 `@AppStorage` 值 `environmentFileId` 至開發環境檔案ID值，而該ID值是您從步驟6中的標籤擷取的 [產生SDK安裝指示](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "b5cbd1a1220e/1857ef6cacb5/launch-2594f26b23cd-development"
   ```

1. 將下列程式碼新增至 `application(_, didFinishLaunchingWithOptions)` 函式。

   ```swift
   // Define extensions
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   
   // Register extensions
   MobileCore.registerExtensions(extensions, {
       // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
       Logger.aepMobileSDK.info("Luma - using mobile config: \(self.environmentFileId)")
       MobileCore.configureWith(appId: self.environmentFileId)
   
       // set this to false or comment it when deploying to TestFlight (default is false),
       // set this to true when testing on your device.
       MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])
       if appState != .background {
           // only start lifecycle if the application is not in the background
           MobileCore.lifecycleStart(additionalContextData: nil)
       }
   
       // assume unknown, adapt to your needs.
       MobileCore.setPrivacyStatus(.unknown)
   })
   ```

上述程式碼會執行下列動作：

1. 註冊必要的副檔名。
1. 設定MobileCore和其他擴充功能以使用標籤屬性設定。
1. 啟用偵錯記錄。 如需詳細資訊和選項，請參閱 [Adobe Experience Platform Mobile SDK檔案](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. 開始生命週期監視。 另請參閱 [生命週期](lifecycle-data.md) 如需詳細資訊，請參閱教學課程中的步驟。
1. 將預設同意設定為未知。 另請參閱 [同意](consent.md) 如需詳細資訊，請參閱教學課程中的步驟。

>[!IMPORTANT]
>
>請確定您已更新 `MobileCore.configureWith(appId: self.environmentFileId)` 使用 `appId` 根據 `environmentFileId` 從您建置以用於（開發、預備或生產）的標籤環境中。
>

>[!SUCCESS]
>
>您現在已安裝必要的套件，並更新專案，以正確註冊您要在教學課程的其餘部分使用的必要Adobe Experience Platform Mobile SDK擴充功能。<br/>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[設定保證](assurance.md)**
