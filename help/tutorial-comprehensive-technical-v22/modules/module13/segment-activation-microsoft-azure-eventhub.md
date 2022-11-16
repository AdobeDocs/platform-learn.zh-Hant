---
title: 區段啟動至Microsoft Azure事件中心
description: 區段啟動至Microsoft Azure事件中心
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 73c2576d-0a69-4d56-a671-9ae1f75580b9
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# 13.Real-Time CDP:區段啟動至Microsoft Azure事件中心

**作者： [馬克·米維斯](https://www.linkedin.com/in/marcmeewis/), [沃特·范·蓋盧韋](https://www.linkedin.com/in/woutervangeluwe/)**

在此模組中，您將設定Microsoft Azure EventHub目的地，作為Adobe Experience Platform即時CDP的即時目的地。 您也將設定並部署Azure函式，每當Adobe Experience Platform將區段裝載傳送至您的Azure EventHub目的地時，即時觸發此函式。 您將觸發的Azure函式將顯示Adobe Experience Platform Real-time CDP啟用功能的機制。

在此模組中，您也將能了解觸發即時CDP將裝載實際傳送至指定目的地的原因。 我們也將討論區段資格的狀態及其與啟動的相關性。

Adobe Experience Platform Real-time CDP支援對串流雲端儲存目的地進行資料啟動，讓您能以JSON格式即時將受眾資料和事件匯出至這些目的地。 然後，您就可以在目的地的這些事件上說明業務邏輯

Microsoft Azure Event Hubs是一種完全管理、即時的資料獲取服務，簡單、受信任且可擴展。 每秒從任何源流傳送數百萬個事件，以構建動態資料管道，並立即應對業務挑戰。

## 學習目標

- 熟悉Microsoft Azure事件中心
- 設定到Microsoft Azure事件中心的RTCDP目標
- 了解Real-time CDP何時啟動，以及啟動裝載的外觀
- 設定Visual Studio代碼以開發、測試和部署您的Azure項目
- 建立並部署Azure函式，該函式佔用RTCDP即時提供的段資格

## 先決條件

- 存取 [Adobe Experience Platform](https://experience.adobe.com/platform)
- 熟悉AEP示範網站環境
- 了解如何定義、使用和啟用Adobe Experience Platform中的串流區段

>[!IMPORTANT]
>
>本教學課程的建立是為了便於使用特定研討會格式。 它使用您可能沒有存取權的特定系統和帳戶。 即使沒有訪問權，我們仍然認為，通過閱讀這些非常詳細的內容，您仍可以學到很多。 如果您是其中一個研討會的參與者，並需要您的訪問認證，請聯繫您的Adobe代表，他將向您提供所需資訊。

## 架構概述

請查看下列架構，其中會強調本模組中將討論和使用的元件。

![架構概述](../../assets/images/architecturem18.png)

## 要使用的沙箱

對於此模組，請使用此沙箱： `--module18sandbox--`.

>[!NOTE]
>
>別忘了安裝、設定和使用Chrome擴充功能，如 [0.1 — 安裝Experience League檔案的Chrome擴充功能](../module0/ex1.md)

## 練習

[13.0配置環境](./ex0.md)

在本練習中，您將設定您的Microsoft Azure環境。

[13.1配置您的Microsoft Azure EventHub環境](./ex1.md)

在本練習中，您將設定您的Microsoft Azure EventHub環境。

[13.2在Adobe Experience Platform中設定您的Azure事件中樞目的地](./ex2.md)

在本練習中，您將設定您的即時CDP目標連接，該連接將即時將區段傳送到您在上次練習中設定的EventHub。

[13.3建立區段](./ex3.md)

在本練習中，您將在Adobe Experience Platform中建立串流區段

[13.4啟用區段](./ex4.md)

在本練習中，您會將串流區段啟用至您的即時CDP EventHub目的地。

[13.5建立您的Microsoft Azure專案](./ex5.md)

在本練習中，您將建立Azure函式，當Adobe Experience Platform將區段資格啟用至對應的Azure事件中心目的地時，即時觸發此函式。

[13.6端到端方案](./ex6.md)

現在，一切都已設定完畢。 您現在可以在AEP示範網站上瀏覽，並取得區段資格並傳送至Microsoft Azure EventHub觸發程式功能。

[摘要和優點](./summary.md)

本模組的摘要，以及優點的概述。

>[!NOTE]
>
>謝謝你花時間去學習關於Adobe Experience Platform的一切。 如果您有疑問，想要分享對未來內容有建議的一般性反饋，請直接聯繫Wouter Van Geluwe，方法是發送電子郵件至 **vangeluw@adobe.com**.

[返回所有模組](../../overview.md)
