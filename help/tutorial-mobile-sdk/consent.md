---
title: 實作同意Platform Mobile SDK實作
description: 瞭解如何在行動應用程式中實施同意。
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 實作同意

瞭解如何在行動應用程式中實施同意。

Adobe Experience Platform同意行動擴充功能可讓您在使用Adobe Experience Platform Mobile SDK和Edge Network擴充功能時，從行動應用程式收集同意偏好設定。 進一步瞭解 [同意擴充功能](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) 在檔案中。

## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。

## 學習目標

在本課程中，您將會：

* 提示使用者同意。
* 根據使用者回應更新擴充功能。
* 瞭解如何取得目前的同意狀態。

## 要求同意

如果您從頭開始按照教學課程進行，您可能會記得您已將「同意」擴充功能中的預設同意設為 **[!UICONTROL 擱置中 — 在使用者提供同意偏好設定之前發生的佇列事件。]**

若要開始收集資料，您必須取得使用者的同意。 在真實世界應用程式中，您會想要諮詢您所在地區的同意最佳實務。 在本教學課程中，您只需透過警報要求使用者同意：

1. 您只想要求使用者同意一次。 您可以將Mobile SDK同意與使用Apple的追蹤所需授權結合以達成此目的 [應用程式追蹤透明度框架](https://developer.apple.com/documentation/apptrackingtransparency). 在此應用程式中，您假設當使用者授權追蹤時，他們同意收集事件。

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** 在「Xcode專案」導覽器中。

   將此程式碼新增至 `updateConsent` 函式。

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 免責宣告檢視]** 在Xcode的專案導覽器中，這是安裝或重新安裝應用程式並首次啟動應用程式後顯示的檢視。 系統會根據Apple提示使用者授權追蹤 [應用程式追蹤透明度框架](https://developer.apple.com/documentation/apptrackingtransparency). 如果使用者授權，您也會更新同意。

   將下列程式碼新增至 `ATTrackingManager.requestTrackingAuthorization { status in` 關閉。

   ```swift
   // Add consent based on authorization
   if status == .authorized {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "y")
   }
   else {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "n")
   }
   ```

## 取得目前的同意狀態

同意行動擴充功能會根據目前的同意值自動隱藏/擱置/允許追蹤。 您也可以自行存取目前的同意狀態：

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** 在Xcode的專案導覽器中。

   將下列程式碼新增至 `getConsents` 函式：

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]** 在Xcode的專案導覽器中。

   將下列程式碼新增至 `.task` 修飾元：

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

在上述範例中，您只是將同意狀態記錄到Xcode中的主控台。 在真實情境中，您可以使用它來修改要向使用者顯示哪些功能表或選項。

## 使用保證進行驗證

1. 從您的裝置或模擬器刪除應用程式，以正確重設和初始化追蹤和同意。
1. 若要將模擬器或裝置連線至Assurance，請檢閱 [設定指示](assurance.md#connecting-to-a-session) 區段。
1. 從移動應用程式時 **[!UICONTROL 首頁]** 熒幕至 **[!UICONTROL 產品]** 畫面並返回 **[!UICONTROL 首頁]** 畫面，您應該會看到 **[!UICONTROL 取得同意回應]** 保證UI中的事件。
   ![驗證同意](assets/consent-update.png)


>[!SUCCESS]
>
>您現在已啟用應用程式，在安裝（或重新安裝）後最初啟動時提示使用者，以使用Adobe Experience Platform Mobile SDK表示同意。
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[收集生命週期資料](lifecycle-data.md)**
