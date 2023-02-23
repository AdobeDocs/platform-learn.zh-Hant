---
title: 使用Platform Web SDK設定Adobe Target
description: 了解如何使用Platform Web SDK實作Adobe Target。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
solution: Data Collection, Target
exl-id: 9084f572-5fec-4a26-8906-6d6dd1106d36
source-git-commit: 13f2c87d7c4cfe21f04a945b9e11dc64e9bf6e0c
workflow-type: tm+mt
source-wordcount: '3801'
ht-degree: 1%

---

# 使用Platform Web SDK設定Adobe Target

了解如何使用Platform Web SDK實作Adobe Target。 了解如何傳遞體驗，以及如何將其他參數傳遞至Target。

[Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html) 是Adobe Experience Cloud應用程式，提供一切所需工具，讓您量身訂造及個人化您的客戶體驗，借此為您的網頁以及行動網站、應用程式和其他數位頻道創造最高的收入。


## 學習目標

在本課程結束時，您將能夠：

* 了解如何新增Platform Web SDK預先隱藏程式碼片段，以防止將Target與非同步標籤內嵌程式碼搭配使用時忽隱忽現
* 設定資料流以啟用Target功能
* 在頁面載入時呈現視覺個人化決策（先前稱為「全域mbox」）
* 將XDM資料傳遞至Target並了解與Target參數的對應
* 將自訂資料傳遞至Target，例如設定檔和實體參數
* 使用Platform Web SDK驗證Target實作

>[!TIP]
>
>查看我們的 [將Target從at.js 2.x移轉至Platform Web SDK](/help/tutorial-migrate-target-websdk/introduction.md) 移轉現有at.js實作的逐步指南教學課程。


## 先決條件

若要完成本節中的課程，您必須先：

