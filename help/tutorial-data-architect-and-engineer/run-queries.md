---
title: 執行查詢
seo-title: Run queries | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 執行查詢
description: 在本課程中，您將瞭解如何設定、編寫和執行查詢以驗證您擷取的資料。
role: Data Architect, Data Engineer
feature: Queries
jira: KT-4348
thumbnail: 4348-run-queries.jpg
exl-id: a37531cb-96ad-4547-86af-84f7ed65f019
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 執行查詢

<!-- 15 min-->
在本課程中，您將學習如何設定、編寫和執行查詢以驗證您擷取的資料。

Adobe Experience Platform查詢服務可讓您使用標準SQL在Platform中查詢資料，協助您瞭解資料。 使用查詢服務，您可以聯結Data Lake中的任何資料集，並將查詢結果擷取為新資料集，以用於報表、機器學習或擷取到即時客戶個人檔案中。

**資料架構師**&#x200B;和&#x200B;**資料工程師**&#x200B;需要在本教學課程之外使用查詢服務。

在開始練習之前，請觀看此短片，以進一步瞭解查詢服務：
>[!VIDEO](https://video.tv.adobe.com/v/29795?learn=on&enablevpops)

## 需要的許可權

在[設定許可權](configure-permissions.md)課程中，您已設定完成本課程所需的所有存取控制。

<!-- Settings > **[!UICONTROL Services]** > **[!UICONTROL Query Service]**
* Permission items Data Management > **[!UICONTROL View Datasets]** and  **[!UICONTROL Manage Datasets]**
* Permission item Sandboxes > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 簡單查詢

讓我們從一些簡單的查詢開始：

1. 在Platform使用者介面中，前往左側導覽中的&#x200B;**查詢**
1. 選取右上角的&#x200B;**建立查詢**&#x200B;按鈕，開啟文字方塊以執行查詢
1. 在編輯器中輸入下列查詢，然後按Shift+Enter或Shift+Return以執行查詢。

   ```
   SHOW TABLES
   ```

1. 這會顯示可用表格的清單

   ![顯示資料表查詢](assets/queries-showTables.png)


1. 現在嘗試此查詢，將`_techmarketingdemos`取代為您自己的租使用者名稱空間，如果您記得的話，這些名稱空間會顯示在您的結構描述中。

   ```
   SELECT person.name.lastName,loyalty.tier
   FROM luma_loyalty_dataset
   WHERE loyalty.tier ='gold'
   ```

   ![從熟客資料集中選取資料](assets/queries-loyaltySelect.png)

1. 如果發生任何錯誤，**[!UICONTROL 主控台]**索引標籤中將會顯示詳細訊息，如下圖所示
   ![查詢發生錯誤](assets/queries-error.png)

1. 使用成功的查詢，**[!UICONTROL 命名]** `Luma Gold Level Customers`
1. 選取&#x200B;**[!UICONTROL 儲存]**按鈕
   ![正在儲存查詢](assets/queries-loyaltySelect-save.png)


<!--SELECT COUNT(DISTINCT (_techmarketingdemos.systemIdentifier.loyaltyId)) FROM luma_loyalty_dataset 


SELECT _techmarketingdemos.systemIdentifier.loyaltyId, COUNT(_techmarketingdemos.systemIdentifier.loyaltyId)
FROM luma_loyalty_dataset 
GROUP BY _techmarketingdemos.systemIdentifier.loyaltyId
HAVING COUNT(_techmarketingdemos.systemIdentifier.loyaltyId) > 1;-->

## 其他練習

其他查詢服務練習將於稍後新增至教學課程。
<!--
## Join Datasets

In this exercise, we will join two datasets `Luma Loyalty Dataset` and `Luma Offline Purchase` to get list of gold customers who have spend over $500 dollars in one purchase.

1. Create a new query
1. Copy and paste following query in query editor and execute, again replacing `_techmarketingdemos` with your own tenant namespace
    
    ```
    SELECT DISTINCT lopd.commerce.order.purchaseID as PurchaseId ,
        lld.person.name.firstName as LastName ,
        lld.person.name.lastName as LastName ,
        lopd.personalEmail.address as email,
        lopd.commerce.order.priceTotal as Total

    FROM luma_loyalty_dataset lld
    JOIN luma_offline_purchase_event_dataset lopd
    ON lopd._techmarketingdemos.systemIdentifier.loyaltyId = lld._techmarketingdemos.systemIdentifier.loyaltyId

    WHERE lld._techmarketingdemos.loyalty.level ='gold' AND lopd.commerce.order.priceTotal >500;
    ```

1. You should get list of Gold Customers who have spend over $500 in single purchase.

## Output datasets

1. Select on Output Dataset button
1. Provide name and description to the dataset
1. Save.
1. Go to **Datasets** under **Data Management** to find new dataset created.

-->
<!--Add content for Adobe Defined Functions-->

## 其他資源

* [查詢服務檔案](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=zh-Hant)
* [查詢服務API參考](https://www.adobe.io/experience-platform-apis/references/query-service/)

現在開始最後一個實作課程，[建立區段](build-segments.md)！
