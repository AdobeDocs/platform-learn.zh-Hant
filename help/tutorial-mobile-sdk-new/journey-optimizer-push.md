---
title: Adobe Journey Optimizer推送訊息
description: 瞭解如何使用Platform Mobile SDK和Adobe Journey Optimizer建立推送訊息至行動應用程式。
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
hide: true
source-git-commit: 2f9298a140c7bd483c8c533427f0e90d90d14af0
workflow-type: tm+mt
source-wordcount: '1899'
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
* 實體iOS裝置或模擬器以進行測試。

## 學習目標

在本課程中，您將會：

* 向Apple推播通知服務(APN)註冊應用程式ID。
* 建立 **[!UICONTROL 應用程式表面]** 在AJO中。
* 更新您的 **[!UICONTROL 綱要]** 以包含推送訊息欄位。
* 安裝與設定 **[!UICONTROL Adobe Journey Optimizer]** 標籤延伸。
* 更新您的應用程式以包含AJO標籤擴充功能。
* 驗證Assurance中的設定。
* 傳送測試訊息。
* 在Journey Optimizer中定義您自己的推播通知事件、歷程和體驗。
* 從應用程式內傳送您自己的推播通知。


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
   1. 選取 **[!UICONTROL 儲存至程式庫並建置]**.
      ![AJO擴充功能設定](assets/push-tags-ajo.png)

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
1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]**.
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

1. 新增 `MobileCore.setPushIdentifier` 至 `func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data)` 函式。

   ```swift
   // Send push token to Experience Platform
   MobileCore.setPushIdentifier(deviceToken)
   ```

   此函式擷取安裝應用程式的裝置所獨有的裝置代號。 然後使用您已設定的設定來設定推播通知傳送的代號，該設定依賴Apple的推播通知服務(APNS)。

## 使用保證進行驗證

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


## 建立您自己的推播通知

若要建立自己的推播通知，您必須在Journey Optimizer中定義觸發歷程的事件，負責傳送推播通知。

### 定義事件

1. 在Journey Optimizer UI中，選取 **[!UICONTROL 設定]** 從左側邊欄。

1. 在 **[!UICONTROL 儀表板]** 熒幕，選取 **[!UICONTROL 管理]** 中的按鈕 **[!UICONTROL 活動]** 圖磚。

1. 在 **[!UICONTROL 活動]** 熒幕，選取 **[!UICONTROL 建立事件]**.

1. 在 **[!UICONTROL 編輯事件event1]** 窗格：

   1. 輸入 `LumaTestEvent` 作為 **[!UICONTROL 名稱]** 事件的。
   1. 提供 **[!UICONTROL 說明]**，例如 `Test event to trigger push notifications in Luma app`.

   1. 選取您先前在中建立的行動應用程式體驗事件結構描述 [建立XDM結構描述](create-schema.md) 從 **[!UICONTROL 結構描述]** 清單，例如 **[!UICONTROL Luma行動應用程式事件結構描述v.1]**.
   1. 選取 ![編輯](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) 在 **[!UICONTROL 欄位]** 清單。

      ![編輯事件步驟1](assets/ajo-edit-event1.png)

      在 **[!UICONTROL 欄位]** 對話方塊，確定已選取下列欄位(在永遠選取的預設欄位之上（_id、id和時間戳記）)。 您可以使用下拉式清單在 **[!UICONTROL 已選取]**， **[!UICONTROL 全部]** 和 **[!UICONTROL 主要]** 或使用 ![搜尋](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) 欄位。

      * **[!UICONTROL 已識別的應用程式(ID)]**，
      * **[!UICONTROL 事件型別(eventType)]**，
      * **[!UICONTROL 主要（主要）]**.

      ![編輯事件欄位](assets/ajo-event-fields.png)

      然後選取 **[!UICONTROL 確定]**.

   1. 選取 ![編輯](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) 在 **[!UICONTROL 事件ID條件]** 欄位。

      1. 在 **[!UICONTROL 新增事件ID條件]** 對話方塊，拖放 **[!UICONTROL 應用程式識別碼(ID)]** 底下 **[!UICONTROL 應用程式（應用程式）]** 開啟到 **[!UICONTROL 將元素拖放到這裡]**.
      1. 在彈出視窗中，輸入來自Xcode的套件組合識別碼，例如 `com.adobe.luma.tutorial.swiftui` 在旁邊的欄位中 **[!UICONTROL 等於]**.
      1. 按一下 **[!UICONTROL 確定]**.
      1. 按一下 **[!UICONTROL 確定]**.
         ![編輯事件條件](assets/ajo-edit-condition.png)

   1. 選取 **[!UICONTROL ECID (ECID)]** 從 **[!UICONTROL 名稱空間]** 清單。 自動 **[!UICONTROL 設定檔識別碼]** 欄位已填入 **[!UICONTROL 對應identityMap的索引鍵ECID的第一個元素的ID]**.
   1. 選取「**[!UICONTROL 儲存]**」。
      ![編輯事件步驟2](assets/ajo-edit-event2.png)

您剛才已根據您先前在本教學課程中建立的行動應用程式體驗事件結構描述建立事件設定。 此事件設定將會使用您的行動應用程式識別碼篩選傳入的體驗事件，因此您確定只有從行動應用程式起始的事件才會觸發您將在下一個步驟中建立的歷程。

### 建立歷程

您的下一個步驟是建立歷程，在收到適當事件時觸發推播通知的傳送。

