---
title: 查詢服務 — 查詢服務API
description: 查詢服務 — 查詢服務API
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 2%

---

# 5.1.7查詢服務API

## 目標

- 使用「查詢服務API」來管理查詢範本與查詢排程

## 內容

在本練習中，您將執行API呼叫，以使用Postman集合管理查詢範本和查詢排程。 您將定義查詢範本、執行一般查詢和CTAS查詢。 **CTAS**&#x200B;查詢（建立資料表做為選取查詢）會將其結果集儲存在明確資料集中。 雖然一般查詢儲存在隱含（或系統產生的）資料集中，但通常會以parquet檔案格式匯出。

## 文件

- [Adobe Experience Platform查詢服務說明](https://experienceleague.adobe.com/docs/experience-platform/query/api/getting-started.html)
- [查詢服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml)

## 5.1.7.1查詢服務API

查詢服務API可讓您針對Adobe Experience Platform Data-Lake管理非互動式查詢。

非互動式表示執行查詢的請求將不會導致立即回應。 將會處理查詢，其結果集將儲存在隱含或明確（CTAS：建立表格為選取）的資料集中。

## 5.1.7.2範例查詢

作為範例查詢，您將使用[4.3中列出的第一個查詢 — 查詢、查詢、查詢……和流失分析](./ex3.md)：

我們每天檢視多少項產品？

**SQL**

```sql
select date_format( timestamp , 'yyyy-MM-dd') AS Day,
       count(*) AS productViews
from   demo_system_event_dataset_for_website_global_v1_1
where  --aepTenantId--.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal')
and eventType = 'commerce.productViews'
group by Day
limit 10;
```

## 5.1.7.3查詢

在電腦上開啟Postman。 在單元3中，您已建立Postman環境並匯入Postman集合。 請依照[練習2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md)中的指示操作，以防您尚未執行該操作。

在您匯入的Postman集合中，您會看到資料夾&#x200B;**3。 查詢服務**。 如果沒有看見此資料夾，請重新下載[Postman集合](./../../../assets/postman/postman_profile.zip)，並依照[練習2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md)中的指示，在Postman中重新匯入該集合。

![QS](./images/pm3.png)

>[!NOTE]
>
>此時僅資料夾&#x200B;**1。 查詢**&#x200B;包含要求。 其他請求將會在圖層階段新增。

開啟該資料夾並瞭解查詢服務API呼叫，以執行、監控和下載查詢結果集。

對具有下列裝載的[/query/queries]的POST呼叫將觸發我們查詢的執行；

### 5.1.7.3.1建立查詢

按一下名為&#x200B;**1.1 QS — 建立查詢**&#x200B;的要求，並移至&#x200B;**標頭**。 然後您會看到以下內容：

![區段](./images/s1_call.png)

讓我們專注於此標題欄位：

| 索引鍵 | 值 |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>您必須指定正在使用的Adobe Experience Platform沙箱名稱。 標頭欄位&#x200B;**x-sandbox-name**&#x200B;應為`--module7sandbox--`。

移至此請求的&#x200B;**內文**&#x200B;區段。 在此請求的&#x200B;**內文**&#x200B;中，您會看到下列內容：

![區段](./images/s1_bodydtl.png)

```sql
{
    "name" : "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"description": "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "module7:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

注意：請更新下列要求中的變數&#x200B;**名稱**，將&#x200B;**ldap**&#x200B;取代為您的特定&#x200B;**ldap**。

新增您的特定&#x200B;**ldap**&#x200B;之後，Body應該看起來類似這樣：

```json
{
    "name" : "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "module7:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

>[!NOTE]
>
>上述JSON內文中的索引鍵&#x200B;**dbName**&#x200B;參考您Adobe Experience Platform執行個體中使用的沙箱。 如果您使用PROD沙箱，dbName應該是&#x200B;**prod：all**；如果您使用另一個沙箱（例如執行個體&#x200B;**module7**），dbName應該等於&#x200B;**module7：all**。

接著，按一下藍色的&#x200B;**傳送**&#x200B;按鈕以建立區段並檢視其結果。

![區段](./images/s1_bodydtl_results.png)

成功後，POST請求將傳回以下回應：

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "module7:all",
        "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
        "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
        "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
    },
    "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
    "elapsedTime": 0,
    "updated": "2021-01-20T13:23:13.951Z",
    "client": "API",
    "userId": "A3392DB95FFF08EE0A495E87@techacct.adobe.com",
    "created": "2021-01-20T13:23:13.951Z",
    "_links": {
        "self": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

查詢的目前&#x200B;**狀態**&#x200B;是&#x200B;**SUBMITTED**，一旦執行，其狀態將變成&#x200B;**SUCCESS**。

您也可以透過Adobe Experience Platform UI查詢已提交的查詢、開啟[Adobe Experience Platform](https://experience.adobe.com/#/@experienceplatform/platform/home)、導覽至&#x200B;**查詢**、至&#x200B;**記錄**&#x200B;並選取您的查詢：

![區段](./images/s1_bodydtl_results_qs.png)

### 5.1.7.3.2取得查詢

按一下名為&#x200B;**1.2 QS — 取得查詢**&#x200B;並移至&#x200B;**標頭**。 然後您會看到以下內容：

![區段](./images/s2_call.png)

讓我們專注於此標題欄位：

| 索引鍵 | 值 |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>您必須指定正在使用的Adobe Experience Platform沙箱名稱。 標頭欄位&#x200B;**x-sandbox-name**&#x200B;應為`--module7sandbox--`。

移至&#x200B;**引數**。 然後您會看到以下內容：

![區段](./images/s2_call_p.png)

**orderby**&#x200B;引數可讓您根據&#x200B;**created**&#x200B;屬性指定排序順序。 請注意&#x200B;**&#39;-&#39;**&#x200B;登入已建立之前，這表示傳回查詢清單的順序將使用其建立日期，順序為&#x200B;**遞減**。 您的查詢應位於清單頂端。

接著，按一下藍色的&#x200B;**傳送**&#x200B;按鈕以建立區段並檢視其結果。

![區段](./images/s2_bodydtl_results.png)

成功後，請求將傳回與以下內容類似的回應。 回應的&#x200B;**狀態**&#x200B;可能是&#x200B;**已提交**、**IN_PROGRESS**&#x200B;或&#x200B;**成功**。 查詢可能需數分鐘才會有&#x200B;**SUCCESS**&#x200B;狀態。 您可以重複傳送此要求多次，直到看到&#x200B;**SUCCESS**&#x200B;狀態為止。

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "module7:all",
                "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
                "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
                "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
            },
            "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
            "state": "SUCCESS",
            "rowCount": 1,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "elapsedTime": 217481,
            "updated": "2021-01-20T13:26:51.432Z",
            "client": "API",
            "userId": "A3392DB95FFF08EE0A495E87@techacct.adobe.com",
            "created": "2021-01-20T13:23:13.951Z",
            "_links": {
                "self": {
                    "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "60080ace62c49a19490c5870",
                        "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/60080ace62c49a19490c5870"
                    }
                ]
            }
        }
     ]
    },
    "version": 1
}
```

當狀態為&#x200B;**SUCCESS**&#x200B;時，請繼續下一個要求。

### 5.1.7.3.3取得查詢狀態

按一下名為&#x200B;**1.3 QS — 取得查詢狀態**&#x200B;並移至&#x200B;**標頭**。 然後您會看到以下內容：

![區段](./images/s3_call.png)

讓我們專注於此標題欄位：

| 索引鍵 | 值 |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>您必須指定正在使用的Adobe Experience Platform沙箱名稱。 標頭欄位&#x200B;**x-sandbox-name**&#x200B;應為`--module7sandbox--`。

接著，按一下藍色的&#x200B;**傳送**&#x200B;按鈕以建立區段並檢視其結果。

![區段](./images/s3_bodydtl_results.png)

成功後，請求將傳回與以下內容類似的回應。

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "module7:all",
        "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
        "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
        "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
    },
    "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
    "state": "SUCCESS",
    "rowCount": 1,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
    "elapsedTime": 217481,
    "updated": "2021-01-20T13:26:51.432Z",
    "client": "API",
    "userId": "A3392DB95FFF08EE0A495E87@techacct.adobe.com",
    "created": "2021-01-20T13:23:13.951Z",
    "_links": {
        "self": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "referenced_datasets": [
            {
                "id": "60080ace62c49a19490c5870",
                "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/60080ace62c49a19490c5870"
            }
        ]
    }
}
```

