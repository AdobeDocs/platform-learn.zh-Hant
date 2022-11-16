---
title: Adobe Experience Platform資料收集與即時伺服器端轉送
description: 在本模組中，您將使用先前設定的資料集、結構描述和Adobe Experience Platform資料收集伺服器屬性來收集資料，然後將該資料伺服器端轉送至您所選擇的端點。
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c157ca52-c84f-4398-a658-2b6067e41707
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# 十四、Real-Time CDP聯繫：事件轉送

**作者： [沃特·范·蓋盧韋](https://www.linkedin.com/in/woutervangeluwe/), [克萊門特·德拉蘭德](https://www.linkedin.com/in/clement-delalande/)**

在本模組中，您將使用先前設定的資料集、結構描述和Adobe Experience Platform資料收集用戶端屬性來收集資料，然後將該資料從伺服器端轉送至您選擇的端點。

在此模組中，您會：

- 建立Adobe Experience Platform資料收集伺服器屬性
- 在Adobe Experience Platform Data Collection中安裝及使用Adobe雲端連接器擴充功能
- 建立Google函式端點並將資料串流至該端點
- 建立AWS端點並將資料串流至該端點

請觀看此影片，了解價值、客戶歷程和設定程式：

>[!VIDEO](https://video.tv.adobe.com/v/331987?quality=12&learn=on)

## 學習目標

- 熟悉Adobe Experience Platform資料收集伺服器屬性和新的Adobe雲端連接器擴充功能
- 了解如何在Google和AWS等第三方解決方案中重複使用Adobe Experience Platform Web SDK資料
- 了解Adobe Experience Platform資料收集和伺服器端轉送背後的架構。

## 先決條件

- 存取Adobe Experience Platform和Adobe Experience Platform資料收集
- 了解Adobe Experience Platform資料集和XDM

>[!IMPORTANT]
>
>本教學課程的建立是為了便於使用特定研討會格式。 它使用您可能沒有存取權的特定系統和帳戶。 即使沒有訪問權，我們仍然認為，通過閱讀這些非常詳細的內容，您仍可以學到很多。 如果您是其中一個研討會的參與者，並需要您的訪問認證，請聯繫您的Adobe代表，他將向您提供所需資訊。

## 架構概述

請查看下列架構，其中會強調本模組中將討論和使用的元件。

![架構概述](../../assets/images/architecturem21.png)

## 要使用的沙箱

對於此模組，請使用此沙箱： `--aepSandboxId--`.

>[!NOTE]
>
>別忘了安裝、設定和使用Chrome擴充功能，如 [0.1 — 安裝Experience League檔案的Chrome擴充功能](../module0/ex1.md)

## 練習

[14.1建立資料收集事件轉送屬性](./ex1.md)

在本練習中，您將建立Adobe Experience Platform資料收集事件轉送屬性。

[14.2更新您的資料流，讓資料可供您的資料收集事件轉送屬性使用](./ex2.md)

在本練習中，您將更新現有的Datastream，讓Adobe Experience Platform資料收集用戶端屬性所收集的資料可供Adobe Experience Platform資料收集伺服器屬性使用。

[14.3建立和設定自訂網頁鈎點](./ex3.md)

在本練習中，您將建立並設定自訂WebHook，然後開始將Web SDK收集的資料轉送至該自訂WebHook。

[14.4建立和設定Google雲端函式](./ex4.md)

在本練習中，您將建立並設定Google雲端函式，然後開始將Web SDK所收集的資料轉送至Google。

[14.5向AWS生態系統發展的前進活動](./ex5.md)

在本練習中，您將使用AWS API閘道、AWS Kinesis、AWS Firehose和AWS S3來設定AWS環境，之後您將開始轉送Web SDK所收集的事件資料。

[摘要和優點](./summary.md)

本模組的摘要，以及優點的概述。

>[!NOTE]
>
>謝謝你花時間去學習關於Adobe Experience Platform的一切。 如果您有疑問，想要分享對未來內容有建議的一般性反饋，請直接聯繫Wouter Van Geluwe，方法是發送電子郵件至 **vangeluw@adobe.com**.

[返回所有模組](../../overview.md)
