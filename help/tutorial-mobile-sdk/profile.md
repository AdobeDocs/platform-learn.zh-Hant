---
title: 設定檔
description: 瞭解如何在行動應用程式中收集設定檔資料。
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# 設定檔

瞭解如何在行動應用程式中收集設定檔資料。

您可以使用Profile擴充功能在使用者端上儲存使用者的相關屬性。 此資訊稍後可用於線上上或離線情況下鎖定目標及個人化訊息，而不必連線至伺服器以獲得最佳效能。 設定檔擴充功能可管理使用者端作業設定檔(CSOP)、提供對API做出反應的方式、更新使用者設定檔屬性，以及將使用者設定檔屬性作為產生的事件與系統其他部分共用。

其他擴充功能會使用設定檔資料來執行設定檔相關動作。 規則引擎擴充功能就是一個範例，它會使用設定檔資料，並根據設定檔資料執行規則。 進一步瞭解 [設定檔副檔名](https://developer.adobe.com/client-sdks/documentation/profile/) 在檔案中

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


## 設定和更新

快速知道使用者以前是否曾在應用程式中購買過產品，有助於鎖定目標和/或個人化。 讓我們在Luma應用程式中設定它。

1. 瀏覽到 `Cart.swift`

1. 將下列程式碼新增至 `processOrder() `函式。

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

個人化團隊可能也想要根據使用者的忠誠度來鎖定目標。 讓我們在Luma應用程式中設定它。

1. 瀏覽到 `Account.swift`

1. 將下列程式碼新增至 `showUserInfo()` 函式。

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

其他 `updateUserAttributes` 可找到檔案 [此處](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## 取得

更新使用者的屬性後，其他AdobeSDK即可使用該屬性，但您也可以明確擷取屬性。

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

其他 `getUserAttributes` 可找到檔案 [此處](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## 使用保證進行驗證

1. 檢閱 [設定指示](assurance.md) 區段。
1. 安裝應用程式。
1. 使用保證產生的URL啟動應用程式。
1. 選取「帳戶」圖示，然後選取「登入」。 注意：您未提供任何認證。
1. 關閉登入功能表，然後再次選取帳戶圖示。 這會將您帶到帳戶詳細資訊畫面，其中 `loyaltyLevel` 已設定。
1. 您應會看到 **[!UICONTROL UserProfileUpdate]** 使用更新的Assurance UI中的事件 `profileMap` 值。
   ![驗證設定檔](assets/mobile-profile-validate.png)

下一步： **[將資料對應至Adobe Analytics](analytics.md)**

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Mobile SDK。 若您有任何疑問、想分享一般意見或對未來內容有任何建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)