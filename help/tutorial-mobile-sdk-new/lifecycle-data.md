---
title: 收集生命週期資料
description: 瞭解如何在行動應用程式中收集生命週期資料。
hide: true
exl-id: a3b26e45-2a17-4b44-aec0-fdf83526a273
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 3%

---

# 收集生命週期資料

瞭解如何在行動應用程式中收集生命週期資料。

Adobe Experience Platform Mobile SDK生命週期擴充功能可啟用來自行動應用程式的收集生命週期資料。 Adobe Experience Platform Edge Network擴充功能會將此生命週期資料傳送至Platform Edge Network，再根據您的資料流設定轉送至其他應用程式和服務。 進一步瞭解 [生命週期延伸](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/) 產品檔案內。


## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。 在本課程中，您已啟動生命週期監視。 另請參閱 [安裝SDK — 更新AppDelegate](install-sdks.md#update-appdelegate) 以檢閱。
* 已註冊保證擴充功能，如中所述 [上一課程](install-sdks.md).

## 學習目標

在本課程中，您將會：

<!--
* Add lifecycle field group to the schema.
* -->
* 當應用程式在前景和背景之間移動時，透過正確啟動/暫停來啟用精確的生命週期量度。
* 從應用程式傳送資料至Platform Edge Network。
* 在Assurance中進行驗證。

<!--
## Add lifecycle field group to schema

The Consumer Experience Event field group you added in the [previous lesson](create-schema.md) already contains the lifecycle fields, so you can skip this step. If you don't use Consumer Experience Event field group in your own app, you can add the lifecycle fields by doing the following:

1. Navigate to the schema interface as described in the [previous lesson](create-schema.md).
1. Open the **Luma Mobile App Event Schema** schema and select **[!UICONTROL Add]** next to Field groups.
    ![select add](assets/lifecycle-add.png)
1. In the search bar, enter "lifecycle".
1. Select the checkbox next to **[!UICONTROL AEP Mobile Lifecycle Details]**.
1. Select **[!UICONTROL Add field groups]**.
    ![add field group](assets/lifecycle-lifecycle-field-group.png)
1. Select **[!UICONTROL Save]**.
    ![save](assets/lifecycle-lifecycle-save.png)
-->

## 實作變更

現在您可以更新專案以註冊生命週期事件。

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** 在「Xcode專案」導覽器中。

1. 啟動時，如果您的應用程式正從背景狀態恢復，iOS可能會呼叫您的 `sceneWillEnterForeground:` 委派方法，而且您想要在此觸發生命週期開始事件。 將此程式碼新增至 `func sceneWillEnterForeground(_ scene: UIScene)`：

   ```swift
   // When in foreground start lifecycle data collection
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. 當應用程式進入背景時，您想要暫停來自應用程式的生命週期資料收集 `sceneDidEnterBackground:` 委派方法。 將此程式碼新增至  `func sceneDidEnterBackground(_ scene: UIScene)`：

   ```swift
   // When in background pause lifecycle data collection
   MobileCore.lifecyclePause()
   ```

## 使用保證進行驗證

1. 檢閱 [設定指示](assurance.md#connecting-to-a-session) 區段來將您的模擬器或裝置連線到Assurance。
1. 將應用程式傳送至背景。 檢查 **[!UICONTROL LifecyclePause]** Assurance UI中的事件。
1. 將應用程式移至前景。 檢查 **[!UICONTROL LifecycleResume]** Assurance UI中的事件。
   ![驗證生命週期](assets/lifecycle-lifecycle-assurance.png)


## 將資料轉送至Platform Edge Network

上個練習會將前景和背景事件傳送至Adobe Experience Platform Mobile SDK。 若要將這些事件轉送至Platform Edge Network：

1. 選取 **[!UICONTROL 規則]** （在Tags屬性中）。
   ![建立規則](assets/rule-create.png)
1. 選取 **[!UICONTROL 初始建置]** 作為要使用的程式庫。
1. 選取&#x200B;**[!UICONTROL 「建立新規則」]**。
   ![建立新規則](assets/rules-create-new.png)
1. 在 **[!UICONTROL 建立規則]** 熒幕，輸入 `Application Status` 的 **[!UICONTROL 名稱]**.
1. 選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增]** 以下 **[!UICONTROL 活動]**.
   ![建立規則對話方塊](assets/rule-create-name.png)
1. 在 **[!UICONTROL 事件設定]** 步驟：
   1. 選取 **[!UICONTROL 行動核心]** 作為 **[!UICONTROL 副檔名]**.
   1. 選取 **[!UICONTROL 前景]** 作為 **[!UICONTROL 事件型別]**.
   1. 選取&#x200B;**[!UICONTROL 「保留變更」]**。
      ![規則事件設定](assets/rule-event-configuration.png)
1. 返回 **[!UICONTROL 建立規則]** 熒幕，選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增]** 旁邊 **[!UICONTROL 行動核心 — 前景]**.
   ![下一個事件設定](assets/rule-event-configuration-next.png)
1. 在 **[!UICONTROL 事件設定]** 步驟：
   1. 選取 **[!UICONTROL 行動核心]** 作為 **[!UICONTROL 副檔名]**.
   1. 選取 **[!UICONTROL 背景]** 作為 **[!UICONTROL 事件型別]**.
   1. 選取&#x200B;**[!UICONTROL 「保留變更」]**。
      ![規則事件設定](assets/rule-event-configuration-background.png)
1. 返回 **[!UICONTROL 建立規則]** 熒幕，選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增]** 底下 **[!UICONTROL 動作]**.
   ![規則新增動作](assets/rule-action-button.png)
1. 在 **[!UICONTROL 動作設定]** 步驟：
   1. 選取 **[!UICONTROL AdobeExperience Edge Network]** 作為 **[!UICONTROL 副檔名]**.
   1. 選取 **[!UICONTROL 將事件轉送至Edge Network]** 作為 **[!UICONTROL 動作型別]**.
   1. 選取&#x200B;**[!UICONTROL 「保留變更」]**。
      ![規則動作設定](assets/rule-action-configuration.png)
1. 選取 **[!UICONTROL 儲存至程式庫]**.
   ![規則 — 儲存至程式庫](assets/rule-save-to-library.png)
1. 選取 **[!UICONTROL 建置]** 以重建程式庫。
   ![規則 — 建置](assets/rule-build.png)

當您成功建立屬性後，事件會傳送至Platform Edge Network，而事件會根據您的資料流設定轉送至其他應用程式和服務。

您應該會看到 **[!UICONTROL 應用程式關閉（背景）]** 和 **[!UICONTROL 應用程式啟動（前景）]** 包含Assurance中XDM資料的事件。

![驗證傳送至Platform Edge的生命週期](assets/lifecycle-edge-assurance.png)

>[!SUCCESS]
>
>您現在已設定應用程式，將應用程式狀態（前景、背景）事件傳送至Adobe Experience Platform Edge Network，以及您在資料流中定義的所有服務。
>
> 感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[追蹤事件資料](events.md)**
