---
title: 身分
description: 瞭解如何在行動應用程式中收集身分資料。
feature: Mobile SDK,Identities
hide: true
source-git-commit: e119e2bdce524c834cdaf43ed9eb9d26948b0ac6
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 6%

---

# 身分

瞭解如何在行動應用程式中收集身分資料。

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更清楚瞭解客戶及其行為。 身分欄位和名稱空間是將不同資料來源連線在一起，以建立360度即時客戶個人檔案的膠水。

進一步瞭解 [身分擴充功能](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) 和 [identity service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hant) 在檔案中。

## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。

## 學習目標

在本課程中，您將會：

* 設定自訂身分名稱空間。
* 更新身分。
* 驗證身分圖表。
* 取得ECID和其他身分。


## 設定自訂身分名稱空間

身分名稱空間是元件 [Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hant) 作為身分相關內容的指示器。 例如，他們將 `name@email.com` 的值區分為電子郵件地址，或將值區分為 `443522` 作為數值 CRM ID。

1. 在資料收集介面中，選取 **[!UICONTROL 身分]** 左側導覽列中。
1. 選取&#x200B;**[!UICONTROL 建立身分識別命名空間]**。
1. 提供 **[!UICONTROL 顯示名稱]** 之 `Luma CRM ID` 和 **[!UICONTROL 身分符號]** 值 `lumaCRMId`.
1. 選取 **[!UICONTROL 跨裝置ID]**.
1. 選取「**[!UICONTROL 建立]**」。

   ![建立身分名稱空間](assets/identity-create.png)




## 更新身分

您想要在使用者登入應用程式時更新標準身分（電子郵件）和自訂身分(Luma CRM ID)。

1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** 在Xcode專案導覽器中找到 `func updateIdentities(emailAddress: String, crmId: String)` 函式實作。 將下列程式碼新增至函式。

   ```swift
   // Set up identity map
   let identityMap: IdentityMap = IdentityMap()
   
   // Add identity items to identity map
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
   // Update identities
   Identity.updateIdentities(with: identityMap)
   ```

   此程式碼：

   1. 建立空白 `IdentityMap` 物件。

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. 設定 `IdentityItem` 電子郵件和CRM ID的物件。

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. 新增這些 `IdentityItem` 物件至 `IdentityMap` 物件。

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. 傳送 `IdentityItem` 物件，作為 `Identity.updateIdentities` 對Edge Network的API呼叫。

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```

1. 瀏覽至 **[!UICONTROL Luma]** **[!UICONTROL Luma]** > **[!UICONTROL 檢視]** > **[!UICONTROL 一般]** > **[!UICONTROL 登入工作表]** 在Xcode專案導覽器中，尋找在選取 **[!UICONTROL 登入]** 按鈕。 新增下列程式碼：

   ```swift
   // call updaeIdentities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>您可在單一檔案中傳送多個身分 `updateIdentities` 呼叫。 您也可以修改先前傳送的身分。


## 移除身分

您可以使用 `removeIdentity` 從儲存的使用者端IdentityMap移除身分識別。 身分擴充功能會停止將識別碼傳送至Edge Network。 使用此API不會從伺服器端使用者設定檔圖形或身分圖形中移除識別碼。

1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 一般]** > **[!UICONTROL MobileSDK]** 在Xcode專案導覽器中，新增下列程式碼至 `func removeIdentities(emailAddress: String, crmId: String)` 函式：

   ```swift
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   // reset email and CRM Id to their defaults
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 檢視]** > **[!UICONTROL 一般]** > **[!UICONTROL 登入工作表]** 在Xcode專案導覽器中，尋找在選取 **[!UICONTROL 登出]** 按鈕。 新增下列程式碼：

   ```swift
   // call removeIdentities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)
   dismiss()                   
   ```


## 使用保證進行驗證

1. 檢閱 [設定指示](assurance.md) 區段並將模擬器或裝置連線至Assurance。
1. 在Luma應用程式中
   1. 選取 **[!UICONTROL 首頁]** 標籤。
   1. 選取 <img src="assets/login.png" width="15" /> 圖示加以選取。
   1. 提供電子郵件地址和CRM ID，或
   1. 選擇 <img src="assets/insert.png" width="15" /> 隨機產生 **[!UICONTROL 電子郵件]** 和 **[!UICONTROL CRM ID]**.
   1. 選取 **[!UICONTROL 登入]**.

      <img src="./assets/identity1.png" width="300"> <img src="./assets/identity2.png" width="300">


1. 檢視Assurance Web UI以取得**[!UICONTROL 邊緣身分更新身分]**事件來自 **[!UICONTROL com.adobe.griffon.mobile]** 廠商。
1. 選取事件並檢閱中的資料 **[!UICONTROL ACPExtensionEventData]** 物件。 您應該會看到已更新的身分識別。
   ![驗證身分更新](assets/identity-validate-assurance.png)

## 使用身分圖表進行驗證

一旦您完成 [Experience Platform課程](platform.md)，您便能在Platforms身分圖表檢視器中確認身分擷取：

1. 選取 **[!UICONTROL 身分]** 在資料收集UI中。
1. 選取 **[!UICONTROL 身分圖表]** 從頂端列。
1. 輸入 `Luma CRM ID` 作為 **[!UICONTROL 身分名稱空間]** 和您的CRM ID (例如 `24e620e255734d8489820e74f357b5c8`)作為 **[!UICONTROL 身分值]**.
1. 您會看到 **[!UICONTROL 身分]** 已列出。

   ![驗證身分圖表](assets/identity-validate-graph.png)


>[!SUCCESS]
>
>您現在已設定應用程式，以在Edge Network和（設定後）Adobe Experience Platform中更新身分識別。<br/>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[個人資料](profile.md)**
