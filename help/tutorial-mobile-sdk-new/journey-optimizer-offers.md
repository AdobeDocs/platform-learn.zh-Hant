---
title: Adobe Journey Optimizer優惠方案
description: 瞭解如何使用Platform Mobile SDK和Adobe Journey Optimizer Decision Management來建立和顯示優惠方案。
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Offers
hide: true
source-git-commit: 5f0fa0b524cd4a12aaab8c8c0cd560a31003fbd8
workflow-type: tm+mt
source-wordcount: '2344'
ht-degree: 2%

---

# Journey Optimizer優惠方案

瞭解如何透過Platform Mobile SDK在行動應用程式中顯示Journey Optimizer決定管理所提供的優惠方案。

Journey Optimizer決策管理可協助您在適當的時間為所有接觸點的客戶提供最佳優惠和體驗。 設計完成後，透過個人化優惠目標定位對象。

決策管理透過集中行銷優惠資料庫和決定引擎輕鬆實現個人化，該決策引擎將規則和限制套用於Adobe Experience Platform建立的豐富即時設定檔。 因此，它可讓您在適當的時間傳送適當的優惠方案給客戶。 另請參閱 [關於決定管理](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/starting-offer-decisioning.html?lang=en) 以取得詳細資訊。


>[!NOTE]
>
>本課程為選修課程，僅適用於希望使用決定管理功能在行動應用程式中顯示優惠的Journey Optimizer使用者。


## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。
* 存取Journey Optimizer — 決定管理，並依照所述以適當許可權管理優惠和決定 [此處](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).


## 學習目標

在本課程中，您將學習

* 更新您的Edge設定以進行決策管理。
* 使用Journey Optimizer - Decisioning擴充功能更新標籤屬性。
* 更新您的結構描述以擷取主張事件。
* 驗證Assurance中的設定。
* 根據Journey Optimizer中的優惠建立優惠決定 — 決定管理。
* 更新您的應用程式以包含Optimizer擴充功能。
* 在您的應用程式中實施來自Decision Management的優惠。


## 設定您的應用程式

>[!TIP]
>
>如果您已將應用程式設定為 [使用Target設定A/B測試](target.md) 教學課程，您可以略過 [安裝Adobe Journey Optimizer - Decisioning標籤擴充功能](#install-adobe-journey-optimizer---decisioning-tags-extension) 和 [更新您的結構描述](#update-your-schema).

### 更新邊緣組態

為確保將從您的行動應用程式傳送到Edge Network的資料轉送到Journey Optimizer — 決策管理，請更新您的Experience Edge設定。

1. 在資料收集UI中，選取 **[!UICONTROL 資料串流]**，並選取您的資料串流，例如 **[!UICONTROL Luma行動應用程式]**.
1. 選取 ![更多](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) 的 **[!UICONTROL Experience Platform]** 並選取 ![編輯](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL 編輯]** 從內容功能表。
1. 在 **[!UICONTROL 資料串流]** > ![資料夾](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) >  **[!UICONTROL Adobe Experience Platform]** 畫面，確認 **[!UICONTROL offer decisioning]**， **[!UICONTROL 邊緣細分]**， **[!UICONTROL 個人化目的地]**、和 **[!UICONTROL Adobe Journey Optimizer]** 已選取。 另請參閱 [Adobe Experience Platform設定](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) 以取得詳細資訊。
1. 若要儲存資料流設定，請選取 **[!UICONTROL 儲存]** .

   ![AEP資料流設定](assets/datastream-aep-configuration.png)


### 安裝Journey Optimizer - Decisioning標籤擴充功能

1. 瀏覽至 **[!UICONTROL 標籤]** 並尋找您的行動標籤屬性並開啟屬性。
1. 選取 **[!UICONTROL 擴充功能]**.
1. 選取 **[!UICONTROL 目錄]**.
1. 搜尋 **[!UICONTROL Adobe Journey Optimizer - Decisioning]** 副檔名。
1. 安裝擴充功能。 此擴充功能不需要額外設定。

   ![新增決策擴充功能](assets/tag-add-decisioning-extension.png)


### 更新您的結構描述

1. 導覽至資料收集UI並選取 **[!UICONTROL 方案]** 從左側邊欄。
1. 選取 **[!UICONTROL 瀏覽]** 從頂端列。
1. 選取要開啟的結構描述。
1. 在架構編輯器中，選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增]** 欄位群組旁。
1. 在 **[!UICONTROL 新增欄位群組]** 對話方塊， ![搜尋](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) 搜尋 `proposition`，選取 **[!UICONTROL 體驗事件 — 主張互動]** 並選取 **[!UICONTROL 新增欄位群組]**.
   ![主張](assets/schema-fieldgroup-proposition.png)
