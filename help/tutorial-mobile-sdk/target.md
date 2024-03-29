---
title: 使用Target和Platform Mobile SDK在行動應用程式中執行A/B測試
description: 瞭解如何在行動應用程式中搭配Platform Mobile SDK和Adobe Target使用Target A/B測試。
solution: Data Collection,Target
feature-set: Target
feature: A/B Tests
jira: KT-14641
exl-id: 87546baa-2d8a-4cce-b531-bec3782d2e90
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 2%

---

# 使用Adobe Target最佳化及個人化

瞭解如何使用Platform Mobile SDK和Adobe Target將行動應用程式中的體驗最佳化及個人化。

Target提供一切所需工具，讓您量身打造及個人化您的客戶體驗。 Target可協助您在網站和行動網站、應用程式、社群媒體和其他數位頻道上獲得最大收入。 Target可以執行A/B測試、多變數測試、建議產品和內容、鎖定內容、使用AI自動個人化內容等等。 本課程著重於Target的A/B測試功能。 請參閱 [A/B測試概覽](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=en) 以取得詳細資訊。

![架構](assets/architecture-at.png)

使用Target執行A/B測試之前，您必須確保有適當的設定和整合。

>[!NOTE]
>
>本課程為選修課程，僅適用於希望執行A/B測試的Adobe Target使用者。


## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。
* 使用許可權、正確設定的角色、工作區和屬性存取Adobe Target，如下所述 [此處](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=zh-Hant).


## 學習目標

在本課程中，您將會：

* 更新您的Target整合資料流。
* 使用Journey Optimizer - Decisioning擴充功能更新標籤屬性。
* 更新您的結構描述以擷取主張事件。
* 驗證Assurance中的設定。
* 在Target中建立簡單的A/B測試。
* 更新您的應用程式以註冊Optimizer擴充功能。
* 在您的應用程式中實作A/B測試。
* 驗證Assurance中的實作。


## 設定

>[!TIP]
>
>如果您已將應用程式設定為 [Journey Optimizer優惠方案](journey-optimizer-offers.md) 課程，您可能已執行過此設定章節中的某些步驟。

### 更新資料流設定

#### Adobe Target

為確保從您的行動應用程式傳送到Experience Platform Edge Network的資料能轉送到Adobe Target，您必須更新資料流設定。

