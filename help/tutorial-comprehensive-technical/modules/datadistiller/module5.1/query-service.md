---
title: 查詢服務
description: 查詢服務
kt: 5342
doc-type: tutorial
exl-id: 6eb65de3-d0e8-49d4-a702-5c9d6a1952b7
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# 5.1查詢服務

**作者：[Marc Meewis](https://www.linkedin.com/in/marcmeewis/)，[Wouter Van Greuwe](https://www.linkedin.com/in/woutervangeluwe/)**

在本單元中，您將實際預覽Adobe Experience Platform查詢服務。 查詢服務可讓您對所有Adobe Experience Cloud應用程式資料執行全通道查詢，加入及分析跨Adobe Campaign、Analytics、Audience Manager、Target和Advertising Cloud的資料，以及其他載入/插入Adobe Experience Platform的客戶資料。

查詢服務是一種無伺服器工具。 透過其PostgreSQL相容性，支援來自多個使用者端應用程式的SQL查詢和連線。
我們將使用已透過網頁互動資料、客服中心互動及上傳至平台之客戶忠誠度資料，整合至平台的資料。

## 學習目標

- 熟悉Adobe Experience Platform UI
- 連線到查詢服務並執行您的SQL查詢
- 探索Adobe Experience Platform中的資料集
- 將Tableau或Power BI連線至Adobe Experience Platform查詢服務，以建立視覺效果和報表

## 先決條件

- 建議您先熟悉SQL，但不需要
- 存取Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 資料集（實驗室期間使用的資料集，為您預先載入）
- PostgreSQL
- Tableau或MicrosoftPower BI案頭
- **下載這些資產**：
   - [JSON — 範例資料：網站互動](./../../../assets/json/ee.json)
   - [JSON — 範例資料：客服中心互動](./../../../assets/json/callcenter.json)
   - [JSON — 範例資料：忠誠度](./../../../assets/json/loyalty.json)

>[!NOTE]
>
>別忘了安裝、設定及使用[安裝Chrome擴充功能以取得Experience League檔案](../../gettingstarted/gettingstarted/ex1.md)中參考的Chrome擴充功能

## 練習

[5.1.0必要條件](./ex0.md)

您必須安裝PSQL，才能執行此啟用練習中的查詢。 根據您的作業系統，您必須安裝MicrosoftPower BI或Tableau。 Windows使用者可以選擇Power BI或Tableau。 Mac使用者應安裝Tableau。

[5.1.1快速入門](./ex1.md)

在本練習中，您將探索Adobe Experience Platform查詢服務使用者介面、瞭解資料集、尋找您的查詢，以及最終設定來自PSQL的連線。

[5.1.2使用查詢服務](./ex2.md)

在本練習中，您將瞭解基本查詢服務語法，並可以在查詢中識別XDM結構的屬性。

[5.1.3查詢、查詢、查詢……和流失分析](./ex3.md)

在本練習中，您將進行查詢，在進行某些流失分析時會瞭解Adobe定義的函式。 最後，您將撰寫查詢以準備資料集，以便用於MicrosoftPower BI。

[5.1.4從查詢產生資料集](./ex4.md)

在本練習中，您將會從上一個執行的查詢產生資料集，並在下一個練習中使用此資料集。

[5.1.5查詢服務與Power BI](./ex5.md)

在本練習中，您會將Power BI連線至Adobe Experience Platform和查詢服務，以執行Callcenter互動分析。

[5.1.6 Query Service和Tableau](./ex6.md)

在本練習中，您會將Tableau連線至Adobe Experience Platform和查詢服務，以執行Callcenter互動分析。

[5.1.7查詢服務API](./ex7.md)

在本練習中，您將使用「查詢服務API」來管理查詢範本和查詢排程。

[摘要和優點](./summary.md)

本單元摘要和優點概觀。

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform及其應用程式的所有知識。 如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。

[返回所有模組](../../../overview.md)
