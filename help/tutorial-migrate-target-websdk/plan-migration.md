---
title: 規劃 — 將Target從at.js 2.x移轉至Web SDK
description: 瞭解如何針對從at.js 2.x到Adobe Experience Platform Web SDK的Adobe Target實作進行規劃。
exl-id: 0e8f9cde-f361-4f69-886d-aad3074cd9b2
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 規劃從at.js移轉至Platform Web SDK的程式

在網站上升級至Platform Web SDK之前，您應該先評估目前的實施。

## 評估目前的at.js實作

成功移轉的第一步，就是要清楚瞭解您目前的at.js Target實作。 有些您可能會使用的功能、函式及自訂程式碼需要更新。 評估時請考量下列事項：

### 支援哪些功能？

Platform Web SDK正在持續積極開發，並會定期新增功能和增強功能。 當您評估目前的at.js實作時，請參閱[支援的使用案例](https://github.com/orgs/adobe/projects/18/views/1)頁面以取得最新資訊。

### 您現在使用哪些功能？

Platform Web SDK是新的程式庫，可將網站的所有Adobe解決方案整合為單一SDK。 如此一來，您便可更緊密整合，並啟用Adobe Experience Platform獨有的新功能。 不過，這也表示at.js函式無法與Platform Web SDK回溯相容。 評估目前實作時，請注意下列事項：

- at.js函式，例如`getOffer()`和`applyOffer()`
- 修改Target的全域設定
- 與 Adobe Analytics 整合
- 使用閃爍的緩解指令碼
- 使用回應Token
- mbox、設定檔和實體引數的使用
- 實作特有的自訂程式碼

### 您將採取哪種移轉方法？

重新檢視at.js實作後，您必須決定移轉方法。 有兩個選項：

- 一次移轉整個網站的所有Adobe應用程式
- 逐頁移轉

由於Platform Web SDK結合併啟用多個Adobe應用程式，因此您必須協調其他Adobe應用程式(例如Analytics和Audience Manager)的Target移轉。 指定頁面上的所有Adobe程式庫都應同時移轉。 不支援在特定頁面上混合實作適用於Target的Platform Web SDK和適用於Analytics的AppMeasurement。 不過，我們支援跨不同頁面的混合實作，例如頁面A上的Platform Web SDK以及頁面B上具有AppMeasurement的at.js。

當您移轉時，您應該計畫遵循公司的流程和發佈新計畫碼，並在發佈到生產環境之前使用開發、qa和中繼環境等。

>[!CAUTION]
>
>如果從含有一個程式庫的頁面重新導向至含有不同程式庫的頁面，在逐頁移轉中不支援重新導向選件


接下來，檢閱at.js與Platform Web SDK[&#128279;](detailed-comparison.md)的詳細比較，以更清楚瞭解技術差異，並找出需要額外關注的領域。

>[!NOTE]
>
>我們致力協助您成功將Target從at.js移轉至Web SDK。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=zh-Hant#M463)中張貼以告知我們。
