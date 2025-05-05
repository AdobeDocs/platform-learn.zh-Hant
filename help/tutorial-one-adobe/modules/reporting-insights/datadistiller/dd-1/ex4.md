---
title: 查詢服務 — 查詢、查詢、查詢……和流失分析
description: 查詢服務 — 查詢、查詢、查詢……和流失分析
kt: 5342
doc-type: tutorial
exl-id: 98bacc45-5130-46f2-8592-4628d51fa224
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 0%

---

# 2.1.4查詢、查詢、查詢……和流失分析

## 目標

- 寫入資料分析的查詢
- 撰寫結合線上、客服中心和忠誠度資料的SQL查詢(可在Adobe Experience Platform中使用)
- 瞭解Adobe定義的函式

## 內容

在本練習中，您將編寫查詢來分析產品檢視、產品漏斗、流失率等。

本章中列出的所有查詢將會在您的&#x200B;**PSQL命令列介面**&#x200B;中執行。 您應該複製(CTRL-c)以&#x200B;**SQL**&#x200B;表示的陳述式區塊，並將其貼到&#x200B;**PSQL命令列介面**&#x200B;中(CTRL-v)。 **查詢結果**&#x200B;區塊會顯示貼上的SQL陳述式和相關聯的查詢結果。

## 寫入資料分析的基本查詢

### 時間戳記

在Adobe Experience Platform中擷取的資料會加上時間戳記。 **timestamp**&#x200B;屬性可讓您分析一段時間的資料。

我們每天檢視多少項產品？

**SQL**

```sql
select date_format( timestamp , 'yyyy-MM-dd') AS Day,
       count(*) AS productViews
from   demo_system_event_dataset_for_website_global_v1_1
where  --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
and eventType = 'commerce.productViews'
group by Day
limit 10;
```

複製上述陳述式，並在&#x200B;**PSQL命令列介面**&#x200B;中執行。

**查詢結果**

```text
tech-insiders:all=> select date_format( timestamp , 'yyyy-MM-dd') AS Day,
       count(*) AS productViews
from   demo_system_event_dataset_for_website_global_v1_1
where  _experienceplatform.demoEnvironment.brandName IN ('Citi Signal')
and eventType = 'commerce.productViews'
group by Day
limit 10;
    Day     | productViews 
------------+--------------
 2024-12-04 |         2297
(1 row)
```

### 已檢視的前5大產品

檢視的前5項產品為何？

#### SQL

```sql
select productListItems.name, count(*)
from   demo_system_event_dataset_for_website_global_v1_1
where  --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
and    eventType = 'commerce.productViews'
group  by productListItems.name
order  by 2 desc
limit 5;
```

複製上述陳述式，並在&#x200B;**PSQL命令列介面**&#x200B;中執行。

**查詢結果**

```text
tech-insiders:all=> select productListItems.name, count(*)
from   demo_system_event_dataset_for_website_global_v1_1
where  _experienceplatform.demoEnvironment.brandName IN ('Citi Signal')
and    eventType = 'commerce.productViews'
group  by productListItems.name
order  by 2 desc
limit 5;
                  name                   | count(1) 
-----------------------------------------+----------
 {Google Pixel XL 32GB Black Smartphone} |      938
 {SIM Only}                              |      482
 {Samsung Galaxy S8}                     |      456
 {Samsung Galaxy S7 32GB Black}          |      421
(4 rows)
```

### 產品互動漏斗，從檢視到購買

**SQL**

```sql
select eventType, count(*)
from   demo_system_event_dataset_for_website_global_v1_1
where  --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
and    eventType is not null
and    eventType <> ''
group  by eventType;
```

複製上述陳述式，並在&#x200B;**PSQL命令列介面**&#x200B;中執行。

**查詢結果**

```text
tech-insiders:all=> select eventType, count(*)
from   demo_system_event_dataset_for_website_global_v1_1
where  _experienceplatform.demoEnvironment.brandName IN ('Citi Signal')
and    eventType is not null
and    eventType <> ''
group  by eventType;
        eventType         | count(1) 
--------------------------+----------
 commerce.productListAdds |      494
 commerce.purchases       |      246
 commerce.productViews    |     2297
(3 rows)
```

