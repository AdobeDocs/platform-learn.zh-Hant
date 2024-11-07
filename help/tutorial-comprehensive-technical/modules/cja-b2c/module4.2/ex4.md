---
title: 使用BigQuery Source Connector在Adobe Experience Platform中擷取和分析Google Analytics資料 — 將BigQuery中的資料載入Adobe Experience Platform
description: 使用BigQuery Source Connector在Adobe Experience Platform中擷取和分析Google Analytics資料 — 將BigQuery中的資料載入Adobe Experience Platform
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 2%

---

# 4.2.4從BigQuery將資料載入Adobe Experience Platform

## 目標

- 將BigQuery資料對應至XDM結構描述
- 將BigQuery資料載入Adobe Experience Platform
- 熟悉BigQuery Source聯結器UI

## 開始之前

練習12.3之後，您應該在Adobe Experience Platform中開啟此頁面：

![示範](./images/datasets.png)

**如果您已開啟它，請繼續進行練習12.4.1。**

**如果您尚未開啟它，請移至[Adobe Experience Platform](https://experience.adobe.com/platform/home)。**

在左側選單中，前往來源。 然後您會看到&#x200B;**來源**&#x200B;首頁。 在&#x200B;**來源**&#x200B;功能表中，按一下&#x200B;**資料庫**。

![示範](./images/sourceshome.png)

選取&#x200B;**Google BigQuery** Source聯結器，然後按一下&#x200B;**+設定**。

![示範](./images/bq.png)

接著您會看到Google BigQuery帳戶選取畫面。

![示範](./images/0-c.png)

選取您的帳戶並按一下[下一步] ****。

![示範](./images/ex4/0-d.png)

然後您會看到&#x200B;**新增資料**&#x200B;檢視。

![示範](./images/datasets.png)

## 4.2.4.1 BigQuery表格選取專案

在&#x200B;**新增資料**&#x200B;檢視中，選取您的BigQuery資料集。

![示範](./images/datasets.png)

您現在可以在BigQuery中看到Google Analytics資料的範例資料預覽。

按一下&#x200B;**下一步**。

![示範](./images/ex4/3.png)

## 4.2.4.2 XDM對應

您現在會看到以下內容：

![示範](./images/xdm4a.png)

您現在必須建立新資料集或選取現有資料集，才能將Google Analytics資料載入其中。 針對此練習，已建立資料集和結構描述。 您不需要建立新的結構描述或資料集。

選取&#x200B;**現有的資料集**。 開啟下拉式功能表以選取資料集。 搜尋名為`Demo System - Event Dataset for BigQuery (Global v1.1)`的資料集並加以選取。 按一下&#x200B;**下一步**。

![示範](./images/xdm6.png)

向下捲動。 您現在需要將每個&#x200B;**Source欄位**&#x200B;從Google Analytics/BigQuery對應到XDM **目標欄位**，依欄位進行對應。

![示範](./images/xdm8.png)

請針對此練習使用下列對應表格。

| 來源欄位 | 目標欄位 |
| ----------------- |-------------| 
| **_id** | _id |
| **_id** | 頻道。_id |
| 時間戳記 | 時間戳記 |
| GA_ID | ``--aepTenantId--``.identification.core.gaid |
| customerID | ``--aepTenantId--``.identification.core.loyaltyId |
| 頁面 | web.webPageDetails.name |
| 裝置 | device.type |
| 瀏覽器 | environment.browserDetails.vendor |
| 行銷管道 | marketing.trackingCode |
| TrafficSource | channel.typeAtSource |
| 流量媒介 | channel.mediaType |
| 交易ID | commerce.order.payments.transactionID |
| Ecommerce_Action_Type | eventType |
| 頁面檢視 | web.webPageDetails.pageViews.value |
| Unique_Purchases | commerce.purchases.value |
| Product_Detail_Views | commerce.productViews.value |
| Adds_To_Cart | commerce.productListAdds.value |
| Product_Removes_From_Cart | commerce.productListRemovals.value |
| 產品結帳 | commerce.checkouts.value |

將上述對應複製並貼到Adobe Experience Platform UI後，請確認您是否未看到因拼字或前導/尾隨空格而導致的任何錯誤。

您現在有如下的&#x200B;**對應**：

![示範](./images/xdm34.png)

來源欄位&#x200B;**GA_ID**&#x200B;和&#x200B;**customerID**&#x200B;對應到這個XDM結構描述中的識別碼。 這可讓您以忠誠度或客服中心資料等其他資料集，擴充Google Analytics資料（網頁/應用程式行為資料）。

按一下&#x200B;**下一步**。

![示範](./images/ex4/38.png)

## 4.2.4.3連線與資料擷取排程

您現在會看到&#x200B;**排程**&#x200B;標籤：

![示範](./images/xdm38a.png)

在&#x200B;**排程**&#x200B;索引標籤中，您可以為此&#x200B;**對應**&#x200B;和資料定義資料擷取程式的頻率。

由於您在Google BigQuery中使用不會重新整理的示範資料，因此實際上不需要在本練習中設定排程。 您確實必須選取一些專案，而且若要避免太多無用的資料擷取程式，您必須設定頻率，如下所示：

- 頻率： **周**
- 間隔： **200**

![示範](./images/ex4/39.png)

**重要**：請確定您已啟動&#x200B;**回填**&#x200B;引數。

![示範](./images/ex4/39a.png)

最後但並非最不重要的是，您必須定義&#x200B;**delta**&#x200B;欄位。

![示範](./images/ex4/36.png)

**delta**&#x200B;欄位用於排程連線，並僅上傳進入BigQuery資料集的新列。 差異欄位通常永遠是時間戳記欄。 因此，對於未來的排程資料擷取，只會擷取具有新的、更新時間戳記的列。

選取&#x200B;**時間戳記**&#x200B;做為差異欄位。

![示範](./images/ex4/37.png)

您現在擁有此專案。

![示範](./images/xdm37a.png)

按一下&#x200B;**下一步**。

![示範](./images/ex4/42.png)

## 4.2.4.4檢閱並啟動連線

在&#x200B;**資料集流程詳細資料**&#x200B;檢視中。 您必須為連線命名，以便稍後尋找。

請使用此命名慣例：

| 欄位 | 命名 | 範例 |
| ----------------- |-------------| -------------|
| 資料集流程名稱 | DataFlow - ldap - BigQuery網站互動 | DataFlow - vangeluw - BigQuery網站互動 |
| 說明 | DataFlow - ldap - BigQuery網站互動 | DataFlow - vangeluw - BigQuery網站互動 |

![示範](./images/xdm44.png)

按一下&#x200B;**下一步**。

![示範](./images/ex4/45.png)

您現在會看到連線的詳細概觀。 在繼續之前，請確定所有事項都正確無誤，因為有些設定之後將無法再變更，例如XDM對應。

![示範](./images/xdm46.png)

按一下&#x200B;**完成**。

![示範](./images/ex4/finish.png)

設定連線可能需要一些時間，因此，如果您看到以下內容，請不要擔心：

![示範](./images/ex4/47.png)

建立連線後，您會看到以下內容：

![示範](./images/xdm48.png)

您現在已準備好繼續進行下一個練習，您將使用Customer Journey Analytics在Google Analytics資料之上建立強大的視覺效果。

下一步： [4.2.5使用Customer Journey Analytics分析Google Analytics資料](./ex5.md)

[返回模組4.2](./customer-journey-analytics-bigquery-gcp.md)

[返回所有模組](./../../../overview.md)
