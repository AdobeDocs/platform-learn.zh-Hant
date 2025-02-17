---
title: Audience Activation到Microsoft Azure事件中心
description: Audience Activation到Microsoft Azure事件中心
kt: 5342
doc-type: tutorial
exl-id: c1f5566d-0f57-4554-95ee-950d66373716
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 2.4 Real-Time CDP： Audience Activation至Microsoft Azure事件中心

在此單元中，您將設定Microsoft Azure EventHub目的地為Adobe Experience Platform Real-time CDP的即時目的地。 您也會設定和部署Azure函式，每當Adobe Experience Platform將對象裝載傳遞至Azure EventHub目的地時，就會即時觸發。 您即將觸發的Azure函式將會顯示Adobe Experience Platform Real-time CDP啟用功能的機制。

在此單元中，您也會瞭解什麼會觸發Real-time CDP將裝載實際傳送至指定目的地。 我們也會討論對象資格的狀態，以及它與啟用之間的關係。

Adobe Experience Platform Real-time CDP支援對串流雲端儲存空間目的地啟用資料，可讓您以JSON格式即時將對象資料和事件匯出到這些目的地。 接著，您就可以在目的地中針對這些事件說明商業邏輯

Microsoft Azure事件中樞是一項完全受管理的即時資料擷取服務，簡單、受信任且可擴充。 每秒從任何來源串流數百萬個事件以建置動態資料管道，並立即回應業務挑戰。

## 學習目標

- 熟悉Microsoft Azure事件中樞
- 設定RTCDP目的地至您的Microsoft Azure事件中樞
- 瞭解Real-time CDP何時啟用，以及啟用裝載的外觀
- 設定Visual Studio Code以開發、測試和部署您的Azure專案
- 建立並部署Azure函式，該函式會採用RTCDP即時提供的對象資格

## 先決條件

- 存取[Adobe Experience Platform](https://experience.adobe.com/platform)
- 瞭解如何在Adobe Experience Platform中定義、使用及啟用對象

>[!NOTE]
>
>別忘了安裝、設定和使用[安裝Chrome檔案的Chrome擴充功能](../../../getting-started/gettingstarted/ex1.md)中提到的Experience League擴充功能

## 練習

[2.4.1設定環境](./ex1.md)

在本練習中，您將設定您的Microsoft Azure環境。

[2.4.2設定您的Microsoft Azure EventHub環境](./ex2.md)

在本練習中，您將設定您的Microsoft Azure EventHub環境。

[2.4.3在Adobe Experience Platform中設定Azure事件中樞目的地](./ex3.md)

在本練習中，您將設定您的Real-time CDP目標連線，以將對象即時傳送至您在上一個練習中已設定的事件中心執行個體。

[2.4.4建立對象](./ex4.md)

在本練習中，您將會在Adobe Experience Platform中建立受眾

[2.4.5啟用您的對象](./ex5.md)

在本練習中，您將會在EventHub目的地啟用對象。

[2.4.6建立您的Microsoft Azure專案](./ex6.md)

在本練習中，您將建立一個Azure函式，當Adobe Experience Platform將對象資格提供給相對應的Azure事件中樞目的地時，就會即時觸發。

[2.4.7端對端案例](./ex7.md)

此時，一切都已設定。 您現在可以在示範網站上進行瀏覽，並將對象資格傳送至您的Microsoft Azure事件中心觸發程式功能。

[摘要和優點](./summary.md)

本單元摘要和優點概觀。

![技術內部人士](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform及其應用程式的所有知識。 如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。

[返回所有模組](./../../../../overview.md)