* 完成Platform Web SDK初始設定的所有課程，包括設定資料元素和規則。
* 確定您有 [編輯者或核准者角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80).
* 安裝 [可視化體驗撰寫器Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 如果您使用Google Chrome瀏覽器。
* 了解如何在Target中設定活動。 如果您需要重新整理，下列教學課程和指南將有助於本課程：
   * [使用可視化體驗撰寫器(VEC)Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html)
   * [使用 Visual Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [使用表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [建立體驗鎖定目標活動](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

## 新增忽隱忽現緩解

開始之前，請根據標籤程式庫的載入方式，判斷是否需要額外的忽隱忽現處理解決方案。

>[!NOTE]
>
>本教學課程使用 [Luma網站](https://luma.enablementadobe.com/content/luma/us/en.html) 已採用非同步實作標籤和忽隱忽現緩解。 本節供參考，以了解忽隱忽現緩解與Platform Web SDK搭配使用的方式。


### 非同步實作

非同步載入標籤程式庫時，Target執行內容交換之前，頁面可能會完成轉譯。 此行為可能會導致所謂的「閃爍」問題，發生此問題時，會先短暫地顯示預設內容，然後再更換為Target指定的個人化內容。 若要避免發生這種閃爍問題，Adobe建議在非同步標籤內嵌程式碼之前，立即新增特殊的預先隱藏程式碼片段。

此程式碼片段已存在於Luma網站上，但讓我們進一步了解此程式碼的功能：

```html
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
</script>
```

預先隱藏的程式碼片段會在含有您選擇之CSS定義的頁面標題中建立樣式標籤。 收到來自Target的回應或逾時時，就會移除此樣式標籤。

預先隱藏行為是由程式碼片段尾端的兩個設定所控制。

* `body { opacity: 0 !important }` 指定在Target載入前，要用於預先隱藏的CSS定義。 依預設，會隱藏整個頁面。 您可以將此定義更新為要預先隱藏的選取器，以及要如何隱藏選取器。 您可以包含多個定義，因為此值只是插入預先隱藏樣式標籤中的值。 如果您有可輕鬆識別的容器元素將內容包裝在導覽下，則可以使用此設定將預先隱藏限制為該容器元素。
* `3000` 指定預先隱藏的逾時（毫秒）。 如果在逾時前未收到來自Target的回應，則會移除預先隱藏的樣式標籤。 達到此逾時的情況應少之又少。

>[!NOTE]
>
>Platform Web SDK的預先隱藏程式碼片段與Target at.js資料庫使用的程式碼片段稍有不同。 請務必為Platform Web SDK使用正確的程式碼片段，因為它使用的樣式ID不同 `alloy-prehiding`. 如果使用at.js的預先隱藏程式碼片段，該程式碼片段可能無法正常運作。

預先隱藏程式碼片段也可在標籤中使用：

1. 前往 **[!UICONTROL 擴充功能]** 標籤區段
1. 選擇 **[!UICONTROL 設定]** Adobe Experience Platform Web SDK擴充功能的
1. 選取 **[!UICONTROL 將預先隱藏的程式碼片段複製到剪貼簿]** 按鈕

   ![非同步實作的Target預先隱藏程式碼片段](assets/target-flicker-async.png)

   >[!NOTE]
   >
   >從Platform Web SDK擴充功能複製的預設預先隱藏程式碼片段，可能包含您網站上不存在的CSS定義，例如 `.personalization-container { opacity: 0 !important }`. 請務必檢查並適當修改網站的預先隱藏程式碼片段。

### 同步實作

Adobe建議非同步實作標籤，如Luma網站上所示。 不過，如果同步載入標籤程式庫，則不需要預先隱藏程式碼片段。 而是會在Platform Web SDK擴充功能設定中指定預先隱藏樣式。

同步實施的預先隱藏樣式可依下列方式設定：

1. 前往 **[!UICONTROL 擴充功能]** 標籤區段
1. 選取 **[!UICONTROL 設定]** Platform Web SDK擴充功能的按鈕
1. 選取 **[!UICONTROL 編輯預先隱藏樣式]** 按鈕

   ![非同步實作的Target預先隱藏程式碼片段](assets/target-flicker-sync.png)

1. 修改CSS以包含您要使用的選取器和隱藏方法，例如： `body { opacity: 0 !important }` 若您想要預先隱藏頁面的整個內文。
1. 儲存變更並建置至程式庫

>[!NOTE]
>
>預先隱藏樣式設定僅用於同步實施。 如果您使用非同步的標籤實作，此樣式應空白或留言。

若要進一步了解Platform Web SDK如何管理忽隱忽現的情形，請參閱指南區段： [管理個人化體驗的忽隱忽現情形](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html).


## 設定資料流

必須先在資料流設定中啟用Target,Platform Web SDK才能傳送任何Target活動。

若要在資料流中設定Target:

1. 前往 [資料收集](https://experience.adobe.com/#/data-collection){target="blank"} 介面
1. 在左側導覽列中，選取 **[!UICONTROL 資料流]**
1. 選取先前建立的 `Luma Web SDK` 資料流

   ![選取Luma Web SDK資料流](assets/datastream-luma-web-sdk.png)

1. 選擇 **[!UICONTROL 添加服務]**

   ![新增服務至資料流](assets/target-datastream-addService.png)
1. 選擇 **[!UICONTROL Adobe Target]** 作為 **[!UICONTROL 服務]**
1. 視需要，依照下列指引輸入Target實作的選用詳細資訊。
1. 選擇 **[!UICONTROL 儲存]**

   ![目標資料流配置](assets/target-datastream.png)

### 屬性代號

Target Premium客戶可以選擇使用屬性管理使用者權限。 Target屬性可讓您建立使用者可執行Target活動的位置界限。 請參閱 [企業權限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) Target檔案的一節以取得詳細資訊。

若要設定或尋找屬性代號，請導覽至 **Adobe Target** > **[!UICONTROL 管理]** > **[!UICONTROL 屬性]**. 此 `</>` 圖示會顯示實作代碼。 此 `at_property` value是您要在資料流中使用的屬性代號。

![Target屬性代號](assets/target-admin-properties.png)

>[!NOTE]
>
>每個資料流只能指定一個屬性代號。


### 目標環境ID

[環境](https://experienceleague.adobe.com/docs/target/using/administer/environments.html) 在Target中，可協助您管理所有開發階段的實作。 此選用設定會指定您要與每個資料流搭配使用的Target環境。

Adobe建議針對每個開發、測試和生產資料流以不同方式設定Target環境ID，以簡化操作。

若要設定或尋找環境ID，請導覽至 **Adobe Target** > **[!UICONTROL 管理]** > **[!UICONTROL 環境]**.

![目標環境](assets/target-admin-environments.png)

>[!NOTE]
>
>若未指定Target環境ID，則會假設為生產Target環境。

### Target第三方ID命名空間

此選用設定可讓您指定要用於Target第三方ID的身分符號。 Target僅支援在單一身分符號或命名空間上進行設定檔同步。 如需詳細資訊，請參閱 [mbox3rdPartyId的即時設定檔同步](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) 部分。

身分符號位於 **資料收集** > **[!UICONTROL 客戶]** > **[!UICONTROL 身分]**.

![身分清單](assets/target-identities.png)

在使用Luma網站的本教學課程中，請使用身分符號 `lumaCrmId` 在課程中設定關於 [身分](configure-identities.md).


## 轉譯視覺個人化決策

首先，您應了解Target和標籤介面中使用的術語。

* **活動**:鎖定在一或多個對象的一組體驗。 例如，簡單的A/B測試可能是具有兩個體驗的活動。
* **體驗**:一組以一個或多個位置或決策範圍為目標的操作。
* **決策範圍**:Target體驗傳送的位置。 如果您熟悉使用舊版Target，決策範圍等同於「mbox」。
* **個人化決策**:應應用伺服器確定的操作。 這些決定可能是根據對象條件和Target活動優先順序。
* **主張**:伺服器在Platform Web SDK回應中傳送的決策結果。 例如，交換橫幅影像是個建議。

### 更新頁面載入規則

如果資料流中已啟用Target，則Target的視覺個人化決策會由Platform Web SDK傳送。 不過， _不會自動呈現_. 您必須修改全域頁面載入規則，才能啟用自動呈現。

1. 在 [資料收集](https://experience.adobe.com/#/data-collection){target="blank"} 介面，開啟您用於本教學課程的標籤屬性
1. 開啟 `all pages - library load - AA & AT` 規則
1. 選取 `Adobe Experience Platform Web SDK - Send event` 動作
1. 啟用 **[!UICONTROL 轉譯視覺個人化決策]** 複選框

   ![啟用呈現視覺化個人化決策](assets/target-rule-enable-visual-decisions.png)

1. 儲存變更並建置至程式庫

呈現視覺化個人化決策設定可讓Platform Web SDK自動套用使用Target可視化體驗撰寫器或「全域mbox」指定的任何修改。

>[!NOTE]
>
>通常， [!UICONTROL 轉譯視覺個人化決策] 設定只應針對每個完整頁面載入的單一「傳送事件」動作啟用。 如果多個「傳送事件」動作已啟用此設定，則會忽略後續的轉譯請求。

如果您偏好自行使用自訂程式碼來呈現或處理這些決策，可將 [!UICONTROL 轉譯視覺個人化決策] 設定已停用。 Platform Web SDK具有彈性，可提供此功能，讓您完全控制。 如需詳細資訊，請參閱指南 [手動轉譯個人化內容](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html).

### 使用可視化體驗撰寫器設定Target活動

現在基本實作部分已完成，請在Target中建立體驗鎖定目標(XT)活動，以驗證一切都正常運作。 如需相關資訊，請參閱Target教學課程 [建立體驗鎖定目標活動](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html) 如果你需要幫助。

>[!NOTE]
>
>如果您使用Google Chrome作為瀏覽器，則 [可視化體驗撰寫器(VEC)Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=en) 必須正確載入網站才能在VEC中編輯。

1. 導覽至Target
1. 使用活動URL的Luma首頁，建立體驗鎖定目標(XT)活動

   ![建立新XT活動](assets/target-xt-create-activity.png)

1. 修改頁面，例如變更首頁橫幅上的文字

   ![Target VEC修改](assets/target-xt-vec-modification.png)

1. 選擇Adobe Analytics作為報表來源，並以適當的報表套裝和訂單量度為目標

   >[!NOTE]
   >
   >如果您未使用Adobe Analytics，請選取Target作為報表來源，並選擇其他量度，例如 **參與>頁面檢視** 。 儲存和預覽活動需要目標量度。

1. 儲存活動
1. 如果您熟悉變更，則可啟動活動。 否則，如果您想要預覽體驗而不要啟動，可以複製 [QA預覽URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).
1. 載入Luma首頁，您應該會看到已套用變更
1. 幾小時後，您應該就能在Adobe Analytics中看到Target活動資料和轉換。 請參閱Target指南，了解 [Analytics for Target(A4T)報表](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/reporting.html?lang=en).



### 使用Debugger進行驗證

如果您設定活動，應該會在頁面上看到您的內容呈現。 不過，即使沒有任何活動上線，您也可以查看傳送事件網路呼叫，確認Target已正確設定。

>[!CAUTION]
>
>如果您使用Google Chrome，且 [可視化體驗撰寫器(VEC)Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=en) 已安裝，請確定 **插入Target資料庫** 設定已停用。 啟用此設定將會產生額外的Target請求。

1. 開啟Adobe Experience Platform Debugger瀏覽器擴充功能
1. 前往 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 並使用偵錯工具 [將網站上的標籤屬性切換至您自己的開發屬性](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 重新載入頁面
1. 選取 **[!UICONTROL 網路]** 工具
1. 篩選依據 **[!UICONTROL Adobe Experience Platform Web SDK]**
1. 選取第一次呼叫的事件列中的值

   ![Adobe Experience Platform偵錯工具中的網路呼叫](assets/target-debugger-network.png)

1. 請注意，下面有鍵 `query` > `personalization` 和  `decisionScopes` 的值為 `__view__`. 此範圍等同於Target的「全域mbox」。 此平台Web SDK呼叫已請求Target做出決策。

   ![__檢視__ decisionScope請求](assets/target-debugger-view-scope.png)

1. 關閉覆蓋並選取第二個網路呼叫的事件詳細資料。 只有在Target傳回活動時，才會出現此呼叫。
1. 請注意，有關從Target傳回的活動和體驗的詳細資料。 此Platform Web SDK呼叫會傳送通知，告知使用者已呈現Target活動，並增加曝光次數。

   ![Target活動曝光數](assets/target-debugger-activity-impression.png)

## 設定並呈現自訂決策範圍

自訂決策範圍（舊稱「mbox」）可使用Target表單式體驗撰寫器，以結構化方式傳送HTML或JSON內容。 傳送至其中一個自訂範圍的內容不會由Platform Web SDK自動轉譯。

### 將範圍新增至頁面載入規則

修改頁面載入規則以新增自訂決策範圍：

1. 開啟 `all pages - library load - AA & AT` 規則
1. 選取 `Adobe Experience Platform Web SDK - Send Event` 動作
1. 添加一個或多個要使用的範圍。 在此範例中，請使用 `homepage-hero`.

   ![自訂範圍](assets/target-rule-custom-scope.png)

1. 儲存變更並建置至程式庫

>[!TIP]
>
>在本教學課程中，您將使用單一手動定義的範圍來進行示範。 如果您決定使用多個特定頁面專用的決策範圍，則應考慮使用資料元素，該元素會根據頁面路徑有條件地傳回範圍陣列。 此方法可協助您維持簡單且可擴充的實施。

### 處理來自Target的回應

現在您已設定Platform Web SDK來請求 `homepage-hero` 範圍，您必須對回應執行動作。 Platform Web SDK標籤擴充功能提供 [!UICONTROL 傳送事件完成] 事件，可在 [!UICONTROL 傳送事件] 已接收動作。

1. 建立規則，稱為 `homepage - send event complete - render homepage-hero`.
1. 新增事件至規則。 使用 **Adobe Experience Platform Web SDK** 擴充功能和 **[!UICONTROL 傳送事件完成]** 事件類型。
1. 新增條件以限制規則至Luma首頁(沒有查詢字串的路徑等於 `/content/luma/us/en.html`)。
1. 新增動作至規則。 使用 **核心** 擴充功能與 **自訂程式碼** 動作類型。

   ![呈現首頁主圖規則](assets/target-rule-render-hero.png)

   >[!TIP]
   >
   >為規則事件、條件和動作提供描述性名稱，而非使用預設名稱。 強大的規則元件名稱可讓搜尋結果更實用。

1. 輸入要讀取的自定義代碼，並對從Platform Web SDK響應返回的主張執行操作。 此範例中的自訂程式碼使用指南中概述的方法， [手動轉譯個人化內容](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#manually-rendering-content). 程式碼已針對 `homepage-hero` 使用標籤規則動作的範例範圍。

   ```javascript
   var propositions = event.propositions;
   
   var heroProposition;
   if (propositions) {
      // Find the hero proposition, if it exists.
      for (var i = 0; i < propositions.length; i++) {
         var proposition = propositions[i];
         if (proposition.scope === "homepage-hero") {
            heroProposition = proposition;
            break;
         }
      }
   }
   
   var heroHtml;
   if (heroProposition) {
      // Find the item from proposition that should be rendered.
      // Rather than assuming there a single item that has HTML
      // content, find the first item whose schema indicates
      // it contains HTML content.
      for (var j = 0; j < heroProposition.items.length; j++) {
         var heroPropositionItem = heroProposition.items[j];
         if (heroPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
            heroHtml = heroPropositionItem.data.content;
            break;
         }
      }
   }
   
   if (heroHtml) {
      // Hero HTML exists. Time to render it.
      var heroElement = document.querySelector(".heroimage");
      heroElement.innerHTML = heroHtml;
      // For this example, we assume there is only a signle place to update in the HTML.
   }
   
   // Send a "display" event 
   alloy("sendEvent", {
      xdm: {
         eventType: "propositionDisplay",
         _experience: {
            decisioning: {
               propositions: [
                  {
                     id: heroProposition.id,
                     scope: heroProposition.scope,
                     scopeDetails: heroProposition.scopeDetails
                  }
               ]
            }
         }
      }
   });
   ```

1. 儲存變更並建置至程式庫
1. 載入Luma首頁幾次，這應該足以建立新的 `homepage-hero` 目標介面中的決策範圍註冊器。

### 使用表單式體驗撰寫器設定Target活動

現在您有可手動轉譯自訂決策範圍的規則，可以在Target中建立其他體驗鎖定目標(XT)活動。 這次使用表單式體驗撰寫器。

1. 開啟 [Adobe Target](https://experience.adobe.com/target)
1. 停用用於上一課的活動
1. 使用表單式體驗撰寫器選項建立體驗鎖定目標(XT)活動

   ![建立新XT活動](assets/target-xt-create-form-activity.png)

1. 選取 **`homepage-hero`** 位置下拉式清單中的位置，以及 **[!UICONTROL 建立HTML選件]** 從「內容」下拉式清單中。 如果位置不可用，您可以在中輸入。 Target在收到該位置或範圍的請求後，會定期填入新的位置名稱。

   ![建立新XT活動](assets/target-xt-form-activity.png)

1. 將下列程式碼貼到內容方塊中。 此程式碼是具有不同背景影像的基本主圖橫幅：

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

1. 在 [!UICONTROL 目標與設定] 步驟，選擇Adobe Target作為報表來源，並 [!UICONTROL 參與] > [!UICONTROL 頁面檢視] 作為目標
1. 儲存活動
1. 如果您熟悉變更，則可啟動活動。 否則，如果您想要預覽體驗而不要啟動，可以複製 [QA預覽URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).
1. 載入Luma首頁，您應該會看到已套用變更

>[!NOTE]
>
>「點擊mbox」轉換目標無法自動運作。 由於Platform Web SDK不會自動呈現自訂範圍，因此不會追蹤您選擇套用內容之位置的點按次數。 您可以使用「點擊」，為每個範圍建立自己的點擊追蹤 `eventType` 適用 `_experience` 詳細資訊，使用 `sendEvent` 動作。

### 使用Debugger進行驗證

如果您已啟動活動，應該會在頁面上看到您的內容呈現。 不過，即使沒有任何已上線的活動，您也可以查看 [!UICONTROL 傳送事件] 網路呼叫，確認Target正在請求自訂範圍的內容。

1. 開啟Adobe Experience Platform Debugger瀏覽器擴充功能
1. 前往 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 並使用偵錯工具 [將網站上的標籤屬性切換至您自己的開發屬性](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 重新載入頁面
1. 選取 **[!UICONTROL 網路]** 工具
1. 篩選依據 **[!UICONTROL Adobe Experience Platform Web SDK]**
1. 選取第一次呼叫的事件列中的值

   ![Adobe Experience Platform偵錯工具中的網路呼叫](assets/target-debugger-network.png)

1. 請注意，下面有鍵 `query` > `personalization` 和  `decisionScopes` 的值為 `__view__` 和以前一樣，但現在 `homepage-hero` 範圍。 此Platform Web SDK呼叫要求Target針對使用VEC和特定 `homepage-hero` 位置。

   ![__檢視__ decisionScope請求](assets/target-debugger-view-scope.png)

1. 關閉覆蓋並選取第二個網路呼叫的事件詳細資料。 只有在Target傳回活動時，才會出現此呼叫。
1. 請注意，有關從Target傳回的活動和體驗的詳細資料。 此Platform Web SDK呼叫會傳送通知，告知使用者已呈現Target活動，並增加曝光次數。

   ![Target活動曝光數](assets/target-debugger-activity-impression.png)

## 將其他資料傳遞至Target

在本節中，您將傳遞Target專用資料，並進一步了解XDM資料與Target參數的對應方式。

有些資料點可能對Target有用，但並未從XDM物件對應。 這些特殊Target參數包括：

* [設定檔屬性](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/methods/in-page-profile-attributes.html?lang=en)
* [Recommendations實體屬性](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en)
* [Recommendations保留參數](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html?lang=en#pass-behavioral)
* 類別值 [類別親和性](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html?lang=en)

### 為Target參數建立資料元素

首先，您需為設定檔屬性、實體屬性、類別值設定一些額外的資料元素，然後建構 `data` 用於傳遞非XDM資料的物件：

* **`target.entity.id`** 已對應至 `digitalData.product.0.productInfo.sku`
* **`target.entity.name`** 已對應至 `digitalData.product.0.productInfo.title`
* **`target.user.categoryId`** 使用下列自訂程式碼來剖析頂層類別的網站URL:

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

在XDM物件外部傳遞Target的其他資料時，需要更新任何適用的規則。 在此範例中，您唯一必須進行的修改是包含新的 **data.content** 一般頁面載入規則和產品頁面檢視規則的資料元素。

1. 開啟 `all pages - library load - AA & AT` 規則
1. 選取 `Adobe Experience Platform Web SDK - Send event` 動作
1. 新增 `data.content` 資料元素至「資料」欄位

   ![將Target資料新增至規則](assets/target-rule-data.png)

1. 儲存變更並建置至程式庫
1. 對 **產品檢視 — 程式庫載入 — AA** 規則

>[!NOTE]
>
>上述範例使用 `data` 未在所有頁面類型上完全填入的物件。 標籤可適當處理此情況，並省略具有未定義值的鍵值。 例如， `entity.id` 和 `entity.name` 不會在產品詳細資訊以外的任何頁面上傳遞。

### 使用除錯工具進行驗證

規則更新後，您就可以使用Adobe偵錯工具來驗證資料是否正確傳遞。

1. 導覽至 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 並透過電子郵件登入 `test@adobe.com` 和密碼 `test`
1. 導覽至產品詳細資訊頁面
1. 開啟Adobe Experience Platform Debugger瀏覽器擴充功能，然後 [將標籤屬性切換至您自己的開發屬性](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 重新載入頁面
1. 選取 **網路** 工具，並依 **Adobe Experience Platform Web SDK**
1. 選取第一次呼叫的事件列中的值
1. 請注意，下面有鍵 `data` > `__adobe` > `target` 而且會填入產品、類別和登入狀態的相關資訊。

   ![__檢視__ decisionScope請求](assets/target-debugger-data.png)

### 在Target介面中驗證

接下來，查看Target介面，確認已收到資料，且可供對象和活動使用。 XDM資料會自動對應至自訂Target參數。 您可以建立對象，以驗證Target是否收到XDM資料。

1. 開啟 [Adobe Target](https://experience.adobe.com/target)
1. 導覽至 **[!UICONTROL 對象]** 節
1. 建立對象並選擇 **[!UICONTROL 自訂]** 屬性類型
1. 搜尋 **[!UICONTROL 參數]** 欄位 `web`. 下拉式功能表應會填入與網頁詳細資料相關的所有XDM欄位。

接下來，驗證登錄狀態配置檔案屬性是否已成功傳遞。

1. 選擇 **[!UICONTROL 訪客資料]** 屬性類型
1. 搜尋 `loggedIn`. 如果屬性可在下拉式功能表中使用，則屬性已正確傳遞至Target。 Target UI中可能需要數分鐘才能提供新屬性。

如果您有Target Premium，您也可以驗證實體資料已正確傳遞，且產品資料已寫入Recommendations產品目錄。

1. 導覽至 **[!UICONTROL Recommendations]** 節
1. 選擇 **[!UICONTROL 目錄搜尋]** 在左側導覽中
1. 搜尋您先前在Luma網站上造訪的產品SKU或產品名稱。 產品應顯示在產品目錄中。 新產品可能需要數分鐘時間才能在Recommendations產品目錄中搜尋。

完成本課程後，您應該已使用Platform Web SDK開始實作Adobe Target。

[下一個： ](setup-consent.md)

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
