---
title: Microsoft Azure事件中心的區段啟用
description: Microsoft Azure事件中心的區段啟用
kt: 5342
doc-type: tutorial
exl-id: 23713cb4-2055-43e8-9380-0ca8845a75e8
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# 2.4 Real-Time CDP：Microsoft Azure事件中心的區段啟用

**作者：[Marc Meewis](https://www.linkedin.com/in/marcmeewis/)，[Wouter Van Greuwe](https://www.linkedin.com/in/woutervangeluwe/)**

在此單元中，您將設定Microsoft Azure EventHub目的地為Adobe Experience Platform Real-time CDP的即時目的地。 您也將設定和部署Azure函式，每當Adobe Experience Platform將區段裝載傳遞至Azure EventHub目的地時，就會即時觸發。 您即將觸發的Azure函式將會顯示Adobe Experience Platform Real-time CDP啟用功能的機制。

在此單元中，您也會瞭解什麼會觸發Real-time CDP將裝載實際傳送至指定目的地。 我們也會討論區段資格的狀態，以及其與啟用的關係。

Adobe Experience Platform Real-time CDP支援對串流雲端儲存空間目的地啟用資料，可讓您以JSON格式即時將對象資料和事件匯出到這些目的地。 接著，您就可以在目的地中針對這些事件說明商業邏輯

Microsoft Azure事件中樞是一項完全受管理的即時資料擷取服務，簡單、受信任且可擴充。 每秒從任何來源串流數百萬個事件以建置動態資料管道，並立即回應業務挑戰。

## 學習目標

- 熟悉Microsoft Azure事件中樞
- 設定RTCDP目的地至您的Microsoft Azure事件中樞
- 瞭解Real-time CDP何時啟用，以及啟用裝載的外觀
- 設定Visual Studio Code以開發、測試和部署您的Azure專案
- 建立並部署Azure函式，該函式會使用RTCDP即時提供的區段資格

## 先決條件

- 存取[Adobe Experience Platform](https://experience.adobe.com/platform)
- 熟悉AEP示範網站環境
- 瞭解如何定義、使用及啟用Adobe Experience Platform中的串流區段

>[!NOTE]
>
>別忘了安裝、設定及使用[安裝Chrome擴充功能以取得Experience League檔案](../../gettingstarted/gettingstarted/ex1.md)中參考的Chrome擴充功能

## 練習

[2.4.0設定環境](./ex0.md)

在本練習中，您將設定您的Microsoft Azure環境。

[2.4.1設定您的Microsoft Azure EventHub環境](./ex1.md)

在本練習中，您將設定您的Microsoft Azure EventHub環境。

[2.4.2在Adobe Experience Platform中設定Azure事件中樞目的地](./ex2.md)

在本練習中，您將設定您的Real-time CDP目標連線，以便將區段即時傳送至您在上一個練習中已設定的EventHub。

[2.4.3建立區段](./ex3.md)

在本練習中，您將會在Adobe Experience Platform中建立串流區段

[2.4.4啟用區段](./ex4.md)

在本練習中，您將會對Real-time CDP EventHub目的地啟用串流區段。

[2.4.5建立您的Microsoft Azure專案](./ex5.md)

在本練習中，您將建立一個Azure函式，當Adobe Experience Platform對相對應的Azure事件中心目的地啟用區段資格時，該函式將即時觸發。

[2.4.6端對端案例](./ex6.md)

此時，一切都已設定。 您現在可以在AEP示範網站上進行瀏覽，並取得已傳送至Microsoft Azure EventHub Trigger函式的區段資格。

[摘要和優點](./summary.md)

本單元摘要和優點概觀。

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform及其應用程式的所有知識。 如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。

[返回所有模組](../../../overview.md)
