---
title: 使用Platform Web SDK設定決定管理
description: 瞭解如何使用Platform Web SDK實作決定管理。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Decision Management,Offers
source-git-commit: 324ce76ff9f6b926ca330de1a1e827f8e88dc12d
workflow-type: tm+mt
source-wordcount: '2464'
ht-degree: 0%

---


# 使用Platform Web SDK設定決定管理

瞭解如何使用Platform Web SDK實作決定管理。 本指南說明基本的決策管理先決條件、設定的詳細步驟，並深入探討以忠誠度狀態為中心的使用案例。

依照本教學課程指示，Journey Optimizer使用者能夠有效地套用offer decisioning功能，增強其客戶互動的個人化與關聯性。

## 學習目標

在本課程結束時，您能夠：

* 掌握Adobe Journey Optimizer中決策管理的核心概念，及其與Adobe Experience Platform Web SDK的整合。

* 瞭解設定Web SDK以進行Offer decisioning的逐步程式，確保與Journey Optimizer無縫整合。

* 探索以忠誠度狀態優惠為中心的詳細使用案例，深入瞭解如何有效建立和管理優惠、決定和位置。

* 了解決策管理框架中的基本術語及其影響。

* 了解決定規則、集合限定詞和遞補優惠方案在向正確使用者提供正確優惠方案中的重要性。

* 深入探討進階主題，例如模擬和自訂事件資料收集，讓您能夠測試、驗證及增強優惠方案傳送機制。

## 先決條件

若要完成本節中的課程，您必須先：

* 確保您的組織可以存取Adobe Journey Optimizer Ultimate (Journey Optimizer和Offer Decisioning)或Adobe Experience Platform和Offer Decisioning應用程式服務附加元件。

* 完成所有Platform Web SDK初始設定的課程。

* 讓您的組織能夠進行邊緣決策。

* 瞭解如何設定刊登版位，以及在決策範圍JSON中例項化刊登版位和活動ID。

## 限制

請注意下列限制：

* Adobe Journey Optimizer目前不支援事件型選件。 如果您根據事件建立決定規則，則無法在優惠中套用它。

## 授予決策管理的存取權限

