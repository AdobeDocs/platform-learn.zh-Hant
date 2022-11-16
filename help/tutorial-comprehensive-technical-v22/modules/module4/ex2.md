---
title: 查詢服務 — 使用查詢服務
description: 查詢服務 — 使用查詢服務
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: dbf19991-cb09-43cf-887c-52996dfd2986
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# 4.2使用查詢服務

## 目標

- 尋找和探索資料集
- 了解如何在查詢中處理Experience Data Model物件和屬性

## 內容

在本課程中，您將學習如何使用PSQL擷取可用資料集的相關資訊、如何撰寫Experience Data Model(XDM)查詢，以及如何使用Query Service和Citi Signal資料集撰寫您的第一個簡單報表查詢。

## 4.2.1基本查詢

在本課程中，您將了解如何擷取可用資料集的相關資訊，以及如何使用XDM資料集的查詢正確擷取資料。

我們在1開頭透過Adobe Experience Platform探索的所有資料集，也可以透過SQL介面以表格形式存取。 若要列出這些表格，您可以使用 **顯示表格；** 命令。

執行 **顯示表格；** 在 **PSQL命令行介面**. （別忘了以分號結束命令）。

複製命令 **顯示表格；** 並貼到提示：

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

在冒號處，按空格鍵查看結果集的下一頁，或輸入 `q` 回復到命令提示符。

Platform中的每個資料集都有對應的「查詢服務」表格。 您可以透過資料集ui找到資料集的表格：

![ui-dataset-tablename.png](./images/ui-dataset-tablename.png)

此 `demo_system_event_dataset_for_website_global_v1_1` 表是與 `Demo System - Event Schema for Website (Global v1.1)` 資料集。

若要查詢某個產品被檢視位置的相關資訊，我們將選取 **地理** 資訊。

複製下方的陳述式，然後貼到您 **PSQL命令行介面** 然後點擊輸入：

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

在查詢結果中，您會發現Experience Data Model(XDM)中的欄可能是複雜類型，而不只是標量類型。 在上述查詢中，我們要識別 **commerce.productViews** 已發生。 識別 **commerce.productViews** 我們必須使用 **.** （點）記號。

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

請注意，結果是平面物件，而非單一值？ 此 **placecontext.geo** 物件包含四個屬性：模式、國家/地區和城市。 當物件宣告為欄時，會將整個物件傳回為字串。 XDM架構可能比您熟悉的更複雜，但功能非常強大，且旨在支援許多解決方案、管道和使用案例。

若要選取物件的個別屬性，請使用 **.** （點）記號。

複製下方的陳述式，然後貼到您 **PSQL命令行介面**:

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

上述查詢的結果應如下所示。
結果現在是設定的簡單值：

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

不用擔心，您可以透過簡單的方式取得特定屬性的路徑。 在以下部分，您將學習如何操作。

您需要編輯查詢，因此，我們先開啟一個編輯器。

在Windows上

按一下 **搜尋** 表徵圖，鍵入 **記事本** 在 **搜尋** 欄位，按一下 **記事本** 結果：

![windows-start-notepad.png](./images/windows-start-notepad.png)

在Mac

安裝 [方括弧](https://github.com/adobe/brackets/releases/download/release-1.14/Brackets.Release.1.14.dmg) 或者，如果您沒有安裝文本編輯器，則使用其他選擇的文本編輯器，並按照說明進行操作。 安裝後，請搜尋 **方括弧** 透過Mac的精選搜尋並開啟。

將以下語句複製到記事本或括弧中：

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

返回Adobe Experience Platform UI（應在瀏覽器中開啟）或導覽至 [https://platform.adobe.com](https://platform.adobe.com).

選擇 **結構**，輸入 `Demo System - Event Schema for Website (Global v1.1)` 在 **搜尋** 欄位和選取 `Demo System - Event Schema for Website (Global v1.1) Schema` 從清單中。

![browse-schema.png](./images/browse-schema.png)

探索適用於 **示範系統 — 網站事件結構（全域v1.1）**，方法是按一下物件。 展開樹 **placecontext**, **地理** 和 **綱要**. 選取實際屬性時 **經度**，您會在醒目提示的紅色方塊中看到完整路徑。 要複製屬性的路徑，請按一下複製路徑表徵圖。

![explore-schema-for-path.png](./images/explore-schema-for-path.png)

切換到記事本/括弧並刪除 **your_attribute_path_here** 從第一行開始。 將游標放在 **選取** 在第一行上並貼上(CTRL-V)。

從記事本/方括弧複製修改後的語句，然後貼到您的 **PSQL命令行介面** 然後按Enter。

結果應該如下：

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

下一步： [4.3查詢、查詢、查詢……和流失分析](./ex3.md)

[返回模組4](./query-service.md)

[返回所有模組](../../overview.md)