### 識別有流失風險的訪客（造訪頁面=>取消服務）

**SQL**

```sql
select distinct --aepTenantId--.identification.core.ecid
from   demo_system_event_dataset_for_website_global_v1_1
where  --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
and    web.webPageDetails.name = 'Cancel Service'
group  by --aepTenantId--.identification.core.ecid
limit 10;
```

複製上述陳述式，並在&#x200B;**PSQL命令列介面**&#x200B;中執行。

**查詢結果**

```text
tech-insiders:all=> select distinct _experienceplatform.identification.core.ecid
from   demo_system_event_dataset_for_website_global_v1_1
where  _experienceplatform.demoEnvironment.brandName IN ('Citi Signal')
and    web.webPageDetails.name = 'Cancel Service'
group  by _experienceplatform.identification.core.ecid
limit 10;
               ecid               
----------------------------------
 86069928882940477620713284798772
 75691756152042231410852704832434
 47381264398548915586824480724480
 51294194577949645447313762862726
 95873885060131472480685538836534
 71192995127345419624952514250737
 81469709164961922907426138040032
 53545252726821876244061095202780
 13294750130353985087337266864522
 58843891994459565443501421307174
(10 rows)
```

在下一組查詢中，我們將擴充上述查詢，以完整檢視瀏覽「取消服務」頁面的客戶及其行為。 您將瞭解如何使用Adobe定義的函式來將資訊工作階段化、識別事件的順序和時間。 您也將聯合資料集，以進一步豐富及準備資料，以便在Microsoft Power BI中進行分析。

## 進階查詢

大部分的商業邏輯需要收集客戶的接觸點並依時間排序。 Spark SQL會以視窗函式的形式提供這項支援。 視窗函式是標準SQL的一部分，並受到許多其他SQL引擎的支援。

### Adobe定義的函式

Adobe已將一組&#x200B;**Adobe定義的函式**&#x200B;新增至標準SQL語法，讓您更清楚瞭解您的體驗資料。 在接下來的幾個查詢中，您將瞭解這些ADF函式。 您可以在檔案[&#128279;](https://experienceleague.adobe.com/docs/experience-platform/query/sql/adobe-defined-functions.html)中找到詳細資訊和完整清單。

### 當使用者進入工作階段的第3頁時，「取消服務」頁面前會在網站上執行什麼動作？

透過此查詢，您將發現前兩個Adobe定義的函式&#x200B;**SESS_TIMEOUT**&#x200B;和&#x200B;**NEXT**

> **SESS_TIMEOUT()**&#x200B;會重新產生使用Adobe Analytics找到的造訪群組。 它會執行類似的以時間為基礎的分組，但可自訂引數。
>
> **NEXT()**&#x200B;和&#x200B;**PREVIOUS()**&#x200B;可協助您瞭解客戶如何瀏覽您的網站。

**SQL**

```sql
SELECT
  webPage,
  webPage_2,
  webPage_3,
  webPage_4,
  count(*) journeys
FROM
  (
      SELECT
        webPage,
        NEXT(webPage, 1, true)
          OVER(PARTITION BY ecid, session.num
                ORDER BY timestamp
                ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
          AS webPage_2,
        NEXT(webPage, 2, true)
          OVER(PARTITION BY ecid, session.num
                ORDER BY timestamp
                ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
          AS webPage_3,
        NEXT(webPage, 3, true)
           OVER(PARTITION BY ecid, session.num
                ORDER BY timestamp
                ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
          AS webPage_4,
        session.depth AS SessionPageDepth
      FROM (
            select a.--aepTenantId--.identification.core.ecid as ecid,
                   a.timestamp,
                   web.webPageDetails.name as webPage,
                    SESS_TIMEOUT(timestamp, 60 * 30) 
                       OVER (PARTITION BY a.--aepTenantId--.identification.core.ecid 
                             ORDER BY timestamp 
                             ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
                  AS session
            from   demo_system_event_dataset_for_website_global_v1_1 a
            where  a.--aepTenantId--.identification.core.ecid in ( 
                select b.--aepTenantId--.identification.core.ecid
                from   demo_system_event_dataset_for_website_global_v1_1 b
                where  b.--aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
                and    b.web.webPageDetails.name = 'Cancel Service'
            )
        )
)
WHERE SessionPageDepth=1
and   webpage_3 = 'Cancel Service'
GROUP BY webPage, webPage_2, webPage_3, webPage_4
ORDER BY journeys DESC
LIMIT 10;
```

