---
title: 規劃移轉 — 從Adobe Target移轉到Adobe Journey Optimizer - Decisioning Mobile擴充功能
description: 瞭解at.js與Platform Web SDK之間的主要差異，以及如何規劃您的移轉作業。
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# 規劃移轉

從Target擴充功能移轉至Decisioning擴充功能的工作量等級，取決於您目前實作和所用產品功能的複雜性。

無論您的實作有多麼簡單或複雜，移轉前都必須充分瞭解您目前的狀態。 本指南可協助您劃分目前實作的元件，並制訂管理得宜的計畫來移轉每個專案。

移轉程式包含下列重要步驟：

1. 評估您目前的實施，並決定移轉方法
1. 設定初始元件以連線至Adobe Experience PlatformEdge Network
1. 更新基本實作，以取代Target擴充功能和Decisioning擴充功能
1. 針對您的特定使用案例增強「最佳化SDK」實作。 這可能涉及傳遞其他引數、使用回應Token等。
1. 更新Target介面中的物件，例如設定檔指令碼、活動和對象定義
1. 在生產環境中切換之前，請驗證最終實施

## Target擴充功能與決策擴充功能之間的主要差異

在開始移轉程式之前，請務必瞭解Target擴充功能與決定擴充功能之間的差異。

### 營運差異

| | Target at.js 2.x | 平台網頁SDK |
|---|---|---|
| 程式 | 變更Target實作可能會遵循的流程與其他應用程式（例如Analytics）具有不同的步調或QA需求。 | 對決策擴充功能實作的變更應考慮所有下游應用程式，並應相應地調整QA和發佈程式。 |
| 共同作業 | Target專屬的資料可直接在Target呼叫中傳遞。 如果Target報表來源是Adobe Analytics，則當Target擴充功能中呼叫適當的追蹤方法來用於Target內容顯示和互動時，特定於Target的資料也可以傳遞到Adobe Analytics。 | 如果Target報表來源為Adobe Analytics、已在資料串流中啟用Adobe Analytics，且顯示Target內容並與之互動時，系統可將Decisioning擴充功能呼叫中傳遞的資料轉送至Target和Analytics。 |

### 技術差異

| | 目標延伸功能 | Decisioning擴充功能 |
|---|---|---|
| 相依性 | 僅取決於行動核心SDK | 取決於行動核心和Edge NetworkSDK |
| 程式庫功能 | 僅支援從Adobe Target擷取內容 | 支援從Adobe Target和Offer decisioning擷取內容 |
| 請求 | Target呼叫基本上獨立於其他網路呼叫 | Target網路呼叫會針對其他Edge型解決方案(例如Edge SDK中的傳訊)與網路呼叫一起排入佇列，並依序執行。 |
| Edge Network | 使用Target伺服器值或具有使用者端代碼(clientcode.tt.omtrdc.net)的Adobe Experience CloudEdge Network，兩者都在資料收集UI的[Target組態](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui)中指定 | 在資料收集UI中使用Adobe Experience Platform [Edge Network組態](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui)中指定的Edge網路網域。 |
| 基本術語 | mbox， TargetParameters | 目標引數的DecisionScope， Map (Android)/dictionary (iOS) |
| 預設內容 | 允許在TargetRequest中傳遞使用者端預設內容，如果網路呼叫失敗或導致錯誤，則會傳回此內容。 | 不允許傳遞使用者端預設內容。 如果網路呼叫失敗或導致錯誤，則不會傳回任何內容。 |
| Target引數 | 允許傳遞每個要求的全域TargetParameters和每個mbox的不同TargetParameters | 僅允許傳遞每個要求的全域TargetParameters |

接下來，檢閱Target擴充功能與Decisioning擴充功能](detailed-comparison.md)的詳細[比較，以更清楚瞭解技術差異，並找出需要額外關注的領域。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
