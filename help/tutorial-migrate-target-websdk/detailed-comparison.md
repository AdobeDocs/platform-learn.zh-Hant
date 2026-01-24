---
title: at.js 2.x與Web SDK的比較 — 將Target從at.js 2.x移轉至Web SDK
description: 瞭解at.js 2.x與Platform Web SDK之間的差異，包括功能、功能、設定和資料流程。
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: 7d3c1728925e322f9313cf71f081500e0c0bac0b
workflow-type: tm+mt
source-wordcount: '2018'
ht-degree: 1%

---

# at.js與Platform Web SDK比較

獨立Adobe Target at.js程式庫與Platform Web SDK有顯著的差異。 下表為參考資料，可協助您評估在移轉程式期間可能需要著重的實作領域。

檢閱下列資訊並評估您目前的技術at.js實作後，您應該能夠瞭解下列內容：

- Platform Web SDK支援哪些目標功能
- 哪些at.js函式具有Platform Web SDK同等功能
- 如何將Target設定套用至Platform Web SDK
- at.js與Platform Web SDK的資料流程有何不同

如果您是初次使用Platform Web SDK，別擔心，本教學課程將更詳細地介紹下列專案。

## 功能比較

| | Target at.js 2.x | 平台網頁SDK |
|---|---|---|
| 更新Target設定檔 | 支援 | 支援 |
| SPA的觸發檢視 | 支援 | 支援 |
| Target建議 | 支援 | 支援 |
| 擷取表單式選件 | 支援 | 支援 |
| 追蹤事件 | 支援 | 支援 |
| A4T：單頁應用程式 | 支援 | 支援 |
| A4T：點選追蹤 | 支援 | 支援 |
| A4T：使用者端記錄 | 支援 | 支援 |
| A4T：伺服器端記錄 | 支援 | 支援 |
| 套用優惠方案 | 支援 | 支援 |
| 在SPA中重新呈現檢視，而不需通知 | 支援 | 支援 |
| 混合式應用程式 | 支援 | 支援 |
| QA URL | 支援 | 支援 |
| Mbox第三方ID | 支援 | 支援 |
| 客戶屬性 | 支援 | 支援 |
| 遠端選件 | 支援 | 部分支援。 不支援動態遠端選件。 |
| 重新導向選件 | 支援 | 支援。 不過，不支援從具有Platform Web SDK的頁面重新導向至具有at.js的頁面（且方向相反）。 |
| 裝置上決策 | 支援 | 目前不支援 |
| 預先擷取Mbox | 支援自訂範圍和SPA VEC | 預先擷取是網頁SDK的預設模式 |
| 自訂事件 | 支援 | 不支援。 檢視[公開藍圖](https://github.com/orgs/adobe/projects/18/views/1?pane=item&itemId=17372355{target="_blank"})目前的狀態。 |
| 回應Token | 支援 | 支援。 如需at.js和Platform Web SDK之間的程式碼範例和差異，請參閱[專屬回應Token檔案](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hant) |
| 資料提供者 | 支援 | 不支援。 自訂程式碼在從其他提供者擷取資料後，可用於觸發Platform Web SDK `sendEvent`命令。 |


## 值得注意的圖說文字

| | Target at.js 2.x | 平台網頁SDK |
|---|---|---|
| 減少忽隱忽現情形 | 非同步實施的預先隱藏程式碼片段使用樣式ID `at-body-style`。 at.js會在收到回應後尋找此元素ID以移除樣式。 | 預設預先隱藏程式碼片段使用`alloy-prehiding`的樣式識別碼。 Web SDK與at.js預先隱藏程式碼片段不相容，因此在移轉程式期間必須加以變更。 |
| 頁面載入時自動轉譯內容 | 使用Target全域設定控制。 當`pageLoadEnabled`設定為`true`時啟用。 | 在Platform Web SDK `sendEvent`命令中指定。 將`renderDecisions`選項設定為`true`以啟用。 |
| 手動呈現內容 | `applyOffer()`和`applyOffers()`函式僅支援設定HTML | `applyPropositions`命令支援設定、取代或附加HTML以增加彈性 |
| 追蹤自訂事件 | 支援`trackEvent()`和`sendNotifications()`函式。 這些函式專用於Target，不會影響Adobe Analytics量度。 | Platform Web SDK `sendEvent`呼叫的所有資料都會轉送到Target。 Target特別需要的補充資料應包含在具有`sendEvent`或`decisioning.propositionDisplay`eventType的`decisioning.propositionInteract`命令中，以確保Adobe Analytics量度不受影響。 |
| 目標CNAME | 支援。 這與用於Analytics和Experience Cloud ID服務的CNAME不同。 | 不再相關。 單一CNAME可用於所有Platform Web SDK呼叫。 |
| 偵錯 | `mboxDisable`、`mboxDebug`和`mboxTrace` URL引數可用來使用瀏覽器的開發人員工具進行偵錯。<br><br>Adobe Experience Platform Debugger也是支援的偵錯工具。 | 不支援`mboxDisable`、`mboxDebug`和`mboxTrace` URL引數。<br><br>您可以將`alloy_debug=true`新增至查詢字串或在開發人員主控台中執行`alloy("setDebug", { "enabled": true });`，以開啟Web SDK偵錯。<br><br>Adobe Experience Platform Debugger瀏覽器擴充功能可用來起始除錯的邊緣追蹤。<br><br>如需詳細資訊，請參閱[偵錯Platform Web SDK](debugging.md)檔案。 |
| Analytics for Target (A4T) | 使用SDID值來拼接Target和Analytics呼叫 | 原生支援，無需拼接 |

>[!NOTE]
>
>不支援將Target移轉至Platform Web SDK，同時保留指定頁面的現有AppMeasurement Adobe Analytics實作。
>
> 您可以將at.js (和AppMeasurement.js)實作一次移轉一頁至Platform Web SDK。 如果您採取這個方法，最好使用[`idMigrationEnabled`命令將](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hant#id-migration-enabled) [`targetMigrationEnabled`和](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hant#targetMigrationEnabled)`true`選項設定為`configure`。

## at.js函式和平台Web SDK對等函式

許多at.js函式都有等同於使用Platform Web SDK的方法，如下表所述。 如需[at.js函式](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)的詳細資訊，請參閱Adobe Target開發人員指南。

| at.js 2.x函式 | Platform Web SDK對等函式 |
| --- | --- | 
| `getOffer()` 和 `getOffers()` | 若要要求並[自動轉譯](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=zh-Hant#automatically-rendering-content)目標的VEC型體驗，請使用`sendEvent`命令並將`renderDecisions`選項設定為true。<br><br>若要要求表單式體驗或[手動轉譯](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=zh-Hant#manually-rendering-content)內容，請使用`decisionScopes`命令指定`sendEvent` (mbox)的陣列。 |
| `applyOffer()` 和 `applyOffers()` | 使用[`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=zh-Hant#applypropositions)命令套用內容。 您可以選擇設定、取代HTML，或將其附加至特定選取器。 |
| `triggerView()` | 如果[屬性設定在](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html?lang=zh-Hant#how-to-trigger-a-view-change-in-a-single-page-application)命令的`web.webPageDetails.viewName`選項下，則Platform Web SDK會自動針對SPA VEC觸發`xdm`檢視變更`sendEvent`。 |
| `trackEvent()` 和 `sendNotifications()` | 使用包含`sendEvent`特定[`eventType`集合的](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html?lang=zh-Hant#how-to-track-events)命令：<br><br>`decisioning.propositionDisplay`代表活動的轉譯<br><br>`decisioning.propositionInteract`代表使用者與活動的互動，例如滑鼠點按。 |
| `targetGlobalSettings()` | 沒有直接的對等方法。 如需其他詳細資訊，請參閱[目標設定比較](detailed-comparison.md)。 |
| `targetPageParams()` 和 `targetPageParamsAll()` | 在`xdm`命令的`sendEvent`選項中傳遞的所有資料都會對應至Target mbox引數。 由於mbox引數是以序列化的點標籤法來命名，若移轉至Platform Web SDK，您可能需要更新現有的對象和活動，才能使用新的mbox引數名稱。 <br><br>作為`data.__adobe.target`命令的`sendEvent`的一部分傳遞的資料對應到[目標設定檔和Recommendations特定引數](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=zh-Hant#single-profile-update)。 |
| at.js自訂事件 | 不支援。 檢視[公開藍圖](https://github.com/orgs/adobe/projects/18/views/1?pane=item&itemId=17372355{target="_blank"})目前的狀態。 [回應Token](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html?lang=zh-Hant)在`propositions`呼叫的回應中公開為`sendEvent`的一部分。 |

## at.js設定和平台Web SDK同等專案

at.js程式庫可使用Target UI中的各種設定進行設定和下載。 也可以使用[`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/)函式更新這些設定。 下表將這些設定與Platform Web SDK中可用的設定進行比較。

| at.js設定 | Platform Web SDK對等函式 |
| --- | --- |
| `bodyHiddenStyle` | 使用[`prehidingStyle`命令設定](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hant#prehidingStyle)`configure` |
| `bodyHidingEnabled` | 如果使用`prehidingStyle`命令定義`configure`，則會啟用此功能。 如果未定義樣式，則Platform Web SDK不會嘗試隱藏任何內容。 |
| `clientCode` | 自動設定 |
| `cookieDomain` | 不適用 |
| `crossDomain` | 使用`thirdPartyCookiesEnabled`命令將`true`選項設為`configure`，以啟用跨網域使用案例的第一方和第三方Cookie |
| `cspScriptNonce` 和 `cspStyleNonce` | 請參閱[設定CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html?lang=zh-Hant)的檔案 |
| `dataProviders` | 不支援 |
| `decisioningMethod` | 所有Platform Web SDK `sendEvent`命令都使用伺服器端決策。 不支援混合式決策和裝置上決策。 |
| `defaultContentHiddenStyle` 和 `defaultContentVisibleStyle` | 僅適用於at.js 1.x。與at.js 2.x類似，使用自訂程式碼即可緩解表單式體驗的忽隱忽現問題。 |
| `deviceIdLifetime` | 不支援。 如果使用`targetMigrationEnabled`命令將`true`設為`configure`，則會將`mbox` Cookie設定為裝置存留期設為2年。 此值無法設定。 |
| `enabled` | 資料流設定可啟用或停用Target功能 |
| `globalMboxAutoCreate` | 使用`renderDecisions`命令將`true`選項設為`sendEvent`，以自動擷取及轉譯VEC型體驗。如果您偏好手動轉譯VEC型體驗，請<br><br>要求`decisionScope`的`__view__`。 |
| `imsOrgId` | 使用`orgId`命令設定`configure` |
| `optinEnabled` 和 `optoutEnabled` | 請參閱Platform Web SDK [隱私權選項](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?lang=zh-Hant)。 `defaultConsent`選項適用於Platform Web SDK支援的所有Adobe解決方案。 |
| `overrideMboxEdgeServer` 和 `overrideMboxEdgeServerTimeout` | 不適用。 所有Platform Web SDK請求都會使用Adobe Experience Platform Edge網路。 |
| `pageLoadEnabled` | 使用`renderDecisions`命令將`true`選項設為`sendEvent` |
| `secureOnly` | 不支援。 Platform Web SDK會設定具有`secure`和`sameSite="none"`屬性的所有Cookie。 |
| `selectorsPollingTimeout` | 不支援。 Platform Web SDK使用5秒的值。 如有必要，可以使用自訂程式碼來手動轉譯內容。 |
| `serverDomain` | 將`edgeDomain`設定與`configure`命令搭配使用 |
| `telemetryEnabled` | 不適用 |
| `timeout` | 不支援。 建議您將任何忽隱忽現的緩解程式碼都納入適當的逾時。 |
| `viewsEnabled` | 不支援。 若`sendEvent()`設為`renderDecisions`或請求中包含`true` decisionScope，則一律會在第一個`__view__`呼叫上擷取Target檢視的內容。 |
| `visitorApiTimeout` | 不適用 |


## 系統圖表比較

下列圖表應可協助您瞭解使用at.js的Target實作與使用Platform Web SDK的實作之間的資料流程差異。

### at.js 2.x系統圖表

![at.js 2.0在頁面載入時的行為](assets/target-at-js-2x-diagram.png){zoomable="yes"}

| 呼叫 | 詳細資料 |
| --- | --- |
| 1 | 呼叫會傳回Experience Cloud ID (ECID)。 如果使用者已通過驗證，則另一個呼叫會同步客戶ID。 |
| 2 | at.js程式庫會同步載入並隱藏檔案本文（也可使用將頁面上實作的程式碼片段預先隱藏的選項，以非同步方式載入at.js）。 |
| 3 | 提出頁面載入請求，包含所有已設定的引數、ECID、SDID和客戶ID。 |
| 4 | 個人資料指令碼執行並注入個人資料存放區。 存放區會從受眾資料庫中要求合格受眾(例如從Analytics、Audience Manager等共用的受眾)。 客戶屬性會透過批次程式傳送至設定檔存放區。 |
| 5 | Target會根據URL、請求引數和設定檔資料，決定可針對目前頁面和未來檢視傳回哪些活動和體驗給訪客。 |
| 6 | 目標內容會傳回至頁面，選擇性地包括其他個人化的設定檔值。<br><br>目前頁面上的目標內容會儘快出現，不會有忽隱忽現的預設內容。<br><br>單一頁面應用程式未來檢視的目標內容會快取在瀏覽器中，因此當檢視觸發時，可以立即套用，而不需要額外的伺服器呼叫。 |
| 7 | 從頁面傳送至資料收集伺服器的Analytics資料。 |
| 8 | Target資料會透過SDID來比對Analytics資料，然後經過處理放入Analytics報表儲存體中。 然後就可以在Analytics與Target中，透過A4T報表來檢視Analytics資料。 |

請參閱開發人員指南，以取得如何[針對單頁應用程式使用at.js實作Target](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/)的詳細資訊。

### Platform Web SDK系統圖表

![使用Platform Web SDK的Adobe Target Edge Decisioning圖表](assets/target-platform-web-sdk.png)

| 呼叫 | 詳細資料 |
| --- | --- |
| 1 | 裝置載入Platform Web SDK。 Platform Web SDK會傳送要求給Edge Network，要求包含XDM資料、資料串流環境ID、傳入引數和客戶ID （選用）。 頁面（或容器）會預先隱藏。 |
| 2 | Edge Network會傳送要求給Edge Services，以使用訪客ID、同意和其他訪客內容資訊（例如地理位置和方便使用的裝置名稱）來擴充要求。 |
| 3 | 邊緣網路會使用訪客ID和傳入的引數將擴充的個人化請求傳送至Target邊緣。 |
| 4 | 設定檔指令碼執行，然後注入到Target設定檔儲存空間。 設定檔儲存空間會從對象庫擷取區段(例如從Adobe Analytics、Adobe Audience Manager、Adobe Experience Platform共用的區段)。 |
| 5 | Target會根據URL要求引數和設定檔資料，決定要針對目前頁面檢視和未來預先擷取檢視顯示的訪客活動和體驗。 然後Target會將此傳送回邊緣網路。 |
| 6 | a. Edge網路會將個人化回應傳送回頁面，選擇性地包括其他個人化的設定檔值。 目前頁面上的個人化內容會儘快出現，不會有忽隱忽現的預設內容。<br><br>b。作為使用者在單頁應用程式(SPA)中的動作結果而顯示的檢視個人化內容，會快取以供立即呈現，而不需要額外的伺服器呼叫。<br><br>c。邊緣網路會傳送訪客ID和Cookie中的其他值（例如同意、工作階段ID、身分、Cookie檢查、個人化等）。 |
| 7 | 邊緣網路將Analytics for Target (A4T)詳細資料（活動、體驗和轉換中繼資料）轉送給Analytics邊緣。 |

請參閱開發人員指南，以取得如何[使用平台網頁SDK實作Target以供單頁應用程式使用的詳細資訊](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html?lang=zh-Hant)。

在您對目前的Target實作和您使用的功能有良好的技術瞭解後，下一步就是執行[初始設定](initial-setup.md)。

>[!NOTE]
>
>我們致力協助您成功將Target從at.js移轉至Web SDK。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=zh-Hant#M463)中張貼以告知我們。
