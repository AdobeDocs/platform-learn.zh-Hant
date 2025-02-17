---
title: 將Apache Kafka的資料串流至Adobe Experience Platform
description: 在本單元中，您將瞭解如何設定您自己的Apache Kafka叢集、定義主題、製作者和消費者，並使用Kafka Connect的Adobe Experience Platform Sink Connector將資料串流到Adobe Experience Platform。
kt: 5342
doc-type: tutorial
exl-id: 28c63675-272e-46ff-88fc-6cd4096d66ca
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# 2.6將Apache Kafka的資料串流至Adobe Experience Platform

在本單元中，您將瞭解如何設定您自己的Apache Kafka叢集、定義主題、製作者和消費者，以及透過Kafka Connect使用Adobe Experience Platform Sink Connector將資料串流到Adobe Experience Platform。

## 學習目標

- 執行本機Kafka叢集的基本設定
- 建立Kafka主題，使用Kafka製作者和Kafka消費者
- 設定Kafka連線和Adobe Experience Platform接收器聯結器
- 手動產生事件並檢視這些事件是否在Adobe Experience Platform中擷取
- 使用來自Kafka Connect的現有Twitter製作程式庫，將Twitter資料串流至Adobe Experience Platform

## 先決條件

- 您的電腦必須安裝Java JDK23或以上版本，您可以在此處下載該JDK： [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- 存取Adobe Experience Platform

>[!NOTE]
>
>別忘了安裝、設定和使用[安裝Chrome檔案的Chrome擴充功能](../../../getting-started/gettingstarted/ex1.md)中提到的Experience League擴充功能

## 練習

[2.6.1 Apache Kafka簡介](./ex1.md)

在本練習中，您將瞭解Apache Kafka的基礎知識

[2.6.2安裝及設定Kafka叢集](./ex2.md)

在本練習中，您將下載、安裝和設定基本的Apache Kafka叢集。

[2.6.3在Adobe Experience Platform中設定HTTP API串流端點](./ex3.md)

在本練習中，您將會在Adobe Experience Platform中設定HTTP API Source Connector 。

[2.6.4安裝並設定Kafka Connect和Adobe Experience Platform接收器聯結器](./ex4.md)

在本練習中，您將使用Kafka Connect來安裝並使用Adobe Experience Platform接收器聯結器，而且您將手動將事件傳送到Adobe Experience Platform。

[摘要和優點](./summary.md)

本單元摘要和優點概觀。

![技術內部人士](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform及其應用程式的所有知識。 如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。

[返回所有模組](./../../../../overview.md)
