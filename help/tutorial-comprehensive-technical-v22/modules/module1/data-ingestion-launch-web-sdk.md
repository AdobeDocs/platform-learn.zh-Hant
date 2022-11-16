---
title: 1.Adobe Experience Platform資料收集與Web SDK擴充功能的設定
description: Foundation — 設定Adobe Experience Platform資料收集與Web SDK擴充功能
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 86da7132-cb06-4be3-b6b8-ea3ab937e6dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 1. Foundation — 設定Adobe Experience Platform資料收集與Web SDK擴充功能

**作者： [馬修·約瑟夫·伍利](https://www.linkedin.com/in/matthewjwoolley/), [沃特·范·蓋盧韋](https://www.linkedin.com/in/woutervangeluwe/)**

本基礎模組會向您介紹Adobe的資料收集願景，並說明如何透過Adobe Experience Platform資料收集、Adobe Experience Platform SDK和Adobe Experience Platform Edge Network，將資料從網站和行動應用程式匯入Adobe Experience Platform和其他應用程式。 本模組介紹一些概念和技術，這些概念和技術的影響超出Adobe Experience Platform技術教學課程的範圍。 請務必清楚了解這些練習的哪些部分是完整教學課程的其餘部分的基礎，這些教學課程會詳細教您如何了解Experience Edge及其功能，以及如何取得詳細資訊和教學課程。

## 學習目標

- 了解品牌如何使用Adobe Experience Platform資料收集作為其Tag Management系統(TMS)。
- 了解品牌用來將資料內嵌至其Adobe產品的資料流程。
- 了解如何透過Adobe Experience Platform Edge Network將資料傳送至Adobe Experience Platform和其他產品。
- 了解如何建立可從網頁和行動裝置收集資料的資料元素和規則。
- 了解Web SDK追蹤事件，以及如何偵錯其內容。
- 了解資料層是什麼，以及實作資料層時Adobe有何建議。
- 從草稿開始了解實作Web SDK的步驟。
- 了解網頁和行動實作之間的差異。

## 先決條件

- 存取 Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 存取Adobe Experience Platform資料收集： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 存取示範網站

>[!IMPORTANT]
>
>本教學課程的建立是為了便於使用特定研討會格式。 它使用您可能沒有存取權的特定系統和帳戶。 即使沒有訪問權，我們仍然認為，通過閱讀這些非常詳細的內容，您仍可以學到很多。 如果您是其中一個研討會的參與者，並需要您的訪問認證，請聯繫您的Adobe代表，他將向您提供所需資訊。

## 架構概述

請查看下列架構，其中會強調本模組中將討論和使用的元件。

![架構概述](../../assets/images/architecturem1.png)

## 要使用的沙箱

對於此模組，請使用此沙箱： `--aepSandboxId--`.

>[!NOTE]
>
>別忘了安裝、設定和使用Chrome擴充功能，如 [0.1 — 安裝Experience League檔案的Chrome擴充功能](../module0/ex1.md)

## 練習

[1.1了解Adobe Experience Platform資料收集](./ex1.md)

在本練習中，請探索Adobe Experience Platform資料收集UI，並了解其功能。

[1.2邊緣網路、資料流和伺服器端資料收集](./ex2.md)

在本練習中，您將學習如何在Adobe Experience Platform資料收集介面中將資料轉送至Adobe產品，並調查示範網站使用的資料流。

[1.3Adobe Experience Platform資料收集簡介](./ex3.md)

在本練習中，您將學習如何設定擴充功能、建立資料元素和規則，並將它們發佈至網頁。

[1.4用戶端Web資料收集](./ex4.md)

在本練習中，對已安裝的Web SDK進行除錯，以了解其運作方式，以及將來練習中將使用哪些資料。

[1.5實作Adobe Analytics和Adobe Audience Manager](./ex5.md)

在本練習中，請參閱並使用Adobe Analytics和Adobe Audience Manager中透過Web SDK收集的網頁資料。

[1.6實作Adobe Target](./ex6.md)

在本練習中，在Adobe Target中設定活動，透過Web SDK實作。

[1.7Adobe Experience Platform的XDM結構需求](./ex7.md)

為確保Web SDK和alloy.js能將資料內嵌至Adobe Experience Platform中，特定XDM Mixin必須成為Adobe Experience Platform中XDM結構的一部分。

[摘要和優點](./summary.md)

本模組的摘要，以及優點的概述。

>[!NOTE]
>
>謝謝你花時間去學習關於Adobe Experience Platform的一切。 如果您有疑問，想要分享對未來內容有建議的一般性反饋，請直接聯繫Wouter Van Geluwe，方法是發送電子郵件至 **vangeluw@adobe.com**.

[返回所有模組](../../overview.md)
