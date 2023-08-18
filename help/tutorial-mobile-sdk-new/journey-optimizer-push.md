---
title: Adobe Journey Optimizer推送訊息
description: 瞭解如何使用Platform Mobile SDK和Adobe Journey Optimizer建立推送訊息至行動應用程式。
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 2%

---

# Adobe Journey Optimizer推送訊息

瞭解如何使用Platform Mobile SDK和Adobe Journey Optimizer為行動應用程式建立推送訊息。

Journey Optimizer可讓您建立歷程，並傳送訊息給目標對象。 在使用Journey Optimizer傳送推播通知之前，您必須確保有適當的設定和整合。 若要瞭解Adobe Journey Optimizer中的推播通知資料流程，請參閱 [說明檔案](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>本課程為選修課程，僅適用於想要傳送推送訊息的Adobe Journey Optimizer使用者。


## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。
* 如所述存取Adobe Journey Optimizer和足夠的許可權 [此處](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). 此外，您需要具備下列Adobe Journey Optimizer功能的足夠許可權。
   * 建立應用程式表面。
   * 建立歷程
   * 建立訊息.
   * 建立訊息預設集.
* 付費的Apple開發人員帳戶，具有建立憑證、識別碼和金鑰的足夠存取權。
* 用於測試的實體iOS裝置。

## 學習目標

在本課程中，您將會：

* 向Apple推播通知服務(APN)註冊應用程式ID。
* 建立 **[!UICONTROL 應用程式表面]** 在AJO中。
* 更新您的 **[!UICONTROL 綱要]** 以包含推送訊息欄位。
* 安裝與設定 **[!UICONTROL Adobe Journey Optimizer]** 標籤延伸。
* 更新您的應用程式以包含AJO標籤擴充功能。
* 驗證Assurance中的設定。
* 傳送測試訊息。


## 向APN註冊應用程式ID

下列步驟並非特定於Adobe Experience Cloud，而是設計用於引導您完成APN設定。

### 建立私密金鑰

1. 在Apple開發人員入口網站中，導覽至 **[!UICONTROL 金鑰]**.
1. 若要建立金鑰，請選取 **[!UICONTROL +]**.
   ![建立新金鑰](assets/mobile-push-apple-dev-new-key.png)

1. 提供 **[!UICONTROL 金鑰名稱]**.
1. 選取 **[!UICONTROL APN]** 核取方塊。
1. 選取 **[!UICONTROL 繼續]**.
   ![設定新金鑰](assets/mobile-push-apple-dev-config-key.png)
1. 檢閱設定並選取 **[!UICONTROL 註冊]**.
1. 下載 `.p8` 私密金鑰。 它用於App Surface設定。
1. 記下 [!UICONTROL 金鑰ID]. 它用於App Surface設定。
1. 記下 [!UICONTROL 團隊ID]. 它用於App Surface設定。
   ![金鑰詳細資訊](assets/push-apple-dev-key-details.png)

其他檔案包括 [可在此處找到](https://help.apple.com/developer-account/#/devcdfbb56a3).

## 在資料收集中新增應用程式推送認證

1. 從 [資料收集介面](https://experience.adobe.com/data-collection/)，選取 **[!UICONTROL 應用程式表面]** 在左側面板中。
1. 若要建立組態，請選取 **[!UICONTROL 建立應用程式表面]**.
   ![應用程式表面首頁](assets/push-app-surface.png)
1. 輸入 **[!UICONTROL 名稱]** 例如，針對設定 `Luma App Tutorial`  .
1. 在行動應用程式設定中，選取 **[!UICONTROL Apple iOS]**.
1. 在「應用程式ID (iOS套件組合ID)」欄位中輸入行動應用程式套件組合ID。 如果您使用Luma應用程式進行追蹤，則該值為 `com.adobe.luma.tutorial.swiftui`.
1. 切換至 **[!UICONTROL 推送認證]** 按鈕以新增您的認證。
1. 拖放您的 `.p8` **Apple推播通知驗證金鑰** 檔案。
1. 提供 **[!UICONTROL 金鑰ID]**，在建立期間指派的10個字元字串 `p8` 驗證金鑰。 此區域位於 **[!UICONTROL 金鑰]** 定位於 **憑證、識別碼和設定檔** Apple開發人員入口網站頁面的頁面。
1. 提供 **[!UICONTROL 團隊ID]**. 團隊ID是一個值，可在下找到 **會籍** 標籤或Apple開發人員入口網站頁面頂端。
1. 選取「**[!UICONTROL 儲存]**」。

   ![應用程式表面設定](assets/push-app-surface-config.png)

## 安裝Adobe Journey Optimizer標籤擴充功能

1. 瀏覽至 **[!UICONTROL 標籤]** > **[!UICONTROL 擴充功能]** > **[!UICONTROL 目錄]**，
1. 開啟您的屬性，例如 **[!UICONTROL Luma行動應用程式教學課程]**.
1. 選取 **[!UICONTROL 目錄]**.
1. 搜尋 **[!UICONTROL Adobe Journey Optimizer]** 副檔名。
1. 安裝擴充功能。
1. 在 **[!UICONTROL 安裝擴充功能]** 對話方塊
   1. 選取環境，例如 **[!UICONTROL 開發]**.
   1. 選取 **[!UICONTROL AJO推播追蹤體驗事件資料集]** 資料集 **[!UICONTROL 事件資料集]** 下拉式清單。
      ![AJO擴充功能設定](assets/push-tags-ajo.png)
   1. 選取 **[!UICONTROL 儲存至程式庫並建置]**.

>[!NOTE]
>
>如果您沒有看到 `AJO Push Tracking Experience Event Dataset` 如需使用，請聯絡客戶服務。
>

## 在應用程式中實作Adobe Journey Optimizer

如先前課程所述，安裝行動標籤擴充功能僅會提供設定。 接下來，您必須安裝並註冊傳訊SDK。 如果這些步驟不清楚，請查閱 [安裝SDK](install-sdks.md) 區段。

>[!NOTE]
>
>如果您已完成 [安裝SDK](install-sdks.md) 區段，則已安裝SDK且您可以跳至步驟#7。
>

1. 在Xcode中，確認 [AEP傳訊](https://github.com/adobe/aepsdk-messaging-ios.git) 會新增至套件相依性中的套件清單中。 另請參閱 [Swift封裝管理程式](install-sdks.md#swift-package-manager).
1. 開啟Xcode並導覽至 **[!UICONTROL AppDelegate]**.
1. 確定 `AEPMessaging` 是匯入清單的一部分。

   `import AEPMessaging`

1. 確定 `Messaging.self` 是您註冊的擴充功能陣列的一部分。

   ```swift
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
   ```

1. 新增 `MobileCore.setPushIdentifier` 至 `application(_, didRegisterForRemoteNotificationsWithDeviceToken)` 函式。

   ```swift {highlight="7"}
   func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       // Required to log the token
       let tokenParts = deviceToken.map { data in String(format: "%02.2hhx", data) }
       let token = tokenParts.joined()
       Logger.notifications.info("didRegisterForRemoteNotificationsWithDeviceToken - device token: \(token)")
   
       // Send push token to Experience Platform
       MobileCore.setPushIdentifier(deviceToken)
       currentDeviceToken = token
   }
   ```

   此函式擷取安裝應用程式的裝置所獨有的裝置代號，並將代號傳送至AdobeApple以進行推送訊息傳送。

## 透過傳送測試推送訊息來驗證

1. 檢閱 [設定指示](assurance.md) 區段。
1. 在您的實體裝置或模擬器上安裝應用程式。
1. 使用保證產生的URL啟動應用程式。
1. 在Assurance UI中，選取 **[!UICONTROL 設定]**.
   ![設定點按](assets/push-validate-config.png)
1. 選取 ![加號](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 按鈕旁邊 **[!UICONTROL 推送偵錯]**.
1. 選取「**[!UICONTROL 儲存]**」。
   ![儲存](assets/push-validate-save.png)
1. 選取 **[!UICONTROL 推送偵錯]** 從左側導覽。
1. 選取 **[!UICONTROL 驗證設定]** 標籤。
1. 從中選擇您的裝置 **[!UICONTROL 使用者端]** 清單。
1. 確認您沒有收到任何錯誤。
   ![驗證](assets/push-validate-confirm.png)
1. 選取 **[!UICONTROL 傳送測試推播]** 標籤。
1. （選擇性）變更預設詳細資料 **[!UICONTROL 標題]** 和 **[!UICONTROL 內文]**
1. 選取 ![錯誤](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL 傳送測試推播通知]**.
1. 檢查 **[!UICONTROL 測試結果]**.
1. 您應該會在應用程式中看到推播通知。

   <img src="assets/luma-app-push.png" width="300" />


>[!SUCCESS]
>
>您現在已使用Adobe Experience Platform Mobile SDK的Adobe Journey Optimizer擴充功能為推播通知啟用應用程式。<br/>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[結論和後續步驟](conclusion.md)**
