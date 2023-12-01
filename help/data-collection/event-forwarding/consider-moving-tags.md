---
title: 考慮將廠商標籤移動到事件轉送
description: 瞭解如何評估伺服器端資料散發的使用者端廠商標籤。
feature: Event Forwarding, Tags, Integrations
role: Admin, Developer, Architect, Data Engineer
level: Intermediate, Experienced
jira: KT-9921
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: 7edf8fc46943ae2f1e6e2e20f4d589d7959310c8
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 3%

---

# 考慮將用戶端廠商標籤移動到事件轉送

考慮將使用者端廠商標籤移出瀏覽器和裝置，並移至伺服器有幾個吸引人的理由。 在本文中，我們將討論如何評估使用者端廠商標籤以潛在地將其移動到事件轉送屬性。

只有當您考慮移除使用者端廠商標籤，並在事件轉送屬性中將其取代為伺服器端資料發佈時，才需要執行這項評估。 本文假設您熟悉以下內容的基本知識 [資料彙集](https://experienceleague.adobe.com/docs/data-collection.html)、和 [事件轉送](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html).

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)。

瀏覽器廠商正在改變他們對待協力廠商Cookie的方式。 廣告和行銷供應商及技術通常需要使用許多使用者端標籤。 這些挑戰只是我們的客戶增加伺服器端資料散佈的兩個極具吸引力的原因。

>[!NOTE]
>
>`Tag` 在本文中，是指使用者端代碼，通常是來自廠商的JavaScript，用於在訪客與網站或應用程式互動時，於瀏覽器或裝置中進行資料收集。 `Website` 或 `site` 這裡是指行動裝置的網站、網頁應用程式或應用程式。 用於這些用途的「標籤」通常也稱為畫素。

## 使用案例和資料 {#use-cases-data}

