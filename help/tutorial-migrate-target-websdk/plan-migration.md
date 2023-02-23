---
title: 規劃 |將Target從at.js 2.x移轉至Web SDK
description: 了解如何針對從at.js 2.x到Adobe Target Web SDK的Adobe Experience Platform實作進行規劃。
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 規劃從at.js移轉至Platform Web SDK

在升級至網站上的Platform Web SDK之前，您應先評估目前的實作。

## 評估目前的at.js實作

成功移轉的第一步，就是能對您目前的at.js Target實作有深入的了解。 您可能會使用某些功能、函式和自訂程式碼，需要更新。 評估時，請考量下列事項：

### 支援哪些功能？

Platform Web SDK正在持續進行主動開發，並會定期新增功能和增強功能。 評估目前的at.js實作時，請參閱 [支援的使用案例](https://github.com/orgs/adobe/projects/18/views/1) 頁面以取得最新資訊。

### 你今天用什麼功能？

Platform Web SDK是新的程式庫，將網站的所有Adobe解決方案整合為單一SDK。 如此可進行更緊密的整合，並啟用Adobe Experience Platform獨有的新功能。 不過，這也表示at.js函式不會向後相容於Platform Web SDK。 評估目前的實作時，請注意下列事項：

- at.js函式，例如 `getOffer()` 和 `applyOffer()`
- 修改Target的全域設定
- 與 Adobe Analytics 整合
- 使用忽隱忽現緩解指令碼
- 回應Token的使用
- 使用mbox、設定檔和實體參數
- 實作特有的自訂程式碼

### 您會採取哪種移轉方法？

重新檢視at.js實作後，您需要決定移轉方法。 有兩個選項：

- 跨整個站點一次遷移所有Adobe應用程式
- 逐頁移轉

由於Platform Web SDK結合併啟用多個Adobe應用程式，因此您必須協調其他Adobe應用程式(例如Analytics和Audience Manager)的Target移轉。 指定頁面上的所有Adobe程式庫應同時移轉。 不支援在特定頁面上混合實作適用於Target的Platform Web SDK和適用於Analytics的AppMeasurement。 不過，我們支援跨不同頁面的混合實作，例如頁面A上的Platform Web SDK，以及頁面B上的at.js與AppMeasurement。

在移轉時，您應先規劃要遵循公司的程式來測試和發行新程式碼，並在發行至生產環境之前先使用開發、qa和測試環境等項目。

>[!CAUTION]
>
>如果從具有一個程式庫的頁面重新導向至具有不同程式庫的頁面，則逐頁移轉不支援重新導向選件


接下來，查看詳細資訊 [at.js與Platform Web SDK的比較](detailed-comparison.md) 更好地了解技術差異，並確定需要更多重點的領域。

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
