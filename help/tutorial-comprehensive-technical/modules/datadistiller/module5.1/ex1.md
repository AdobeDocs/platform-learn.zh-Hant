---
title: 查詢服務 — 必要條件
description: 查詢服務 — 必要條件
kt: 5342
doc-type: tutorial
exl-id: b8a404d1-7796-46e3-b245-553acdc753ae
source-git-commit: d9d9a38c1e160950ae755e352a54667c8a7b30f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 5.1.1必要條件

## 安裝PSQL命令列公用程式

依照Adobe Experience Platform檔案中概述的指示，安裝psql使用者端：
[PSQL安裝指南](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html?lang=zh-Hant)

安裝PSQL之後，您可能需要在終端機視窗中執行下列命令，以更新您的&#x200B;**PATH**：

對於macOS （以下命令中的XX取代為您安裝的PSQL版本號碼）：

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## 安裝Power BI

僅適用於Windows使用者

[安裝MicrosoftPower BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html?lang=zh-Hant)

請確定您如檔案中所述，安裝確切的&#x200B;**npgsql**&#x200B;版本，否則您將無法將Power BI連線到Adobe Experience Platform查詢服務。

## 安裝Tableau

Windows或Mac使用者

根據檔案[安裝Tableau案頭](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html?lang=zh-Hant)。

Tableau會自動提供14天的試用期。

如果您想要在這14天之後使用Tableau，您需要授權金鑰。

下一步： [5.1.2快速入門](./ex2.md)

[返回模組5.1](./query-service.md)

[返回所有模組](../../../overview.md)
