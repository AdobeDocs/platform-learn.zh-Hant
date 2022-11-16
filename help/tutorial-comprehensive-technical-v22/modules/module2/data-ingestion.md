---
title: Foundation — 資料擷取
description: Foundation — 資料擷取
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: dbbc0539-ae1b-488d-b312-76a74d4d361f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---

# 2.基礎 — 資料擷取

**作者： [沃特·范·蓋盧韋](https://www.linkedin.com/in/woutervangeluwe/)**

在本模組中，目標是要了解所有資料擷取。 您將學習如何透過串流和批次匯入資料。 您將使用Launch實作串流資料擷取，讓實驗操作網站上的客戶行為即時串流至Adobe Experience Platform。 您將了解如何使用Adobe Experience Platform工作流程擷取CSV檔案、對應XDM結構，然後將其擷取至Adobe Experience Platform，以批次資料擷取。

## 學習目標

- 了解如何在Adobe Experience Platform中建立XDM結構
- 了解如何在Adobe Experience Platform中建立資料集
- 了解如何在Launch中建立串流端點並設定Adobe Experience Platform擴充功能
- 了解如何在Launch中建立規則，將資料串流至Adobe Experience Platform
- 了解如何將Adobe Experience Platform Launch整合至網頁
- 了解如何使用Adobe Experience Platform工作流程將CSV檔案擷取至Adobe Experience Platform

## 先決條件

- 存取 Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 存取Adobe Experience Platform Launch: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 存取 [https://public.aepdemo.net](https://public.aepdemo.net)
- 存取Postman

>[!IMPORTANT]
>
>本教學課程的建立是為了便於使用特定研討會格式。 它使用您可能沒有存取權的特定系統和帳戶。 即使沒有訪問權，我們仍然認為，通過閱讀這些非常詳細的內容，您仍可以學到很多。 如果您是其中一個研討會的參與者，並需要您的訪問認證，請聯繫您的Adobe代表，他將向您提供所需資訊。

## 架構概述

請查看下列架構，其中會強調本模組中將討論和使用的元件。

![架構概述](../../assets/images/architecturem2.png)

## 要使用的沙箱

對於此模組，請使用此沙箱： `--module2sandbox--`.

>[!NOTE]
>
>別忘了安裝、設定和使用Chrome擴充功能，如 [0.1 — 安裝Experience League檔案的Chrome擴充功能](../module0/ex1.md)

## 練習

[2.1瀏覽網站](./ex1.md)

在本練習中，您將探索將用於此培訓的網站。

[2.2設定結構和設定識別碼](./ex2.md)

在本練習中，您將設定必要的XDM結構，以擷取設定檔資訊和客戶行為。 在每個XDM結構中，您也必須設定主要識別碼，將所有資訊連結至。

[2.3設定資料集](./ex3.md)

在本練習中，您將擷取所需的資料集，以擷取和儲存設定檔資訊和客戶行為。

[2.4從離線來源擷取資料](./ex4.md)

在本練習中，您會前往網站和行動應用程式，並以客戶的方式行事，將資料串流至Platform。

[2.5資料登陸區](./ex5.md)

使用Azure Blob儲存設定您的資料著陸區來源連接器。

[摘要和優點](./summary.md)

本模組的摘要，以及優點的概述。

>[!NOTE]
>
>謝謝你花時間去學習關於Adobe Experience Platform的一切。 如果您有疑問，想要分享對未來內容有建議的一般性反饋，請直接聯繫Wouter Van Geluwe，方法是發送電子郵件至 **vangeluw@adobe.com**.

[返回所有模組](../../overview.md)
