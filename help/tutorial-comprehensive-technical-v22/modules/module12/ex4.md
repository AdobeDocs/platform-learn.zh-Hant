---
title: 使用BigQuery Source Connector內嵌和分析Adobe Experience Platform中的Google Analytics資料 — 將BigQuery的資料載入Adobe Experience Platform
description: 使用BigQuery Source Connector內嵌和分析Adobe Experience Platform中的Google Analytics資料 — 將BigQuery的資料載入Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 150df432-e87a-402a-b821-ca9e33c5fd80
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 3%

---

# 12.4將資料從BigQuery載入Adobe Experience Platform

## 目標

- 將BigQuery資料對應至XDM結構
- 將BigQuery資料載入Adobe Experience Platform
- 熟悉BigQuery Source Connector UI

## 開始之前

在12.3練習後，您應在Adobe Experience Platform中開啟此頁面：

![示範](./images/datasets.png)

**如果已開啟，請繼續練習12.4.1。**

**如果沒有開啟，請前往 [Adobe Experience Platform](https://experience.adobe.com/platform/home).**

在左側功能表中，前往來源。 然後您會看到 **來源** 首頁。 在 **來源** 按一下 **資料庫**.

![示範](./images/sourceshome.png)

選取 **Google BigQuery** 源連接器，然後按一下 **+配置**.

![示範](./images/bq.png)

然後您會看到「Google BigQuery帳戶」選取畫面。

![示範](./images/0-c.png)

選取您的帳戶，然後按一下 **下一個**.

![示範](./images/ex4/0-d.png)

然後您會看到 **新增資料** 檢視。

![示範](./images/datasets.png)

## 12.4.1 BigQuery表選擇

在 **新增資料** 檢視，選取您的BigQuery資料集。

![示範](./images/datasets.png)

您現在可以在BigQuery中看到Google Analytics資料的範例資料預覽。

按&#x200B;**「下一步」**。

![示範](./images/ex4/3.png)

## 12.4.2 XDM對應

您現在會看到：

![示範](./images/xdm4a.png)

您現在必須建立新資料集或選取現有資料集，才能將Google Analytics資料載入。 本練習已建立資料集和結構。 您不需要建立新結構或資料集。

選擇 **現有資料集**. 開啟下拉式功能表以選取資料集。 搜尋名為的資料集 `Demo System - Event Dataset for BigQuery (Global v1.1)` 並加以選取。 按&#x200B;**「下一步」**。

![示範](./images/xdm6.png)

向下捲動。 您現在需要將 **源欄位** 從Google Analytics/BigQuery到XDM **目標欄位**，依欄位

![示範](./images/xdm8.png)

使用下面的映射表進行本練習。

| 源欄位 | 目標欄位 |
| ----------------- |-------------| 
| **_id** | _id |
| **_id** | channel._id |
| timeStamp | timestamp |
| GA_ID | ``--aepTenantId--``.identification.core.gaid |
| customerID | ``--aepTenantId--``.identification.core.loyatyId |
| 頁面 | web.webPageDetails.name |
| 裝置 | device.type |
| 瀏覽器 | environment.browserDetails.vendor |
| 行銷管道 | marketing.trackingCode |
| 流量來源 | channel.typeAtSource |
| 流量媒體 | channel.mediaType |
| TransactionID | commerce.order.payments.transactionID |
| Ecommerce_Action_Type | eventType |
| 頁面檢視 | web.webPageDetails.pageViews.value |
| 不重複購買(_P) | commerce.purchases.value |
| Product_Detail_Views | commerce.productViews.value |
| Adds_To_Cart | commerce.productListAdds.value |
| Product_Removes_From_Cart | commerce.productListRemovals.value |
| Product_Checkouts | commerce.checkouts.value |

將上述對應複製並貼入Adobe Experience Platform UI後，請確認您是否未看見因錯字或開頭/結尾空格而導致的任何錯誤。

您現在有 **對應** 就像這個。

![示範](./images/xdm34.png)

來源欄位 **GA_ID** 和 **customerID** 會對應至此XDM結構中的識別碼。 這可讓您以「忠誠度」或「客服中心」資料等其他資料集，讓Google Analytics資料（網頁/應用程式行為資料）更為豐富。

按&#x200B;**「下一步」**。

![示範](./images/ex4/38.png)

## 12.4.3連線與資料擷取排程

您現在會看到 **排程** 標籤：

![示範](./images/xdm38a.png)

在 **排程** 索引標籤，您可以為此定義資料擷取程式的頻率 **對應** 和資料。

由於您使用的是不會重新整理的Google BigQuery示範資料，因此在本練習中不需要設定排程。 您確實必須選取某個項目，並避免有太多無用的資料擷取程式，您需要像這樣設定頻率：

- 頻率： **周**
- 間隔： **200**

![示範](./images/ex4/39.png)

**重要**:務必啟動 **回填** 切換。

![示範](./images/ex4/39a.png)

最後，您必須定義 **delta** 欄位。

![示範](./images/ex4/36.png)

此 **delta** 欄位可用來排程連線，並僅上傳進入BigQuery資料集的新列。 差異欄位通常一律為時間戳記欄。 因此，若是未來排程的資料擷取，只會擷取具有最新新時間戳記的列。

選擇 **timeStamp** 作為增量欄位。

![示範](./images/ex4/37.png)

你現在有了這個。

![示範](./images/xdm37a.png)

按&#x200B;**「下一步」**。

![示範](./images/ex4/42.png)

## 12.4.4審查和啟動連接

在 **資料集流量詳細資料** 檢視。 您需要為連線命名，這可協助您稍後尋找。

請使用此命名慣例：

| 欄位 | 命名 | 範例 |
| ----------------- |-------------| -------------|
| 資料集流程名稱 | DataFlow - ldap - BigQuery網站互動 | DataFlow - vangeluw - BigQuery網站互動 |
| 說明 | DataFlow - ldap - BigQuery網站互動 | DataFlow - vangeluw - BigQuery網站互動 |

![示範](./images/xdm44.png)

按&#x200B;**「下一步」**。

![示範](./images/ex4/45.png)

您現在會看到連線的詳細概觀。 繼續之前，請確定一切都正確，因為有些設定在之後無法再變更，例如XDM對應。

![示範](./images/xdm46.png)

按一下&#x200B;**完成**。

![示範](./images/ex4/finish.png)

設定連線可能需要一些時間，因此若您看到以下內容，則無需擔心：

![示範](./images/ex4/47.png)

建立連線後，您就會看到：

![示範](./images/xdm48.png)

您現在已準備好繼續下一個練習，您將透過Customer Journey Analytics，在Google Analytics資料上建立強大的視覺效果。

下一步： [12.5使用Google Analytics分析Customer Journey Analytics資料](./ex5.md)

[返回模組12](./customer-journey-analytics-bigquery-gcp.md)

[返回所有模組](./../../overview.md)
