---
title: 查詢服務 — Power BI/Tableau
description: 查詢服務 — Power BI/Tableau
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 11525d05-1c19-4d41-8f47-4feb3e8aed66
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 4.4從查詢產生資料集

## 目標

了解如何從查詢結果產生資料集將MicrosoftPower BI案頭/Tableau直接連結至查詢服務在MicrosoftPower BI案頭/Tableau案頭中建立報表

## 課程內容

用於查詢資料的命令行介面令人興奮，但呈現不好。 在本課程中，我們將引導您完成建議的工作流程，了解如何直接使用MicrosoftPower BI案頭/Tableau查詢服務，為相關人員建立視覺報表。

## 4.4.1從SQL查詢建立資料集

查詢的複雜性將影響查詢服務返回結果所需的時間。 直接從命令列或其他解決方案(例如MicrosoftPower BI/Tableau)查詢時，查詢服務會以5分鐘逾時（600秒）設定。 在某些情況下，這些解決方案將會設定較短的逾時時間。 若要執行較大的查詢並在傳回結果所花費的時間前載入，我們提供一項功能，可從查詢結果產生資料集。 此功能利用標準SQL功能，即「按選擇建立表」(CTAS)。 它可在Platform UI中的「查詢清單」中使用，也可直接從命令列使用PSQL運行。

在前一次你 **輸入您的姓名** 在PSQL中執行之前，使用自己的ldap。

```sql
select /* enter your name */
       e.--aepTenantId--.identification.core.ecid as ecid,
       e.placeContext.geo.city as city,
       e.placeContext.geo._schema.latitude latitude,
       e.placeContext.geo._schema.longitude longitude,
       e.placeContext.geo.countryCode as countrycode,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callFeeling as callFeeling,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic as callTopic,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callContractCancelled as contractCancelled,
       l.--aepTenantId--.loyaltyDetails.level as loyaltystatus,
       l.--aepTenantId--.loyaltyDetails.points as loyaltypoints,
       l.--aepTenantId--.identification.core.loyaltyId as crmid
from   demo_system_event_dataset_for_website_global_v1_1 e
      ,demo_system_event_dataset_for_call_center_global_v1_1 c
      ,demo_system_profile_dataset_for_loyalty_global_v1_1 l
where  e.--aepTenantId--.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal')
and    e.web.webPageDetails.name in ('Cancel Service', 'Call Start')
and    e.--aepTenantId--.identification.core.ecid = c.--aepTenantId--.identification.core.ecid
and    l.--aepTenantId--.identification.core.ecid = e.--aepTenantId--.identification.core.ecid;
```

導覽至Adobe Experience Platform UI - [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

您將在搜尋欄位中輸入ldap，以在Adobe Experience Platform查詢UI中搜尋已執行的陳述式：

選擇 **查詢**，前往 **記錄檔** 並在搜索欄位中輸入ldap。

![search-query-for-ctas.png](./images/search-query-for-ctas.png)

選取您的查詢，然後按一下 **輸出資料集**.

![search-query-for-ctas.png](./images/search-query-for-ctasa.png)

輸入 `--demoProfileLdap-- Callcenter Interaction Analysis` 名稱和說明，然後按 **運行查詢** 按鈕

![create-ctas-dataset.png](./images/create-ctas-dataset.png)

因此，您會看到狀態為的新查詢 **已提交**.

![ctas-query-submitted.png](./images/ctas-query-submitted.png)

完成後，您會看到 **已建立資料集** （您可能需要重新整理頁面）。

![ctas-dataset-created.png](./images/ctas-dataset-created.png)

建立資料集後（可能需要5-10分鐘），您就可以繼續練習。

下一步 — 選項A: [4.5查詢服務和Power BI](./ex5.md)

下一步 — 選項B: [4.6查詢服務和Tableau](./ex6.md)

[返回模組4](./query-service.md)

[返回所有模組](../../overview.md)
