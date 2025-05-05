---
title: 查詢服務 — 必要條件
description: 查詢服務 — 必要條件
kt: 5342
doc-type: tutorial
exl-id: e9e4d478-cb8d-42a9-87a3-319e5a8b8522
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# 2.1.1必要條件

## 安裝PSQL命令列公用程式

依照Adobe Experience Platform檔案中概述的指示，安裝psql使用者端：
[PSQL安裝指南](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html?lang=zh-Hant)

安裝PSQL之後，您可能需要在終端機視窗中執行下列命令，以更新您的&#x200B;**PATH**：

對於macOS （以下命令中的XX取代為您安裝的PSQL版本號碼）：

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## 安裝Power BI

僅適用於Windows使用者

[安裝Microsoft Power BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html?lang=zh-Hant)

請確定您如檔案中所述，安裝確切的&#x200B;**npgsql**&#x200B;版本，否則您將無法將Power BI連線至Adobe Experience Platform查詢服務。

## 安裝Tableau

Windows或Mac使用者

根據檔案[安裝Tableau案頭](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html?lang=zh-Hant)。

Tableau會自動提供14天的試用期。

如果您想要在這14天之後使用Tableau，您需要授權金鑰。

## 後續步驟

移至[2.1.2快速入門](./ex2.md){target="_blank"}

返回[查詢服務](./query-service.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
