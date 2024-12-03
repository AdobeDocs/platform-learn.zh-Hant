---
title: 查詢服務 — 使用查詢服務
description: 查詢服務 — 使用查詢服務
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
exl-id: 31c14a9b-cb62-48ab-815c-caa6e832794f
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# 5.1.3使用查詢服務

## 目標

- 尋找和探索資料集
- 瞭解如何在查詢中處理Experience Data Models物件和屬性

## 內容

在本課程中，您將學習如何使用PSQL來擷取有關可用資料集的資訊、如何編寫Experience Data Model (XDM)的查詢，以及使用查詢服務和Citi Signal資料集編寫您的第一個簡單報告查詢。

## 基本查詢

在本節中，您將瞭解如何擷取可用資料集的資訊，以及如何透過XDM資料集的查詢正確擷取資料。

我們在1月初透過Adobe Experience Platform探索過的所有資料集，也都可以透過SQL介面做為表格存取。 若要列出這些表格，您可以使用&#x200B;**show tables；**&#x200B;命令。

在您的&#x200B;**PSQL命令列介面**&#x200B;中執行&#x200B;**顯示資料表；**。 （別忘了以分號結束您的命令）。

複製命令&#x200B;**show tables；**&#x200B;並在提示字元貼上：

![command-prompt-show-tables.png](./images/command-prompt-show-tables.png)

您會看到下列結果：

```text
aepenablementfy21:all=> show tables;
                            name                            |        dataSetId         |                            dataSet                             | description | resolved 
------------------------------------------------------------+--------------------------+----------------------------------------------------------------+-------------+----------
 demo_system_event_dataset_for_call_center_global_v1_1      | 5fd1a9dea30603194baeea43 | Demo System - Event Dataset for Call Center (Global v1.1)      |             | false
 demo_system_event_dataset_for_mobile_app_global_v1_1       | 5fd1a9de250e4f194bec84cd | Demo System - Event Dataset for Mobile App (Global v1.1)       |             | false
 demo_system_event_dataset_for_voice_assistants_global_v1_1 | 5fd1a9de49ee76194b85f73c | Demo System - Event Dataset for Voice Assistants (Global v1.1) |             | false
 demo_system_event_dataset_for_website_global_v1_1          | 5fd1a9dee3224d194cdfe786 | Demo System - Event Dataset for Website (Global v1.1)          |             | false
 demo_system_profile_dataset_for_loyalty_global_v1_1        | 5fd1a9de250e4f194bec84cc | Demo System - Profile Dataset for Loyalty (Global v1.1)        |             | false
 demo_system_profile_dataset_for_ml_predictions_global_v1_1 | 5fd1a9de241f58194b0cb117 | Demo System - Profile Dataset for ML Predictions (Global v1.1) |             | false
 demo_system_profile_dataset_for_mobile_app_global_v1_1     | 5fd1a9deddf353194a2e00b7 | Demo System - Profile Dataset for Mobile App (Global v1.1)     |             | false
 demo_system_profile_dataset_for_website_global_v1_1        | 5fd1a9de42a61c194dd7b810 | Demo System - Profile Dataset for Website (Global v1.1)        |             | false
 journey_step_events                                        | 5fd1a7f30268c5194bbb7e5e | Journey Step Events                                            |             | false
```

在冒號處，按空格鍵檢視結果集的下一頁，或輸入`q`還原到命令提示字元。

Platform中的每個資料集都有其對應的查詢服務表格。 您可以透過資料集UI找到資料集的表格：

![ui-dataset-tablename.png](./images/ui-dataset-tablename.png)

`demo_system_event_dataset_for_website_global_v1_1`資料表是與`Demo System - Event Schema for Website (Global v1.1)`資料集對應的查詢服務資料表。

若要查詢產品檢視位置的相關資訊，我們將選取&#x200B;**地理**&#x200B;資訊。

複製下列陳述式，並在&#x200B;**PSQL命令列介面**&#x200B;的提示字元貼上，然後按下Enter：

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

在您的查詢結果中，您會注意到Experience Data Model (XDM)中的欄可以是複雜型別，而不只是純量型別。 在上述查詢中，我們想要識別&#x200B;**commerce.productViews**&#x200B;確實發生的地理位置。 若要識別&#x200B;**commerce.productViews**，我們必須使用&#x200B;**瀏覽XDM模型。** （點）標籤法。

```text
aepenablementfy21:all=> select placecontext.geo
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
                  geo                   
----------------------------------------
 ("(57.4694803,-3.1269422)",Tullich,GB)
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
aepenablementfy21:all=> select placecontext.geo._schema.longitude
aepenablementfy21:all->       ,placecontext.geo._schema.latitude
aepenablementfy21:all->       ,placecontext.geo.city
aepenablementfy21:all->       ,placecontext.geo.countryCode
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  |  latitude  |  city   | countrycode 
------------+------------+---------+-------------
 -3.1269422 | 57.4694803 | Tullich | GB
(1 row)
```

別擔心，要取得特定屬性的路徑，有一個簡單的方式。 在接下來的部分中，您將瞭解如何操作。

您將需要編輯查詢，因此讓我們先開啟編輯器。

在Windows上

按一下Windows工具列中的&#x200B;**搜尋**&#x200B;圖示，在&#x200B;**搜尋**&#x200B;欄位中輸入&#x200B;**記事本**，按一下&#x200B;**記事本**&#x200B;結果：

![windows-start-notepad.png](./images/windows-start-notepad.png)

在Mac上

安裝[Brackets](https://github.com/adobe/brackets/releases/download/release-1.14/Brackets.Release.1.14.dmg)，或者如果您尚未安裝，則使用其他選擇的文字編輯器，然後依照指示操作。 安裝後，透過Mac的Spotlight搜尋來搜尋&#x200B;**Brackets**&#x200B;並開啟。

將下列陳述式複製到記事本或方括弧：

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

返回您的Adobe Experience Platform UI （應在瀏覽器中開啟）或導覽至[https://platform.adobe.com](https://platform.adobe.com)。

選取&#x200B;**結構描述**，在&#x200B;**搜尋**&#x200B;欄位中輸入`Demo System - Event Schema for Website (Global v1.1)`，然後從清單中選取`Demo System - Event Schema for Website (Global v1.1) Schema`。

![browse-schema.png](./images/browse-schema.png)

按一下物件，以探索&#x200B;**示範系統 — 網站（全域v1.1）**&#x200B;的事件結構描述的XDM模型。 展開&#x200B;**placecontext**、**geo**&#x200B;和&#x200B;**結構描述**&#x200B;的樹狀結構。 當您選取實際屬性&#x200B;**longitude**&#x200B;時，您會在醒目提示的紅色方塊中看到完整路徑。 若要複製屬性的路徑，請按一下複製路徑圖示。

![explore-schema-for-path.png](./images/explore-schema-for-path.png)

切換到您的記事本/括弧，並從第一行移除&#x200B;**your_attribute_path_here**。 將游標放在第一行上&#x200B;**選取**&#x200B;之後並貼上(CTRL-V)。

從記事本/方括弧複製修改過的陳述式，然後貼到&#x200B;**PSQL命令列介面**&#x200B;的提示字元，然後按Enter鍵。

結果應如下所示：

```text
aepenablementfy21:all=> select placeContext.geo._schema.longitude
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  
------------
 -3.1269422
```

下一步： [5.1.4查詢、查詢、查詢……和流失分析](./ex4.md)

[返回模組5.1](./query-service.md)

[返回所有模組](../../../overview.md)
