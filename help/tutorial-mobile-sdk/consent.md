---
title: 實作同意Platform Mobile SDK實作
description: 瞭解如何在行動應用程式中實施同意。
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---

# 實作同意

瞭解如何在行動應用程式中實施同意。

Adobe Experience Platform同意行動擴充功能可讓您在使用Adobe Experience Platform Mobile SDK和Edge Network擴充功能時，從行動應用程式收集同意偏好設定。 在檔案中進一步瞭解[同意延伸](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/)。

## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。

## 學習目標

在本課程中，您將會：

* 提示使用者同意。
* 根據使用者回應更新擴充功能。
* 瞭解如何取得目前的同意狀態。

## 要求同意

如果您從頭開始按照教學課程進行，您可能會記得您已將「同意」擴充功能中的預設同意設定為&#x200B;**[!UICONTROL 擱置中 — 佇列事件（在使用者提供同意偏好設定之前發生）。]**

若要開始收集資料，您必須取得使用者的同意。 在真實世界應用程式中，您會想要諮詢您所在地區的同意最佳實務。 在本教學課程中，您只需透過警報要求使用者同意：

>[!BEGINTABS]

>[!TAB iOS]

1. 您只想要求使用者同意一次。 您結合行動SDK同意與使用Apple的[應用程式追蹤透明度架構](https://developer.apple.com/documentation/apptrackingtransparency)進行追蹤所需的授權。 在此應用程式中，您假設當使用者授權追蹤時，他們同意收集事件。

1. 導覽至Xcode專案導覽器中的&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**。

   將此程式碼新增至`updateConsent`函式。

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. 導覽至Xcode專案導覽器中的&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 免責宣告檢視]**。 Xode的專案導覽器是在安裝或重新安裝應用程式並首次啟動應用程式後顯示的檢視。 系統會根據Apple的[應用程式追蹤透明度架構](https://developer.apple.com/documentation/apptrackingtransparency)，提示使用者授權追蹤。 如果使用者授權，您也會更新同意。

   將下列程式碼新增至`ATTrackingManager.requestTrackingAuthorization { status in`結尾。

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

>[!TAB Android]

1. 您只想要求使用者同意一次。 在此應用程式中，您假設當使用者授權追蹤時，他們同意收集事件。

1. 在Android Studio導覽器中，導覽至&#x200B;**[!UICONTROL 應用程式]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL 模型]** > **[!UICONTROL MobileSDK]**。

   將此程式碼新增至`updateConsent(value: String)`函式。

   ```kotlin
   // Update consent
   val collectConsent = mapOf("collect" to mapOf("val" to value))
   val currentConsents = mapOf("consents" to collectConsent)
   Consent.update(currentConsents)
   MobileCore.updateConfiguration(currentConsents)
   ```

1. 在Android Studio導覽器中，導覽至&#x200B;**[!UICONTROL 應用程式]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL 檢視]** > **[!UICONTROL DisclaimerView.kt]**。

   將下列程式碼新增至`DisclaimerView(navController: NavController)`和`// Set content to yes`下方的`// Set content to no`函式。

   ```kotlin
   // Add consent based on authorization
   if (status) {
      showPersonalizationWarning = false
   
      // Set consent to yes
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.AUTHORIZED)
      MobileSDK.shared.updateConsent("y")
   } else {
      Toast.makeText(
            context,
            "You will not receive offers and location tracking will be disabled.",
            Toast.LENGTH_LONG
      ).show()
      showPersonalizationWarning = true
   
      // Set consent to no
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.DENIED)
      MobileSDK.shared.updateConsent("n")
   }
   ```

>[!ENDTABS]

## 取得目前的同意狀態

同意行動擴充功能會根據目前的同意值自動隱藏/擱置/允許追蹤。 您也可以自行存取目前的同意狀態：

>[!BEGINTABS]

>[!TAB iOS]

1. 導覽至Xcode專案導覽器中的&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**。

   將下列程式碼新增至`getConsents`函式：

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. 導覽至Xcode專案導覽器中的&#x200B;**[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]**。

   將下列程式碼新增至`.task`修飾元：

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

在上述範例中，您只是將同意狀態記錄到Xcode中的主控台。 在真實情境中，您可以使用它來修改要向使用者顯示哪些功能表或選項。

>[!TAB Android]

1. 在Android Studio導覽器中，導覽至&#x200B;**[!UICONTROL 應用程式]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL 模型]** > **[!UICONTROL MobileSDK]**。

   將下列程式碼新增至`getConsents()`函式：

   ```kotlin
   // Get consents
   Consent.getConsents { callback ->
      if (callback != null) {
            val jsonStr = JSONObject(callback).toString(4)
            Log.i("MobileSDK", "Consent getConsents: $jsonStr")
      }
   }
   ```

1. 在Android Studio導覽器中，導覽至&#x200B;**[!UICONTROL 應用程式]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL 檢視]** > **[!UICONTROL HomeView.kt]**。

   將下列程式碼新增至`LaunchedEffect(unit)`：

   ```kotlin
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

在上述範例中，您只是將同意狀態記錄到Android Studio中的主控台。 在真實情境中，您可以使用它來修改要向使用者顯示哪些功能表或選項。

>[!ENDTABS]

## 使用保證進行驗證

1. 從您的裝置或模擬器刪除應用程式，以正確重設和初始化追蹤和同意。
1. 若要將模擬器或裝置連線至Assurance，請檢閱[設定指示](assurance.md#connecting-to-a-session)區段。
1. 將應用程式從&#x200B;**[!UICONTROL 首頁]**&#x200B;畫面移至&#x200B;**[!UICONTROL 產品]**&#x200B;畫面並返回&#x200B;**[!UICONTROL 首頁]**&#x200B;畫面時，您應該會在Assurance UI中看到&#x200B;**[!UICONTROL 取得同意回應]**&#x200B;事件。
   ![驗證同意](assets/consent-update.png){zoomable="yes"}


>[!SUCCESS]
>
>您現在已啟用應用程式，在安裝（或重新安裝）後最初啟動時提示使用者，以同意使用Adobe Experience Platform Mobile SDK。
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=zh-Hant)上分享

下一個： **[收集生命週期資料](lifecycle-data.md)**