若要授與決策管理功能的存取權，您必須建立 **產品設定檔** 並將對應許可權指派給使用者。 [在本節中進一步瞭解管理Journey Optimizer使用者和許可權](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

## 設定資料串流

offer decisioning必須在以下位置啟用： **資料流** Platform Web SDK提供任何決定管理活動之前的設定。

若要在資料流中設定Offer decisioning：

1. 前往 [資料彙集](https://experience.adobe.com/#/data-collection) 介面。

1. 在左側導覽中選取 **資料串流**.

1. 選取先前建立的Luma Web SDK資料流。

   ![選取資料流](../assets/decisioning-datastream-select.png)

1. 選取 **編輯** 在 **Adobe Experience Platform服務**.

   ![編輯服務](../assets/decisioning-edit-datastream.png)

1. 檢查 **offer decisioning** 方塊。

   ![新增熒幕擷圖](../assets/decisioning-check-offer-box.png)

1. 選取「**儲存**」。

這可確保Journey Optimizer的傳入事件可由 **Adobe Experience Platform Edge**.

## 設定SDK以進行決定管理

視您的Web SDK實作型別而定，決定管理需要其他SDK步驟。 有兩個可用選項可設定SDK以進行決定管理。

* SDK獨立安裝
   1. 設定 `sendEvent` 使用您的動作 `decisionScopes`.

      ```javascript
      alloy("sendEvent", {
         ...
         "decisionScopes": [
            "[DECISION SCOPE 1]",
            "[DECISION SCOPE 2]"
         ]
      })
      ```

* SDK標籤安裝
   1. 前往資料收集介面。

   1. 在左側導覽中選取 **標籤**.

      ![選取標籤](../assets/decisioning-data-collection-tags.png)

   1. 選取 **標籤屬性**.

   1. 建立您的 **規則**.
      * 新增Platform Web SDK **傳送事件動作** 並新增相關 `decisionScopes` 至該動作的設定。

   1. 建立並發佈 **資料庫** 包含所有相關 **規則**， **資料元素**、和 **擴充功能** 您已設定。

## 術語

首先，您應該了解決定管理介面中使用的術語。

* **上限**：指定選件出現頻率的限制。 兩種型別：
   * 上限：選件可在目標對象中顯示的最大次數。
   * 設定檔上限：可向特定使用者顯示選件的次數。
* **集合**：依行銷人員設定之特定條件分組的優惠方案子集，例如，優惠方案類別。
* **決定**：指定選擇選件的邏輯。
* **決定規則**：優惠方案上的限制，用於瞭解使用者的資格。
* **符合資格的優惠**：符合預先設定條件約束的優惠方案，可向使用者顯示。
* **決定管理**：使用商業邏輯和決定規則編撰及分送個人化優惠的系統。
* **遞補優惠**：當使用者不符合集合中任何優惠方案的資格時，顯示的預設優惠方案。
* **選件**：具有決定其檢視者之潛在適用性規則的行銷訊息。
* **選件資料庫**：管理優惠方案、決定和相關規則的中央存放庫。
* **個人化優惠**：根據資格限制量身打造的自訂行銷訊息。
* **版位**：向使用者顯示優惠方案的設定或案例。
* **優先順序**：優惠方案的排名量度，會考量各種限制，例如適用性和上限。
* **表示方式**：頻道特定資訊，例如，位置或語言，可指引優惠方案的顯示。

## 使用案例概述 — 忠誠度獎勵

在本課程中，您會實作一個熟客獎勵範例使用案例，以瞭解使用Web SDK的決策管理。

此使用案例可讓您更瞭解Journey Optimizer如何運用集中式優惠資料庫和優惠決定引擎，為客戶提供最佳優惠。

>[!NOTE]
>
> 由於本教學課程的目標是實施者，因此請注意，本課程涉及Journey Optimizer的大量介面工作。 雖然這類介面任務通常由行銷人員處理，但對於實作者來說，即使他們對於決策管理行銷活動的長期建立並不負責，獲得對流程的深入瞭解也會很有幫助。

## 元件

在開始建立優惠方案之前，您必須定義數個必要元件。

### 建立熟客方案位置

**版位** 是用來展示優惠方案的容器。 在此範例中，您會在Luma網站頂端建立版位。

位置清單可在 **元件** 功能表。 篩選器可協助您根據特定頻道或內容擷取版位。

![檢視位置](../assets/decisioning-placements-list.png)

若要建立位置，請執行下列步驟：

1. 按一下 **建立位置**.

   ![建立位置](../assets/decisioning-create-placement.png)

1. 定義位置的屬性：
   * **名稱**：位置的名稱。 假設此範例為投放位置 *&#39;首頁橫幅&#39;*.
   * **頻道型別**：使用位置的管道。 讓我們使用 *&#39;網頁&#39;* 因為優惠方案會顯示在Luma網站上。
   * **內容型別**：允許位置顯示的內容型別：文字、HTML、影像連結或JSON。 您可以使用 *&#39;HTML&#39;* 適用於選件。
   * **說明**：位置的說明（選用）。

   ![新增詳細資料](../assets/decisioning-placement-details.png)

1. 按一下&#x200B;**儲存**。
1. 位置建立後，會顯示在「位置」清單中。
1. 選取包含新版位的列，並記下版位ID，因為這在您的決定範圍內進行設定可能是必要的。

   ![請參閱版位ID ](../assets/decisioning-placement-id.png)

### 熟客狀態的決定規則

**決定規則** 指定提供優惠的條件。 在此範例中，您會建立決定規則，以根據使用者的忠誠度狀態提供不同的優惠方案。

決定規則清單可在 **元件** 功能表。

若要建立決定規則，請遵循下列步驟：

1. 導覽至 **規則** 標籤，然後按一下 **建立規則**.

   ![建立規則](../assets/decisioning-create-rule.png)

1. 讓我們命名第一個規則&#39;*金級忠誠度狀態規則*&#39;. 您可以使用XDM欄位來定義規則。 Adobe Experience Platform **區段產生器** 是可用來建立規則條件的直覺式介面。

   ![定義規則](../assets/decisioning-define-rule.png)

1. 按一下 **儲存** 以確認規則條件。
1. 新儲存的&#39;*金級忠誠度狀態規則*&#39;將顯示在 **規則清單**. 選取它以顯示其屬性。

   ![檢視建立的規則](../assets/decisioning-view-rules.png)

1. 現在建立使用案例的剩餘熟客方案規則條件。


### 集合限定詞

**集合限定詞** 可讓您輕鬆整理及搜尋優惠資料庫中的優惠方案。 在此範例中，您可將集合限定詞新增至「忠誠度獎勵」優惠方案，以改善優惠方案組織。

集合限定詞清單可在 **元件** 功能表。

若要建立「熟客獎勵」收集限定詞，請遵循下列步驟：

1. 導覽至 **集合限定詞** 標籤，然後按一下 **建立集合限定詞**.

   ![建立集合限定詞](../assets/decisioning-create-collection-qualifier.png)

1. 讓我們命名集合限定詞&#39;*熟客方案獎勵*『

   ![為集合命名](../assets/decisioning-name-collection.png)

1. 新的集合限定詞現在應顯示在 **集合限定詞** 標籤

## 優惠

現在該建立忠誠獎勵優惠方案了。

優惠清單的存取位置為 **選件** 功能表。

![檢視選件功能表](../assets/decisioning-offers-menu.png)


### 建立不同忠誠度層級的優惠方案

首先建立不同Luma忠誠度等級的個人化優惠方案。

若要建立第一個 **優惠方案**，請遵循下列步驟：

1. 按一下 **建立選件**，然後選取 **個人化優惠**.

1. 讓我們命名第一個選件&#39;*Luma忠誠度等級 — 金級*&#39;. 您必須指定此優惠方案的開始/結束日期和時間。 您也應該關聯 **集合限定詞** 『*熟客方案獎勵*」轉換為選件，讓您更妥善地在 **選件資料庫**. 之後，按一下 **下一個**.

   ![新增優惠詳細資料](../assets/decisioning-add-offer-details.png)

1. 現在您必須新增 **表示方式** 以定義優惠方案的顯示位置。 讓我們選擇 **Web channel**. 我們也請選擇「*首頁橫幅*『 **刊登** 您先前已設定。 選取的 **刊登** 是HTML型別，因此您可以直接新增HTML、JSON或文字內容至編輯器，以使用建置選件 **自訂** 選項按鈕。

   ![新增代表詳細資料](../assets/decisioning-add-representation-details.png)

1. 直接使用編輯選件內容 **運算式編輯器**. 請記住，您可以新增HTML、JSON或TEXT內容至此版位。 請確定您選取正確的專案 **模式** （視您的內容型別而定）底部的URL。 您也可以點選 **驗證** 以確保沒有錯誤。

   ![新增優惠HTML](../assets/decisioning-add-offer-html.png)

1. 您也可以使用運算式編輯器來擷取儲存在Adobe Experience Platform中的屬性。 將設定檔的名字新增至優惠內容，以便更妥善地為忠誠會員進行1:1層級的個人化。

   ![新增優惠個人化](../assets/decisioning-add-offer-personalization.png)

1. 新增條件約束，以僅顯示符合以下條件的設定檔的優惠：*金級忠誠度狀態規則*&#39;.

   ![新增規則限制](../assets/decisioning-add-rule-constraint.png)

1. 檢閱完優惠方案後，請按一下 **完成**. 選取 **儲存並核准**.

現在為各種Luma忠誠度層級建立其餘的優惠方案

### 遞補優惠

您仍想要為Luma網站的非Luma忠誠度訪客提供優惠方案。 若要這麼做，您可以設定 **遞補優惠** 促銷活動。

若要建立遞補優惠，請依照下列步驟進行：

1. 按一下 **建立選件**，然後選取 **遞補優惠**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 讓我們命名遞補優惠&#39;*非Luma忠誠度*&#39;. 您也可以關聯先前建立的 **集合限定詞**， &#39;*熟客方案獎勵*&#39;變更為遞補優惠，讓優惠方案組織更輕鬆。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 將遞補優惠內容新增至 **運算式編輯器**. 請記住，您可以新增HTML、JSON或TEXT內容至此版位。 請確定您選取正確的專案 **模式** （視您的內容型別而定）底部的URL。 您也可以點選 **驗證** 以確保沒有錯誤。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 如果所有專案都已正確設定，請按 **完成** 然後 **儲存並核准**.
<!--
   ![ADD SCREENSHOT](#)
-->

## 決策

**決定** 是優惠方案的容器，可依據目標為客戶挑選最佳優惠方案。

決定清單可在 **決定** 的標籤 **選件** 功能表。
<!--
   ![ADD SCREENSHOT](#)
-->

### 建立忠誠度優惠的決定

讓我們為Luma忠誠度獎勵使用案例建立決定。

若要建立決定，請遵循下列步驟：

1. 按一下 **建立決定**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 讓我們來呼叫決定， &#39;*12月Luma忠誠度優惠*&#39;. 選件應持續1個月，所以我們在這裡指定。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 現在您必須定義 **決定範圍**. 首先，選取位置。 您可以使用先前建立的&#39;*首頁橫幅*&#39;.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 接下來，您必須新增 **評估准則** 用於決定範圍。 按一下 **新增** 並選擇先前建立的&#39;*熟客方案獎勵*『 **集合** 包含要考慮的所有熟客方案。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 在「*熟客方案獎勵*&#39;集合，您可以使用適用性欄位，將選件傳遞限製為Luma訪客的子集。 不過，針對此使用案例，您希望每位訪客都能收到其中一個選件。 記住，您已設定 **遞補優惠** 適用於所有不忠誠的訪客。 將資格設為「無」。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 此外，您也可以使用 **排名方法** 如果多個選件符合使用者/位置組合的資格，則欄位可選取每個Luma訪客的最佳選件。 對於此使用案例，您可以使用 **優惠優先順序** 方法，使用選件中定義的值來提供最佳選件。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 現在新增 **遞補優惠** 以做出決定。 提醒，如果Luma訪客未歸入任何Luma忠誠度受眾，則遞補優惠是顯示給Luma訪客的預設優惠。 選取&#39;*非Luma忠誠度*」的可用遞補優惠清單中的「 」*首頁橫幅*&#39;位置。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 在啟用決定之前，請先檢閱決定範圍、遞補優惠、預覽可用優惠，以及估計合格的設定檔。 一切看起來正常後，您可以按一下 **完成** 和 **儲存並啟動**.
<!--
   ![ADD SCREENSHOT](#)
-->

## 模擬

最佳實務是驗證Luma忠誠度決策邏輯，確保將正確的優惠方案傳遞至正確的忠誠度對象。 您可以透過使用完成此操作 **測試設定檔**. 同時，也建議您先透過測試設定檔來測試優惠方案的變更，然後再將新優惠方案版本推送至生產環境。

若要開始測試，請選取 **模擬** 標籤從 **選件** 功能表。

### 測試忠誠度優惠

1. 選取要用於模擬的測試設定檔。 按一下 **管理設定檔**. [若要建立或指定新的測試設定檔以進行選件測試，請遵循本指南](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles.html?lang=en#create-test-profiles-csv).
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 將一個或多個測試設定檔新增到模擬中，並儲存您的選擇。 在使用案例測試中，您應該確保已為每個Luma忠誠度獎勵對象設定了測試設定檔。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 選取要測試的決定範圍。 選取 **新增決定範圍**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 選取先前建立的&#39;*首頁橫幅*&#39;位置。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 系統會顯示可用的決定，請選取先前建立的&#39;*12月Luma忠誠度優惠*&#39;決定，然後按一下 **新增**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 選取測試設定檔後，按一下 **檢視結果**. 最佳可用選件會顯示給「 」的選定測試設定檔&#x200B;*12月Luma忠誠度優惠*&#39;決定。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 選取其他測試設定檔，然後按一下 **檢視結果**. 理想情況下，您應該看到不同的模擬優惠方案，與測試設定檔的忠誠度等級相對應。

## 使用Adobe Experience Platform Debugger的決策管理驗證

此 **Adobe Experience Platform Debugger** 擴充功能適用於Chrome和Firefox，可分析您的網頁，以識別Adobe Experience Cloud解決方案實作中的問題。

您可以在Luma網站上使用除錯工具，驗證生產環境中的決策邏輯。 當忠誠獎勵使用案例啟動並執行時，這是不錯的做法，可確保一切都已正確設定。

[瞭解如何使用這裡的指南，在瀏覽器中設定除錯工具](https://experienceleague.adobe.com/docs/platform-learn/data-collection/debugger/overview.html?lang=en).

若要使用除錯工具開始驗證：

1. 導覽至包含優惠方案版位的Luma網頁。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 在網頁上，開啟 **Adobe Experience Platform debugger**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 瀏覽至 **摘要**. 確認 **資料串流ID** 符合 **資料流** 在 **Adobe資料彙集** 您已為其啟用Offer Decisioning的。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 在 **解決方案** 導覽至 **Experience PlatformWeb SDK**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 在 **設定** 標籤，切換開啟 **啟用偵錯**. 如此可啟用記錄中的工作階段 **Adobe Experience Platform保證** 工作階段。
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. 接著，您可以使用各種Luma忠誠度帳戶登入網站，並使用除錯工具驗證傳送至 **Adobe Experience Platform Edge網路**. 這些要求均應擷取至 **保證** 用於記錄追蹤。
<!--
   ![ADD SCREENSHOT](#)
-->