1. 選取 **[!UICONTROL 儲存]** 以儲存對結構描述的變更。


## 驗證Assurance中的設定

若要驗證Assurance中的設定：

1. 前往Assurance UI。
1. 選取 **[!UICONTROL 設定]** 在左側邊欄中並選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 旁邊 **[!UICONTROL 驗證設定]** 底下 **[!UICONTROL Adobe Journey Optimizer決策]**.
1. 選取「**[!UICONTROL 儲存]**」。
1. 選取 **[!UICONTROL 驗證設定]** 在左側邊欄中。 資料串流設定都會經過驗證，並且會在您的應用程式中設定SDK。
   ![AJO決策驗證](assets/ajo-decisioning-validation.png)


## 建立優惠方案

1. 在Journey Optimizer UI中，選取 ![選件](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Offers_18_N.svg)  **[!UICONTROL 選件]** 從 **[!UICONTROL 決定管理]** 在左側邊欄中。
1. 在 **[!UICONTROL 選件]** 熒幕，選取 **[!UICONTROL 瀏覽]** 以檢視優惠方案清單。
1. 選取 **[!UICONTROL 建立選件]**.
1. 在 **[!UICONTROL 新優惠]** 對話方塊，選取 **[!UICONTROL 個人化優惠]** 並按一下 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 詳細資料]** 第步/共步 **[!UICONTROL 建立新的個人化優惠方案]**：
   1. 輸入 **[!UICONTROL 名稱]** 例如，針對選件 `Luma - Juno Jacket`，並輸入 **[!UICONTROL 開始日期和時間]** 和 **[!UICONTROL 結束日期和時間]**. 在這些日期之外，決策引擎將不會選取選件。
   1. 選取&#x200B;**[!UICONTROL 「下一步」]**。
      ![優惠 — 詳細資料](assets/ajo-offers-details.png)

1. 在 **[!UICONTROL 新增表示方式]** 第步/共步 **[!UICONTROL 建立新的個人化優惠方案]**：
   1. 選取 ![行動](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DevicePhone_18_N.svg) **[!UICONTROL 行動]** 從 **[!UICONTROL 頻道]** 清單，然後選取 **[!UICONTROL 行動JSON]** 從 **[!UICONTROL 刊登]** 清單。
   1. 選取 **[!UICONTROL 自訂]** 的 **[!UICONTROL 內容]**.
   1. 選取 **[!UICONTROL 新增內容]**. 在 **[!UICONTROL 新增個人化]** 對話方塊：
      1. 輸入下列JSON：

         ```json
         { 
             "title": "Juno Jacket",
             "text": "On colder-than-comfortable mornings, you'll love warming up in the Juno All-Ways Performanc Jacket, designed to compete with wind and chill. Built-in Cocona&trade; technology aids evaporation, while a special zip placket and stand-up collar keep your neck protected.", 
             "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/jackets/wj06-purple_main.jpg" 
         }  
         ```

      1. 選取「**[!UICONTROL 儲存]**」。
         ![選件 — 自訂內容](assets/ajo-offers-customcontent.png)
   1. 選取&#x200B;**[!UICONTROL 「下一步」]**。
      ![優惠方案宣告](assets/ajo-offers-representations.png)