1. 在Journey Optimizer UI中，選取 **[!UICONTROL 歷程]** 從左側邊欄。
1. 選取 **[!UICONTROL 建立歷程]**.
1. 在 **[!UICONTROL 歷程屬性]** 面板：

   1. 輸入 **[!UICONTROL 名稱]** 例如，對於歷程 `Luma - Test Push Notification Journey`.
   1. 輸入 **[!UICONTROL 說明]** 例如，對於歷程 `Journey for test push notifications in Luma mobile app`.
   1. 確定 **[!UICONTROL 允許重新進入]** 已選取並設定 **[!UICONTROL 重新進入等待期]** 至 **[!UICONTROL 30]** **[!UICONTROL 秒]**.
   1. 選取 **[!UICONTROL 確定]**.
      ![歷程屬性](assets/ajo-journey-properties.png)

1. 回到歷程畫布，從 **[!UICONTROL 活動]**，拖放您的 ![事件](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg) **[!UICONTROL LumaTestEvent]** 在畫布上顯示 **[!UICONTROL 選取進入事件或讀取對象活動]**.

   * 在事件中： **[!UICONTROL LumaTestEvent]** 面板，輸入 **[!UICONTROL 標籤]**，例如 `Luma Test Event`.

1. 從 **[!UICONTROL 動作]** 下拉式清單、拖放 ![推播](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PushNotification_18_N.svg) **[!UICONTROL 推播]** 於 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 直接顯示至您的 **[!UICONTROL LumaTestEvent]** 活動。 在 **[!UICONTROL 動作：推播]** 窗格：

   1. 提供 **[!UICONTROL 標籤]**，例如 `Luma Test Push Notification`，提供 **[!UICONTROL 說明]**，例如 `Test push notification for Luma mobile app`，選取 **[!UICONTROL 異動]** 從 **[!UICONTROL 類別]** 清單並選取 **[!UICONTROL Luma]** 從 **[!UICONTROL 推播表面]**.
   1. 選取 ![編輯](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 編輯內容]** 以開始編輯實際的推播通知。
      ![推送屬性](assets/ajo-push-properties.png)

      在 **[!UICONTROL 推播通知]** 編輯者：

      1. 輸入 **[!UICONTROL 標題]**，例如 `Luma Test Push Notification` 並輸入 **[!UICONTROL 內文]**，例如 `Test push notification for Luma mobile app`.
      1. 若要儲存並離開編輯器，請選取 ![左側V形](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronLeft_18_N.svg).
         ![推播編輯器](assets/ajo-push-editor.png)

   1. 若要儲存並完成推播通知定義，請選取「 」 **[!UICONTROL 確定]**.

1. 您的歷程應如下所示。 選取 **[!UICONTROL 發佈]** 以發佈並啟用您的歷程。
   ![完成的歷程](assets/ajo-journey-finished.png)


## 觸發推播通知

您已具備傳送推播通知的所有要素。 剩下的問題是如何觸發此推播通知。 本質上，它與您之前看到的相同：只要傳送具有適當裝載的體驗事件即可。

此時，您即將傳送的體驗事件未建構為建構簡單的XDM字典。 您即將使用代表推播通知裝載的結構。 定義專用資料型別是在應用程式中實作建構體驗事件裝載的替代方式。

1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 模型]** > **[!UICONTROL XDM]** > **[!UICONTROL TestPushPayload]** 並檢查程式碼。

   ```swift
   import Foundation
   
   // MARK: - TestPush
   struct TestPushPayload: Codable {
      let application: Application
      let eventType: String
   }
   
   // MARK: - Application
   struct Application: Codable {
      let id: String
   }
   ```

   程式碼可呈現您要傳送以觸發測試推播通知歷程的下列簡單裝載

   ```json
   {
      "eventType": string,
      "application" : [
          "id": string
      ]
   }
   ```

1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** 在Xcode專案導覽器中，新增下列程式碼至 `func sendTestPushEvent(applicationId: String, eventType: String)`：

   ```swift
   Task {
       let testPushPayload = TestPushPayload(
           application: Application(
               id: applicationId
           ),
           eventType: eventType
       )
       // send the final experience event
       await sendExperienceEvent(
           xdm: testPushPayload.asDictionary() ?? [:]
       )
   }
   ```

   此程式碼會建立 `testPushPayload` 使用提供給函式的引數建立例項(`applicationId` 和 `eventType`)然後呼叫 `sendExperienceEvent` 將裝載轉換為字典時。 這次的程式碼也考慮到了呼叫Adobe Experience Platform SDK的非同步層面，該環節使用Swift的並行模式，並基於 `await` 和 `async`.

1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 檢視]** > **[!UICONTROL 一般]** > **[!UICONTROL 組態檢視]** 在Xcode專案導覽器中。 在推播通知按鈕定義中，新增下列程式碼，以傳送測試推播通知體驗事件裝載，以便在點選按鈕時觸發您的歷程。

   ```swift
   // Setting parameters and calling function to send push notification
   let eventType = "mobileapp.testpush"
   let applicationId = Bundle.main.bundleIdentifier ?? "No bundle id found"
   await MobileSDK.shared.sendTestPushEvent(applicationId: applicationId, eventType: eventType)   
   ```


## 使用您的應用程式進行驗證

1. 在裝置上或在模擬器中開啟您的應用程式。

1. 前往 **[!UICONTROL 設定]** 標籤。

1. 點選 **[!UICONTROL 推播通知]**. 您會看到推播通知出現在應用程式中。
   <img src="assets/ajo-test-push.png" width="300" />


## 在您的應用程式中實作

您現在應該擁有所有工具，可以開始將推播通知（如有必要）新增至Luma應用程式。 例如，在登入應用程式或接近特定地理位置時歡迎使用者。

>[!SUCCESS]
>
>您現在已針對Adobe Experience Platform Mobile SDK使用Adobe Journey Optimizer和Adobe Journey Optimizer擴充功能，為推播通知啟用應用程式。<br/>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[使用Journey Optimizer的應用程式內傳訊](journey-optimizer-inapp.md)**

