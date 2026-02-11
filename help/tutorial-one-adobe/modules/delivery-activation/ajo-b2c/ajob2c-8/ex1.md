---
title: 設定您的關聯式資料基礎
description: 設定您的關聯式資料基礎
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: bf3bebfa3bd79829da5352e950aed3f4ef5bf6d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 6%

---

# 3.8.1設定您的關聯式資料基礎

前往[https://experience.adobe.com](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![AJO OC](./images/aechome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。

![AJO OC](./images/ajohome.png)

## 3.8.1.1關聯式架構設定

關聯式架構是以模型為基礎的資料模型的正式定義。

它會指定：

- 表格集
- 每個表格中的欄
- 限制
- 跨資料表的關係

在以模型為基礎的資料模型中組織結構描述或表格，就是將資料結構化成多個表格。 確保每個表格都儲存一種實體/結構描述型別。

將資料擷取至以用於Adobe Journey Optimizer協調的行銷活動時，可使用下列來源：

- Amazon S3
- Google Cloud Storage
- SFTP
- Snowflake
- Google BigQuery
- 資料登陸區域
- Azure Databricks
- 本機檔案上傳

本練習的第一步是設定關聯式XDM架構。 在左側功能表中，向下捲動至&#x200B;**資料管理**&#x200B;並選取&#x200B;**結構描述**。 按一下&#x200B;**+建立結構描述**。

![AJO OC](./images/ajoocdata1.png)

選取&#x200B;**關聯式**。

![AJO OC](./images/ajoocdata2.png)

選取&#x200B;**上傳DDL檔案**，然後按一下&#x200B;**選擇檔案**。

![AJO OC](./images/ajoocdata3.png)

現在您的關聯式XDM方案已設定完畢，且資料已內嵌，您就可以開始使用該資料來建立下一個練習中的協調行銷活動。

## 3.8.1.2個資料擷取


## 後續步驟

移至[建立您的協調行銷活動](./ex2.md){target="_blank"}

返回[Adobe Journey Optimizer：行銷活動](./ajocampaigns.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
