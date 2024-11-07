---
title: Adobe Journey Optimizer — 外部氣象API、SMS動作等
description: Adobe Journey Optimizer — 外部氣象API、SMS動作等
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7f3d6dcb-845d-4ff1-97c3-8e93b8d2c624
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# 3.2 Adobe Journey Optimizer：外部資料來源和自訂動作

**作者：[Wouter Van Glouwe](https://www.linkedin.com/in/woutervangeluwe/)**

在此單元中，您將使用Adobe Journey Optimizer來線上及離線監聽客戶行為，並以智慧、情境式且即時的方式回應。 您已在單元6中對Adobe Journey Optimizer有初始的實作體驗。 在本練習中，您將更深入並探索更進階的使用案例，其中外部資料來源會作為歷程的一部分使用。

## 學習目標

- 瞭解如何在Adobe Journey Optimizer中建立事件、外部資料來源和歷程
- 瞭解如何從開放式氣象API使用天氣資訊
- 瞭解如何使用Twilio等自訂動作目的地和Adobe Journey Optimizer的Slack

## 先決條件

- 存取Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 存取Adobe Journey Optimizer
- 存取開放氣象API

## 業務內容

身為品牌，您已在個人化線上體驗上投入巨資。 現在，您想要與離線體驗產生關聯性和相關性。
在此單元中，您將利用客戶在離線商店的存在，然後在商店內透過在店內熒幕展示相關內容給該客戶，並同時想要即時提供個人化推播或簡訊訊息給該客戶，藉此提供個人化體驗。
身為品牌，您也會瞭解內容對客戶的興趣有重大影響，因此您想要引進客戶所在位置的目前天氣資訊，以決定要顯示的內容或促銷活動。

>[!NOTE]
>
>別忘了安裝、設定和使用[0.1中參考的Chrome擴充功能 — 安裝Experience League檔案的Chrome擴充功能](../../gettingstarted/gettingstarted/ex1.md)

## 練習

[3.2.1定義事件](./ex1.md)

瞭解如何使用Adobe Journey Optimizer定義自訂事件。

[3.2.2定義外部資料來源](./ex2.md)

瞭解如何使用Adobe Journey Optimizer設定外部資料來源。

[3.2.3定義自訂動作](./ex3.md)

瞭解如何使用Adobe Journey Optimizer定義外部動作。

[3.2.4建立您的歷程和訊息](./ex4.md)

將事件、資料來源和動作結合到智慧型與情境式歷程中。

[3.2.5觸發您的歷程](./ex5.md)

觸發您的特定歷程。

[摘要和優點](./summary.md)

本單元摘要和優點概觀。

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform及其應用程式的所有知識。 如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。

[返回所有模組](../../../overview.md)
