---
title: 設定檔
description: 瞭解如何在行動應用程式中收集設定檔資料。
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 2%

---

# 設定檔

瞭解如何在行動應用程式中收集設定檔資料。

>[!INFO]
>
> 在2023年11月下旬，此教學課程將由使用新範例行動應用程式的新教學課程取代

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


## 設定和更新

快速瞭解使用者之前是否已在應用程式中購買產品，有助於目標定位和/或個人化。 讓我們在Luma應用程式中設定它。

1. 瀏覽到 `Cart.swift`

1. 將下列程式碼新增至 `processOrder() `函式。

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

個人化團隊可能也會想要根據使用者的忠誠度來鎖定目標。 讓我們在Luma應用程式中設定它。

1. 瀏覽到 `Account.swift`

1. 將下列程式碼新增至 `showUserInfo()` 函式。

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

其他 `updateUserAttributes` 可找到檔案 [此處](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## 取得

更新使用者的屬性後，其他Adobe SDK即可使用該屬性，但您也可以明確擷取屬性。

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
1. 關閉登入功能表，然後再次選取帳戶圖示。 這會將您導向至帳戶詳細資訊畫面，其中 `loyaltyLevel` 已設定。
1. 您應該會看到 **[!UICONTROL UserProfileUpdate]** 使用更新的Assurance UI中的事件 `profileMap` 值。
   ![驗證設定檔](assets/mobile-profile-validate.png)

下一步： **[將資料對應至Adobe Analytics](analytics.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)