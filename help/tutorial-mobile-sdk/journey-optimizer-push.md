---
title: Adobe Journey Optimizer推送訊息
description: 瞭解如何使用Platform Mobile SDK和Adobe Journey Optimizer建立推送訊息至行動應用程式。
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 2%

---

# Adobe Journey Optimizer推送訊息

瞭解如何使用Platform Mobile SDK和Adobe Journey Optimizer為行動應用程式建立推送訊息。

>[!INFO]
>
> 在2023年11月下旬，此教學課程將由使用新範例行動應用程式的新教學課程取代

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

### 建立 `.p8` 私密金鑰

1. 在Apple開發人員入口網站中，導覽至 **[!UICONTROL 金鑰]**.
1. 選取+圖示以建立金鑰。
   ![建立新金鑰](assets/mobile-push-apple-dev-new-key.png)

1. 提供 **[!UICONTROL 金鑰名稱]**.
1. 選取 **[!UICONTROL APN]** 核取方塊。
1. 選取 **[!UICONTROL 繼續]**.
   ![設定新金鑰](assets/mobile-push-apple-dev-config-key.png)
1. 檢閱設定並選取 **[!UICONTROL 註冊]**.
1. 下載 `.p8` 私密金鑰。 它用於App Surface設定。
1. 記下 **[!UICONTROL 金鑰ID]**. 它用於App Surface設定。

其他檔案包括 [可在此處找到](https://help.apple.com/developer-account/#/devcdfbb56a3).

### 擷取您的Apple開發人員團隊ID

1. 在Apple開發人員入口網站中，導覽至 **[!UICONTROL 會籍]**.
1. 您的 **[!UICONTROL 團隊ID]** 會與其他會員資格資訊一併列出。 它用於App Surface設定。

## 在資料收集中新增應用程式推送認證

1. 從 [資料收集介面](https://experience.adobe.com/data-collection/)，選取左側面板中的「應用程式表面」索引標籤。
1. 選取 **[!UICONTROL 建立應用程式表面]** 以建立組態。
   ![應用程式表面首頁](assets/mobile-push-app-surface.png)
1. 輸入 **[!UICONTROL 名稱]** 例如，針對設定 `Luma App Tutorial`  .
1. 在行動應用程式設定中，選取 **[!UICONTROL Apple iOS]**.
1. 在「應用程式ID (iOS套件組合ID)」欄位中輸入行動應用程式套件組合ID。 如果您使用Luma應用程式進行追蹤，則該值為 `com.adobe.luma.tutorial`.
1. 切換至 **[!UICONTROL 推送認證]** 按鈕以新增您的認證。
1. 拖放您的 `.p8` **Apple推播通知驗證金鑰** 檔案。
1. 提供索引鍵ID，在建立期間指派的10個字元字串 `p8` 驗證金鑰。 您可在的索引鍵索引標籤下找到它 **憑證、識別碼和設定檔** 頁面。
1. 提供團隊ID。 此為字串值，可在 **會籍** 標籤。
1. 選取「**[!UICONTROL 儲存]**」。
   ![應用程式表面設定](assets/mobile-push-app-surface-config.png)

## 安裝Adobe Journey Optimizer標籤擴充功能

1. 瀏覽至 [!UICONTROL 標籤] > [!UICONTROL 擴充功能] > [!UICONTROL 目錄]，並找到 **[!UICONTROL Adobe Journey Optimizer]** 副檔名。
1. 安裝擴充功能。
   ![安裝ajo擴充功能](assets/mobile-push-tags-install.png)
1. 選取 `CJM Push Tracking Experience Event Dataset` Adobe Experience Platform資料集。
   ![AJO擴充功能設定](assets/mobile-push-tags-ajo.png)
1. 選取 **[!UICONTROL 儲存至程式庫並建置]**.

>[!NOTE]
>如果您沒有看到「CJM推播追蹤體驗事件資料集」選項，請聯絡客戶服務。
>

## 在應用程式中實作Adobe Journey Optimizer

如先前課程所述，安裝行動標籤擴充功能僅會提供設定。 接下來，您必須安裝並註冊傳訊SDK。 如果這些步驟不清楚，請查閱 [安裝SDK](install-sdks.md) 區段。

>[!NOTE]
>
>如果您已完成 [安裝SDK](install-sdks.md) 區段，則已安裝SDK且您可以跳至步驟#7。

1. 開啟您的 `Podfile` 並新增以下行並儲存檔案。

   `pod 'AEPMessaging', '~>1'`
1. 開啟您的終端機，並導覽至包含 `Podfile`.
1. 執行命令以安裝SDK `pod install`.
   ![驗證同意](assets/mobile-push-terminal-install.png)
1. 開啟Xcode並瀏覽至 `AppDelegate.swift`.
1. 將下列專案新增至您的匯入清單。

   `import AEPMessaging`
1. 新增 `Messaging.self` 至您正在註冊的擴充功能陣列。
1. 將下列函式新增至檔案。

   ```swift
   func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       MobileCore.setPushIdentifier(deviceToken)
   }
   ```

   此函式擷取應用程式安裝所在裝置所獨有的裝置代號，並傳送至Adobe/Apple以進行推送訊息傳送。

## 透過傳送測試推送訊息來驗證

1. 檢閱 [設定指示](assurance.md) 區段。
1. 在您的實體裝置上安裝應用程式。
1. 使用保證產生的URL啟動應用程式。
1. 將應用程式傳送至背景。
1. 在Assurance UI中，選取 **[!UICONTROL 設定]**.
   ![設定點按](assets/mobile-push-validate-config.png)
1. 選取 **[!UICONTROL +]** 按鈕旁邊 **[!UICONTROL 推送偵錯]**.
1. 選取「**[!UICONTROL 儲存]**」。
   ![儲存](assets/mobile-push-validate-save.png)
1. 選取 **[!UICONTROL 推送偵錯]** 從左側導覽。
1. 從中選擇您的裝置 **[!UICONTROL 使用者端清單]**.
1. 確認您沒有收到任何錯誤。
   ![驗證](assets/mobile-push-validate-confirm.png)
1. 向下捲動並選取 **[!UICONTROL 傳送測試推播通知]**.
1. 確認您沒有收到和錯誤，以及在裝置上收到訊息。
   ![傳送測試推播](assets/mobile-push-validate-send-test.png)

下一步： **[結論和後續步驟](conclusion.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)