---
title: 使用Platform Web SDK設定Adobe Target
description: 瞭解如何使用Platform Web SDK實作Adobe Target。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
solution: Data Collection, Target
source-git-commit: 58034fc649a06b4e17ffddfd0640a81a4616f688
workflow-type: tm+mt
source-wordcount: '4288'
ht-degree: 0%

---

# 使用Platform Web SDK設定Adobe Target

瞭解如何使用Platform Web SDK實作Adobe Target。 瞭解如何傳遞體驗以及如何將其他引數傳遞至Target。

[Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html) 是Adobe Experience Cloud應用程式，提供一切所需工具，讓您量身訂造及個人化您的客戶體驗，藉此為您的網頁以及行動網站、應用程式和其他數位頻道創造最高的收入。

![Web SDK和Adobe Target圖表](assets/dc-websdk-at.png)

## 學習目標

在本課程結束時，您將能夠：

* 瞭解如何新增Platform Web SDK預先隱藏程式碼片段，以防止搭配非同步標籤內嵌程式碼使用Target時忽隱忽現的情形
* 設定資料流以啟用Target功能
* 頁面載入時呈現視覺化個人化決策（先前稱為「全域mbox」）
* 傳遞XDM資料至Target並瞭解對應至Target引數
* 將自訂資料傳遞至Target，例如設定檔和實體引數
* 使用Platform Web SDK驗證Target實作
* 傳送與Adobe Analytics請求分開的Target主張請求，並稍後解決其顯示事件

>[!TIP]
>
>請參閱我們的 [將Target從at.js 2.x移轉至Platform Web SDK](/help/tutorial-migrate-target-websdk/introduction.md) 教學課程以逐步說明如何移轉您現有的at.js實作。


## 先決條件

若要完成本節中的課程，您必須先：

