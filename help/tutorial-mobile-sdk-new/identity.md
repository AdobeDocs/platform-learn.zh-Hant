---
title: 收集身分資料
description: 瞭解如何在行動應用程式中收集身分資料。
feature: Mobile SDK,Identities
hide: true
exl-id: e6ec9a4f-3163-47fd-8d5c-6e640af3b4ba
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 4%

---

# 收集身分資料

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

>[!NOTE]
>
>行動SDK會在安裝應用程式時，在其專屬的名稱空間中產生唯一身分識別，命名為Experience CloudID (ECID)。 此ECID會儲存在行動裝置的永久性記憶體中，並隨著每次點選而傳送。 ECID會在使用者解除安裝應用程式，或將Mobile SDK全域隱私權狀態設為選擇退出時移除。 在範例Luma應用程式中，您應該移除並重新安裝應用程式，以建立具有自己唯一ECID的新設定檔。


若要建立新的身分名稱空間：

1. 在資料收集介面中，選取 **[!UICONTROL 身分]** 左側導覽列中。
1. 選取&#x200B;**[!UICONTROL 建立身分識別命名空間]**。
1. 提供 **[!UICONTROL 顯示名稱]** 之 `Luma CRM ID` 和 **[!UICONTROL 身分符號]** 值 `lumaCRMId`.
1. 選取 **[!UICONTROL 跨裝置ID]**.
1. 選取「**[!UICONTROL 建立]**」。

   ![建立身分名稱空間](assets/identity-create.png)




## 更新身分

您想要在使用者登入應用程式時更新標準身分（電子郵件）和自訂身分(Luma CRM ID)。

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** 在Xcode專案導覽器中，並找到 `func updateIdentities(emailAddress: String, crmId: String)` 函式實作。 將下列程式碼新增至函式。

   ```swift
   // Set up identity map, add identities to map and update identities
   let identityMap: IdentityMap = IdentityMap()
   
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
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

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 登入工作表]** 在Xcode專案導覽器中，尋找在選取 **[!UICONTROL 登入]** 按鈕。 新增下列程式碼：

   ```swift
   // Update identities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>您可在單一檔案中傳送多個身分 `updateIdentities` 呼叫。 您也可以修改先前傳送的身分。


## 移除身分

您可以使用 [`Identity.removeIdentity`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#removeidentity) 用於從儲存的使用者端身分對應中移除身分的API。 身分擴充功能會停止將識別碼傳送至Edge Network。 使用此API不會從伺服器端身分識別圖形中移除識別碼。 另請參閱 [檢視身分圖](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/view-identity-graphs.html?lang=en) 以取得身分圖表的詳細資訊。

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** 在Xcode專案導覽器中，新增下列程式碼至 `func removeIdentities(emailAddress: String, crmId: String)` 函式：

   ```swift
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL 登入工作表]** 在Xcode專案導覽器中，尋找在選取 **[!UICONTROL 登出]** 按鈕。 新增下列程式碼：

   ```swift
   // Remove identities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                  
   ```


## 使用保證進行驗證

1. 檢閱 [設定指示](assurance.md#connecting-to-a-session) 區段來將您的模擬器或裝置連線到Assurance。
1. 在Luma應用程式中
   1. 選取 **[!UICONTROL 首頁]** 標籤並將「保證」圖示移至左側。
   1. 選取 <img src="assets/login.png" width="15" /> 圖示加以選取。

      <img src="./assets/identity1.png" width="300">

   1. 提供電子郵件地址和CRM ID，或
   1. 選擇 <img src="assets/insert.png" width="15" /> 隨機產生 **[!UICONTROL 電子郵件]** 和 **[!UICONTROL CRM ID]**.
   1. 選取 **[!UICONTROL 登入]**.

      <img src="./assets/identity2.png" width="300">


1. 檢視Assurance Web介面中的 **[!UICONTROL 邊緣身分更新身分]** 來自的事件 **[!UICONTROL com.adobe.griffon.mobile]** 廠商。
1. 選取事件並檢閱中的資料 **[!UICONTROL ACPExtensionEventData]** 物件。 您應該會看到已更新的身分識別。
   ![驗證身分更新](assets/identity-validate-assurance.png)

## 使用身分圖表進行驗證

一旦您完成 [Experience Platform課程](platform.md)，您便能在Platforms身分圖表檢視器中確認身分擷取：

1. 選取 **[!UICONTROL 身分]** 在資料收集UI中。
1. 選取 **[!UICONTROL 身分圖表]** 從頂端列。
1. 輸入 `Luma CRM ID` 作為 **[!UICONTROL 身分名稱空間]** 和您的CRM ID (例如 `24e620e255734d8489820e74f357b5c8`)作為 **[!UICONTROL 身分值]**.
1. 您會看到 **[!UICONTROL 身分]** 已列出。

   ![驗證身分圖表](assets/identity-validate-graph.png)

>[!INFO]
>
>應用程式中沒有可重設ECID的程式碼，這表示您只能透過解除安裝應用程式並重新安裝，來重設ECID （並有效建立具有新ECID的新設定檔）。 若要實作識別碼的重設，請參閱 [`Identity.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#resetidentities) 和 [`MobileCore.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#resetidentities) API呼叫。 不過，使用推播通知識別碼時，請務必注意(請參閱 [傳送推播通知](journey-optimizer-push.md))，該識別碼會成為裝置上的另一個「粘性」設定檔識別碼。


>[!SUCCESS]
>
>您現在已設定應用程式，以在Edge Network和（設定後）Adobe Experience Platform中更新身分識別。
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

下一步： **[收集設定檔資料](profile.md)**
