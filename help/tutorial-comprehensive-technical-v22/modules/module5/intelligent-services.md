---
title: Intelligent Services
description: Intelligent Services
kt: 5342
audience: Data Engineer, Data Architect, Data Scientist
doc-type: tutorial
activity: develop
exl-id: 99b56722-95bf-4c51-b4d6-8b5a8e5fd936
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# 5. Intelligent Services

**作者： [迪皮曼·巴達耶納](https://www.linkedin.com/in/diptiman-badajena-1b178019/), [沃特·范·蓋盧韋](https://www.linkedin.com/in/woutervangeluwe/)**

在本模組中，您將學習如何設定、設定和使用Adobe Experience Platform Intelligent Services。

## 學習目標

- 熟悉Adobe Experience Platform
- 設定結構/資料集以與Intelligent Services搭配使用
- 建立新的Customer AI例項
- 計分控制面板和區段

## 先決條件

- 存取 Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

>[!IMPORTANT]
>
>本教學課程的建立是為了便於使用特定研討會格式。 它使用您可能沒有存取權的特定系統和帳戶。 即使沒有訪問權，我們仍然認為，通過閱讀這些非常詳細的內容，您仍可以學到很多。 如果您是其中一個研討會的參與者，並需要您的訪問認證，請聯繫您的Adobe代表，他將向您提供所需資訊。

## 架構概述

請查看下列架構，其中會強調本模組中將討論和使用的元件。

![架構概述](../../assets/images/architecturem5.png)

## 要使用的沙箱

對於此模組，請使用此沙箱： `--module10sandbox--`.

>[!NOTE]
>
>別忘了安裝、設定和使用Chrome擴充功能，如 [0.1 — 安裝Experience League檔案的Chrome擴充功能](../module0/ex1.md)

## 練習

[5.1 Customer AI — 資料準備（擷取）](./ex1.md)

客戶資料會透過Adobe Experience Platform上的Experience Data Model(XDM)進行擷取和轉換。 尤其是Intelligent Services中使用的所有資料集，都必須符合Consumer ExperienceEvent(CEE)XDM結構。

[5.2 Customer AI — 建立新執行個體（設定）](./ex2.md)

行銷分析人員會指定業務規則並識別相關資料，以設定所需的預測。 設定模型後，請排程執行和檢閱分數。

[5.3客戶AI — 計分控制面板和區段（預測並採取動作）](./ex3.md)

在模型完成訓練和計分後，分數會寫回Platform。 您可以決定要使用預測採取的動作，例如定義區段、建立自訂控制面板等。

>[!NOTE]
>
>謝謝你花時間去學習關於Adobe Experience Platform的一切。 如果您有疑問，想要分享對未來內容有建議的一般性反饋，請直接聯繫Wouter Van Geluwe，方法是發送電子郵件至 **vangeluw@adobe.com**.

[返回所有模組](../../overview.md)