1. 在 **[!UICONTROL 新增限制]** 的步驟 **[!UICONTROL 建立新的個人化優惠方案]**：
   1. 設定 **[!UICONTROL 優先順序]** 至 `10`.
   1. 切換 **[!UICONTROL 包含上限]** 關閉。
   1. 選取&#x200B;**[!UICONTROL 「下一步」]**。
      ![優惠 — 限制](assets/ajo-offers-constraints.png)

1. 在 **[!UICONTROL 檢閱]** 第步/共步 **[!UICONTROL 建立新的個人化]** 選件：
   1. 檢閱選件，然後選取 **[!UICONTROL 完成]**.
   1. 在 **[!UICONTROL 儲存選件]** 對話方塊，選取 **[!UICONTROL 儲存並核准]**.

1. 重複步驟3至8，再建立四個具有不同名稱和內容的選件。 所有其他設定值（例如開始日期和時間或優先順序）與您建立的第一個選件類似。 您可以快速建立重複和編輯選件。

   1. 在Journey Optimizer UI中，選取 ![選件](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Offers_18_N.svg) **[!UICONTROL 選件]** 從左側邊欄，然後從頂端列選取選件。
   1. 選取您建立之優惠方案的列。
   1. 在右窗格中，選取 ![更多](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmall_18_N.svg) **[!UICONTROL 更多動作]** 從快顯選單中選取 ![複製](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Duplicate_18_N.svg) **[!UICONTROL 複製]**.

      使用下表來定義其他四個選件。

      | 優惠方案名稱 | 選件內容 |
      |---|---|
      | Luma - Affirm Water Bottle | `{ "title": "Affirm Water Bottle", "text": "You'll stay hydrated with ease with the Affirm Water Bottle by your side or in hand. Measurements on the outside help you keep track of how much you're drinking, while the screw-top lid prevents spills. A metal carabiner clip allows you to attach it to the outside of a backpack or bag for easy access.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/fitness-equipment/ug06-lb-0.jpg" }` |
      | Luma - Desiree健身T恤 | `{ "title": "Desiree Fitness Tee", "text": "When you're too far to turn back, thank yourself for choosing the Desiree Fitness Tee. Its ultra-lightweight, ultra-breathable fabric wicks sweat away from your body and helps keeps you cool for the distance.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/tees/ws05-yellow_main.jpg" }` |
      | Luma - Adrienne Trek Jacket | `{ "title": "Adrienne Trek Jacket", "text": "You're ready for a cross-country jog or a coffee on the patio in the Adrienne Trek Jacket. Its style is unique with stand collar and drawstrings, and it fits like a jacket should.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/jackets/wj08-gray_main.jpg" }` |
      | Luma - Aero每日健身運動鞋 | `{ "title": "Adrienne Trek Jacket", "text": "You're ready for a cross-country jog or a coffee on the patio in the Adrienne Trek Jacket. Its style is unique with stand collar and drawstrings, and it fits like a jacket should.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/jackets/wj08-gray_main.jpg" }` |

      {style="table-layout:fixed"}

1. 最後一步您必須建立遞補優惠，如果客戶不符合其他優惠方案的資格，就會傳送此優惠方案給客戶。
   1. 選取 **[!UICONTROL 建立選件]**.
   1. 在 **[!UICONTROL 詳細資料]** 第步/共步 **[!UICONTROL 建立新的個人化優惠方案]**：
   1. 輸入 **[!UICONTROL 名稱]** 例如，針對選件 `Luma - Fallback Offer`，並輸入 **[!UICONTROL 開始日期和時間]** 和 **[!UICONTROL 結束日期和時間]**.
   1. 選取&#x200B;**[!UICONTROL 「下一步」]**。

