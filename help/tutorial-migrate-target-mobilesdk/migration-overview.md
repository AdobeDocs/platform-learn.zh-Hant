---
title: 移轉概述 — 從Adobe Target移轉到Adobe Journey Optimizer - Decisioning Mobile擴充功能
description: 瞭解at.js和Platform Web SDK之間的主要差異，以及如何規劃您的移轉作業。
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# Target at.js移轉至Platform Web SDK概覽

從at.js移轉至Platform Web SDK的工作量層級會視您目前實作和產品功能的複雜度而定。

無論您的實作有多麼簡單或複雜，移轉前都必須充分瞭解您目前的狀態。 本指南可協助您劃分目前實作的元件，並制訂管理得宜的計畫來移轉每個專案。

移轉程式包含下列重要步驟：

1. 評估您目前的實施，並決定移轉方法
1. 設定初始元件以連線至Adobe Experience PlatformEdge Network
1. 更新基礎實作，以Platform Web SDK取代at.js
1. 針對您的特定使用案例增強Platform Web SDK實作。 這可能涉及傳遞其他引數、說明單頁應用程式(SPA)檢視變更、使用回應Token等。
1. 更新Target介面中的物件，例如設定檔指令碼、活動和對象定義
1. 在生產環境中切換之前，請驗證最終實施

## at.js和Platform Web SDK之間的主要差異

在開始移轉程式之前，請務必瞭解at.js和平台Web SDK之間的差異。

### 營運差異

Platform Web SDK將多個Adobe應用程式的功能結合為單一程式庫。 此統一方法表示您應考慮跨團隊的責任和流程，以確保健康的實施。

| | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| 所有權 | at.js程式庫獨立於其他應用程式程式庫。 這些不同程式庫的自訂和擁有權可能會與組織中不同的團隊一致。 | Platform Web SDK程式庫和傳遞的資料會針對所有Adobe應用程式統一。 Platform Web SDK實作的擁有權應代表所有下游應用程式的利害關係人。 |
| 維護 | 不同的團隊可能會處理每個Adobe應用程式（例如Target和Analytics）的實作增強功能。 | 理想情況下，應由單一團隊負責影響Platform Web SDK實作的增強功能。 |
| 程式 | 變更Target實作可能會遵循的流程與其他應用程式（例如Analytics）具有不同的步調或QA需求。 | Platform Web SDK實作的變更應考慮所有下游應用程式，並應相應地調整QA和發佈程式。 |
| 共同作業 | Target專屬的資料可直接在Target呼叫中傳遞。 根據實作，可能會有其他Target呼叫。 這對Adobe Analytics資料沒有直接影響，而且與分析團隊的協調也不重要。 | 在Platform Web SDK呼叫中傳遞的資料可轉送至Target和Analytics。 團隊之間需要進行協調，以確保變更不會對特定應用程式造成負面影響。 |

### 技術差異

Platform Web SDK並非Target at.js程式庫的演化。 這是新的統一方法，可實作網路頻道的所有Adobe應用程式。 您需注意幾項技術差異。

| | Target at.js 2.x | Platform Web SDK |
|---|---|---|
| 程式庫功能 | at.js提供的Target功能。 與Visitor.js和AppMeasurement.js提供的其他應用程式整合 | 單一Platform Web SDK程式庫提供的所有Adobe應用程式的功能： alloy.js |
| 績效 | at.js是必須載入的多個資料庫之一，才能跨應用程式正確整合。 這會導致載入時間少於最佳值。 | Platform Web SDK是單一輕量型程式庫，可免除使用多個應用程式專屬程式庫的需求，進而提供較佳的頁面載入效能。 |
| 請求 | 為每個Adobe應用程式分別發出呼叫。 Target呼叫基本上獨立於其他網路呼叫。 | 針對所有Adobe應用程式發出單一呼叫。 變更這些呼叫中傳遞的資料可能會影響多個下游應用程式。 |
| 載入順序 | 與其他Adobe應用程式正確整合，需要程式庫和網路呼叫的特定載入順序。 | 適當的整合不仰賴拼接不同應用程式專屬網路呼叫的資料，因此不必擔心載入順序。 |
| Edge Network | 使用Adobe Experience CloudEdge Network(tt.omtrdc.net)，可選擇性地搭配Target專屬的CNAME。 | 使用Adobe Experience PlatformEdge Network(edge.adobedc.net)，可選擇搭配單一CNAME。 |
| 基本術語 | at.js命名： <br> - `mbox` <br> - `pageLoad`事件（全域mbox） <br> - `offer` | Platform Web SDK同等專案： <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### 影片概觀

下列影片會概略介紹Adobe Experience Platform Web SDK和Adobe Experience PlatformEdge Network。


現在您已瞭解at.js和Platform Web SDK之間的高階差異，您可以[規劃移轉](plan-migration.md)。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
