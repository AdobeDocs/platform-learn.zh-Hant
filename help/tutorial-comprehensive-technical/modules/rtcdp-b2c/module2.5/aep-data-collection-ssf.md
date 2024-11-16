---
title: Adobe Experience Platform資料收集和即時伺服器端轉送
description: 在此單元中，您會使用先前設定的資料集、結構描述和Adobe Experience Platform資料收集伺服器屬性來收集資料，然後將該資料伺服器端轉送至所選擇的端點。
kt: 5342
doc-type: tutorial
exl-id: aa3ab1eb-6fee-4ea9-9a0d-0d8ca803d7c2
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# 2.5 Real-Time CDP連線：事件轉送

**作者：[Wouter Van Greuwe](https://www.linkedin.com/in/woutervangeluwe/)，[Clement Delalande](https://www.linkedin.com/in/clement-delalande/)**

在此單元中，您會使用先前設定的資料集、結構描述和Adobe Experience Platform資料收集使用者端屬性來收集資料，然後將該資料伺服器端轉送至所選擇的端點。

在本單元中，您將：

- 建立Adobe Experience Platform資料收集伺服器屬性
- 在Adobe Experience Platform資料彙集中安裝並使用Adobe Cloud Connector擴充功能
- 建立Google函式端點，並將資料串流至該端點
- 建立AWS端點並為其串流資料

觀看此影片以瞭解價值、客戶歷程和設定程式：

>[!VIDEO](https://video.tv.adobe.com/v/331987?quality=12&learn=on)

## 學習目標

- 熟悉Adobe Experience Platform資料收集伺服器屬性和新的Adobe Cloud Connector擴充功能
- 瞭解如何在Google和AWS等第三方解決方案中重複使用Adobe Experience Platform Web SDK資料
- 瞭解Adobe Experience Platform資料收集和伺服器端轉送的架構。

## 先決條件

- 存取Adobe Experience Platform和Adobe Experience Platform資料收集
- 瞭解Adobe Experience Platform資料集和XDM

>[!NOTE]
>
>別忘了安裝、設定及使用[安裝Chrome擴充功能以取得Experience League檔案](../../gettingstarted/gettingstarted/ex1.md)中參考的Chrome擴充功能

## 練習

[2.5.1建立資料收集事件轉送屬性](./ex1.md)

在本練習中，您將建立您的Adobe Experience Platform資料收集事件轉送屬性。

[2.5.2更新您的資料串流，讓您的資料收集事件轉送屬性可以使用資料](./ex2.md)

在本練習中，您將更新現有的資料流，讓Adobe Experience Platform資料收集使用者端屬性收集的資料可供Adobe Experience Platform資料收集伺服器屬性使用。

[2.5.3建立和設定自訂webhook](./ex3.md)

在本練習中，您將建立並設定自訂webhook，並且開始將Web SDK收集的資料轉送至該自訂webhook。

[2.5.4建立及設定Google雲端功能](./ex4.md)

在本練習中，您將建立並設定Google雲端功能，並將開始將Web SDK收集的資料轉送至Google。

[2.5.5前往AWS生態系統推進事件](./ex5.md)

在本練習中，您將使用AWS API Gateway、AWS Kinesis、AWS Firehose和AWS S3設定您的AWS環境，之後您將開始轉送Web SDK收集的事件資料。

[摘要和優點](./summary.md)

本單元摘要和優點概觀。

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform及其應用程式的所有知識。 如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。

[返回所有模組](../../../overview.md)
