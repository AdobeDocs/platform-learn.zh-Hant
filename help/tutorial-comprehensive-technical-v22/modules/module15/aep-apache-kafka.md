---
title: 將資料從Apache Kafka串流至Adobe Experience Platform
description: 在本模組中，您將學習如何使用Adobe Experience Platform Sink Connector for Kafka Connect來設定您自己的Apache Kafka叢集、定義主題、製作者和消費者，以及將資料串流至Adobe Experience Platform。
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: e1e283b1-93b7-4d06-b9ed-beac48a99c3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 1%

---

# 15.將資料從Apache Kafka流入Adobe Experience Platform

**作者： [維韋克蒂瓦里](https://www.linkedin.com/in/vivek-tiwari-25092656/), [尼本·奈爾](https://www.linkedin.com/in/nipunnair/), [沃特·范·蓋盧韋](https://www.linkedin.com/in/woutervangeluwe/)**

在本模組中，您將學習如何使用Adobe Experience Platform Sink Connector，透過Kafka Connect來設定您自己的Apache Kafka叢集、定義主題、製作者和消費者，以及將資料串流至Adobe Experience Platform。

## 學習目標

- 執行本地Kafka群集的基本設定
- 建立Kafka主題，使用Kafka製作人和Kafka消費者
- 配置Kafka Connect和Adobe Experience Platform Sink連接器
- 手動產生事件並查看這些事件在Adobe Experience Platform中擷取
- 使用來自Kafka Connect的現有Twitter製作程式庫，將Twitter資料串流至Adobe Experience Platform

## 先決條件

- 您的電腦上需要安裝Java JDK11或更高版本，您可以在此處下載該JDK: [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- 存取 Adobe Experience Platform

## 架構概述

請查看下列架構，其中會強調本模組中將討論和使用的元件。

![架構概述](../../assets/images/architecturem24.png)

## 要使用的沙箱

對於此模組，請使用此沙箱： `--aepSandboxId--`.

>[!NOTE]
>
>別忘了安裝、設定和使用Chrome擴充功能，如 [0.1 — 安裝Experience League檔案的Chrome擴充功能](../module0/ex1.md)

## 練習

[15.1 Apache Kafka簡介](./ex1.md)

在本練習中，您將了解Apache Kafka的基本知識

[15.2安裝和配置您的Kafka群集](./ex2.md)

在本練習中，您將下載、安裝和配置基本的Apache Kafka群集。

[15.3在Adobe Experience Platform中設定HTTP API串流端點](./ex3.md)

在本練習中，您將在Adobe Experience Platform中設定HTTP API來源連接器。

[15.4安裝並配置Kafka Connect和Adobe Experience Platform Sink Connector](./ex4.md)

在本練習中，您將使用Kafka Connect來安裝和使用Adobe Experience Platform Sink Connector ，並手動將事件發送到Adobe Experience Platform。

[摘要和優點](./summary.md)

本模組的摘要，以及優點的概述。

>[!NOTE]
>
>謝謝你花時間去學習關於Adobe Experience Platform的一切。 如果您有疑問，想要分享對未來內容有建議的一般性反饋，請直接聯繫Wouter Van Geluwe，方法是發送電子郵件至 **vangeluw@adobe.com**.

[返回所有模組](../../overview.md)