1. 在 **[!UICONTROL 新增表示方式]** 的步驟 **[!UICONTROL 建立新的個人化優惠方案]** 畫面：
   1. 選取 ![行動](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DevicePhone_18_N.svg) **[!UICONTROL 行動]** 從 **[!UICONTROL 頻道]** 清單，然後選取 **[!UICONTROL 行動JSON]** 從 **[!UICONTROL 刊登]** 清單。
   1. 選取 **[!UICONTROL 自訂]** 的 **[!UICONTROL 內容]**.
   1. 選取 **[!UICONTROL 新增內容]**. 在 **[!UICONTROL 新增個人化]** 對話方塊：
      1. 輸入下列JSON：

         ```json
         {  
             "title": "Luma",
             "text": "Your store for sports wear and equipment.", 
             "image": "https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png" 
         }  
         ```

      1. 選取「**[!UICONTROL 儲存]**」。
   1. 選取&#x200B;**[!UICONTROL 「下一步」]**。


1. 在 **[!UICONTROL 檢閱]** 第步/共步 **[!UICONTROL 建立新的個人化]** 選件：
   1. 檢閱選件，然後選取 **[!UICONTROL 完成]**.
   1. 在 **[!UICONTROL 儲存選件]** 對話方塊，選取 **[!UICONTROL 儲存並核准]**.

您現在應該擁有下列優惠方案清單。
![選件清單](assets/ajo-offers-list.png)


## 建立集合

若要向行動應用程式使用者呈現優惠方案，您必須定義優惠方案集合，其中包含您建立的一或多個優惠方案。

1. 在Journey Optimizer UI中，選取 **[!UICONTROL 選件]** 從左側邊欄。
1. 選取 **[!UICONTROL 集合]** 從頂端列。
1. 選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 建立集合]**.
1. 在 **[!UICONTROL 新集合]** 強制回應視窗，輸入 **[!UICONTROL 名稱]** 例如，您的集合 `Luma - Mobile App Collection`，選取 **[!UICONTROL 建立靜態集合]**，然後按一下 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL Luma — 行動應用程式集合]**，選取您要納入集合中的優惠方案。 在本教學課程中，請挑選您建立的五個選件。
   ![優惠 — 集合](assets/ajo-collection-offersselected.png)
1. 選取「**[!UICONTROL 儲存]**」。


## 建立決定

最後一個步驟是定義決定，此決定是一或多個決定範圍與您的遞補優惠的組合。

決定範圍是特定位置(例如電子郵件中的HTML，或行動應用程式中的JSON)與一個或多個評估標準的組合。

評估准則為

* 優惠收藏，
* 適用性規則：例如優惠方案僅適用於特定對象，
* 排名方法：如果有多個優惠方案可供挑選，您要使用哪個方法來為其排名（例如依優惠方案優先順序、使用公式或AI模型）。

另請參閱 [建立和管理優惠的重要步驟](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/key-steps.html?lang=en) 如果您想更深入瞭解位置、規則、排名、優惠、代表、集合、決定等如何相互互動及建立關聯。 本教學課程僅著重於使用決定的輸出，而非定義決定的彈性。

1. 在Journey Optimizer UI中，選取 **[!UICONTROL 選件]** 從左側邊欄。
1. 選取 **[!UICONTROL 決定]** 從頂端列。
1. 選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 建立決定]**.
1. 在 **[!UICONTROL 詳細資料]** 第步/共步 **[!UICONTROL 建立新的優惠決定]**：
   1. 輸入 **[!UICONTROL 名稱]** 用於決定，例如 `Luma - Mobile App Decision`，輸入 **[!UICONTROL 開始日期和時間]** 和 **[!UICONTROL 結束日期和時間]**.
   1. 選取&#x200B;**[!UICONTROL 「下一步」]**。

1. 在 **[!UICONTROL 新增決定範圍]** 第步/共步 **[!UICONTROL 建立新的優惠決定]**：
   1. 選取 **[!UICONTROL 行動JSON]** 從 **[!UICONTROL 刊登]** 清單。
   1. 在 **[!UICONTROL 評估准則]** 圖磚，選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增]**.
      1. 在 **[!UICONTROL 新增優惠收藏]** 對話方塊中，選取您的優惠收藏。 例如， **[!UICONTROL Luma — 行動應用程式集合]**.
      1. 選取 **[!UICONTROL 新增]**.
         ![決定 — 選取集合](assets/ajo-decision-selectcollection.png)
   1. 確定 **[!UICONTROL 無]** 已選取用於 **[!UICONTROL 資格]**、和 **[!UICONTROL 優惠優先順序]** 已選取作為 **[!UICONTROL 排名方法]**.
   1. 選取&#x200B;**[!UICONTROL 「下一步」]**。
      ![決定範圍](assets/ajo-decision-scopes.png).
