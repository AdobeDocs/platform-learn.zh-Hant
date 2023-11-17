---
title: 生命週期資料
description: 瞭解如何在行動應用程式中收集生命週期資料。
exl-id: 75b2dbaa-2f84-4b95-83f6-2f38a4f1d438
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---

# 生命週期資料

瞭解如何在行動應用程式中收集生命週期資料。

>[!INFO]
>
> 在2023年11月下旬，此教學課程將由使用新範例行動應用程式的新教學課程取代

Adobe Experience Platform Mobile SDK生命週期擴充功能可啟用來自行動應用程式的收集生命週期資料。 Adobe Experience Platform Edge Network擴充功能會將此生命週期資料傳送至Platform Edge Network，再根據您的資料流設定轉送至其他應用程式和服務。 進一步瞭解 [生命週期延伸](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/) 產品檔案內。


## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。
* 已匯入保證SDK。

  ```swift
  import AEPAssurance
  ```

* 已註冊保證擴充功能，如中所述 [上一課程](install-sdks.md).

## 學習目標

在本課程中，您將會：

* 將生命週期欄位群組新增至結構描述。
* 當應用程式在前景和背景之間移動時，透過正確啟動/暫停來啟用精確的生命週期量度。
* 從應用程式傳送資料至Platform Edge Network。
* 在Assurance中進行驗證。

## 將生命週期欄位群組新增至結構描述

您在中新增的消費者體驗事件欄位群組 [上一課程](create-schema.md) 已經包含生命週期欄位，因此您可以略過此步驟。 如果您沒有在自己的應用程式中使用取用者體驗事件欄位群組，您可以執行下列動作來新增生命週期欄位：

1. 導覽至結構介面，如 [上一課程](create-schema.md).
1. 開啟「Luma應用程式」結構描述，然後選取 **[!UICONTROL 新增]**.
   ![選取新增](assets/mobile-lifecycle-add.png)
1. 在搜尋列中，輸入「lifecycle」。
1. 選取旁邊的核取方塊 **[!UICONTROL AEP行動生命週期詳細資料]**.
1. 選取&#x200B;**[!UICONTROL 「新增欄位群組」]**。
   ![新增欄位群組](assets/mobile-lifecycle-lifecycle-field-group.png)
1. 選取「**[!UICONTROL 儲存]**」。
   ![儲存](assets/mobile-lifecycle-lifecycle-save.png)


## 實作變更

現在您可以更新 `AppDelegate.swift` 註冊生命週期事件：

1. 啟動時，如果您的應用程式正從背景狀態恢復，iOS可能會呼叫您的 `applicationWillEnterForeground:` 委派方法。 新增 `lifecycleStart:`

   ```swift
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. 當應用程式進入背景時，暫停來自您應用程式的 `applicationDidEnterBackground:` 委派方法。

   ```swift
   MobileCore.lifecyclePause()
   ```

>[!NOTE]
>
>若為iOS 13和更新版本，請檢閱 [檔案](https://developer.adobe.com/client-sdks/documentation/mobile-core/lifecycle/#register-lifecycle-with-mobile-core-and-add-appropriate-startpause-calls) 稍有不同的程式碼。

## 使用保證進行驗證

1. 檢閱 [設定指示](assurance.md) 區段並將模擬器或裝置連線至Assurance。
1. 啟動應用程式。
1. 將應用程式傳送至背景。 檢查 `LifecyclePause`.
1. 將應用程式移至前景。 檢查 `LifecycleResume`.
   ![驗證生命週期](assets/mobile-lifecycle-lifecycle-assurance.png)


## 將資料轉送至Platform Edge Network

上一個練習是將前景和背景事件排程到Mobile SDK。 若要將這些事件傳送至Platform Edge Network，請遵循列出的步驟 [此處](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/#configure-a-rule-to-forward-lifecycle-metrics-to-platform). 將事件傳送到Platform Edge Network後，系統會根據您的資料流設定，將事件轉送到其他應用程式和服務。

新增將生命週期事件傳送至Platform Edge Network的規則後，您應會看到 `Application Close (Background)` 和 `Application Launch (Foreground)` 包含Assurance中XDM資料的事件。

![驗證傳送至Platform Edge的生命週期](assets/mobile-lifecycle-edge-assurance.png)



下一步： **[追蹤事件](events.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)