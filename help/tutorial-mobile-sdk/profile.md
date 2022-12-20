---
title: 設定檔
description: 了解如何在行動應用程式中收集設定檔資料。
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# 設定檔

了解如何在行動應用程式中收集設定檔資料。

您可以使用設定檔擴充功能，在用戶端上儲存有關使用者的屬性。 這些資訊稍後可用於線上或離線情況下定位和個人化訊息，而無須連線至伺服器以獲得最佳效能。 設定檔擴充功能可管理用戶端作業設定檔(CSOP)、提供回應API、更新使用者設定檔屬性的方式，以及將使用者設定檔屬性與系統其餘部分共用為產生的事件。

其他擴充功能會使用設定檔資料來執行與設定檔相關的動作。 例如，規則引擎擴充功能會取用設定檔資料，並根據設定檔資料執行規則。 深入了解 [設定檔擴充功能](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile) 在檔案中

>[!IMPORTANT]
>
>本課程中說明的設定檔功能，與Adobe Experience Platform和平台型應用程式中的即時客戶設定檔功能不同。


## 先決條件

* 已安裝並設定SDK，成功建立並執行應用程式。
* 已匯入設定檔SDK。

   ```swift
   import AEPUserProfile
   ```

## 學習目標

在本課程中，您將：

* 設定或更新使用者屬性。
* 檢索用戶屬性。


## 設定和更新

若想快速知道使用者之前是否在應用程式中購買過產品，定位和/或個人化將有所幫助。 在Luma應用程式中設定。

1. 瀏覽到 `Cart.swift`

1. 將下列程式碼新增至 `processOrder() `函式。

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

個人化團隊可能也想根據使用者的忠誠度來鎖定目標。 在Luma應用程式中設定。

1. 瀏覽到 `Account.swift`

1. 將下列程式碼新增至 `showUserInfo()` 函式。

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

其他 `updateUserAttributes` 可找到檔案 [此處](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#update-user-attributes).

## 取得

更新使用者的屬性後，其他AdobeSDK即可使用該屬性，但您也可以明確擷取屬性。

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

其他 `getUserAttributes` 可找到檔案 [此處](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#get-user-attributes).

## 驗證並保證

1. 檢閱 [安裝指示](assurance.md) 區段。
1. 安裝應用程式。
1. 使用「保證」產生的URL啟動應用程式。
1. 選擇「帳戶」表徵圖，然後選擇「登錄」。 注意：您沒有提供任何憑據。
1. 關閉登入功能表，然後再次選取「帳戶」圖示。 這會帶您進入帳戶詳細資訊畫面，其中 `loyaltyLevel` 已設定。
1. 您應會看到 **[!UICONTROL UserProfileUpdate]** 事件（在已更新的保證UI中） `profileMap` 值。
   ![驗證設定檔](assets/mobile-profile-validate.png)

下一個： **[將資料對應至Adobe Analytics](analytics.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)