第一步是定義使用使用者端廠商標籤實作的使用案例。 例如，以Facebook (Meta)畫素為例。 將其從我們的網站移至 [中繼轉換API](https://exchange.adobe.com/apps/ec/109168/meta-conversions-api) 使用事件轉送擴充功能，表示會先記錄特定使用案例。

若為目前使用者端廠商程式碼：

- 哪些特定事件和其他資料點會公開並傳遞至使用者端標籤？
- 資料傳輸何時何地發生？

提供清單、試算表、圖表或其他資料和事件順序的記錄，以記錄此評估會很有幫助 — 即使它僅供您自己使用。 請務必加入資料來源的標籤 — 來源位置？ 目的地 — 前往何處？ 以及轉換 — 來源和目的地之間會發生什麼情況？

在我們的範例中，當訪客在檢視Facebook廣告後與我們的網站互動時，我們使用Facebook畫素追蹤轉換。 他們檢視其他社交平台上的相關廣告後，也可以與我們的網站互動。 若要在Facebook廣告工具和報表中檢視這些轉換，必須將Facebook中所需的資料取得。 此資料可能包含下載、註冊、喜歡或購買等轉換事件。

### 資料 {#data}

有了現有的使用者端標籤，當標籤在我們的網站上執行或執行時，使用案例的資料會發生什麼事？ 我們可以擷取使用者端中所需的資料，而不使用廠商標籤，以便傳送給事件轉送嗎？ 使用時 [標籤](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) 標籤管理系統或其他標籤管理系統中，大部分的訪客互動資料都可用於收集和分發。 但我們在使用案例中所需的資料，是否可以在需要時、在需要的地方以需要的格式提供，而不需要使用者端廠商的標籤？ 以下是進一步要考慮的資料問題：

- 每個事件是否需要廠商使用者ID？
- 若是如此，如何收集或產生檔案而不使用使用者端標籤？
- 廠商在執行階段是否特別需要其使用者端代碼？
- 需要哪些其他資料？ 這些資料會來自何處？

大部分使用者端廠商標籤對於任何特定使用案例不需要許多資料點，但在這些評估期間記下使用案例和所需資料會很有幫助。

## 廠商API {#vendor-apis}

現在我們知道要實作的特定使用案例、所需的資料，以及從來源到目的地的事件順序。 為了判斷使用案例是否適合事件轉送，我們現在可以調查供應商API詳細資訊。

>[!IMPORTANT]
>
>雖然許多廠商都啟用API進行伺服器對伺服器傳輸，但也有許多廠商目前沒有適合這些用途的API。

### 調查API {#investigate-apis}

以下是一些調查廠商API端點的步驟。

廠商是否設計有API以用於伺服器對伺服器的事件資料傳輸？ 首先，找出這些特定API端點的需求：

- API端點存在以傳送所需資料嗎？ 若要尋找支援您使用案例的端點，請參閱供應商的開發人員或API檔案。
- 它們是否允許串流事件資料，或僅允許批次資料？
- 它們支援哪些驗證方法？ 權杖、HTTP、OAuth使用者端憑證版本或其他？ 另請參閱 [此處](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) 適用於事件轉送支援的方法。
- 其API的重新整理位移為何？ 此限制是否與事件轉送最小值相容？ 詳細資料 [此處](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- 它們需要哪些資料才能用於相關端點？
- 它們是否需要在每次呼叫端點時都使用廠商特定使用者識別碼？
- 如果他們需要該識別碼，可以在哪裡以及如何產生或擷取（無需使用者端代碼）？

換句話說：

- 供應商是否提供我們使用案例所需的API端點？
- 他們是否有相容的驗證方法用於事件轉送？
- 我們是否可從使用者端或其他API呼叫存取事件轉送實施所需的所有資料？

如果我們可以對這些問題回答「是」，則標籤可能是從使用者端移至事件轉送屬性中我們伺服器的良好候選項。

如果廠商沒有可支援使用案例的API端點，那麼廠商標籤顯然不適合使用事件轉送來取代使用者端廠商標籤。

如果他們有API，但在每個API呼叫中也需要一些不重複訪客或使用者ID，該怎麼辦？ 如果網站上未執行廠商使用者端代碼（標籤），我們如何存取該ID？

有些廠商在沒有協力廠商Cookie的情況下會針對新世界更換系統。 這些變更包括使用替代唯一識別碼，例如 [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) 或其他 [客戶產生的ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html). 如果廠商允許客戶產生的ID，我們就能使用Web或Mobile SDK從使用者端將其傳送至Platform Edge Network，或透過事件轉送中的API呼叫取得。 我們在事件轉送規則中傳送資料給該供應商時，只需視需要納入該識別碼即可。

如果廠商需要只有其自己的使用者端標籤才能產生或存取的資料（例如廠商特有的唯一ID），那麼該廠商標籤就很可能不是移動的良好候選者。 _不建議嘗試透過將資料收集移至事件轉送（而不使用適當的API）的想法，對使用者端標籤進行反向工程。_

此 [Adobe Experience Platform雲端聯結器](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) 擴充功能可視需要向具備適當的API以用於伺服器對伺服器事件資料傳輸的廠商提出HTTP請求。 雖然廠商專用的擴充功能已很好用，而且目前有更多的擴充功能正在積極開發中，但我們現在可以使用Cloud Connector擴充功能實作事件轉送規則，不需等候其他廠商的擴充功能。

## 工具 {#tools}

透過如下的工具，更容易調查和測試廠商API端點 [Postman](https://www.postman.com/)或文字編輯器擴充功能，例如Visual Studio Code [Thunder使用者端](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)，或 [http使用者端](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## 後續步驟 {#next-steps}

本文提供了一系列步驟，用於評估廠商使用者端標籤，以及在事件轉送屬性中可能將其移動到伺服器端。 如需相關主題的詳細資訊，請參閱下列連結：

- [標籤管理](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) 在Adobe Experience Platform中
- [事件轉送](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) 用於伺服器端處理
- [術語更新](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) 在資料收集中