* 完成所有Platform Web SDK初始設定的課程，包括設定資料元素和規則。
* 確定您有 [編輯者或核准者角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 在Adobe Target中。
* 安裝 [視覺化體驗撰寫器Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 如果您使用Google Chrome瀏覽器。
* 瞭解如何在Target中設定活動。 如果您需要複習程式，下列教學課程和指南對本課程很有幫助：
   * [使用視覺化體驗撰寫器(VEC) Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html)
   * [使用 Visual Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [使用表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [建立體驗鎖定目標活動](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

## 新增減少忽隱忽現情形

開始之前，請根據標籤程式庫的載入方式，決定是否需要額外的閃爍處理解決方案。

>[!NOTE]
>
>本教學課程使用 [Luma網站](https://luma.enablementadobe.com/content/luma/us/en.html) 非同步實作標籤，並有防止忽隱忽現的機制。 本節內容僅供瞭解閃爍緩解如何與Platform Web SDK搭配運作之用。


### 非同步實施

以非同步方式載入標籤庫時，頁面可能會在Target執行內容交換之前完成轉譯。 此行為可能會導致所謂的「閃爍」問題，發生此問題時，會先短暫地顯示預設內容，然後再更換為Target指定的個人化內容。 若要避免發生這種閃爍問題，Adobe建議在非同步標籤內嵌程式碼的前面加上特殊的預先隱藏程式碼片段。

此程式碼片段已存在於Luma網站上，但讓我們進一步瞭解此程式碼的作用：

```html
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, ".personalization-container { opacity: 0 !important }", 3000);
</script>
```

預先隱藏程式碼片段會使用您選擇的CSS定義，在頁面標題中建立樣式標籤。 在收到來自Target的回應或達到逾時時間時，會移除此樣式標籤。

預先隱藏行為是由程式碼片段尾端的兩項設定所控制。

* `body { opacity: 0 !important }` 指定在Target載入之前，要用於預先隱藏的CSS定義。 依預設，會隱藏整個頁面。 您可以將此定義更新為要預先隱藏的選擇器，以及要如何隱藏它們。 您可以包含多個定義，因為此值只是插入到預先隱藏樣式標籤中的值。 如果您有可輕鬆識別的容器元素，可將內容包裝在導覽下，則可使用此設定將預先隱藏限定為該容器元素。
* `3000` 指定預先隱藏的逾時（毫秒）。 如果逾時前未收到來自Target的回應，則會移除預先隱藏樣式標籤。 達到此逾時的情況應該很少見。

>[!NOTE]
>
>Platform Web SDK的預先隱藏程式碼片段與Target at.js程式庫所使用的程式碼片段有些不同。 請務必對Platform Web SDK使用正確的程式碼片段，因為它使用不同的樣式ID： `alloy-prehiding`. 如果使用適用於at.js的預先隱藏程式碼片段，該程式碼片段可能無法正常運作。

標籤中也提供預先隱藏的程式碼片段：

1. 前往 **[!UICONTROL 擴充功能]** 標籤區段
1. 選取 **[!UICONTROL 設定]** 適用於Adobe Experience Platform Web SDK擴充功能
1. 選取 **[!UICONTROL 將預先隱藏的程式碼片段複製到剪貼簿]** 按鈕

   ![非同步實施的Target預先隱藏程式碼片段](assets/target-flicker-async.png)

   >[!NOTE]
   >
   >從Platform Web SDK擴充功能複製的預設預先隱藏程式碼片段可能包含您網站上不存在的CSS定義，例如 `.personalization-container { opacity: 0 !important }`. 請務必檢查並修改您網站的預先隱藏程式碼片段。

### 同步實施

Adobe建議如Luma網站所示，以非同步方式實作標籤。 不過，如果同步載入標籤程式庫，則不需要預先隱藏程式碼片段。 而是在Platform Web SDK擴充功能設定中指定預先隱藏樣式。

同步實施的預先隱藏樣式可依照以下方式設定：

1. 前往 **[!UICONTROL 擴充功能]** 標籤區段
1. 選取 **[!UICONTROL 設定]** Platform Web SDK擴充功能的按鈕
1. 選取 **[!UICONTROL 編輯預先隱藏樣式]** 按鈕

   ![非同步實施的Target預先隱藏程式碼片段](assets/target-flicker-sync.png)

1. 修改CSS以包含您要使用的選取器和隱藏方法，例如： `body { opacity: 0 !important }` 是否想要預先隱藏頁面的整個內文。
1. 儲存變更並建置至程式庫

>[!NOTE]
>
>預先隱藏樣式設定僅適用於同步實施。 如果您使用非同步實作標籤，此樣式應該空白或標籤為註解。

若要瞭解有關Platform Web SDK如何管理忽隱忽現情況的詳細資訊，請參閱指南區段： [管理個人化體驗的閃爍](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html).


## 設定資料串流

必須先在資料流設定中啟用Target，Platform Web SDK才能傳遞任何Target活動。

若要在資料流中設定Target：

1. 前往 [資料彙集](https://experience.adobe.com/#/data-collection){target="blank"} 介面
1. 在左側導覽中選取 **[!UICONTROL 資料串流]**
1. 選取先前建立的 `Luma Web SDK` 資料流

   ![選取Luma Web SDK資料流](assets/datastream-luma-web-sdk.png)

1. 選取 **[!UICONTROL 新增服務]**
   ![將服務新增至資料流](assets/target-datastream-addService.png)
1. 選取 **[!UICONTROL Adobe Target]** 作為 **[!UICONTROL 服務]**
1. 如有需要，請依照下列指引，輸入有關Target實作的選擇性詳細資料。
1. 選取 **[!UICONTROL 儲存]**

   ![目標資料流設定](assets/target-datastream.png)

### 屬性代號

Target Premium客戶可選擇使用屬性管理使用者許可權。 Target屬性可讓您建立使用者可執行Target活動的邊界。 請參閱 [企業許可權](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 區段以取得詳細資訊。

若要設定或尋找屬性代號，請導覽至 **Adobe Target** > **[!UICONTROL 管理]** > **[!UICONTROL 屬性]**. 此 `</>` 圖示會顯示實作程式碼。 此 `at_property` value是您要在資料流中使用的屬性Token。

![目標屬性Token](assets/target-admin-properties.png)

<a id="advanced-pto"></a>

每個資料流只能指定一個屬性代號，但屬性代號覆寫可讓您指定替代屬性代號，以取代資料流中定義的主要屬性代號。 的更新 `sendEvent` 覆寫資料流也需要動作。

![身分清單](assets/advanced-property-token.png)

### 目標環境ID

[環境](https://experienceleague.adobe.com/docs/target/using/administer/environments.html) 在Target中，可協助您在開發的所有階段管理實作。 此選擇性設定會指定您要與每個資料流搭配使用的Target環境。

Adobe建議針對您的每個開發、測試和生產資料流分別設定不同的目標環境ID，以保持事情簡單。 或者，您也可以在Target介面中使用 [主機](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 功能。

若要設定或尋找環境ID，請導覽至 **Adobe Target** > **[!UICONTROL 管理]** > **[!UICONTROL 環境]**.

![目標環境](assets/target-admin-environments.png)

>[!NOTE]
>
>若未指定目標環境ID，則會假設是生產目標環境。

### 目標第三方ID名稱空間

此選擇性設定可讓您指定用於Target第三方ID的身分符號。 Target僅支援在單一身分符號或名稱空間上同步設定檔。 如需詳細資訊，請參閱 [mbox3rdPartyId的即時設定檔同步](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) 一節。

身分符號位於下方的身分清單中 **資料彙集** > **[!UICONTROL 客戶]** > **[!UICONTROL 身分]**.

![身分清單](assets/target-identities.png)

出於本教學課程使用Luma網站的目的，請使用身分識別符號 `lumaCrmId` 在課程中設定關於 [身分](configure-identities.md).




## 呈現視覺個人化決定

首先，您應該瞭解Target和標籤介面中使用的術語。

* **活動**：一組鎖定至一或多個對象的體驗。 例如，簡單的A/B測試可能是具有兩個體驗的活動。
* **體驗**：一組以一或多個位置或決定範圍為目標的動作。
* **決定範圍**：傳送Target體驗的位置。 如果您熟悉使用舊版Target，則決定範圍等同於「mbox」。
* **個人化決策**：伺服器判斷應套用的動作。 這些決定可能會根據對象條件和Target活動優先順序。
* **主張**：伺服器所做決策的結果，會以Platform Web SDK回應傳送。 例如，交換橫幅影像會是一種主張。

### 更新頁面載入規則

如果在資料流中啟用了Target，Platform Web SDK則會傳送來自Target的視覺個人化決策。 不過， _它們不會自動呈現_. 您必須修改全域頁面載入規則，才能啟用自動轉譯。

1. 在 [資料彙集](https://experience.adobe.com/#/data-collection){target="blank"} 介面，開啟您用於本教學課程的標籤屬性
1. 開啟 `all pages - library load - AA & AT` 規則
1. 選取 `Adobe Experience Platform Web SDK - Send event` 動作
1. 啟用 **[!UICONTROL 呈現視覺個人化決定]** 勾選核取方塊

   ![啟用呈現視覺個人化決策](assets/target-rule-enable-visual-decisions.png)

1. 在**中[!UICONTROL 資料流設定覆寫**] 此 **[!UICONTROL 目標屬性Token]** 能以靜態值或資料元素覆寫。 僅屬性代號定義於 [**進階屬性代號覆寫**](#advanced-pto) 中的區段 **資料流設定** 將會傳回結果。

   ![覆寫屬性代號](assets/target-property-token-ovrrides.png)

1. 儲存您的變更，然後建置到您的程式庫

轉譯器視覺個人化決定設定可讓Platform Web SDK自動套用使用Target視覺化體驗撰寫器或「全域mbox」指定的任何修改。

>[!NOTE]
>
>通常 [!UICONTROL 呈現視覺個人化決定] 在每次完整頁面載入時，僅能啟用單一「傳送事件」動作的設定。 如果有多個「傳送事件」動作已啟用此設定，則會忽略後續轉譯請求。

如果您偏好使用自訂程式碼對這些決定自行呈現或執行動作，您可以將 [!UICONTROL 呈現視覺個人化決定] 設定已停用。 Platform Web SDK相當靈活，提供這項功能供您完全控制。 您可以參閱指南以瞭解更多關於 [手動呈現個人化內容](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html).


### 使用視覺化體驗撰寫器設定Target活動

現在基本實施部分已完成，請在Target中建立Experience Targeting (XT)活動，驗證一切都正常運作。 您可以參閱Target教學課程，瞭解 [建立體驗鎖定目標活動](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html) 如果您需要協助。

>[!NOTE]
>
>如果您使用Google Chrome作為瀏覽器， [視覺化體驗撰寫器(VEC) Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=en) 需要正確載入網站，才能在VEC中編輯。

1. 導覽至目標
1. 使用活動URL的Luma首頁建立體驗鎖定目標(XT)活動

   ![建立新的XT活動](assets/target-xt-create-activity.png)

1. 修改頁面，例如變更首頁主圖橫幅上的文字。  完成後，選取 **[!UICONTROL 儲存]** 則 **[!UICONTROL 下一個]**.

   ![Target VEC修改](assets/target-xt-vec-modification.png)

1. 更新事件名稱，然後選取 **[!UICONTROL 下一個]**.

   ![Target VEC更新事件](assets/target-xt-vec-updateevent.png)

1. 選擇Adobe Analytics作為報表來源，搭配適當的報表套裝，並選擇「訂單」量度作為目標

   ![目標VEC報表來源](assets/target-xt-vec-reportingsource.png)

   >[!NOTE]
   >
   >如果您沒有使用Adobe Analytics，請選取Target作為報表來源，然後選擇其他量度，例如 **參與度>頁面檢視** 而非。 必須有目標量度才能儲存及預覽活動。

1. 儲存活動
1. 如果您熟悉變更，那麼可以啟動活動。 否則，如果您想預覽體驗而不啟動，您可以複製 [QA預覽URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).
1. 載入Luma首頁，應該會看到變更已套用
1. 幾小時後，您應該就能在Adobe Analytics中檢視Target活動資料和轉換。 請參閱Target指南，瞭解更多關於 [Analytics for Target (A4T)報表](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/reporting.html?lang=en).



### 使用除錯工具進行驗證

如果您設定活動，應該會在頁面上看到您的內容已呈現。 不過，即使沒有活動上線，您也可以檢視「傳送事件」網路呼叫，以確認Target已正確設定。

>[!CAUTION]
>
>如果您使用Google Chrome，並擁有 [視覺化體驗撰寫器(VEC) Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=en) 已安裝，請確定 **插入Target資料庫** 設定已停用。 啟用此設定將會產生額外的Target請求。

1. 開啟Adobe Experience Platform Debugger瀏覽器擴充功能
1. 前往 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 並使用除錯工具 [將網站上的tag屬性切換為您自己的開發屬性](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 重新載入頁面
1. 選取 **[!UICONTROL 網路]** Debugger中的工具
1. 篩選依據 **[!UICONTROL Adobe Experience Platform Web SDK]**
1. 在事件列中選取第一次呼叫的值

   ![Adobe Experience Platform Debugger中的網路呼叫](assets/target-debugger-network.png)

1. 請注意，底下有索引鍵 `query` > `personalization` 和  `decisionScopes` 具有值 `__view__`. 此範圍等同於Target的「全域mbox」。 此Platform Web SDK呼叫要求Target做出決定。

   ![`__view__` decisionScope要求](assets/target-debugger-view-scope.png)

1. 關閉覆蓋圖並選取第二個網路呼叫的事件詳細資料。 只有在Target傳回活動時，此呼叫才會出現。
1. 請注意，有從Target傳回的活動和體驗的詳細資料。 此Platform Web SDK呼叫會傳送Target活動已轉譯給使用者的通知並增加曝光次數。

   ![Target活動印象](assets/target-debugger-activity-impression.png)

## 設定和演算自訂決定範圍

自訂決策範圍（先前稱為「mbox」）可用於透過Target表單式體驗撰寫器，以結構化的方式傳遞HTML或JSON內容。 Platform Web SDK不會自動轉譯傳遞到這些自訂範圍之一的內容。

### 新增範圍至頁面載入規則

修改您的頁面載入規則以新增自訂決定範圍：

1. 開啟 `all pages - library load - AA & AT` 規則
1. 選取 `Adobe Experience Platform Web SDK - Send Event` 動作
1. 新增一或多個要使用的範圍。 在此範例中，使用 `homepage-hero`.

   ![自訂範圍](assets/target-rule-custom-scope.png)

1. 儲存您的變更並將組建組建至程式庫

>[!TIP]
>
>在本教學課程中，您將使用單一手動定義的範圍來示範。 如果您決定使用專用於特定頁面的數個決定範圍，則應考慮使用資料元素，該元素會根據頁面路徑有條件地傳回範圍陣列。 此方法有助於讓您的實作簡單且可擴充。

### 處理來自Target的回應

現在您已設定Platform Web SDK來請求 `homepage-hero` 範圍，您必須對回應執行動作。 Platform Web SDK標籤擴充功能提供 [!UICONTROL 傳送事件完成] 事件，當回應來自時，立即觸發新規則 [!UICONTROL 傳送事件] 已收到動作。

1. 建立名為的規則 `homepage - send event complete - render homepage-hero`.
1. 將事件新增至規則。 使用 **Adobe Experience Platform Web SDK** 擴充功能與 **[!UICONTROL 傳送事件完成]** 事件型別。
1. 新增條件以將規則限制在Luma首頁(不含查詢字串的路徑等於 `/content/luma/us/en.html`)。
1. 將動作新增至規則。 使用 **Adobe Experience Platform Web SDK** 擴充功能和 **套用主張** 動作型別。

   ![呈現首頁主圖規則](assets/target-rule-render-hero.png)

   >[!TIP]
   >
   >為規則事件、條件和動作指定描述性名稱，而非使用預設名稱。 健全的規則元件名稱可讓搜尋結果更有用。

1. 輸入 `%event.propositions%` 放入主張欄位，因為我們正在使用「傳送事件完成」事件當作此規則的觸發器。
1. 在「主張中繼資料」區段中，選取 **[!UICONTROL 使用表單]**
1. 對於 **[!UICONTROL 範圍]** 欄位輸入 `homepage-hero`
1. 對於 **[!UICONTROL 選擇器]** 欄位輸入 `div.heroimage`
1. 的 **[!UICONTROL 動作型別]** 選取 **[!UICONTROL 設定HTML]**

   ![呈現首頁主圖動作](assets/target-action-render-hero.png)

1. 儲存您的變更並將組建組建至程式庫
1. 載入Luma首頁幾次，這應該足以製作新的 `homepage-hero` 決定範圍在Target介面中註冊。

### 使用表單式體驗撰寫器設定Target活動

現在您有了手動呈現自訂決定範圍的規則，可以在Target中建立另一個體驗鎖定目標(XT)活動。 這次請使用表單式體驗撰寫器。

1. 開啟 [Adobe Target](https://experience.adobe.com/target)
1. 停用上一個課程使用的活動
1. 使用表單式體驗撰寫器選項建立體驗鎖定目標(XT)活動

   ![建立新的XT活動](assets/target-xt-create-form-activity.png)

1. 選取 **`homepage-hero`** 位置(從位置下拉式清單和 **[!UICONTROL 建立HTML選件]** 從內容下拉式清單。 如果該位置無法使用，您可以鍵入該位置。 Target在收到該位置或範圍的請求後，會定期填入新的位置名稱。

   ![建立新的XT活動](assets/target-xt-form-activity.png)

1. 將下列程式碼貼到內容方塊中。 此程式碼為具有不同背景影像的基本主圖橫幅：

   ```html
   <div class="we-HeroImage jumbotron" style="background-image: url('/content/luma/us/en/women/_jcr_content/root/hero_image.coreimg.jpeg');">
      <div class="container cq-dd-image">
         <div class="we-HeroImage-wrapper">
            <p class="h3">New Luma Yoga Collection</p>
            <strong class="we-HeroImage-title h1">Be active with style&nbsp;</strong>
            <p>
               <a class="btn btn-primary btn-action" href="/content/luma/us/en/products.html" role="button">Shop Now</a>
            </p>
         </div>
      </div>
   </div>
   ```

1. 在 [!UICONTROL 目標與設定] 步驟，選擇Adobe Target作為報表來源，然後 [!UICONTROL 參與] > [!UICONTROL 頁面檢視] 作為目標
1. 儲存活動
1. 如果您熟悉變更，那麼可以啟動活動。 否則，如果您想預覽體驗而不啟動，您可以複製 [QA預覽URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).
1. 載入Luma首頁，應該會看到變更已套用

>[!NOTE]
>
>「已點按mbox」轉換目標無法自動運作。 由於Platform Web SDK不會自動轉譯自訂範圍，因此不會追蹤您選擇套用內容之位置的點按。 您可以使用「點選」為每個範圍建立自己的點選追蹤 `eventType` 與適用的 `_experience` 詳細資訊使用 `sendEvent` 動作。

### 使用除錯工具進行驗證

如果您啟動活動，應該會在頁面上看到您的內容轉譯。 不過，即使沒有已上線的活動，您也可以檢視 [!UICONTROL 傳送事件] 網路呼叫，確認Target正在為您的自訂範圍要求內容。

1. 開啟Adobe Experience Platform Debugger瀏覽器擴充功能
1. 前往 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 並使用除錯工具 [將網站上的tag屬性切換為您自己的開發屬性](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 重新載入頁面
1. 選取 **[!UICONTROL 網路]** Debugger中的工具
1. 篩選依據 **[!UICONTROL Adobe Experience Platform Web SDK]**
1. 在事件列中選取第一次呼叫的值

   ![Adobe Experience Platform Debugger中的網路呼叫](assets/target-debugger-network.png)

1. 請注意，底下有索引鍵 `query` > `personalization` 和  `decisionScopes` 具有值 `__view__` 就像之前一樣，但現在也有一個 `homepage-hero` 已包含範圍。 此Platform Web SDK呼叫要求Target針對使用VEC和特定 `homepage-hero` 位置。

   ![`__view__` decisionScope要求](assets/target-debugger-view-scope.png)

1. 關閉覆蓋圖並選取第二個網路呼叫的事件詳細資料。 只有在Target傳回活動時，此呼叫才會出現。
1. 請注意，有從Target傳回的活動和體驗的詳細資料。 此Platform Web SDK呼叫會傳送Target活動已轉譯給使用者的通知並增加曝光次數。

   ![Target活動印象](assets/target-debugger-activity-impression.png)

## 傳遞其他資料至Target

在本節中，您將傳遞Target特定資料，並深入瞭解XDM資料對應至Target引數的方式。

有些資料點未從XDM物件對應，可能對Target有用。 這些特殊的Target引數包括：

* [設定檔屬性](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/methods/in-page-profile-attributes.html?lang=en)
* [Recommendations實體屬性](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en)
* [Recommendations保留的引數](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html?lang=en#pass-behavioral)
* 的類別值 [類別親和性](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html?lang=en)

### 建立Target引數的資料元素

首先，您需要為設定檔屬性、實體屬性、類別值設定一些額外的資料元素，然後建構 `data` 用來傳遞非XDM資料的物件：

* **`target.entity.id`** 已對應至 `digitalData.product.0.productInfo.sku`
* **`target.entity.name`** 已對應至 `digitalData.product.0.productInfo.title`
* **`target.user.categoryId`** 使用下列自訂程式碼來剖析最上層類別的網站URL：

  ```javascript
  var cat = location.pathname.split(/[/.]+/);
  if (cat[5] == 'products') {
     return (cat[6]);
  } else if (cat[5] != 'html') { 
     return (cat[5]);
  }
  ```

* **`data.content`** 使用下列自訂程式碼：

  ```javascript
  var data = {
     __adobe: {
        target: {
           "entity.id": _satellite.getVar("target.entity.id"),
           "entity.name": _satellite.getVar("target.entity.name"),
           "profile.loggedIn": _satellite.getVar("user.profile.attributes.loggedIn"),
           "user.categoryId": _satellite.getVar("target.user.categoryId")
        }
     }
  }
  return data;
  ```

### 更新頁面載入規則

在XDM物件之外傳遞Target的其他資料需要更新任何適用的規則。 在此範例中，您唯一必須做的修改就是加入新的 **data.content** 資料元素至一般頁面載入規則和產品頁面檢視規則。

1. 開啟 `all pages - library load - AA & AT` 規則
1. 選取 `Adobe Experience Platform Web SDK - Send event` 動作
1. 新增 `data.content` 資料元素至資料欄位

   ![新增Target資料至規則](assets/target-rule-data.png)

1. 儲存您的變更並將組建組建至程式庫
1. 針對「 」重複步驟1到4 **產品檢視 — 程式庫載入 — AA** 規則

>[!NOTE]
>
>上述範例使用 `data` 未在所有頁面型別中完全填入的物件。 標籤會適當地處理這種情況，並省略具有未定義值的索引鍵。 例如， `entity.id` 和 `entity.name` 除了產品詳細資料外，不會在任何頁面上傳遞。


## 分割個人化決定和Analytics集合事件

Luma網站上的資料層完全定義在標籤內嵌程式碼之前。 這可讓我們使用單一呼叫，來擷取個人化內容(例如從Adobe Target)並傳送分析資料(例如傳送到Adobe Analytics)。 在許多網站上，資料層的載入時間不夠早或速度不夠快，無法搭配個人化應用程式使用。 在這些情況下，您可以製作兩個 `sendEvent` 會在單一頁面載入時呼叫，並使用第一個進行個人化，並使用第二個進行分析。 以此方式分解事件規則，可讓Target決策事件儘早引發。 Analytics事件可以等到資料層物件填入之後。 這類似於Web SDK之前的實作，Adobe Target會在其中 `target-global-mbox` 在頁面頂端，Adobe Analytics會引發 `s.t()` 呼叫頁面底部的


1. 建立名為的規則 `all pages - page top - request decisions`
1. 將事件新增至規則。 使用 **核心** 擴充功能與 **[!UICONTROL 程式庫已載入（頁面頂端）]** 事件型別
1. 將動作新增至規則。 使用 **Adobe Experience Platform Web SDK** 擴充功能和 **傳送事件** 動作型別
1. 選取 **[!UICONTROL 使用引導式事件]** 然後選取 **[!UICONTROL 要求個人化]**
1. 這樣會鎖定 **型別** 作為 **[!UICONTROL 決策主張擷取]**

   ![send_decision_request_alone](assets/target-decision-request.png)

1. 建立您的 `Adobe Analytics Send Event rule` 使用 **引導式事件樣式** 區段選取 **[!UICONTROL 頁面底部事件 — 收集分析]** 選項按鈕
1. 這樣會鎖定 **[!UICONTROL 包含擱置的顯示通知]** 核取方塊已選取，以便傳送決策請求中的佇列顯示通知。

![send_decision_request_alone](assets/target-aa-request-guided.png)

>[!TIP]
>
>如果您擷取決策主張的事件之後沒有Adobe Analytics事件，請使用 **引導式事件樣式** **[!UICONTROL 未引導 — 顯示所有欄位]**. 您必須手動選取所有選項，但系統會將選項解除鎖定 **[!UICONTROL 自動傳送顯示通知]** 以及擷取要求。


### 使用除錯工具進行驗證

現在規則已更新，您可以使用Adobe Debugger驗證資料是否正確傳遞。

1. 導覽至 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 並使用電子郵件登入 `test@adobe.com` 和密碼 `test`
1. 導覽至產品詳細資料頁面
1. 開啟Adobe Experience Platform Debugger瀏覽器擴充功能，並 [將tag屬性切換為您自己的開發屬性](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 重新載入頁面
1. 選取 **網路** Debugger中的工具並篩選依據 **Adobe Experience Platform Web SDK**
1. 在事件列中選取第一次呼叫的值
1. 請注意，底下有索引鍵 `data` > `__adobe` > `target` 其中會填入產品、類別和登入狀態的相關資訊。

   ![`__view__` decisionScope要求](assets/target-debugger-data.png)

### 在Target介面中驗證

接下來，檢視Target介面，確認已收到資料，且資料可用於對象和活動。 XDM資料會自動對應至自訂Target引數。 您可以驗證Target已收到XDM資料，並且可以透過建立受眾來使用。

1. 開啟 [Adobe Target](https://experience.adobe.com/target)
1. 導覽至 **[!UICONTROL 受眾]** 區段
1. 建立受眾並選擇 **[!UICONTROL 自訂]** 屬性型別
1. 搜尋 **[!UICONTROL 引數]** 欄位 `web`. 下拉式功能表應該會填入與網頁詳細資料相關的所有XDM欄位。

   ![在Target自訂屬性中驗證](assets/validate-in-target-customattribute.png)

接下來，驗證已成功傳遞登入狀態設定檔屬性。

1. 選擇 **[!UICONTROL 訪客資料]** 屬性型別
2. 搜尋 `loggedIn`. 如果下拉式選單中有屬性，表示該屬性已正確傳遞至Target。 新屬性可能需要幾分鐘的時間才能在Target UI中使用。

   ![在Target設定檔中驗證](assets/validate-in-target-profile.png)

如果您有Target Premium，也可以驗證實體資料是否正確傳遞，以及產品資料是否已寫入Recommendations產品目錄。

1. 導覽至 **[!UICONTROL Recommendations]** 區段
1. 選取 **[!UICONTROL 目錄搜尋]** 在左側導覽列中
1. 搜尋您先前在Luma網站上造訪的產品SKU或產品名稱。 產品應顯示在產品目錄中。 新產品可能需要幾分鐘的時間才能在Recommendations產品目錄中搜尋。

   ![在Target目錄搜尋中驗證](assets/validate-in-target-catalogsearch.png)

### 使用保證進行驗證

此外，您可以視情況使用「保證」，確認Target決策請求取得正確的資料，且任何伺服器端轉換皆正確發生。 您也可以確認Adobe Analytics呼叫中包含促銷活動和體驗資訊，即使Target決策和Adobe Analytics呼叫已分別傳送亦然。

1. 開啟 [保證](https://experience.adobe.com/assurance)
1. 啟動新的保證工作，輸入 **[!UICONTROL 工作階段名稱]** 並輸入 **[!UICONTROL 基礎url]** 針對您的網站或您正在測試的任何其他頁面
1. 按一下 **[!UICONTROL 下一個]**

   ![在保證新工作階段中進行驗證](assets/validate-in-assurance-newsession.png)

1. 選取您的連線方法，在此案例中，我們將使用 **[!UICONTROL 複製連結]**
1. 複製連結並貼到新的瀏覽器標籤中
1. 按一下 **[!UICONTROL 完成]**

   ![透過複製連結驗證保證連線](assets/validate-in-assurance-copylink.png)

1. 您的保證工作階段啟動後，您會看到事件標籤中填入的事件
1. 依「tnta」篩選
1. 選取最近的呼叫並展開訊息，以確定其是否正確填入並記下「tnta」值

   ![在保證目標點選中進行驗證](assets/validate-in-assurance-targetevent.png)

1. 接著，保留「tnta」篩選，並選取analytics.mapping事件（在我們剛才檢視的目標事件之後發生）。
1. 檢查「context.mappedQueryParams」。\&lt;yourschemaname>「值」以確認其包含「tnta」屬性，該屬性具有符合在先前目標事件中找到的相符串連字串。

   ![在Assurance Analytics點選中驗證](assets/validate-in-assurance-analyticsevent.png)

這可確認，當我們在頁面上稍後觸發分析追蹤呼叫時，已佇列以供稍後傳輸的A4T資訊已正確傳送。

現在您已完成本課程，應該就能使用Platform Web SDK有效實作Adobe Target。

[下一步： ](setup-consent.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
