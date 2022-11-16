---
title: Adobe Journey Optimizer — 外部氣象API、SMS動作等
description: Adobe Journey Optimizer — 外部氣象API、SMS動作等
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7f3d6dcb-845d-4ff1-97c3-8e93b8d2c624
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# 8.Adobe Journey Optimizer:外部資料來源和自訂動作

**作者： [沃特·范·蓋盧韋](https://www.linkedin.com/in/woutervangeluwe/)**

在本模組中，您將使用Adobe Journey Optimizer線上和離線監聽客戶行為，並以智慧、情境式和即時的方式回應。 您已在模組6中取得Adobe Journey Optimizer的初步實作體驗。 在本練習中，您將深入探討並探索更進階的使用案例，借此在歷程中使用外部資料來源。

## 學習目標

- 了解如何在Adobe Journey Optimizer中建立事件、外部資料來源和歷程
- 了解如何從Open Weather API使用天氣資訊
- 了解如何使用Twilio等自訂動作目的地，以及Adobe Journey Optimizer的Slack

## 先決條件

- 存取 Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 存取Adobe Journey Optimizer
- 存取開放天氣API

>[!IMPORTANT]
>
>本教學課程的建立是為了便於使用特定研討會格式。 它使用您可能沒有存取權的特定系統和帳戶。 即使沒有訪問權，我們仍然認為，通過閱讀這些非常詳細的內容，您仍可以學到很多。 如果您是其中一個研討會的參與者，並需要您的訪問認證，請聯繫您的Adobe代表，他將向您提供所需資訊。

## 架構概述

請查看下列架構，其中會強調本模組中將討論和使用的元件。

![架構概述](../../assets/images/architecturem12.png)

## 業務內容

身為品牌，您在個人化線上體驗方面投入巨資。 現在，您想要與離線體驗一樣情境化且相關。
在此模組中，您會透過在店內螢幕上向該客戶展示相關內容，利用客戶在離線商店的存在，在商店內提供個人化體驗，同時，我們也想要即時傳送個人化推送或簡訊給該客戶。
作為品牌，您也了解上下文會極大地影響客戶的興趣，因此您想要輸入該客戶位置的目前天氣資訊，以決定要顯示的內容或促銷。

## 要使用的沙箱

對於此模組，請使用此沙箱： `--aepSandboxId--`.

>[!NOTE]
>
>別忘了安裝、設定和使用Chrome擴充功能，如 [0.1 — 安裝Experience League檔案的Chrome擴充功能](../module0/ex1.md)

## 練習

[8.1定義事件](./ex1.md)

了解如何使用Adobe Journey Optimizer定義自訂事件。

[8.2定義外部資料來源](./ex2.md)

了解如何使用Adobe Journey Optimizer設定外部資料來源。

[8.3定義自訂動作](./ex3.md)

了解如何使用Adobe Journey Optimizer定義外部動作。

[8.4建立您的歷程和訊息](./ex4.md)

將事件、資料來源和動作結合為智慧型與情境式歷程。

[8.5觸發您的歷程](./ex5.md)

觸發您的特定歷程。

[摘要和優點](./summary.md)

本模組的摘要，以及優點的概述。

>[!NOTE]
>
>謝謝你花時間去學習關於Adobe Experience Platform的一切。 如果您有疑問，想要分享對未來內容有建議的一般性反饋，請直接聯繫Wouter Van Geluwe，方法是發送電子郵件至 **vangeluw@adobe.com**.

[返回所有模組](../../overview.md)
