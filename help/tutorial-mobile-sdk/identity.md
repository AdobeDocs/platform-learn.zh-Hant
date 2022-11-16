---
title: 身分
description: 了解如何在行動應用程式中收集身分資料。
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 4%

---

# 身分

了解如何在行動應用程式中收集身分資料。

Adobe Experience Platform Identity Service可協助您跨裝置和系統橋接身分，以便即時提供具影響力的個人數位體驗，進而更全面了解客戶及其行為。 身分欄位和命名空間是將不同資料來源連結在一起，以建立360度即時客戶設定檔的黏合劑。

深入了解 [身分擴充功能](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) 和 [身分服務](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hant) 中。

## 先決條件

* 已安裝並設定SDK，成功建立並執行應用程式。

## 學習目標

在本課程中，您將：

* 更新標準身分。
* 設定自訂身分。
* 更新自訂身分。
* 驗證身分圖。
* 取得ECID和其他身分識別。

## 更新標準身分

首先，在使用者登入時更新其身分對應。

1. 導覽至 `Login.swift` 若Luma應用程式，並尋找 `loginButt`.

   在Luma範例應用程式中，不提供使用者名稱或密碼驗證。 您只需按一下按鈕即可「登入」。

1. 建立 `IdentityMap` 和 `IdentityItem`.

   ```swift
   let identityMap: IdentityMap = IdentityMap()
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   ```

1. 新增 `IdentityItem` 到 `IdentityMap`

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


## 設定自訂身分命名空間

身分識別命名空間是 [Identity服務](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=en) 作為身份相關背景的指標。 例如，他們會將「name@email.com」值區分為電子郵件地址，或將「443522」區分為數值CRM ID。

1. 在資料收集介面中，選取 **[!UICONTROL 身分]** 的下界。
1. 選擇 **[!UICONTROL 建立身分命名空間]**.
1. 提供 **[!UICONTROL 顯示名稱]** of `Luma CRM ID` 和 **[!UICONTROL 標識符]** 值 `lumaCrmId`.
1. 選擇 **[!UICONTROL 跨裝置ID]**.
1. 選取「**[!UICONTROL 建立]**」。

![建立身分命名空間](assets/mobile-identity-create.png)

## 更新自訂身分

現在您已建立自訂身分識別，請修改以開始收集 `updateIdentities` 您在上一步驟中新增的程式碼。 只需建立IdentityItem並將其添加到IdentityMap即可。 以下是完整程式碼區塊看起來的樣子：

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

您可以使用 `removeIdentity` 從儲存的用戶端IdentityMap中移除身分。 身分擴充功能會停止將識別碼傳送至邊緣網路。 使用此API不會從伺服器端使用者設定檔圖表或身分圖中移除識別碼。

新增下列項目 `removeIdentity` 代碼註銷按鈕，按一下 `Account.swift`.

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
>在上述範例中， `crmId` 和 `emailAddress` 程式碼已硬式編碼，但在實際應用程式中，值會是動態的。

## 驗證並保證

1. 檢閱 [安裝指示](assurance.md) 區段，並將您的模擬器或裝置連線至「保證」。
1. 在應用程式中，從右下方選取「帳戶」圖示。

   ![luma應用程式帳戶](assets/mobile-identity-login.png)
1. 選取 **登入** 按鈕。
1. 系統會提供輸入使用者名稱和密碼的選項，兩者皆為選用，您只需選取 **登入**.

   ![luma應用程式登入](assets/mobile-identity-login-final.png)
1. 查看Assurance Web UI中 `Edge Identity Update Identities` 來自 `com.adobe.griffon.mobile` 供應商。
1. 選取事件並檢閱 `ACPExtensionEventData` 物件。 您應該會看到您更新的身分。
   ![驗證身分更新](assets/mobile-identity-validate-assurance.png)

## 使用身分圖表驗證

完成 [Experience Platform課程](platform.md)，您也可以在平台身分圖表檢視器中確認身分擷取：

![驗證身分圖](assets/mobile-identity-validate.png)


下一個： **[設定檔](profile.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)