複製上述陳述式，並在&#x200B;**PSQL命令列介面**&#x200B;中執行。

**查詢結果**

```text
                webPage                |               webPage_2               |   webPage_3    | webPage_4  | journeys 
---------------------------------------+---------------------------------------+----------------+------------+----------
 Telco Home                            | Citi Signal Sport                     | Cancel Service | Call Start |        2
 Citi Signal Sport                     | Google Pixel XL 32GB Black Smartphone | Cancel Service | Call Start |        2
 Broadband Deals                       | Samsung Galaxy S7 32GB Black          | Cancel Service |            |        2
 TV & Broadband Deals                  | Samsung Galaxy S7 32GB Black          | Cancel Service |            |        2
 SIM Only                              | Citi Signal Shop                      | Cancel Service |            |        2
 Google Pixel XL 32GB Black Smartphone | Broadband Deals                       | Cancel Service |            |        2
 SIM Only                              | Telco Home                            | Cancel Service |            |        2
 Citi Signal Shop                      | Samsung Galaxy S7 32GB Black          | Cancel Service | Call Start |        1
 Google Pixel XL 32GB Black Smartphone | Citi Signal Sport                     | Cancel Service | Call Start |        1
 Google Pixel XL 32GB Black Smartphone | Citi Signal Shop                      | Cancel Service | Call Start |        1
(10 rows)
```

### 訪客造訪「取消服務」頁面後，我們還有多久的時間可以致電客服中心？

若要回答這類查詢，我們將使用&#x200B;**TIME_BETWEEN_NEXT_MATCH()** Adobe定義的函式。

> 上一個或下一個相符函式之間的時間提供一個新維度，可測量自特定事件以來經過的時間。

**SQL**

```sql
select * from (
       select --aepTenantId--.identification.core.ecid as ecid,
              web.webPageDetails.name as webPage,
              TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Call Start', 'seconds')
              OVER(PARTITION BY --aepTenantId--.identification.core.ecid
                  ORDER BY timestamp
                  ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
              AS contact_callcenter_after_seconds
       from   demo_system_event_dataset_for_website_global_v1_1
       where  --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
       and    web.webPageDetails.name in ('Cancel Service', 'Call Start')
) r
where r.webPage = 'Cancel Service'
limit 15;
```

複製上述陳述式，並在&#x200B;**PSQL命令列介面**&#x200B;中執行。

**查詢結果**

```text
               ecid               |    webPage     | contact_callcenter_after_seconds 
----------------------------------+----------------+----------------------------------
 00331886620679939148047665693117 | Cancel Service |                                 
 00626561600197295782131349716866 | Cancel Service |                                 
 00630470663554417679969244202779 | Cancel Service |                             -797
 00720875344152796154458668700428 | Cancel Service |                             -519
 00746064605049656090779523644276 | Cancel Service |                              -62
 00762093837616944422322357210965 | Cancel Service |                                 
 00767875779073091876070699689209 | Cancel Service |                                 
 00798691264980137616449378075855 | Cancel Service |                                 
 00869613691740150556826953447162 | Cancel Service |                             -129
 00943638725078228957873279219207 | Cancel Service |                             -750
 01167540466536077846425644389346 | Cancel Service |                                 
 01412448537869549016063764484810 | Cancel Service |                                 
 01419076946514450291741574452702 | Cancel Service |                             -482
 01533124771963987423015507880755 | Cancel Service |                                 
 01710651086750904478559809475925 | Cancel Service |                                 
(15 rows)
```

