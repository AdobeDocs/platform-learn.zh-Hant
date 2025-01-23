---
title: Foundation — 資料擷取
description: Foundation — 資料擷取
kt: 5342
doc-type: tutorial
exl-id: 976d801a-3dcb-4cd9-8b9f-b1c964fe7c25
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# 1.2 Foundation — 資料擷取

在本單元中，目標是瞭解資料擷取的所有相關資訊。 您將瞭解串流和批次中的資料擷取。 您將使用Launch實作串流資料擷取，好讓實驗動手網站上的客戶行為可即時串流至Adobe Experience Platform。 您將瞭解如何使用Adobe Experience Platform工作流程批次資料擷取，以擷取CSV檔案、將其對應至XDM結構描述，然後擷取至Adobe Experience Platform。

## 學習目標

- 瞭解如何在Adobe Experience Platform中建立XDM結構描述
- 瞭解如何在Adobe Experience Platform中建立資料集
- 瞭解如何在Launch中建立串流端點及設定Adobe Experience Platform擴充功能
- 瞭解如何在Launch中建立規則，將資料串流至Adobe Experience Platform
- 瞭解如何將Adobe Experience Platform Launch整合至網頁
- 瞭解如何使用Adobe Experience Platform工作流程將CSV檔案擷取至Adobe Experience Platform

## 先決條件

- 存取Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 存取Adobe Experience Platform Launch： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 存取Postman

>[!NOTE]
>
>別忘了安裝、設定及使用[安裝Chrome擴充功能以取得Experience League檔案](../../gettingstarted/gettingstarted/ex1.md)中參考的Chrome擴充功能

## 練習

[1.2.1探索網站](./ex1.md)

在本練習中，您將探索要當作此啟用專案的一部分使用的網站。

[1.2.2設定結構描述並設定識別碼](./ex2.md)

在本練習中，您將設定必要的XDM結構描述以擷取設定檔資訊和客戶行為。 在每個XDM綱要中，您也必須設定要連結所有資訊的主要識別碼。

[1.2.3設定資料集](./ex3.md)

在本練習中，您將擷取擷取所需資料集，以擷取及儲存設定檔資訊和客戶行為。

[1.2.4從離線來源擷取資料](./ex4.md)

在本練習中，您將會前往網站和行動應用程式，並像客戶一樣將資料串流至Platform。

[1.2.5資料登陸區域](./ex5.md)

使用Azure Blob儲存設定您的資料登陸區域Source聯結器。

[摘要和優點](./summary.md)

本單元摘要和優點概觀。

![技術內部人士](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform及其應用程式的所有知識。 如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。

[返回所有模組](../../../overview.md)
