---
title: Data Warehouse連線
seo-title: Configure a Data Warehouse connection | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Data Warehouse連線
description: 在本課程中，我們會設定Adobe Experience Platform與您的企業Data Warehouse之間的連線，以啟用同盟對象構成。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-configure-a-data-warehouse-connection.jpg
hide: true
source-git-commit: fcfadca95c12d0123cfb221e44909f7e0fa8abab
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Data Warehouse連線

在本課程中，我們會設定Adobe Experience Platform與您的企業Data Warehouse之間的連線，以啟用同盟對象構成。 這可讓您直接從支援的倉儲查詢資料，而不需進行復寫。 此外，我們也會根據Data Warehouse表格建立方案和資料模型。

本實驗會連線至Snowflake帳戶。 同盟對象構成支援不斷增加的雲端倉儲連線清單。 檢視整合的[更新清單](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}。


## 步驟

1. 瀏覽至左側邊欄上的&#x200B;**同盟資料**&#x200B;區段。
2. 在&#x200B;**同盟資料庫**&#x200B;連結中，按一下&#x200B;**新增同盟資料庫**&#x200B;按鈕。
3. 新增名稱並選取&#x200B;**Snowflake**。
4. 填寫詳細資料，按一下&#x200B;**測試連線**&#x200B;按鈕，然後按一下&#x200B;**部署函式**&#x200B;按鈕。

   ![snowflake-connection-setup](assets/snowflake-connection-setup.png)

   ![snowflake-connection-setup-step2](assets/snowflake-connection-setup-step2.png)

   ![snowflake-connection-setup-step3](assets/snowflake-connection-setup-step3.png)

## 建立結構描述

若要在Federated Audience Composition中建立方案，請遵循下列步驟：

1. 在&#x200B;**同盟資料**&#x200B;區段中，按一下&#x200B;**模型**。
2. 瀏覽&#x200B;**結構描述**&#x200B;索引標籤並按一下&#x200B;**建立結構描述**&#x200B;按鈕。
3. 在清單中選取您的來源資料庫，然後按一下&#x200B;**新增表格**&#x200B;索引標籤。
4. 選取下清單格：
   - FSI_CRM
   - FSI_CRM_CONSENT_PREFERENCE

   ![create-schema](assets/create-schema.png)

   ![select-table](assets/select-table.png)

選取表格後，檢閱每個表格的欄，並選取主索引鍵。 在本練習中，我們選取&#x200B;**電子郵件**&#x200B;作為兩個表格中的主索引鍵。

![create-schema](assets/create-schema.png)

![create-schema-step2](assets/create-schema-step2.png)

## 在結構描述中預覽資料

若要預覽結構描述所代表之資料表中的資料，請瀏覽至&#x200B;**資料**&#x200B;標籤。

按一下&#x200B;**計算**&#x200B;連結以預覽記錄總數。

![preview-data-in-schema](assets/preview-data-in-schema.png)

## 建立資料模型

資料模型可讓您在表格之間建立連結。 可以在相同資料庫中的表格之間建立連結，例如Snowflake中的表格，或在不同資料庫中的表格之間建立連結，例如Snowflake中的表格與Amazon Redshift中的表格之間的連結。

若要在Federated Audience Composition中建立資料模型，請執行下列步驟：

1. 在&#x200B;**同盟資料**&#x200B;區段中，按一下&#x200B;**模型**，然後按一下&#x200B;**資料模型**。
2. 按一下&#x200B;**建立資料模型**&#x200B;按鈕。
3. 為您的資料模型提供名稱。
4. 按一下&#x200B;**新增結構描述**&#x200B;並選取&#x200B;**FSI_CRM**&#x200B;和&#x200B;**FSI_CRM_CONSENT_PREFERENCE**&#x200B;結構描述。
5. 按一下&#x200B;**建立連結**，在這些資料表之間建立連結。

建立連結時，請選擇適用的基數：

- **1-N**：來源表格的一個出現次數可以具有多個目標表格的對應出現次數，但目標表格的一個出現次數最多可以具有來源表格的一個對應出現次數。
- **N-1**：目標表格的一個出現次數可以有來源表格的多個對應出現次數，但來源表格的一個出現次數最多可以有目標表格的對應出現次數。
- **1-1**：來源資料表的一個執行個體最多可以具有目標資料表的一個對應執行個體。

以下是為實驗練習建立的連結預覽。 連結可讓CRM和同意表格之間聯結，使用&#x200B;**EMAIL**&#x200B;的主索引鍵執行聯結。

![預覽 — 資料模型](assets/preview-data-model.png)

現在，我們已準備好[建立和對象](audience-creation-exercise.md)。
