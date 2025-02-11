---
title: Target擴充功能與決策擴充功能的比較
description: 瞭解Target擴充功能與Decisioning擴充功能之間的差異，包括功能、功能、設定和資料流程。
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 314f0279ae445f970d78511d3e2907afb9307d67
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 1%

---

# Target擴充功能與決策擴充功能的比較

Adobe Journey Optimizer - Decisioning擴充功能與適用於行動應用程式的Adobe Target擴充功能不同。 下表為參考資料，可協助您評估在移轉程式期間可能需要著重的實作領域。

檢閱下列資訊並評估您目前的技術Target擴充功能實作後，您應該就能瞭解下列內容：

- Adobe Journey Optimizer支援哪些Target功能 — Decisioning
- 哪些Adobe Target擴充功能具有Adobe Journey Optimizer — 決策等效功能
- 如何將Target設定套用至Adobe Journey Optimizer — 決策
- 使用Adobe Journey Optimizer - Decisioning擴充功能時資料流動的方式

## 營運差異

| | 目標延伸功能 | Decisioning擴充功能 |
|---|---|---|
| 程式 | 變更Target實作可能會遵循的流程與其他應用程式（例如Analytics）具有不同的步調或QA需求。 | 對決策擴充功能實作的變更應考慮所有下游應用程式，並應相應地調整QA和發佈程式。 |
| 共同作業 | Target專屬的資料可直接在Target呼叫中傳遞。 如果Target報表來源是Adobe Analytics (A4T)，則當Target擴充功能中呼叫適當的追蹤方法來用於Target內容顯示和互動時，特定於Target的資料也可以傳遞到Adobe Analytics。 | 如果Target報表來源為Adobe Analytics (A4T)、已在資料串流中啟用Adobe Analytics，且顯示Target內容並與之互動時，系統可將Decisioning擴充功能呼叫中傳遞的資料轉送至Target和Analytics。 |

## 基本差異

| | 目標延伸功能 | Decisioning擴充功能 |
|---|---|---|
| 相依性 | 僅取決於行動核心SDK | 仰賴行動核心和Edge Network SDK |
| 程式庫功能 | 僅支援從Adobe Target擷取內容 | 支援從Adobe Target和Offer Decisioning擷取內容 |
| 請求 | Target呼叫基本上獨立於其他網路呼叫 | Target網路呼叫會針對其他Edge型解決方案(例如Edge SDK中的傳訊)與網路呼叫一起排入佇列，並依序執行。 |
| Edge Network | 使用Target伺服器值或具有使用者端代碼(clientcode.tt.omtrdc.net)的Adobe Experience Cloud Edge Network，兩者都在資料收集UI的[Target組態](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui)中指定 | 在資料收集UI中使用Adobe Experience Platform [Edge Network組態](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui)中指定的Edge網路網域。 |
| 基本術語 | mbox， TargetParameters | 目標引數的DecisionScope， Map (Android)/dictionary (iOS) |
| 預設內容 | 允許在TargetRequest中傳遞使用者端預設內容，如果網路呼叫失敗或導致錯誤，則會傳回此內容。 | 不允許傳遞使用者端預設內容。 如果網路呼叫失敗或導致錯誤，則不會傳回任何內容。 |
| Target引數 | 允許傳遞每個要求的全域TargetParameters和每個mbox的不同TargetParameters | 僅允許傳遞每個要求的全域TargetParameters |



## 功能比較

| 功能 | 目標延伸功能 | 決策擴充功能(透過Edge的Target) |
|---|---|---|
| 預先擷取模式 | 支援 | 支援 |
| 執行模式 | 支援 | 不支援 |
| 自訂引數 | 支援 | 支援* |
| 輪廓參數 | 支援 | 支援* |
| 實體引數 | 支援 | 支援* |
| 目標客群 | 支援 | 支援 |
| Real-Time CDP對象 | 不支援 | 支援 |
| Real-Time CDP屬性 | 不支援 | 支援 |
| 生命週期量度 | 支援 | 透過資料收集規則支援 |
| thirdPartyId (mbox3rdPartyId) | 支援 | 透過資料流中的身分對應和目標第三方ID名稱空間支援 |
| 通知（顯示、按一下） | 支援 | 支援 |
| 回應Token | 支援 | 支援 |
| Analytics for Target (A4T) | 僅限使用者端 | 使用者端和伺服器端 |
| 行動裝置預覽（QA模式） | 支援 | Assurance的有限支援 |

>[!IMPORTANT]
>
> \*在要求中傳送的引數會套用至要求中的所有範圍。 如果您需要為不同的範圍設定不同的引數，則必須提出其他要求。



## 值得注意的圖說文字

>[!NOTE]
>
>即使您將應用程式程式碼移轉至Decisioning擴充功能後，仍能維持Target擴充功能標籤的組態和設定。 這可協助確保尚未將應用程式更新至新版本的客戶能夠繼續使用Target。
>
>如果您使用Analytics for Target整合(A4T)，在將Target實作移轉至Decisioning擴充功能的同時，請務必將Analytics實作與Edge Bridge擴充功能一起移轉。





>[!IMPORTANT]
>
> 即使您將應用程式程式碼移轉至Decisioning擴充功能後，Target擴充功能設定仍會妥善保留。 這可協助確保尚未更新應用程式的使用者能夠繼續使用Target。

## 決策擴充功能系統圖

下圖應可協助您瞭解使用Adobe Journey Optimizer - Decisioning擴充功能的資料流程。

![使用使用者端Mobile SDK的Adobe Target Edge Decisioning](assets/diagram.png)


>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
