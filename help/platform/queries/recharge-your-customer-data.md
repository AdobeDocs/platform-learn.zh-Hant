---
title: 為您的客戶資料重新充電，提供絕佳的體驗
description: 瞭解如何減輕低品質資料的影響、縮短實現價值的時間，並透過在許多使用案例中使用相同的資料來倍增ROI。
feature: Queries
role: Data Engineer, Data Architect, Developer
level: Beginner
jira: KT-10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 為您的客戶資料重新充電，提供絕佳的體驗

全通路資料是關鍵要素，可支援行銷人員使用的可操作客戶設定檔，以協調啟動並測量產生的客戶歷程。 但是，組織面臨管理這些資料的品質、規模和多樣性的挑戰。 這些需求需要簡化的解決方案，以減輕低品質資料的影響、縮短實現價值的時間，並透過對大量使用案例使用相同的資料來倍增ROI。
如需詳細資訊，請瀏覽[查詢服務檔案](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=zh-Hant)。

本影片會探索：

* 您可以善用的Adobe Experience Platform資料準備功能
* 提高Adobe Real-Time CDP、Adobe Journey Optimizer和Customer Journey Analytics的投資報酬率

>[!VIDEO](https://video.tv.adobe.com/v/342533?learn=on&enablevpops)

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

>[!NOTE]
>
>此影片是摘錄自Adobe Summit 2020工作階段&#x200B;*[為充滿活力的體驗重新充電全通路資料](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*。
