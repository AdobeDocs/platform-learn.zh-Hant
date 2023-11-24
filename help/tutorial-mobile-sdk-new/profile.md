---
title: 收集設定檔資料
description: 瞭解如何在行動應用程式中收集設定檔資料。
hide: true
exl-id: 6ce02ccc-6280-4a1f-a96e-1975f8a0220a
source-git-commit: d1338390986a242c91051e94134f8d69e979c0b4
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# 收集設定檔資料

瞭解如何在行動應用程式中收集設定檔資料。

您可以使用設定檔擴充功能在使用者端上儲存使用者的相關屬性。 此資訊稍後可用於線上上或離線情況下目標定位和個人化訊息，不必連線至伺服器以獲得最佳效能。 設定檔擴充功能可管理使用者端作業設定檔(CSOP)、提供對API做出反應的方式、更新使用者設定檔屬性，以及將使用者設定檔屬性作為已產生的事件與系統其他部分共用。

其他擴充功能會使用設定檔資料來執行設定檔相關動作。 規則引擎擴充功能即是一例，它會使用設定檔資料，並根據設定檔資料執行規則。 進一步瞭解 [設定檔副檔名](https://developer.adobe.com/client-sdks/documentation/profile/) 在檔案中

>[!IMPORTANT]
>
>本課程中所述的設定檔功能與Adobe Experience Platform和平台型應用程式中的即時客戶設定檔功能不同。


## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。

## 學習目標

在本課程中，您將會：

* 設定或更新使用者屬性。
* 擷取使用者屬性。


## 設定和更新使用者屬性

快速知道使用者過去或最近是否曾經購買過產品，將有助於應用程式中的目標定位和/或個人化。 讓我們在Luma應用程式中設定它。

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** >  **[!DNL MobileSDK]** 在Xcode專案導覽器中，並找到 `func updateUserAttribute(attributeName: String, attributeValue: String)` 函式。 新增下列程式碼：

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   此程式碼：

   1. 設定空的字典，名為 `profileMap`.

   1. 使用將元素新增至字典 `attributeName` (例如 `isPaidUser`)，以及 `attributeValue` (例如 `yes`)。

   1. 使用 `profileMap` 字典作為值 `attributeDict` 的引數 [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes) API呼叫。

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]** 在Xcode專案導覽器中，尋找呼叫 `updateUserAttributes` （在購買程式碼內） <img src="assets/purchase.png" width="15" /> 按鈕)。 新增下列程式碼：

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttribute(attributeName: "isPaidUser", attributeValue: "yes")
   ```


## 取得使用者屬性

更新使用者的屬性後，其他AdobeSDK即可使用該屬性，但您也可以明確擷取屬性，讓應用程式依您想要的方式運作。

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!DNL HomeView]** 在Xcode專案導覽器中，並找到 `.onAppear` 修飾元。 新增下列程式碼：

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?.count ?? 0 > 0 {
           if attributes?["isPaidUser"] as? String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   此程式碼：

   1. 呼叫 [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) 具有的API `isPaidUser` 屬性名稱，作為中的單一元素 `attributeNames` 陣列。
   1. 然後檢查的值 `isPaidUser` 屬性與時間 `yes`，在網站上放置徽章 <img src="assets/paiduser.png" width="20" /> 圖示加以調整。

可找到其他檔案 [此處](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## 使用保證進行驗證

1. 檢閱 [設定指示](assurance.md#connecting-to-a-session) 區段來將您的模擬器或裝置連線到Assurance。
1. 執行應用程式以登入並與產品互動。

   1. 選取 **[!UICONTROL 首頁]** 標籤列中的。
   1. 將「保證」圖示移至左側。
   1. 若要開啟「登入」工作表，請選取 <img src="assets/login.png" width="15" />。

      <img src="./assets/mobile-app-events-1.png" width="300">

   1. 若要插入隨機電子郵件和客戶ID，請選取 <img src="assets/insert.png" width="15" />。
   1. 選取 **[!UICONTROL 登入]**.

      <img src="./assets/mobile-app-events-2.png" width="300">

   1. 選取 **[!DNL Products]** 標籤列中的。
   1. 選取一個產品。
   1. 選擇 <img src="assets/saveforlater.png" width="15" />。
   1. 選擇 <img src="assets/addtocart.png" width="20" />。
   1. 選擇 <img src="assets/purchase.png" width="15" />。

      <img src="./assets/mobile-app-events-3.png" width="300">

   1. 返回至 **[!UICONTROL 首頁]** 畫面。 您應該會看到徽章已新增 <img src="assets/person-badge-icon.png" width="15" />。

      <img src="./assets/personbadges.png" width="300">



1. 在Assurance UI中，您應該會看到 **[!UICONTROL UserProfileUpdate]** 和 **[!UICONTROL getuserattributes]** 具有已更新內容的事件 `profileMap` 值。
   ![驗證設定檔](assets/profile-validate.png)

>[!SUCCESS]
>
>您現在已設定應用程式，以更新Edge Network和（設定時） Adobe Experience Platform中設定檔的屬性。
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[使用地標](places.md)**