1. 在 **[!UICONTROL 新增遞補優惠]** 第步/共步 **[!UICONTROL 建立新的優惠決定]**：
   1. 選取您的遞補優惠，例如 **[!UICONTROL Luma — 遞補優惠]**.
   1. 選取&#x200B;**[!UICONTROL 「下一步」]**。
1. 在 **[!UICONTROL 摘要]** 第步/共步 **[!UICONTROL 建立新的優惠決定]**：
   1. 選取「**[!UICONTROL 完成]**」。
   1. 在 **[!UICONTROL 儲存優惠決定]** 對話方塊，選取 **[!UICONTROL 儲存並啟動]**.
   1. 在 **[!UICONTROL 決定]** 標籤，您會看到含有狀態的決定 **[!UICONTROL 即時]**.

您的優惠決定（包含一組優惠）現在已可供使用。 若要在應用程式中使用決定，您必須在程式碼中參考決定範圍。

1. 在Journey Optimizer UI中，選取 **[!UICONTROL 選件]**.
1. 選取 **[!UICONTROL 決定]** 從頂端列。
1. 選取您的決定，例如 **[!UICONTROL Luma — 行動應用程式決策]**.
1. 在 **[!UICONTROL 決定範圍]** 圖磚，選取 ![複製](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL 複製]**.
1. 從內容功能表中，選取 **[!UICONTROL 決定範圍]**.
   ![複製決定範圍](assets/ajo-copy-decisionscope.png)
1. 使用任何文字編輯器貼上決定範圍以供稍後使用。 決定範圍具有下列JSON格式。

   ```json
   {
       "xdm:activityId":"xcore:offer-activity:xxxxxxxxxxxxxxx",
       "xdm:placementId":"xcore:offer-placement:xxxxxxxxxxxxxxx"
   }
   ```

## 在您的應用程式中實作選件

如先前課程所述，安裝行動標籤擴充功能僅會提供設定。 接下來，您必須安裝並註冊最佳化SDK。 如果這些步驟不清楚，請查閱 [安裝SDK](install-sdks.md) 區段。

>[!NOTE]
>
>如果您已完成 [安裝SDK](install-sdks.md) 區段，則該SDK已安裝，且您可以略過此步驟。
>