### 連絡的結果如何？

在此查詢中，您會將資料集聯結在一起。 在此情況下，您將使用資料集`demo_system_event_dataset_for_call_center_global_v1_1`加入資料集`demo_system_event_dataset_for_website_global_v1_1`。 這是為了瞭解客服中心互動的結果。

**SQL**

```sql
select distinct r.*,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callFeeling,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callContractCancelled
from (
       select --aepTenantId--.identification.core.ecid ecid,
              web.webPageDetails.name as webPage,
              TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Call Start', 'seconds')
              OVER(PARTITION BY --aepTenantId--.identification.core.ecid
                  ORDER BY timestamp
                  ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
              AS contact_callcenter_after_seconds
       from   demo_system_event_dataset_for_website_global_v1_1
       where  --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
       and    web.webPageDetails.name in ('Cancel Service', 'Call Start')
) r
, demo_system_event_dataset_for_call_center_global_v1_1 c
where r.ecid = c.--aepTenantId--.identification.core.ecid
and r.webPage = 'Cancel Service'
and c.--aepTenantId--.interactionDetails.core.callCenterAgent.callContractCancelled IN (true,false)
and c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic IN ('contract', 'invoice','complaint','wifi')
limit 15;
```

複製上述陳述式，並在&#x200B;**PSQL命令列介面**&#x200B;中執行。

**查詢結果**

```text
               ecid               |    webPage     | contact_callcenter_after_seconds | callfeeling | calltopic | callcontractcancelled 
----------------------------------+----------------+----------------------------------+-------------+-----------+-----------------------
 00630470663554417679969244202779 | Cancel Service |                             -797 | negative    | contract  | f
 00720875344152796154458668700428 | Cancel Service |                             -519 | positive    | contract  | f
 00746064605049656090779523644276 | Cancel Service |                              -62 | positive    | contract  | t
 00869613691740150556826953447162 | Cancel Service |                             -129 | negative    | contract  | t
 00943638725078228957873279219207 | Cancel Service |                             -750 | positive    | contract  | f
 01419076946514450291741574452702 | Cancel Service |                             -482 | neutral     | contract  | f
 01738842540109643781526526573341 | Cancel Service |                             -562 | neutral     | contract  | f
 02052460258994877317679083617975 | Cancel Service |                             -545 | neutral     | contract  | f
 02156496759733199802585567179589 | Cancel Service |                              -83 | neutral     | contract  | t
 02666934104296797891818818456669 | Cancel Service |                             -297 | positive    | contract  | t
 03059764265715537001416957172652 | Cancel Service |                             -243 | negative    | contract  | t
 03347899869945278660479273416679 | Cancel Service |                             -229 | positive    | contract  | t
 04258863338643046907489131372300 | Cancel Service |                             -588 | positive    | contract  | f
 04733864373954008966920919247566 | Cancel Service |                             -795 | neutral     | contract  | f
 05199871096822598772351169572451 | Cancel Service |                             -236 | positive    | contract  | t
(15 rows)
```

### 這些客戶的忠誠度設定檔為何？

在此查詢中，我們會加入已在Adobe Experience Platform中上線的CRM資料。 這使使用CRM資料擴充流失分析成為可能。

**SQL**

```sql
select r.*,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callFeeling,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic,
       l.--aepTenantId--.loyaltyDetails.level,
       l.--aepTenantId--.identification.core.crmId
from (
       select --aepTenantId--.identification.core.ecid ecid,
              web.webPageDetails.name as webPage,
              TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Call Start', 'seconds')
              OVER(PARTITION BY --aepTenantId--.identification.core.ecid
                  ORDER BY timestamp
                  ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
              AS contact_callcenter_after_seconds
       from   demo_system_event_dataset_for_website_global_v1_1
       where  --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
       and    web.webPageDetails.name in ('Cancel Service', 'Call Start')
) r
, demo_system_event_dataset_for_call_center_global_v1_1 c
, demo_system_profile_dataset_for_crm_global_v1_1 l
where r.ecid = c.--aepTenantId--.identification.core.ecid
and r.webPage = 'Cancel Service'
and l.--aepTenantId--.identification.core.ecid = r.ecid
and c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic IN ('contract', 'invoice','complaint','wifi','promo')
limit 15;
```