1. 在資料收集UI中，選取 **[!UICONTROL 資料串流]**，並選取您的資料串流，例如 **[!DNL Luma Mobile App]**.
1. 選取 **[!UICONTROL 新增服務]** 並選取 **[!UICONTROL Adobe Target]** 從 **[!UICONTROL 服務]** 清單。
1. 如果您是Target Premium客戶，且想要使用屬性代號，請輸入Target **[!UICONTROL 屬性Token]** 要用於此整合的值。 Target Standard使用者可跳過此步驟。

   您可以在Target UI的下列位置找到您的屬性： **[!UICONTROL 管理]** > **[!UICONTROL 屬性]**. 選取 ![程式碼](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) 以顯示您要使用之屬性的屬性代號。 屬性代號的格式如下 `"at_property": "xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"`；您只能輸入值 `xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx`.

   您可以選擇指定Target環境ID。 Target會使用環境來組織您的網站和生產前環境，以便輕鬆管理和分隔報表。 預設環境包括生產、測試和開發。 另請參閱 [環境](https://experienceleague.adobe.com/docs/target/using/administer/environments.html?lang=en) 和 [目標環境ID](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=en#target-environment-id) 以取得詳細資訊。

   您可以選擇指定Target第三方ID名稱空間，以支援在身分名稱空間上同步設定檔（例如CRM ID）。 另請參閱 [Target第三方ID名稱空間](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=en#target-third-party-id-namespace) 以取得詳細資訊。

1. 選取「**[!UICONTROL 儲存]**」。

   ![將Target新增至資料串流](assets/edge-datastream-target.png)


#### Adobe Journey Optimizer

為確保將從您的行動應用程式傳送到Edge Network的資料轉送到Journey Optimizer — 決策管理，請更新您的資料流設定。

1. 在資料收集UI中，選取 **[!UICONTROL 資料串流]**，並選取您的資料串流，例如 **[!DNL Luma Mobile App]**.
1. 選取 ![更多](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) 的 **[!UICONTROL Experience Platform]** 並選取 ![編輯](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 編輯]** 從內容功能表。
1. 在 **[!UICONTROL 資料串流]** > ![資料夾](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) >  **[!UICONTROL Adobe Experience Platform]** 畫面，確認 **[!UICONTROL offer decisioning]**， **[!UICONTROL 邊緣細分]**、和 **[!UICONTROL 個人化目的地]** 已選取。 如果您也遵循Journey Optimizer課程，請選取 **[!UICONTROL Adobe Journey Optimizer]**. 另請參閱 [Adobe Experience Platform設定](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) 以取得詳細資訊。
1. 若要儲存資料流設定，請選取 **[!UICONTROL 儲存]** .

   ![AEP資料流設定](assets/datastream-aep-configuration-target.png)


### 安裝Adobe Journey Optimizer - Decisioning標籤擴充功能

1. 瀏覽至 **[!UICONTROL 標籤]**，尋找您的行動標籤屬性，然後開啟屬性。
1. 選取 **[!UICONTROL 擴充功能]**.
1. 選取 **[!UICONTROL 目錄]**.
1. 搜尋 **[!UICONTROL Adobe Journey Optimizer - Decisioning]** 副檔名。
1. 安裝擴充功能。 此擴充功能不需要額外設定。

   ![新增決策擴充功能](assets/tag-add-decisioning-extension.png)


### 更新您的結構描述

1. 導覽至資料收集介面並選取「 」 **[!UICONTROL 方案]** 從左側邊欄。
1. 選取 **[!UICONTROL 瀏覽]** 從頂端列。
1. 選取要開啟的結構描述。
1. 在架構編輯器中，選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增]** 旁邊 **[!UICONTROL 欄位群組]**.
1. 在 **[!UICONTROL 新增欄位群組]** 對話方塊，搜尋 `proposition`，選取 **[!UICONTROL 體驗事件 — 主張互動]** 並選取 **[!UICONTROL 新增欄位群組]**.
   ![主張](assets/schema-fieldgroup-proposition.png)
1. 若要儲存對結構描述的變更，請選取 **[!UICONTROL 儲存]**.


### 驗證Assurance中的設定

若要驗證Assurance中的設定：

1. 前往Assurance UI。
1. 選取 **[!UICONTROL 設定]** 在左側邊欄中並選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 旁邊 **[!UICONTROL 驗證設定]** 底下 **[!UICONTROL Adobe Journey Optimizer決策]**.
1. 選取「**[!UICONTROL 儲存]**」。
1. 選取 **[!UICONTROL 驗證設定]** 在左側邊欄中。 資料串流設定都會經過驗證，並且會在您的應用程式中設定SDK。
   ![AJO決策驗證](assets/ajo-decisioning-validation.png)

## 建立 A/B 測試

如簡介所述，您可以在Adobe Target中建立許多型別的活動，並在行動應用程式中實作。 在本課程中，您將實施A/B測試。

1. 在Target UI中，選取 **[!UICONTROL 活動]** 從頂端列。
1. 選取 **[!UICONTROL 建立活動]** 和 **[!UICONTROL A/B測試]** 從內容功能表。
1. 在 **[!UICONTROL 建立A/B測試活動]** 對話方塊，選取 **[!UICONTROL 行動]** 作為 **[!UICONTROL 型別]**，從中選擇工作區 **[!UICONTROL 選擇工作區]** 清單中，並選取您的屬性，從 **[!UICONTROL 選擇屬性]** 如果您是Target Premium客戶並在資料流中指定屬性代號，請列出此清單。
1. 選取「**[!UICONTROL 建立]**」。
   ![建立Target活動](assets/target-create-activity1.png)

1. 在 **[!UICONTROL 未命名的活動]** 熒幕，位於 **[!UICONTROL 體驗]** 步驟：

   1. 輸入 `luma-mobileapp-abtest` 在 **[!UICONTROL 選取位置]** 底下 **[!UICONTROL 位置1]**. 此位置名稱（通常稱為mbox）稍後會在應用程式實作中使用。
   1. 選取 ![Chrevron下移](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) 旁邊 **[!UICONTROL 預設內容]** 並選取 **[!UICONTROL 建立JSON選件]** 從內容功能表。
   1. 將下列JSON複製到 **[!UICONTROL 輸入有效的JSON物件]**.

      ```json
      { 
          "title": "Luma Anaolog Watch",
          "text": "Designed to stand up to your active lifestyle, this women's Luma Analog Watch features a tasteful brushed chrome finish and a stainless steel, water-resistant construction for lasting durability.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Luma_Analog_Watch.jpg" 
      }
      ```

   1. 選取 **[!UICONTROL +新增體驗]**.

      ![體驗A](assets/target-create-activity-experienceA.png)

   1. 針對體驗B重複步驟b和c，但改用以下JSON：

      ```json
      { 
          "title": "Aim Analog Watch",
          "text": "The flexible, rubberized strap is contoured to conform to the shape of your wrist for a comfortable all-day fit. The face features three illuminated hands, a digital read-out of the current time, and stopwatch functions.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Aim_Watch.jpg" 
      }
      ```

   1. 選取&#x200B;**[!UICONTROL 「下一步」]**。

      ![體驗 B](assets/target-create-activity-experienceB.png)

1. 在 **[!DNL Targeting]** 步驟，檢閱A/B測試的設定。 依預設，這兩個選件會平均分配給所有訪客。 選取&#x200B;**[!UICONTROL 「下一步」]**&#x200B;以繼續。

   ![目標定位](assets/taget-targeting.png)

1. 在 **[!UICONTROL 目標與設定]** 步驟：

   1. 重新命名未命名活動，例如 `Luma Mobile SDK Tutorial - A/B Test Example`.
   1. 輸入 **[!UICONTROL 目標]** 例如用於您的A/B測試 `A/B Test for Luma mobile app tutorial`.
   1. 選取 **[!UICONTROL 轉換]**， **[!UICONTROL 已檢視mbox]** 在 **[!UICONTROL 目標量度]** > **[!UICONTROL 我的主要目標]** 並輸入您的位置(mbox)名稱，例如 `luma-mobileapp-abtest`.
   1. 選取「**[!UICONTROL 儲存並關閉]**」。

      ![目標設定](assets/target-goals.png)

1. 返回 **[!UICONTROL 所有活動]** 畫面：

   1. 選取 ![更多](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) ，依您的活動而定。
   1. 選取 ![播放](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg) **[!UICONTROL 啟動]** 以啟動您的A/B測試。

   ![啟動](assets/target-activate.png)


## 在您的應用程式中實作Target

如先前課程所述，安裝行動標籤擴充功能僅會提供設定。 接下來，您必須安裝並註冊最佳化SDK。 如果這些步驟不清楚，請查閱 [安裝SDK](install-sdks.md) 區段。

>[!NOTE]
>
>如果您已完成 [安裝SDK](install-sdks.md) 區段，則該SDK已安裝，且您可以略過此步驟。
>

1. 在Xcode中，確認 [AEP最佳化](https://github.com/adobe/aepsdk-messaging-ios) 會新增至套件相依性中的套件清單中。 另請參閱 [Swift封裝管理程式](install-sdks.md#swift-package-manager).
1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL AppDelegate]** 在「Xcode專案」導覽器中。
1. 確定 `AEPOptimize` 是匯入清單的一部分。

   `import AEPOptimize`

1. 確定 `Optimize.self` 是您註冊的擴充功能陣列的一部分。

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]** 在「Xcode專案」導覽器中。 尋找 ` func updatePropositionAT(ecid: String, location: String) async` 函式。 新增下列程式碼：

   ```swift
   // set up the XDM dictionary, define decision scope and call update proposition API
   Task {
       let ecid = ["ECID" : ["id" : ecid, "primary" : true] as [String : Any]]
       let identityMap = ["identityMap" : ecid]
       let xdmData = ["xdm" : identityMap]
       let decisionScope = DecisionScope(name: location)
       Optimize.clearCachedPropositions()
       Optimize.updatePropositions(for: [decisionScope], withXdm: xdmData)
   }
   ```

   此函式：

   * 設定XDM字典 `xdmData`，包含ECID以識別您必須呈現A/B測試的設定檔，以及
   * 定義 `decisionScope`，表示A/B測試的一組位置。

   接著，函式會呼叫兩個API： [`Optimize.clearCachedPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#clearpropositions) 和 [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions). 這些函式會清除任何快取的主張，並更新此設定檔的主張。 此情境中的主張是從Target活動（您的A/B測試）中選取且您在中定義的體驗（選件） [建立A/B測試](#create-an-ab-test).

1. 瀏覽至 **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Personalization]** > **[!DNL TargetOffersView]** 在「Xcode專案」導覽器中。 尋找 `func onPropositionsUpdateAT(location: String) async {` 函式並檢查此函式的程式碼。 此函式最重要的部分為  [`Optimize.onPropositionsUpdate`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#onpropositionsupdate) API呼叫，因此：
   * 根據決定範圍（即您在A/B測試中定義的位置）擷取目前設定檔的主張，
   * 從主張中擷取優惠方案，
   * 會取消包裝選件的內容，以便其在應用程式中正確顯示，並且
   * 觸發 `displayed()` 選件的動作會顯示出來，此動作會將事件傳送回Platform Edge Network通知選件。

1. 仍在中 **[!DNL TargetOffersView]**，將下列程式碼新增至 `.onFirstAppear` 修飾元。 此程式碼可確保用於更新優惠方案的回撥僅註冊一次。

   ```swift
   // Invoke callback for offer updates
   Task {
       await self.onPropositionsUpdateAT(location: location)
   }
   ```

1. 仍在中 **[!DNL TargetOffersView]**，將下列程式碼新增至 `.task` 修飾元。 此程式碼會在重新整理檢視時更新選件。

   ```swift
   // Clear and update offers
   await self.updatePropositionsAT(ecid: currentEcid, location: location)
   ```

您可以在個人化查詢要求中傳送其他Target引數（例如mbox、設定檔、產品或訂單引數）至Experience Edge網路，方法是在呼叫 [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions) API。 如需詳細資訊，請參閱 [目標引數](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/#target-parameters).


## 使用應用程式進行驗證

1. 在模擬器中或從Xcode在實體裝置上重建並執行應用程式，使用 ![播放](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. 前往 **[!UICONTROL 個人化]** 標籤。

1. 向下捲動到底部，您會看到在A/B測試中定義的兩個選件之一，顯示在 **[!UICONTROL TARGET]** 圖磚。

   <img src="assets/target-app-offer.png" width="300">


## 驗證Assurance中的實作

驗證Assurance中的A/B測試：

1. 檢閱 [設定指示](assurance.md#connecting-to-a-session) 區段來將您的模擬器或裝置連線到Assurance。
1. 選取 **[!UICONTROL 設定]** 在左側邊欄中並選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 旁邊 **[!UICONTROL 檢閱和模擬]** 底下 **[!UICONTROL Adobe Journey Optimizer決策]**.
1. 選取「**[!UICONTROL 儲存]**」。
1. 選取 **[!UICONTROL 檢閱和模擬]** 在左側邊欄中。 資料串流設定都會經過驗證，並且會在您的應用程式中設定SDK。
1. 選取 **[!UICONTROL 請求]** 在頂端列中。 您會看到 **[!DNL Target]** 要求。
   ![AJO決策驗證](assets/assurance-decisioning-requests.png)

1. 您可以探索 **[!UICONTROL 模擬]** 和 **[!UICONTROL 事件清單]** 索引標籤，以進一步瞭解功能如何檢查您的Target選件設定。

## 後續步驟

您現在應該有所有的工具，可以開始將更多A/B測試或其他Target活動（例如體驗鎖定目標、多變數測試） （如果相關且可適用）新增至應用程式。 如需更深入的資訊，請參閱 [最佳化擴充功能的GitHub存放庫](https://github.com/adobe/aepsdk-optimize-ios) 您也可以在這裡找到專用的連結 [教學課程](https://opensource.adobe.com/aepsdk-optimize-ios/#/tutorials/README) ，瞭解如何追蹤Adobe Target選件。

>[!SUCCESS]
>
>您已為A/B測試啟用應用程式，並針對Adobe Experience Platform Mobile SDK使用Adobe Target和Adobe Journey Optimizer - Decisioning擴充功能顯示A/B測試的結果。
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[結論和後續步驟](conclusion.md)**
