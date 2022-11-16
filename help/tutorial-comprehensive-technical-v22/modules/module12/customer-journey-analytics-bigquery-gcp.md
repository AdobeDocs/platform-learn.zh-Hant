---
title: 使用BigQuery Source Connector在Adobe Experience Platform中內嵌和分析Google Analytics資料
description: 使用BigQuery Source Connector在Adobe Experience Platform中內嵌和分析Google Analytics資料
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c9c28b5a-d158-49fa-9533-1a295876f6c4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---

# 12.使用BigQuery Source Connector在Adobe Experience Platform中擷取及分析Google Analytics資料

**作者： [維克托·德·拉·伊格萊西亞](https://www.linkedin.com/in/victordelaiglesia/), [沃特·范·蓋盧韋](https://www.linkedin.com/in/woutervangeluwe/)**

在本模組中，您將設定自己的Google Cloud Platform例項，在Google Cloud Platform中載入範例資料，然後使用BigQuery Source Connector，將該資料從Google Cloud Platform內嵌至Adobe Experience Platform。 最後，您將使用Customer Journey Analytics來視覺化該資料。

Adobe Experience Platform的來源連接器讓將資料匯入Adobe Experience Platform的程式更簡單。 Google BigQuery是已可用的連接器之一。 有了Adobe Experience Platform和BigQuery Source Connector，我們現在可以將Google Analytics資料以Customer Journey Analytics方式匯入Analysis Workspace。

此外，我們可以將Google Analytics資料與其他資料來源(例如CRM、客服中心或Customer Journey Analytics內的忠誠度資料)結合，以豐富這些資料。

## 學習目標

- 熟悉Google雲端平台和BigQuery使用者介面
- 將 Google Analytics 資料擷取至 Adobe Experience Platform
- 使用Customer Journey Analytics執行Google Analytics資料分析
- 以離線資料豐富Google Analytics資料

## 先決條件

- 最好熟悉Customer Journey Analytics，但不需要
- 存取Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Customer Journey Analytics 的存取權
- 存取Google Cloud Platform和Google BigQuery
- **下載這些資產**:
   - [JSON — 範例資料：忠誠度資料](./../../assets/json/bqLoyalty.json)

>[!IMPORTANT]
>
>本教學課程的建立是為了便於使用特定研討會格式。 它使用您可能沒有存取權的特定系統和帳戶。 即使沒有訪問權，我們仍然認為，通過閱讀這些非常詳細的內容，您仍可以學到很多。 如果您是其中一個研討會的參與者，並需要您的訪問認證，請聯繫您的Adobe代表，他將向您提供所需資訊。

## 架構概述

請查看下列架構，其中會強調本模組中將討論和使用的元件。

![架構概述](../../assets/images/architecturem16.png)

## 要使用的沙箱

對於此模組，請使用此沙箱： `--aepSandboxId--`.

>[!NOTE]
>
>別忘了安裝、設定和使用Chrome擴充功能，如 [0.1 — 安裝Experience League檔案的Chrome擴充功能](../module0/ex1.md)

## 練習

[12.1建立您的Google雲端平台帳戶](./ex1.md)

建立您的Google Cloud Platform帳戶。

[12.2在BigQuery中建立第一個查詢](./ex2.md)

了解如何使用BigQuery來準備資料以載入Platform。

[12.3將GCP和BigQuery連接到Adobe Experience Platform](./ex3.md)

了解如何在Adobe Experience Platform中設定來源連接器。

[12.4將資料從BigQuery載入Adobe Experience Platform](./ex4.md)

了解如何在Adobe Experience Platform中設定BigQuery來源連接器，以內嵌您的Google Analytics資料。

[12.5使用Google Analytics分析Customer Journey Analytics資料](./ex5.md)

了解如何分析Customer Journey Analytics中的Google Analytics資料，並將其與忠誠度資料結合。

[摘要和優點](./summary.md)

本模組的摘要，以及優點的概述。

>[!NOTE]
>
>謝謝你花時間去學習關於Adobe Experience Platform的一切。 如果您有疑問，想要分享對未來內容有建議的一般性反饋，請直接聯繫Wouter Van Geluwe，方法是發送電子郵件至 **vangeluw@adobe.com**.

[返回所有模組](../../overview.md)
