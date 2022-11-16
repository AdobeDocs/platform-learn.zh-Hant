---
title: 為您的客戶資料重新充電以提供振奮人心的體驗
description: 了解如何針對多種使用案例使用相同的資料，以減輕低品質資料的影響、縮短實現價值的時間，並增加投資報酬率。
role: Data Engineer, Data Architect, Developer
feature: Queries
kt: 10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# 為您的客戶資料重新充電以提供振奮人心的體驗

全通路資料是行銷人員用來協調啟動和測量所產生客戶歷程的可操作客戶設定檔的關鍵要素。 但是，組織在管理此資料的質量、規模和種類方面面臨挑戰。 它們需要簡化的解決方案，以減輕低質量資料的影響，縮短價值實現時間，並通過對多個使用案例使用相同的資料來增加投資回報。

本影片探討：

* Adobe Experience Platform資料準備功能，供您運用
* 提高Adobe Real-Time CDP、Adobe Journey Optimizer和Customer Journey Analytics的投資報酬率

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## SQL示例

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
>此影片是Adobe Summit2020工作階段的摘要 *[為電氣化體驗重新充電全管道資料](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
