---
title: 考慮將供應商標籤移動到事件轉發
description: 了解如何評估伺服器端資料分送的用戶端廠商標籤。
feature: Event Forwarding, Tags, Integrations
solution: Data Collection
kt: 9921
level: Intermediate, Experienced
role: Admin, Developer, Architect
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 3%

---

# 考慮將用戶端廠商標籤移動到事件轉送

考慮將用戶端廠商標籤移出瀏覽器和裝置並移到伺服器上，有幾個令人信服的理由。 在本文中，我們討論如何評估用戶端廠商標籤，以將其移至事件轉送屬性。

只有在您考慮移除用戶端廠商標籤，並將其取代為事件轉送屬性中的伺服器端資料分發時，才需要進行此評估。 本文假設您熟悉 [資料匯集](https://experienceleague.adobe.com/docs/data-collection.html)，和 [事件轉送](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html).

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)。

瀏覽器廠商正在變更對待第三方Cookie的方式。 廣告和行銷廠商及技術通常需要使用許多用戶端標籤。 這些難題只是客戶增加伺服器端資料分送的兩個迫切原因。

>[!NOTE]
>
>`Tag` 在本文中，系指用戶端程式碼，通常是來自廠商的JavaScript，當訪客與網站或應用程式互動時，這些廠商用於在瀏覽器或裝置中收集資料。 `Website` 或 `site` 這裡指的是網站、網頁應用程式或行動裝置的應用程式。 用於這些目的的「標籤」通常也稱為像素。

## 使用案例和資料 {#use-cases-data}

第一步是定義使用用戶端廠商標籤實作的使用案例。 例如，請考量Facebook（中繼）像素。 將其從我們的網站移至 [Facebook轉換API](https://exchange.adobe.com/apps/ec/105509/facebook-conversions-api-extension) 使用event forwarding擴充功能，表示會先記錄特定使用案例。

針對目前的用戶端廠商代碼：

- 哪些特定事件和其他資料點會公開並傳遞至用戶端標籤？
- 資料傳輸會在何時何地發生？

將資料和事件順序的清單、試算表、圖表或其他記錄記錄下來記錄此評估是很有幫助的，即使這僅供您自己使用。 請務必加入資料來源的標籤 — 資料來源來自何處？ 目的地，它去哪了？ 和轉換 — 源和目標之間會發生什麼變化？

在我們的範例中，我們是在訪客檢視Facebook廣告後與我們的網站互動時，使用Facebook像素追蹤轉換。 在其他社交平台上檢視相關廣告後，他們也可以與我們的網站互動。 若要在Facebook廣告工具和報表中查看這些轉換，必須將必要資料傳送至Facebook。 此資料可能包含轉換事件，例如下載、註冊、按贊或購買。

### 資料 {#data}

若使用現有的用戶端標籤，當該標籤在我們的網站上執行或執行時，我們的使用案例的資料會發生什麼事？ 我們可以在用戶端中擷取所需的資料，而不需要廠商標籤，以便將其傳送至事件轉送？ 使用時 [標籤](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) 或其他標籤管理系統中，大部分的訪客互動資料都可供收集和分發。 但是，我們使用案例所需的資料是否可在需要時、在需要的位置以及所需的格式提供 — 無需客戶端供應商標籤？ 以下是需要考慮的其他資料問題：

- 每個事件是否需要供應商用戶ID?
- 如果是，如何在不使用用戶端標籤的情況下收集或產生？
- 供應商是否在運行時特別要求其客戶端代碼？
- 需要哪些其他資料？ 這些資料會從哪裡來？

大部分的用戶端廠商標籤對於任何特定使用案例不需要許多資料點，但在評估期間記下使用案例和所需資料會很有幫助。

## 廠商API {#vendor-apis}

現在，我們知道要實作的特定使用案例、所需資料，以及從來源到目的地的事件順序。 為了判斷使用案例是否適合事件轉送，我們現在可以調查廠商API詳細資訊。

>[!IMPORTANT]
>
>雖然許多廠商都啟用API進行伺服器對伺服器的傳輸，但目前也有許多廠商沒有適合這些用途的API。

### 調查API {#investigate-apis}

以下是調查供應商API端點時可採取的一些步驟。

供應商是否有專為事件資料的伺服器對伺服器傳輸而設計的API? 首先，找出這些特定API端點的需求：

- 是否存在API端點以傳送所需資料？ 若要尋找支援您使用案例的端點，請參閱廠商的開發人員或API檔案。
- 是否允許串流事件資料，或僅允許批次資料？
- 他們支援哪些驗證方法？ 代號、HTTP、OAuth用戶端認證版本或其他？ 請參閱 [此處](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) 以取得事件轉送支援的方法。
- 其API的重新整理位移為何？ 該限制是否與事件轉送最低限制相容？ 詳細資料 [此處](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- 他們需要哪些資料才能取得相關端點？
- 是否每次呼叫端點時都需要供應商特定的用戶標識符？
- 如果他們需要該識別碼，該識別碼可在何處、如何產生或擷取，而不需要用戶端代碼？

換句話說：

- 供應商是否提供我們使用案例所需的API端點？
- 他們是否有相容的事件轉送驗證方法？
- 我們是否可存取事件轉送實施（從用戶端或其他API呼叫）所需的所有資料？

如果我們能回答「是」，標籤很可能是從用戶端移至伺服器的事件轉送屬性好候選項目。

如果廠商沒有可支援我們使用案例的API端點，那麼顯然，該廠商標籤並非使用事件轉送取代用戶端廠商標籤的理想候選者。

如果他們有API，但每次API呼叫也需要某些不重複訪客或使用者ID，該怎麼辦？ 如果網站上未執行廠商用戶端代碼（標籤），如何存取該ID?

有些廠商正在針對沒有第三方Cookie的新世界變更其系統。 這些變更包括使用替代的唯一識別碼，例如 [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) 或其他 [客戶產生的ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html). 如果廠商允許由客戶產生的ID，我們可以透過Web或Mobile SDK從用戶端將其傳送至Platform Edge Network，或透過事件轉送時的API呼叫取得。 當我們在事件轉送規則中傳送資料給該廠商時，我們會視需要包含該識別碼。

如果供應商需要只能由其自己的客戶端標籤生成或訪問的資料（例如供應商特定唯一ID），則該供應商標籤可能不是移動的好候選標籤。 _不建議您嘗試在不使用適當API的情況下，以將資料收集移動至事件轉送的想法，對用戶端標籤進行反向工程。_

此 [Adobe Experience Platform Cloud Connector](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) 擴充功能可視需要，向擁有適當API以進行伺服器對伺服器事件資料傳輸的廠商提出HTTP要求。 雖然您可以擁有廠商專屬的擴充功能，且目前正在使用中開發更多擴充功能，但現在我們可以使用Cloud Connector擴充功能實作事件轉送規則，而不需等候其他廠商擴充功能。

## 工具 {#tools}

透過如下工具，調查和測試供應商API端點會更輕鬆 [Postman](https://www.postman.com/)，或文字編輯器擴充功能，例如Visual Studio Code [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)，或 [HTTP客戶端](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## 後續步驟 {#next-steps}

本文提供一系列步驟來評估供應商客戶端標籤，並可能在事件轉發屬性中將其移動到伺服器端。 如需相關主題的詳細資訊，請參閱下列連結：

- [標籤管理](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) 在Adobe Experience Platform
- [事件轉送](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) 伺服器端處理
- [術語更新](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) 資料收集
