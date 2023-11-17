---
title: 身分
description: 瞭解如何在行動應用程式中收集身分資料。
feature: Mobile SDK,Identities
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 4%

---

# 身分

瞭解如何在行動應用程式中收集身分資料。

>[!INFO]
>
> 在2023年11月下旬，此教學課程將由使用新範例行動應用程式的新教學課程取代

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更清楚瞭解客戶及其行為。 身分欄位和名稱空間是將不同資料來源連線在一起，以建立360度即時客戶個人檔案的膠水。

進一步瞭解 [身分擴充功能](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) 和 [identity service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hant) 在檔案中。

## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。

## 學習目標

在本課程中，您將會：

* 更新標準身分。
* 設定自訂身分。
* 更新自訂身分。
* 驗證身分圖表。
* 取得ECID和其他身分。

## 更新標準身分

從使用者登入時更新使用者的身分對應開始。

1. 瀏覽至 `Login.swift` 如果Luma應用程式找到呼叫的函式 `loginButt`.

   在Luma範例應用程式中，沒有使用者名稱或密碼驗證。 只要點選按鈕即可「登入」。

1. 建立 `IdentityMap` 和 `IdentityItem`.

   ```swift
   let identityMap: IdentityMap = IdentityMap()
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   ```

1. 新增 `IdentityItem` 至 `IdentityMap`

   ```swift
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   ```

1. 呼叫 `updateIdentities` 將資料傳送至Platform Edge Network。

   ```swift
   Identity.updateIdentities(with: identityMap)
   ```

>[!NOTE]
>
>您可以在單一updateIdentities呼叫中傳送多個身分。 您也可以修改先前傳送的身分。


## 設定自訂身分名稱空間

身分名稱空間是元件 [Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hant) 作為身分相關內容的指示器。 例如，他們會將「name@email.com」的值做為電子郵件地址，或將「443522」的值做為數值CRM ID。

1. 在資料收集介面中，選取 **[!UICONTROL 身分]** 左側導覽列中。
1. 選取&#x200B;**[!UICONTROL 建立身分識別命名空間]**。
1. 提供 **[!UICONTROL 顯示名稱]** 之 `Luma CRM ID` 和 **[!UICONTROL 身分符號]** 值 `lumaCrmId`.
1. 選取 **[!UICONTROL 跨裝置ID]**.
1. 選取「**[!UICONTROL 建立]**」。

![建立身分名稱空間](assets/mobile-identity-create.png)

## 更新自訂身分

現在您已建立自訂身分識別，請透過修改 `updateIdentities` 您在上一步中新增的程式碼。 只要建立IdentityItem並將其新增到IdentityMap即可。 以下為完整程式碼區塊的樣子：

```swift
//Hardcoded identity values
let emailAddress = "testuser@gmail.com"
let crmId = "112ca06ed53d3db37e4cea49cc45b71e"

// Create identity map
let identityMap: IdentityMap = IdentityMap()
// Add email (standard)
let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item:emailIdentity, withNamespace: "Email")
// Add lumaCrmId (custom)
let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item: crmIdentity, withNamespace: "lumaCrmId")
// Update
Identity.updateIdentities(with: identityMap)
```

## 移除身分

您可以使用 `removeIdentity` 從儲存的使用者端IdentityMap移除身分識別。 身分擴充功能會停止將識別碼傳送至Edge Network。 使用此API不會從伺服器端使用者設定檔圖形或身分圖形中移除識別碼。

新增下列專案 `removeIdentity` 登出按鈕的程式碼點進 `Account.swift`.

```swift
// Logout
let logout = UIAlertAction(title: "Logout", style: .destructive, handler: { (action) -> Void in
    isLoggedIn = false;
    ////Hardcoded identity values
    let emailAddress = "testuser@gmail.com"
    let crmId = "112ca06ed53d3db37e4cea49cc45b71e"
    // Adobe Experience Platform - Remove Identity
    Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
    Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCrmId")
})
```

>[!NOTE]
>在上述範例中， `crmId` 和 `emailAddress` 以硬式編碼顯示，但在實際應用程式中，該值會是動態的。

## 使用保證進行驗證

1. 檢閱 [設定指示](assurance.md) 區段並將模擬器或裝置連線至Assurance。
1. 在應用程式中，從右下方選取「帳戶」圖示。

   ![luma應用程式帳戶](assets/mobile-identity-login.png)
1. 選取 **登入** 按鈕。
1. 畫面會顯示您輸入使用者名稱和密碼的選項，兩者皆為選用專案，您只需選取 **登入**.

   ![luma應用程式登入](assets/mobile-identity-login-final.png)
1. 檢視Assurance Web UI，以瞭解 `Edge Identity Update Identities` 來自的事件 `com.adobe.griffon.mobile` 廠商。
1. 選取事件並檢閱中的資料 `ACPExtensionEventData` 物件。 您應該會看到已更新的身分識別。
   ![驗證身分更新](assets/mobile-identity-validate-assurance.png)

## 使用身分圖表進行驗證

一旦您完成 [Experience Platform課程](platform.md)，您也可以在Platforms身分圖表檢視器中確認身分擷取：

![驗證身分圖表](assets/mobile-identity-validate.png)


下一步： **[個人資料](profile.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)