複製上述陳述式，並在&#x200B;**PSQL命令列介面**&#x200B;中執行。

**查詢結果**

```text
               ecid               |    webPage     | contact_callcenter_after_seconds | callfeeling | calltopic | level  |   crmid   
----------------------------------+----------------+----------------------------------+-------------+-----------+--------+-----------
 00630470663554417679969244202779 | Cancel Service |                             -797 | negative    | contract  | Bronze | 524483285
 00720875344152796154458668700428 | Cancel Service |                             -519 | positive    | contract  | Silver | 860696333
 00746064605049656090779523644276 | Cancel Service |                              -62 | positive    | contract  | Bronze | 072387270
 00869613691740150556826953447162 | Cancel Service |                             -129 | negative    | contract  | Bronze | 789347684
 00943638725078228957873279219207 | Cancel Service |                             -750 | positive    | contract  | Gold   | 033926162
 01419076946514450291741574452702 | Cancel Service |                             -482 | neutral     | contract  | Bronze | 105063634
 01738842540109643781526526573341 | Cancel Service |                             -562 | neutral     | contract  | Gold   | 791324509
 02052460258994877317679083617975 | Cancel Service |                             -545 | neutral     | contract  | Gold   | 443477555
 02156496759733199802585567179589 | Cancel Service |                              -83 | neutral     | contract  | Silver | 305085589
 02666934104296797891818818456669 | Cancel Service |                             -297 | positive    | contract  | Silver | 104266570
 03059764265715537001416957172652 | Cancel Service |                             -243 | negative    | contract  | Silver | 814175245
 03347899869945278660479273416679 | Cancel Service |                             -229 | positive    | contract  | Gold   | 377699708
 04258863338643046907489131372300 | Cancel Service |                             -588 | positive    | contract  | Silver | 298321657
 04733864373954008966920919247566 | Cancel Service |                             -795 | neutral     | contract  | Gold   | 655070958
 05199871096822598772351169572451 | Cancel Service |                             -236 | positive    | contract  | Gold   | 425688874
(15 rows)
```

### 他們從哪個地區造訪我們？

讓我們加入Adobe Experience Platform所擷取的地理資訊，例如經度、態度、城市、國家代碼，以便取得關於客戶流失的地理位置見解。

**SQL**

```sql
       select distinct r.ecid,
              r.city,
              r.countrycode,
              r.lat as latitude,
              r.lon as longitude,
              r.contact_callcenter_after_seconds as seconds_to_contact_callcenter,
              c.--aepTenantId--.interactionDetails.core.callCenterAgent.callFeeling,
              c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic,
              c.--aepTenantId--.interactionDetails.core.callCenterAgent.callContractCancelled,
              l.--aepTenantId--.loyaltyDetails.level,
              l.--aepTenantId--.identification.core.crmId
       from (
              select --aepTenantId--.identification.core.ecid ecid,
                     placeContext.geo._schema.latitude lat,
                     placeContext.geo._schema.longitude lon,
                     placeContext.geo.city,
                     placeContext.geo.countryCode,
                     web.webPageDetails.name as webPage,
                     TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Call Start', 'seconds')
                     OVER(PARTITION BY --aepTenantId--.identification.core.ecid
                         ORDER BY timestamp
                         ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
                     AS contact_callcenter_after_seconds
              from   demo_system_event_dataset_for_website_global_v1_1
              where  --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
              and    web.webPageDetails.name in ('Cancel Service', 'Call Start')
       ) r
       , demo_system_event_dataset_for_call_center_global_v1_1 c
       , demo_system_profile_dataset_for_crm_global_v1_1 l
       where r.ecid = c.--aepTenantId--.identification.core.ecid
       and r.webPage = 'Cancel Service'
       and l.--aepTenantId--.identification.core.ecid = r.ecid
       and c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic IN ('contract', 'invoice','complaint','wifi','promo')
       limit 15;
```

