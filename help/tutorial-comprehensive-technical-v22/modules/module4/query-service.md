---
title: 查詢服務
description: 查詢服務
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 74943e52-8a7e-4db7-9407-7deeab008fa7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---

# 4.查詢服務

**作者： [馬克·米維斯](https://www.linkedin.com/in/marcmeewis/), [沃特·范·蓋盧韋](https://www.linkedin.com/in/woutervangeluwe/)**

在此模組中，您將可取得Adobe Experience Platform Query Service的實作預覽。 Query Service可讓您跨所有Adobe Experience Cloud應用程式資料執行全通路查詢，跨Adobe Campaign、Analytics、Audience Manager、Target和Advertising Cloud加入和分析資料，以及載入/插入Adobe Experience Platform的其他客戶資料。

查詢服務是無伺服器工具。 它通過其PostgreSQL相容性支援來自多個客戶端應用程式的SQL查詢和連接。
我們將使用已插入平台的資料，包括網路互動資料、客服中心互動，以及已上傳至平台的客戶忠誠度資料。

## 學習目標

- 熟悉Adobe Experience Platform UI
- 連接到查詢服務並運行SQL查詢
- 在Adobe Experience Platform中探索資料集
- 將Tableau或Power BI連結至Adobe Experience Platform查詢服務，以建立視覺效果和報表

## 先決條件

- 最好是熟悉SQL，但不需要
- 存取Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 資料集（實驗期間使用的資料集，已為您預先載入）
- PostgreSQL
- Tableau或MicrosoftPower BI案頭
- **下載這些資產**:
   - [JSON — 範例資料：網站互動](./../../assets/json/ee.json)
   - [JSON — 範例資料：客服中心互動](./../../assets/json/callcenter.json)
   - [JSON — 範例資料：忠誠度](./../../assets/json/loyalty.json)

>[!IMPORTANT]
>
>本教學課程的建立是為了便於使用特定研討會格式。 它使用您可能沒有存取權的特定系統和帳戶。 即使沒有訪問權，我們仍然認為，通過閱讀這些非常詳細的內容，您仍可以學到很多。 如果您是其中一個研討會的參與者，並需要您的訪問認證，請聯繫您的Adobe代表，他將向您提供所需資訊。

## 架構概述

請查看下列架構，其中會強調本模組中將討論和使用的元件。

![架構概述](../../assets/images/architecturem7.png)

## 要使用的沙箱

對於此模組，請使用此沙箱： `--module7sandbox--`.

>[!NOTE]
>
>別忘了安裝、設定和使用Chrome擴充功能，如 [0.1 — 安裝Experience League檔案的Chrome擴充功能](../module0/ex1.md)

## 練習

[4.0先決條件](./ex0.md)

您需要安裝PSQL才能執行本啟用練習中的查詢。 視您的作業系統而定，您必須安裝MicrosoftPower BI或Tableau。 Windows使用者可在Power BI或Tableau之間選擇。 Mac使用者應安裝Tableau。

[4.1快速入門](./ex1.md)

在本練習中，您將探索Adobe Experience Platform Query Service使用者介面、了解資料集、尋找查詢，最後從PSQL設定連線。

[4.2使用查詢服務](./ex2.md)

在本練習中，您將了解基本的查詢服務語法，並可在查詢中識別XDM結構的屬性。

[4.3查詢、查詢、查詢……和流失分析](./ex3.md)

在本練習中，您將執行查詢，同時執行Adobe分析時，將了解「定義函式」。 在結尾處，您會撰寫查詢來準備資料集，以用於MicrosoftPower BI。

[4.4從查詢產生資料集](./ex4.md)

在本練習中，您將從上一個練習中執行的查詢產生資料集，並在下一個練習中使用此資料集。

[4.5查詢服務和Power BI](./ex5.md)

在本練習中，您將將Power BI連接到Adobe Experience Platform和Query Service以執行Callcenter交互分析。

[4.6查詢服務和Tableau](./ex6.md)

在本練習中，您會將Tableau連結至Adobe Experience Platform和Query Service，以執行Callcenter互動分析。

[4.7查詢服務API](./ex7.md)

在本練習中，您將使用查詢服務API來管理查詢模板和查詢計畫。

[摘要和優點](./summary.md)

本模組的摘要，以及優點的概述。

>[!NOTE]
>
>謝謝你花時間去學習關於Adobe Experience Platform的一切。 如果您有疑問，想要分享對未來內容有建議的一般性反饋，請直接聯繫Wouter Van Geluwe，方法是發送電子郵件至 **vangeluw@adobe.com**.

[返回所有模組](../../overview.md)
