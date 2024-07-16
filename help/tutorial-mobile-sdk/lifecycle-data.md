---
title: 使用Platform Mobile SDK收集生命週期資料
description: 瞭解如何在行動應用程式中收集生命週期資料。
jira: KT-14630
exl-id: 75b2dbaa-2f84-4b95-83f6-2f38a4f1d438
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# 收集生命週期資料

瞭解如何在行動應用程式中收集生命週期資料。

Adobe Experience Platform Mobile SDK生命週期擴充功能可啟用來自行動應用程式的收集生命週期資料。 Adobe Experience PlatformEdge Network擴充功能會將此生命週期資料傳送至PlatformEdge Network，再根據您的資料流設定轉送至其他應用程式和服務。 在產品檔案中進一步瞭解[生命週期延伸](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/)。


## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。 在本課程中，您已啟動生命週期監視。 請參閱[安裝SDK — 更新AppDelegate](install-sdks.md#update-appdelegate)以進行檢閱。
* 已依照[上一課程](install-sdks.md)中的說明註冊保證延伸。

## 學習目標

在本課程中，您將會：

<!--
* Add lifecycle field group to the schema.
* -->
* 當應用程式在前景和背景之間移動時，透過正確啟動/暫停來啟用精確的生命週期量度。
* 從應用程式傳送資料至平台Edge Network。
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

1. 在Xcode專案導覽器中導覽至&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]**。

1. 啟動時，如果您的應用程式正從背景狀態繼續，iOS可能會呼叫您的`sceneWillEnterForeground:`委派方法，而您想要在此觸發生命週期開始事件。 將此程式碼新增至`func sceneWillEnterForeground(_ scene: UIScene)`：

   ```swift
   // When in foreground start lifecycle data collection
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. 當應用程式進入背景時，您想要暫停來自應用程式`sceneDidEnterBackground:`委派方法的生命週期資料集合。 將此程式碼新增至`func sceneDidEnterBackground(_ scene: UIScene)`：

   ```swift
   // When in background pause lifecycle data collection
   MobileCore.lifecyclePause()
   ```

## 使用保證進行驗證

1. 檢閱[設定指示](assurance.md#connecting-to-a-session)區段，將您的模擬器或裝置連線到Assurance。
1. 將應用程式傳送至背景。 檢查Assurance UI中的&#x200B;**[!UICONTROL LifecyclePause]**&#x200B;事件。
1. 將應用程式移至前景。 檢查保證UI中的&#x200B;**[!UICONTROL LifecycleResume]**事件。
   ![驗證生命週期](assets/lifecycle-lifecycle-assurance.png)


## 將資料轉送至PlatformEdge Network

上個練習會將前景和背景事件傳送至Adobe Experience Platform Mobile SDK。 若要將這些事件轉送至PlatformEdge Network：

1. 在Tags屬性中選取&#x200B;**[!UICONTROL 規則]**。
   ![建立規則](assets/rule-create.png)
1. 選取&#x200B;**[!UICONTROL 初始組建]**&#x200B;作為要使用的程式庫。
1. 選取&#x200B;**[!UICONTROL 建立新規則]**。
   ![建立新規則](assets/rules-create-new.png)
1. 在&#x200B;**[!UICONTROL 建立規則]**&#x200B;畫面中，輸入&#x200B;**[!UICONTROL 名稱]**&#x200B;的`Application Status`。
1. 在&#x200B;**[!UICONTROL EVENTS]**&#x200B;底下選取![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增]**。
   ![建立規則對話方塊](assets/rule-create-name.png)
1. 在&#x200B;**[!UICONTROL 事件設定]**&#x200B;步驟中：
   1. 選取&#x200B;**[!UICONTROL 行動核心]**&#x200B;做為&#x200B;**[!UICONTROL 擴充功能]**。
   1. 選取&#x200B;**[!UICONTROL 前景]**&#x200B;做為&#x200B;**[!UICONTROL 事件型別]**。
   1. 選取&#x200B;**[!UICONTROL 保留變更]**。
      ![規則事件設定](assets/rule-event-configuration.png)
1. 返回&#x200B;**[!UICONTROL 「建立規則」]**&#x200B;畫面，選取&#x200B;**[!UICONTROL 行動核心 — 前景]**&#x200B;旁的![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增]**。
   ![下一個事件設定](assets/rule-event-configuration-next.png)
1. 在&#x200B;**[!UICONTROL 事件設定]**&#x200B;步驟中：
   1. 選取&#x200B;**[!UICONTROL 行動核心]**&#x200B;做為&#x200B;**[!UICONTROL 擴充功能]**。
   1. 選取&#x200B;**[!UICONTROL 背景]**&#x200B;做為&#x200B;**[!UICONTROL 事件型別]**。
   1. 選取&#x200B;**[!UICONTROL 保留變更]**。
      ![規則事件設定](assets/rule-event-configuration-background.png)
1. 返回&#x200B;**[!UICONTROL 建立規則]**&#x200B;畫面，選取&#x200B;**[!UICONTROL 動作]**&#x200B;下的![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增]**。
   ![規則新增動作](assets/rule-action-button.png)
1. 在&#x200B;**[!UICONTROL 動作組態]**&#x200B;步驟中：
   1. 選取&#x200B;**[!UICONTROL Adobe體驗Edge Network]**&#x200B;做為&#x200B;**[!UICONTROL 擴充功能]**。
   1. 選取&#x200B;**[!UICONTROL 轉寄事件至Edge Network]**&#x200B;作為&#x200B;**[!UICONTROL 動作型別]**。
   1. 選取&#x200B;**[!UICONTROL 保留變更]**。
      ![規則動作組態](assets/rule-action-configuration.png)
1. 選取&#x200B;**[!UICONTROL 儲存至資料庫]**。
   ![規則 — 儲存至資料庫](assets/rule-save-to-library.png)
1. 選取&#x200B;**[!UICONTROL 建置]**以重建程式庫。
   ![規則 — 組建](assets/rule-build.png)

當您成功建立屬性後，事件會傳送至PlatformEdge Network，而事件會根據您的資料流設定轉送至其他應用程式和服務。

您應該會在保證中看到包含XDM資料的&#x200B;**[!UICONTROL 應用程式關閉（背景）]**&#x200B;和&#x200B;**[!UICONTROL 應用程式啟動（前景）]**&#x200B;事件。

![驗證傳送至Platform Edge的生命週期](assets/lifecycle-edge-assurance.png)

>[!SUCCESS]
>
>您現在已設定應用程式，將應用程式狀態（前景、背景）事件傳送至Adobe Experience PlatformEdge Network，以及您在資料流中定義的所有服務。
>
> 感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享

下一個： **[追蹤事件資料](events.md)**