複製上述陳述式，並在&#x200B;**PSQL命令列介面**&#x200B;中執行。

**查詢結果**

```text
               ecid               |    city    | countrycode |  latitude  | longitude  | seconds_to_contact_callcenter | callfeeling | calltopic | callcontractcancelled | level  |   crmid   
----------------------------------+------------+-------------+------------+------------+-------------------------------+-------------+-----------+-----------------------+--------+-----------
 00630470663554417679969244202779 | Charlton   | GB          |   51.59119 |  -1.407848 |                          -797 | negative    | contract  | f                     | Bronze | 524483285
 00720875344152796154458668700428 | Ashley     | GB          | 51.4139633 | -2.2685462 |                          -519 | positive    | contract  | f                     | Silver | 860696333
 00746064605049656090779523644276 | Liverpool  | GB          | 53.4913801 |  -2.867264 |                           -62 | positive    | contract  | t                     | Bronze | 072387270
 00869613691740150556826953447162 | Langley    | GB          |  51.888151 |   -0.23924 |                          -129 | negative    | contract  | t                     | Bronze | 789347684
 00943638725078228957873279219207 | Eaton      | GB          | 53.2945961 | -0.9335791 |                          -750 | positive    | contract  | f                     | Gold   | 033926162
 01419076946514450291741574452702 | Tullich    | GB          | 57.4694803 | -3.1269422 |                          -482 | neutral     | contract  | f                     | Bronze | 105063634
 01738842540109643781526526573341 | Whitwell   | GB          | 54.3886617 |  -1.555363 |                          -562 | neutral     | contract  | f                     | Gold   | 791324509
 02052460258994877317679083617975 | Edinburgh  | GB          | 55.9309486 | -3.1859102 |                          -545 | neutral     | contract  | f                     | Gold   | 443477555
 02156496759733199802585567179589 | West End   | GB          |   53.46464 |    0.04134 |                           -83 | neutral     | contract  | t                     | Silver | 305085589
 02666934104296797891818818456669 | Newtown    | GB          | 51.3684218 | -1.3218754 |                          -297 | positive    | contract  | t                     | Silver | 104266570
 03059764265715537001416957172652 | Edinburgh  | GB          | 55.9309486 | -3.1859102 |                          -243 | negative    | contract  | t                     | Silver | 814175245
 03347899869945278660479273416679 | Liverpool  | GB          | 53.4913801 |  -2.867264 |                          -229 | positive    | contract  | t                     | Gold   | 377699708
 04258863338643046907489131372300 | Norton     | GB          | 52.2679288 | -1.1202549 |                          -588 | positive    | contract  | f                     | Silver | 298321657
 04733864373954008966920919247566 | Whitchurch | GB          | 51.4057505 | -2.5573746 |                          -795 | neutral     | contract  | f                     | Gold   | 655070958
 05199871096822598772351169572451 | Stapleford | GB          |   53.10672 |  -0.687802 |                          -236 | positive    | contract  | t                     | Gold   | 425688874
(15 rows)
```

## 客服中心互動分析

在上述查詢中，我們只會檢視最後因服務取消而聯絡客服中心的訪客。 我們希望將此考慮範圍更廣，並考量所有客服中心互動，包括（wifi、促銷、發票、投訴及合約）。

您需要編輯查詢，所以請先開啟記事本或括弧。

在Windows上，按一下Windows工具列中的[搜尋] — 圖示(1)，在[搜尋]欄位中輸入&#x200B;**記事本**，然後按一下(3) [記事本]結果：

![windows-start-notepad.png](./images/windows-start-notepad.png)

在Mac上

![osx-start-brackets.png](./images/osx-start-brackets.png)

將下列陳述式複製到記事本/括弧：

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
       l.--aepTenantId--.identification.core.crmId as crmid
from   demo_system_event_dataset_for_website_global_v1_1 e
      ,demo_system_event_dataset_for_call_center_global_v1_1 c
      ,demo_system_profile_dataset_for_crm_global_v1_1 l
