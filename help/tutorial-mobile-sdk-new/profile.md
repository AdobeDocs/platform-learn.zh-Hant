---
title: 設定檔
description: 瞭解如何在行動應用程式中收集設定檔資料。
hide: true
source-git-commit: c31dd74cf8ff9c0856b29e82d9c8be2ad027df4a
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---

# 設定檔

瞭解如何在行動應用程式中收集設定檔資料。

您可以使用設定檔擴充功能在使用者端上儲存使用者的相關屬性。 此資訊稍後可用於線上上或離線情況下目標定位和個人化訊息，不必連線至伺服器以獲得最佳效能。 設定檔擴充功能可管理使用者端作業設定檔(CSOP)、提供對API做出反應的方式、更新使用者設定檔屬性，以及將使用者設定檔屬性作為已產生的事件與系統其他部分共用。

其他擴充功能會使用設定檔資料來執行設定檔相關動作。 規則引擎擴充功能即是一例，它會使用設定檔資料，並根據設定檔資料執行規則。 進一步瞭解 [設定檔副檔名](https://developer.adobe.com/client-sdks/documentation/profile/) 在檔案中

>[!IMPORTANT]
>
>本課程中所述的設定檔功能與Adobe Experience Platform和平台型應用程式中的即時客戶設定檔功能不同。


## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。
* 已匯入設定檔SDK。

  ```swift
  import AEPUserProfile
  ```

## 學習目標

在本課程中，您將會：

* 設定或更新使用者屬性。
* 擷取使用者屬性。


## 設定和更新使用者屬性

快速瞭解使用者之前是否已在應用程式中購買產品，有助於目標定位和/或個人化。 讓我們在Luma應用程式中設定它。

1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** >  **[!UICONTROL MobileSDK]** 在Xcode專案導覽器中，並找到 `func updateUserAttribute(attributeName: String, attributeValue: String)` 函式。 新增下列程式碼：

   ```swift
   // Create a profile map
   var profileMap = [String: Any]()
   // Add attributes to profile map
   profileMap[attributeName] = attributeValue
   // Use profile map to update user attributes
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   此程式碼：

   1. 設定空的字典，名為 `profileMap`.

   1. 使用將元素新增至字典 `attributeName` (例如 `isPaidUser`)，以及 `attributeValue` (例如 `yes`)。

   1. 使用 `profileMap` 字典作為值 `attributeDict` 的引數 `UserProfile.updateUserAttributes` API呼叫。

1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 檢視]** > **[!UICONTROL 產品]** > **[!UICONTROL 產品檢視]** 在Xcode專案導覽器中，尋找呼叫 `updateUserAttributes` （在購買程式碼內） <img src="assets/purchase.png" width="15" /> 按鈕)：

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttributes(attributeName: "isPaidUser", attributeValue: "yes")
   ```

可找到其他檔案 [此處](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## 取得使用者屬性

更新使用者的屬性後，其他AdobeSDK即可使用該屬性，但您也可以明確擷取屬性。

1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 檢視]** >一般> **[!UICONTROL HomeView]** 在Xcode專案導覽器中，並找到 `.onAppear` 修飾元。 新增下列程式碼：

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?["isPaidUser"] as! String == "yes" {
           showBadgeForUser = true
       }
       else {
           showBadgeForUser = false
       }
   }
   ```

   此程式碼：

   1. 呼叫 `UserProfile.getUserAttributes` 結尾為 `iPaidUser` 屬性名稱，作為中的單一元素 `attributeNames` 陣列。
   1. 然後檢查的值 `isPaidUser` 屬性與時間 `yes`，在網站上放置徽章 <img src="assets/paiduser.png" width="20" /> 圖示加以調整。

可找到其他檔案 [此處](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## 使用保證進行驗證

1. 檢閱 [設定指示](assurance.md) 區段。
1. 安裝應用程式。
1. 使用保證產生的URL啟動應用程式。
1. 執行應用程式以登入並與產品互動。

   1. 將「保證」圖示移至左側。
   1. 選取 **[!UICONTROL 首頁]** 標籤列中的。
   1. 若要開啟「登入」工作表，請選取 <img src="assets/login.png" width="15" />。
   1. 若要插入隨機電子郵件和客戶ID，請選取 <img src="assets/insert.png" width="15" />。
   1. 選取 **[!UICONTROL 登入]**.
   1. 選取 **[!UICONTROL 產品]** 標籤列中的。
   1. 選取一個產品。
   1. 選擇 <img src="assets/saveforlater.png" width="15" />。
   1. 選擇 <img src="assets/addtocart.png" width="20" />。
   1. 選擇 <img src="assets/purchase.png" width="15" />。

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">
   1. 返回至 **[!UICONTROL 首頁]** 畫面。 您應該會看到已新增的徽章 <img src="assets/person-badge-icon.png" width="15" />。

      <img src="./assets/personbadges.png" width="200">



1. 在Assurance UI中，您應該會看到 **[!UICONTROL UserProfileUpdate]** 和 **[!UICONTROL getuserattributes]** 具有已更新內容的事件 `profileMap` 值。
   ![驗證設定檔](assets/profile-validate.png)

>[!SUCCESS]
>
>您現在已設定應用程式，以更新Edge Network和（設定時） Adobe Experience Platform中設定檔的屬性。<br/>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[使用地理定位服務](places.md)**
