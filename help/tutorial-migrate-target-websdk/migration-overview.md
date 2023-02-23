---
title: 移轉概觀 |將Target從at.js 2.x移轉至Web SDK
description: 了解at.js和Platform Web SDK之間的主要差異，以及如何規劃移轉作業。=
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# 將at.js移轉至Platform Web SDK的概述

從at.js移轉至Platform Web SDK的工作量，取決於您目前實作的複雜度和使用的產品功能。

無論實作有多簡單或複雜，在移轉前請務必充分了解您目前的狀態。 本指南可協助您劃分目前實作的元件，並制定可管理的計畫，以移轉每個元件。

移轉程式包含下列關鍵步驟：

1. 評估您目前的實作，並決定移轉方法
1. 設定初始元件以連接至Adobe Experience Platform邊緣網路
1. 更新基本實作，將at.js取代為Platform Web SDK
1. 針對您的特定使用案例增強Platform Web SDK實作。 這可能需要傳遞其他參數、計入單頁應用程式(SPA)檢視變更、使用回應Token等。
1. 更新Target介面中的物件，例如設定檔指令碼、活動和對象定義
1. 在生產環境中切換之前，驗證最終實施

## at.js與Platform Web SDK之間的主要差異

開始移轉程式之前，請務必了解at.js和Platform Web SDK之間的差異。

### 運營差異

Platform Web SDK將多個Adobe應用程式的功能結合為單一程式庫。 此統一方法表示您應考慮跨團隊的責任和程式，以確保實作順利。

|  | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 所有權 | at.js程式庫與其他應用程式程式庫無關。 這些不同程式庫的自訂和所有權可能與組織中的不同團隊一致。 | Platform Web SDK程式庫和傳遞的資料已統一至所有Adobe應用程式。 Platform Web SDK實作的所有權應代表所有下游應用程式的利害關係人。 |
| 維護 | 個別團隊可能會針對每個Adobe應用程式（例如Target和Analytics）進行實作增強功能。 | 理想情況下，應由單一團隊負責影響Platform Web SDK實作的增強功能。 |
| 程序 | 與其他應用程式（如Analytics）相比，Target實作的變更可能會遵循有不同順序或QA要求的程式。 | Platform Web SDK實作的變更應考慮所有下游應用程式，而QA和發佈程式應隨之調整。 |
| 共同作業 | Target的特定資料可直接在Target呼叫中傳遞。 視實施而定，可能會有其他Target呼叫。 這對Adobe Analytics資料沒有直接影響，且與分析團隊的協調並不重要。 | 在Platform Web SDK呼叫中傳遞的資料可以轉送至Target和Analytics。 需要協調各小組，以確保更改不會對特定應用程式產生不利影響。 |

### 技術差異

Platform Web SDK並非Target at.js資料庫的演變。 這是為Web通道實作所有Adobe應用程式的全新統一方法。 需注意的技術差異有數種。

|  | Target at.js 2.x | 平台Web SDK |
|---|---|---|
| 程式庫功能 | at.js提供的Target功能。 與Visitor.js和AppMeasurement.js提供之其他應用程式的整合 | 由單一平台Web SDK程式庫提供之所有Adobe應用程式的功能：alloy.js |
| 效能 | at.js是必須載入的多個程式庫之一，才能在應用程式間正確整合。 這會導致負載時間小於最佳值。 | Platform Web SDK是單一的輕量型程式庫，不需使用多個應用程式專用程式庫，即可產生更佳的頁面載入效能。 |
| 請求 | 為每個Adobe應用程式分開呼叫。 Target呼叫基本上獨立於其他網路呼叫。 | 所有Adobe應用程式的單一呼叫。 變更這些呼叫中傳遞的資料可能會影響多個下游應用程式。 |
| 載入順序 | 與其他Adobe應用程式正確整合，需要特定的程式庫載入順序和網路呼叫。 | 正確的整合不依賴拼接不同應用程式特定網路呼叫的資料，因此不需要考慮載入順序。 |
| 邊緣網路 | 使用Adobe Experience Cloud邊緣網路(tt.omtrdc.net)，選擇性地搭配Target專用的CNAME。 | 使用Adobe Experience Platform Edge Network(edge.adobedc.net)，選擇性地搭配單一CNAME。 |
| 基本術語 | at.js命名： <br> - `mbox` <br> - `pageLoad` 事件（全域mbox） <br> - `offer` | 平台Web SDK的對等方法： <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### 影片概述

以下影片提供Adobe Experience Platform Web SDK和Adobe Experience Platform Edge Network的概觀。

>[!VIDEO](https://video.tv.adobe.com/v/34141/?quality=12&learn=on)

現在您了解at.js和Platform Web SDK之間的高階差異，便可以 [規劃移轉](plan-migration.md).

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).