當查詢達到&#x200B;**SUCCESS**&#x200B;的狀態時，回應也會指出查詢透過&#x200B;**rowCount**&#x200B;屬性擷取的列數。 在我們的範例中，查詢會傳回10列。 讓我們在下一節中瞭解如何擷取10列。

### 5.1.7.3.4擷取查詢結果

上述&#x200B;**SUCCESS**&#x200B;回應包含&#x200B;**referenced_datasets**&#x200B;屬性，其指向儲存查詢結果的隱含資料集。 若要存取結果，我們會使用其&#x200B;**href**&#x200B;或&#x200B;**id**&#x200B;屬性。

按一下名為&#x200B;**1.4 QS — 取得查詢結果**&#x200B;並移至&#x200B;**標頭**。 然後您會看到以下內容：

![區段](./images/s4_call.png)

讓我們專注於此標題欄位：

| 索引鍵 | 值 |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>您必須指定正在使用的Adobe Experience Platform沙箱名稱。 標頭欄位&#x200B;**x-sandbox-name**&#x200B;應為`--module7sandbox--`。

接著，按一下藍色的&#x200B;**傳送**&#x200B;按鈕以建立區段並檢視其結果。

![區段](./images/s4_bodydtl_results.png)

此請求的回應將指向資料集檔案：

