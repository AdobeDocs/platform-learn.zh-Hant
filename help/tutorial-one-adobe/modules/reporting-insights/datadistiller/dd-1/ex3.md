---
title: 查詢服務 — 使用查詢服務
description: 查詢服務 — 使用查詢服務
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
exl-id: ce04fa00-0247-4693-ba60-efc1746b9fec
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# 2.1.3使用查詢服務

## 目標

- 尋找和探索資料集
- 瞭解如何在查詢中處理Experience Data Models物件和屬性

## 內容

在本課程中，您將學習如何使用PSQL來擷取有關可用資料集的資訊、如何編寫Experience Data Model (XDM)的查詢，以及使用查詢服務和Citi Signal資料集編寫您的第一個簡單報告查詢。

## 基本查詢

在本節中，您將瞭解如何擷取可用資料集的資訊，以及如何透過XDM資料集的查詢正確擷取資料。

我們在1月初透過Adobe Experience Platform探索過的所有資料集，也都可以透過SQL介面做為表格存取。 若要列出這些表格，您可以使用&#x200B;**show tables；**&#x200B;命令。

在您的&#x200B;**PSQL命令列介面**&#x200B;中執行`show tables;`。 （別忘了以分號結束您的命令）。

複製命令`show tables;`並在提示時貼上：

![command-prompt-show-tables.png](./images/commandpromptshowtables.png)

您會看到下列結果：

```text
tech-insiders:all=> show tables;
                               name                               |                                                  dataSetId                                                   |                                       dataSet                                        | description |        labels        
------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+-------------+----------------------
 ajo_bcc_feedback_event_dataset                                   | 672a07cb7728e82aefa1ec56                                                                                     | AJO BCC Feedback Event Dataset                                                       |             | 
 ajo_classification_dataset                                       | 672a07cab55b0d2aef6f9626                                                                                     | AJO Classification Dataset                                                           |             | 
 ajo_consent_service_dataset                                      | 672a07c80fd5fd2aee4155ca                                                                                     | AJO Consent Service Dataset                                                          |             | 'PROFILE'
 ajo_email_tracking_experience_event_dataset                      | 672a07c926d57d2aef020230                                                                                     | AJO Email Tracking Experience Event Dataset                  :
                               name                               |                                                  dataSetId                                                   |                                       dataSet                                        | description |        labels        
------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+-------------+----------------------
 ajo_bcc_feedback_event_dataset                                   | 672a07cb7728e82aefa1ec56                                                                                     | AJO BCC Feedback Event Dataset                                                       |             | 
 ajo_classification_dataset                                       | 672a07cab55b0d2aef6f9626                                                                                     | AJO Classification Dataset                                                           |             | 
 ajo_consent_service_dataset                                      | 672a07c80fd5fd2aee4155ca                                                                                     | AJO Consent Service Dataset                                                          |             | 'PROFILE'
 ajo_email_tracking_experience_event_dataset                      | 672a07c926d57d2aef020230                                                                                     | AJO Email Tracking Experience Event Dataset   
```

在冒號處，按空格鍵檢視結果集的下一頁，或輸入`q`還原到命令提示字元。

AEP中的每個資料集都有其對應的查詢服務表格。 您可以透過資料集UI找到資料集的表格：

![ui-dataset-tablename.png](./images/uidatasettablename.png)

`demo_system_event_dataset_for_website_global_v1_1`資料表是與`Demo System - Event Schema for Website (Global v1.1)`資料集對應的查詢服務資料表。

若要查詢產品檢視位置的相關資訊，我們將選取&#x200B;**地理**&#x200B;資訊。

複製下列查詢並貼到&#x200B;**PSQL命令列介面**&#x200B;的提示字元中，然後按下Enter：

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

在您的查詢結果中，您會注意到Experience Data Model (XDM)中的欄可以是複雜型別，而不只是純量型別。 在上述查詢中，我們想要識別&#x200B;**commerce.productViews**&#x200B;確實發生的地理位置。 若要識別&#x200B;**commerce.productViews**，我們必須使用&#x200B;**瀏覽XDM模型。** （點）標籤法。

```text
tech-insiders:all=> select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
                 geo                  
--------------------------------------
 ("(51.59119,-1.407848)",Charlton,GB)
(1 row)
```

是否注意到結果為平面物件，而非單一值？ **placecontext.geo**&#x200B;物件包含四個屬性：結構描述、國家/地區和城市。 當物件宣告為欄時，會將整個物件傳回為字串。 XDM結構描述可能比您熟悉的要複雜，但它的功能非常強大，而且架構可支援許多解決方案、管道和使用案例。

若要選取物件的個別屬性，請使用&#x200B;**。** （點）標籤法。

複製下列陳述式，並貼到&#x200B;**PSQL命令列介面**&#x200B;的提示字元上：

```sql
select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

上述查詢的結果看起來應該像這樣。
結果現在是一組簡單值：

```text
tech-insiders:all=> select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
 longitude | latitude |   city   | countrycode 
-----------+----------+----------+-------------
 -1.407848 | 51.59119 | Charlton | GB
(1 row)
```

別擔心，要取得特定屬性的路徑，有一個簡單的方式。 在接下來的部分中，您將瞭解如何操作。

您將需要編輯查詢，因此讓我們先開啟編輯器。

在Windows上：使用&#x200B;**記事本**

在Mac上：安裝並開啟任何選擇的文字編輯器應用程式。

將下列陳述式複製到文字編輯器：

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

返回您的Adobe Experience Platform UI （應在瀏覽器中開啟）或導覽至[Adobe Experience Platform](https://experience.adobe.com/platform)。

選取&#x200B;**結構描述**，在&#x200B;**搜尋**&#x200B;欄位中輸入`Demo System - Event Schema for Website`並按一下以開啟結構描述`Demo System - Event Schema for Website (Global v1.1) Schema`。

![browse-schema.png](./images/browseschema.png)

按一下物件，以探索&#x200B;**示範系統 — 網站（全域v1.1）**&#x200B;的事件結構描述的XDM模型。 展開&#x200B;**placecontext**、**geo**&#x200B;和&#x200B;**結構描述**&#x200B;的樹狀結構。 當您選取實際屬性&#x200B;**longitude**&#x200B;時，您會在醒目提示的紅色方塊中看到完整路徑。 若要複製屬性的路徑，請按一下複製路徑圖示。

![explore-schema-for-path.png](./images/exploreschemaforpath.png)

切換到您的記事本/括弧，並從第一行移除&#x200B;**your_attribute_path_here**。 將游標放在第一行上&#x200B;**選取**&#x200B;之後並貼上(CTRL-V)。

![explore-schema-for-path.png](./images/exploreschemaforpath1.png)

複製修改過的陳述式，並貼到&#x200B;**PSQL命令列介面**&#x200B;的提示字元中，然後按下Enter。

結果應如下所示：

```text
tech-insiders:all=> select placeContext.geo._schema.longitude
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
 longitude 
-----------
 -1.407848
(1 row)
```

## 後續步驟

移至[2.1.4查詢、查詢、查詢……和流失分析](./ex4.md){target="_blank"}

返回[查詢服務](./query-service.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
