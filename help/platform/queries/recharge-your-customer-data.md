---
title: 為您的客戶資料重新充電，以提供令人振奮的體驗
description: 瞭解如何透過在許多使用案例中使用相同資料來減輕低品質資料的影響、縮短實現價值的時間並倍增ROI。
role: Data Engineer, Data Architect, Developer
feature: Queries
jira: KT-10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# 為您的客戶資料重新充電，以提供令人振奮的體驗

全通路資料是關鍵要素，可支援行銷人員用來協調啟用及衡量所產生客戶歷程的可操作客戶設定檔。 然而，組織面臨管理這些資料的品質、規模和多樣性的挑戰。 它們需要簡化的解決方案，以減輕低品質資料的影響、縮短實現價值的時間，並通過對大量使用案例使用相同的資料來倍增ROI。

本影片會探索：

* 您可以善用的Adobe Experience Platform資料準備功能
* 提高Adobe Real-Time CDP、Adobe Journey Optimizer和Customer Journey Analytics的投資報酬率

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## SQL範例

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceID AS customerId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(C._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset C
WHERE A._experience.analytics.customDimensions.eVars.eVar1 = B.personKey.sourceID
AND A.productListItems[0].sku = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

如需詳細資訊，請造訪 [查詢服務檔案](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=zh-Hant).

>[!NOTE]
>
>本影片摘錄自Adobe Summit2020工作階段 *[為全通路資料重新充電，讓體驗耳目一新](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