```json
{
    "60080ace62c49a19490c5870": {
        "name": "Demo System - Event Dataset for Website (Global v1.1)",
        "description": "Demo System - Event Dataset for Website (Global v1.1)",
        "enableErrorDiagnostics": false,
        "tags": {
            "adobe/siphon/partition/definition": [
                "day(timestamp, _ACP_DATE)",
                "identity(_ACP_BATCHID)"
            ],
            "aep/siphon/partitions": [
                "_ACP_DATE",
                "_ACP_BATCHID"
            ],
            "acp_granular_plugin_validation_flags": [
                "identity:enabled",
                "profile:enabled"
            ],
            "adobe/siphon/buffered-promotion-recency": [
                "live"
            ],
            "adobe/siphon/use-buffered-promotion": [
                "true"
            ],
            "adobe/pqs/table": [
                "demo_system_event_dataset_for_website_global_v1_1"
            ],
            "aep/siphon/expire-snapshot-timestamp": [
                "1611141272703"
            ],
            "acp_granular_validation_flags": [
                "requiredFieldCheck:enabled"
            ],
            "acp_validationContext": [
                "enabled"
            ],
            "adobe/siphon/table/format": [
                "iceberg"
            ],
            "unifiedProfile": [
                "enabled:true",
                "enabledAt:2021-01-20 10:49:51"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "imsOrg": "907075E95BF479EC0A495C73@AdobeOrg",
        "sandboxId": "62cd9f38-8529-4b05-8d9f-388529db0540",
        "lastBatchId": "01EWFQZ15XRNNB1FPKPW5ETRVP",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "01EWFQZ15XRNNB1FPKPW5ETRVP",
        "version": "1.0.6",
        "created": 1611139790698,
        "updated": 1611149266031,
        "createdClient": "750e24ee855b4ac18ccc4f4817f96ee1",
        "createdUser": "3A260B485E909A170A495E76@techacct.adobe.com",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "viewId": "60080ace62c49a19490c5871",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/60080ace62c49a19490c5870/views/60080ace62c49a19490c5871/files",
        "schemaMetadata": {
            "delta": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/experienceplatform/schemas/d9b88a044ad96154637965a97ed63c7b20bdf2ab3b4f642e",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

>[!NOTE]
>
>我們即將新增更多練習，協助您與查詢服務API互動。

下一步： [摘要與優點](./summary.md)

[返回模組5.1](./query-service.md)

[返回所有模組](../../../overview.md)