where  e.--aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
and    e.web.webPageDetails.name in ('Cancel Service', 'Call Start')
and    e.--aepTenantId--.identification.core.ecid = c.--aepTenantId--.identification.core.ecid
and    l.--aepTenantId--.identification.core.ecid = e.--aepTenantId--.identification.core.ecid;
```

和取代

```text
enter your name
```

不要移除`/\*`和`\*/`。 您在記事本中修改過的陳述式應如下所示：

![edit-query-notepad.png](./images/editquerynotepad.png)

將您修改的陳述式從&#x200B;**記事本**&#x200B;複製到&#x200B;**PSQL命令列視窗**，然後按下Enter。 您應該會在PSQL命令列視窗中看到下列結果：

```text
tech-insiders:all=> select /* vangeluw */
       e._experienceplatform.identification.core.ecid as ecid,
       e.placeContext.geo.city as city,
       e.placeContext.geo._schema.latitude latitude,
       e.placeContext.geo._schema.longitude longitude,
       e.placeContext.geo.countryCode as countrycode,
       c._experienceplatform.interactionDetails.core.callCenterAgent.callFeeling as callFeeling,
       c._experienceplatform.interactionDetails.core.callCenterAgent.callTopic as callTopic,
       c._experienceplatform.interactionDetails.core.callCenterAgent.callContractCancelled as contractCancelled,
       l._experienceplatform.loyaltyDetails.level as loyaltystatus,
       l._experienceplatform.loyaltyDetails.points as loyaltypoints,
       l._experienceplatform.identification.core.crmId as crmid
from   demo_system_event_dataset_for_website_global_v1_1 e
      ,demo_system_event_dataset_for_call_center_global_v1_1 c
      ,demo_system_profile_dataset_for_crm_global_v1_1 l
where  e._experienceplatform.demoEnvironment.brandName IN ('Citi Signal')
and    e.web.webPageDetails.name in ('Cancel Service', 'Call Start')
and    e._experienceplatform.identification.core.ecid = c._experienceplatform.identification.core.ecid
and    l._experienceplatform.identification.core.ecid = e._experienceplatform.identification.core.ecid;
               ecid               |    city    |  latitude  | longitude  | countrycode | callFeeling | callTopic | contractCancelled | loyaltystatus | loyaltypoints |   crmid   
----------------------------------+------------+------------+------------+-------------+-------------+-----------+-------------------+---------------+---------------+-----------
 60082543727227001177187726544992 | Normanton  |  52.643749 |  -0.622129 | GB          | neutral     | contract  | f                 | Bronze        |         430.0 | 117969439
 03250145103029549687906576330844 | Charlton   |   51.59119 |  -1.407848 | GB          | none        | none      | f                 | Silver        |         585.0 | 271570836
 87322786414150971711720565798532 | Whitwell   | 54.3886617 |  -1.555363 | GB          | none        | none      | f                 | Bronze        |         872.0 | 570762160
 46736059905281823751180777497223 | Edinburgh  | 55.9309486 | -3.1859102 | GB          | none        | none      | f                 | Gold          |         482.0 | 980678773
 81958524709959359235057647680790 | Linton     | 54.0542238 | -2.0215836 | GB          | none        | none      | f                 | Bronze        |         666.0 | 341873673
 24854602977644353049269284436324 | Tullich    | 57.4694803 | -3.1269422 | GB          | negative    | contract  | f                 | Bronze        |         418.0 | 831581327
 24854602977644353049269284436324 | Tullich    | 57.4694803 | -3.1269422 | GB          | negative    | contract  | f                 | Bronze        |         418.0 | 831581327
```

接下來，您將持續儲存您的查詢（也稱為&#x200B;**建立資料表作為select**&#x200B;或&#x200B;**CTAS**），作為您將在Microsoft Power BI中使用的新資料集。

## 後續步驟

移至[2.1.5從查詢產生資料集](./ex5.md){target="_blank"}

返回[查詢服務](./query-service.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