1. 在Xcode中，確認 [AEP最佳化](https://github.com/adobe/aepsdk-messaging-ios.git) 會新增至套件相依性中的套件清單中。 另請參閱 [Swift封裝管理程式](install-sdks.md#swift-package-manager).
1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** 在「Xcode專案」導覽器中。
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

1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** 在「Xcode專案」導覽器中。 尋找 `func updatePropositionOD(ecid: String, activityId: String, placementId: String, itemCount: Int) async` 函式。 Inspect程式碼

   * 設定XDM字典 `xdmData`，包含ECID以識別您必須提供選件的設定檔。
   * 定義 `decisionScope`，此物件是根據您在Journey Optimizer — 決定管理UI中定義的決定而定義，並使用以下複製的決定範圍來定義： [建立決定](#create-a-decision).
   * 會呼叫兩個API： [`Optimize.clearCachePropositions`](https://support.apple.com/en-ie/guide/mac-help/mchlp1015/mac)  和 [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions).   這些函式會清除任何快取的主張，並更新此設定檔的主張。 Luma應用程式使用設定檔案(`decisions.json`)預設集，會根據下列JSON格式擷取範圍引數：

     ```swift
     "scopes": [
         {
             "name": "luma - Mobile App Decision",
             "activityId": "xcore:offer-activity:177cdaa5e1fd589d",
             "placementId": "xcore:offer-placement:13a3b264ce69bb14",
             "itemCount": 2
         }
     ]
     ```

     不過，您可以使用任何型別的實作，以確保「最佳化API」確實取得正確的引數(`activityId`， `placementId` 和 `itemCount`)，以建構有效的 [`DecisionScope`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#decisionscope) 物件。

1. 瀏覽至 **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL 檢視]** > **[!UICONTROL 個人化]** > **[!UICONTROL EdgeOffersView]** 在「Xcode專案」導覽器中。 尋找 `func getPropositionOD(activityId: String, placementId: String, itemCount: Int) async` 函式並檢查此函式的程式碼。 此函式最重要的部分為  [`Optimize.getPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#getpropositions) API呼叫，此

   * 根據決定範圍(您已在Journey Optimizer — 決定管理中定義)擷取目前設定檔的建議，並
   * 會取消包裝應用程式中可正確顯示的結果，即內容。

1. 仍在中 **[!UICONTROL EdgeOffersView]**，找到 `func updatePropositions(activityId: String, placementId: String, itemCount: Int) async` 函式並新增下列程式碼：

   ```swift
       Task {
           await self.updatePropositionOD(
               ecid: currentEcid,
               activityId: activityId,
               placementId: placementId,
               itemCount: itemCount
           )
       }
       try? await Task.sleep(seconds: 2.0)
       Task {
           await self.getPropositionOD(
               activityId: activityId,
               placementId: placementId,
               itemCount: itemCount
           )
       }
   ```

   此程式碼會確保您更新主張，然後使用步驟5和步驟6中所述的函式擷取結果。


## 使用應用程式進行驗證

1. 在裝置上或在模擬器中開啟您的應用程式。

1. 前往 **[!UICONTROL 個人化]** 標籤。

1. 選取 **[!UICONTROL 邊緣個人化]**.

1. 捲動至頂端，您會看到已在中定義的集合中，顯示兩個隨機選件 **[!UICONTROL 決定LUMA — 行動應用程式決定]** 圖磚。

   <img src="assets/ajo-app-offers.png" width="300">

   優惠是隨機的，因為您已為所有優惠提供相同的優先順序，而決策的排名是根據優先順序。


## 驗證Assurance中的實作

若要驗證Assurance中的優惠方案實作：

1. 前往Assurance UI。
1. 選取 **[!UICONTROL 設定]** 在左側邊欄中並選取 ![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) 旁邊 **[!UICONTROL 檢閱和模擬]** 底下 **[!UICONTROL Adobe Journey Optimizer決策]**.
1. 選取「**[!UICONTROL 儲存]**」。
1. 選取 **[!UICONTROL 檢閱和模擬]** 在左側邊欄中。 資料串流設定都會經過驗證，並且會在您的應用程式中設定SDK。
1. 選取 **[!UICONTROL 請求]** 在頂端列中。 您會看到 **[!UICONTROL 選件]** 要求。
   ![AJO決策驗證](assets/assurance-decisioning-requests.png)

1. 您可以探索 **[!UICONTROL 模擬]** 和 **[!UICONTROL 事件清單]** 索引標籤以進一步瞭解功能，檢查您的Journey Optimizer決定管理設定。

## 後續步驟

您現在應該擁有所有工具，可以開始將更多功能新增到您的Journey Optimizer — 決定管理實作。 例如：

* 套用不同引數至您的選件（例如，優先順序、上限）
* 在應用程式中收集設定檔屬性(請參閱 [個人資料](profile.md))並使用這些設定檔屬性來建立對象。 然後使用這些對象作為您決定中適用性規則的一部分。
* 合併多個決定範圍

>[!SUCCESS]
>
>您已啟用應用程式，以便使用Experience Platform Mobile SDK的Journey Optimizer - Decisioning擴充功能來顯示優惠方案。<br/>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

下一步： **[使用Target執行A/B測試](target.md)**
