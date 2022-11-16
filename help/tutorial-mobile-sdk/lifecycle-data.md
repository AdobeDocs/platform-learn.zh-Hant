---
title: 生命週期資料
description: 了解如何在行動應用程式中收集生命週期資料。
exl-id: 75b2dbaa-2f84-4b95-83f6-2f38a4f1d438
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# 生命週期資料

了解如何在行動應用程式中收集生命週期資料。

Adobe Experience Platform Mobile SDK生命週期擴充功能可啟用您行動應用程式中的收集生命週期資料。 Adobe Experience Platform邊緣網路擴充功能會將此生命週期資料傳送至平台邊緣網路，然後根據您的資料流組態將其轉送至其他應用程式和服務。 深入了解 [生命週期擴充功能](https://aep-sdks.gitbook.io/docs/foundation-extensions/lifecycle-for-edge-network) 在產品檔案中。


## 先決條件

* 已安裝並設定SDK，成功建立並執行應用程式。
* 已匯入保證SDK。

   ```swift
   import AEPAssurance
   ```

* 已註冊「保證」擴充功能，如 [上一課](install-sdks.md).

## 學習目標

在本課程中，您將：

* 將生命週期欄位群組新增至架構。
* 當應用程式在前景和背景之間移動時，請正確啟動/暫停，以啟用精確的生命週期量度。
* 將資料從應用程式傳送至Platform Edge Network。
* 在保證中驗證。

## 將生命週期欄位組添加到架構

您在 [上一課](create-schema.md) 已包含生命週期欄位，因此您可以略過此步驟。 如果您未在自己的應用程式中使用消費者體驗事件欄位群組，您可以執行下列動作來新增生命週期欄位：

1. 依 [上一課](create-schema.md).
1. 開啟「Luma應用程式」架構，然後選取 **[!UICONTROL 新增]**.
   ![選擇添加](assets/mobile-lifecycle-add.png)
1. 在搜尋列中輸入「生命週期」。
1. 選取旁邊的核取方塊 **[!UICONTROL AEP行動生命週期詳細資訊]**.
1. 選擇 **[!UICONTROL 新增欄位群組]**.
   ![新增欄位群組](assets/mobile-lifecycle-lifecycle-field-group.png)
1. 選取「**[!UICONTROL 儲存]**」。
   ![儲存](assets/mobile-lifecycle-lifecycle-save.png)


## 實作變更

現在您可以更新 `AppDelegate.swift` 要註冊生命週期事件，請執行以下操作：

1. 啟動後，如果您的應用程式從背景狀態恢復，iOS可能會呼叫您的 `applicationWillEnterForeground:` 委派方法。 新增 `lifecycleStart:`

   ```swift
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. 當應用程式進入背景時，會暫停應用程式的生命週期資料收集 `applicationDidEnterBackground:` 委派方法。

   ```swift
   MobileCore.lifecyclePause()
   ```

>[!NOTE]
>
>若是iOS 13及更新版本，請檢閱 [檔案](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle#register-lifecycle-with-mobile-core-and-add-appropriate-start-pause-calls) 代碼稍有不同。

## 驗證並保證

1. 檢閱 [安裝指示](assurance.md) 區段，並將您的模擬器或裝置連線至「保證」。
1. 啟動應用程式。
1. 將應用程式傳送至背景。 檢查 `LifecyclePause`.
1. 將應用程式移至前景。 檢查 `LifecycleResume`.
   ![驗證生命週期](assets/mobile-lifecycle-lifecycle-assurance.png)


## 將資料轉發至Platform Edge Network

先前的練習會將前景和背景事件分派至Mobile SDK。 若要將這些事件傳送至Platform Edge Network，請遵循所列步驟 [此處](https://aep-sdks.gitbook.io/docs/foundation-extensions/lifecycle-for-edge-network#configure-a-rule-to-forward-lifecycle-metrics-to-platform). 一旦將事件傳送至Platform Edge Network，就會根據您的資料流組態，將其轉送至其他應用程式和服務。

新增規則以將生命週期事件傳送至Platform Edge Network後，您應會看到 `Application Close (Background)` 和 `Application Launch (Foreground)` 包含XDM資料的事件。

![驗證生命週期是否傳送至Platform Edge](assets/mobile-lifecycle-edge-assurance.png)



下一個： **[追蹤事件](events.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)