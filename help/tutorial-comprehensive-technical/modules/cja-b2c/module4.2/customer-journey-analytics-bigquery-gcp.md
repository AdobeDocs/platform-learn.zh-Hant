---
title: 使用BigQuery Source Connector在Adobe Experience Platform中擷取和分析Google Analytics資料
description: 使用BigQuery Source Connector在Adobe Experience Platform中擷取和分析Google Analytics資料
kt: 5342
doc-type: tutorial
exl-id: b078d003-da25-44c5-b000-77e3b3188fb6
source-git-commit: d6f6423adbc8f0ce8e20e686ea9ffd9e80ebb147
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# 4.2使用BigQuery Source Connector在Adobe Experience Platform中擷取和分析Google Analytics資料

在本單元中，您將設定自己的Google Cloud Platform執行個體、在Google Cloud Platform中載入範例資料，然後使用BigQuery Source Connector將該資料從Google Cloud Platform擷取到Adobe Experience Platform。 最後，您可以使用Customer Journey Analytics將該資料視覺化。

Adobe Experience Platform中的Source聯結器可讓您輕鬆將資料傳入Adobe Experience Platform。 Google BigQuery是其中一個已經可用的聯結器。 有了Adobe Experience Platform和BigQuery Source Connector，我們現在可以將Google Analytics資料以Customer Journey Analytics帶入Analysis Workspace。

此外，我們可以將Google Analytics資料與其他資料來源結合，例如CRM、客服中心或Customer Journey Analytics中的忠誠度資料，藉此豐富該資料。

## 學習目標

- 熟悉Google Cloud Platform和BigQuery使用者介面
- 將Google Analytics資料擷取至Adobe Experience Platform
- 使用Customer Journey Analytics執行Google Analytics資料分析
- 利用離線資料豐富Google Analytics資料

## 先決條件

- 建議您先熟悉一下Customer Journey Analytics，但並不一定需要
- 存取Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 存取Customer Journey Analytics
- 存取Google Cloud Platform和Google BigQuery
- **下載這些資產**：
   - [JSON — 範例資料：忠誠度資料](./../../../assets/json/bqLoyalty.json)

>[!NOTE]
>
>別忘了安裝、設定及使用[安裝Chrome擴充功能以取得Experience League檔案](../../gettingstarted/gettingstarted/ex1.md)中參考的Chrome擴充功能

## 練習

[4.2.1開始使用Google Cloud Platform](./ex1.md)

開始使用您的Google Cloud平台環境。

[4.2.2在BigQuery中建立第一個查詢](./ex2.md)

瞭解如何使用BigQuery準備資料以載入到Platform中。

[4.2.3將GCP和BigQuery連線至Adobe Experience Platform](./ex3.md)

瞭解如何在Adobe Experience Platform中設定來源聯結器。

[4.2.4從BigQuery將資料載入Adobe Experience Platform](./ex4.md)

瞭解如何在Adobe Experience Platform中設定BigQuery來源聯結器以擷取您的Google Analytics資料。

[4.2.5使用Customer Journey Analytics分析Google Analytics資料](./ex5.md)

瞭解如何分析Customer Journey Analytics中的Google Analytics資料，並將其與忠誠度資料結合。

[摘要和優點](./summary.md)

本單元摘要和優點概觀。

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform及其應用程式的所有知識。 如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。

[返回所有模組](../../../overview.md)
