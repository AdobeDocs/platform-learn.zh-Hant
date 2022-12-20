---
title: 運行查詢
seo-title: Run queries | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 運行查詢
description: 在本課程中，您將學習如何設定、寫入和執行查詢，以驗證您所擷取的資料。
role: Data Architect, Data Engineer
feature: Queries
kt: 4348
thumbnail: 4348-run-queries.jpg
exl-id: a37531cb-96ad-4547-86af-84f7ed65f019
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 2%

---

# 運行查詢

<!-- 15 min-->
在本課程中，您將學習如何設定、寫入和執行查詢，以驗證您所擷取的資料。

Adobe Experience Platform Query Service可讓您使用標準SQL在Platform中查詢資料，協助您了解資料的意義。 使用Query Service ，您可以加入Data Lake中的任何資料集，並將查詢結果擷取為新資料集，以用於報表、機器學習或擷取至即時客戶設定檔中。

**資料架構師** 和 **資料工程師** 需要在本教學課程之外使用查詢服務。

在開始練習之前，請觀看此短片以了解有關Query Service的更多資訊：
>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 需要權限

在 [設定權限](configure-permissions.md) 課程中，您設定了完成本課程所需的所有訪問控制。

<!-- Settings > **[!UICONTROL Services]** > **[!UICONTROL Query Service]**
* Permission items Data Management > **[!UICONTROL View Datasets]** and  **[!UICONTROL Manage Datasets]**
* Permission item Sandboxes > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 簡單查詢

讓我們從一些簡單的查詢開始：

1. 在Platform使用者介面中，前往 **查詢** 在左側導覽列中
1. 選取 **建立查詢** 按鈕，開啟一個文本框以運行和執行查詢
1. 在編輯器中輸入以下查詢，然後按Shift+Enter或Shift+Return以執行查詢。

   ```
   SHOW TABLES
   ```

1. 這將顯示可用表的清單

   ![顯示表查詢](assets/queries-showTables.png)


1. 現在，嘗試此查詢，替換 `_techmarketingdemos` 使用您自己的租用戶命名空間，若您回想一下，該命名空間會顯示在您的結構中。

   ```
   SELECT person.name.lastName,loyalty.tier
   FROM luma_loyalty_dataset
   WHERE loyalty.tier ='gold'
   ```

   ![從忠誠度資料集中選取資料](assets/queries-loyaltySelect.png)

1. 如果有任何錯誤，詳細的訊息會顯示在 **[!UICONTROL 主控台]** 標籤，如下圖所示
   ![查詢中出錯](assets/queries-error.png)

1. 通過成功的查詢， **[!UICONTROL 名稱]** it `Luma Gold Level Customers`
1. 選取 **[!UICONTROL 儲存]** 按鈕
   ![保存查詢](assets/queries-loyaltySelect-save.png)


<!--SELECT COUNT(DISTINCT (_techmarketingdemos.systemIdentifier.loyaltyId)) FROM luma_loyalty_dataset 


SELECT _techmarketingdemos.systemIdentifier.loyaltyId, COUNT(_techmarketingdemos.systemIdentifier.loyaltyId)
FROM luma_loyalty_dataset 
GROUP BY _techmarketingdemos.systemIdentifier.loyaltyId
HAVING COUNT(_techmarketingdemos.systemIdentifier.loyaltyId) > 1;-->

## 其他練習

稍後將將新增其他查詢服務練習至教學課程。
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

最後的實踐課， [建立區段](build-segments.md)!
