---
title: 查詢服務 — 查詢服務API
description: 查詢服務 — 查詢服務API
kt: 5342
doc-type: tutorial
exl-id: d356f7e2-523b-41a2-9cc6-1ea2a028c3a7
source-git-commit: c49b41e1b033573dbebc9ced3a3f4071bf94d04e
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 2%

---

# 5.1.8查詢服務API

## 目標

- 使用「查詢服務API」來管理查詢範本與查詢排程

## 內容

在本練習中，您將執行API呼叫，以使用Postman集合管理查詢範本和查詢排程。 您將定義查詢範本、執行一般查詢和CTAS查詢。 **CTAS**&#x200B;查詢（建立資料表做為選取查詢）會將其結果集儲存在明確資料集中。 雖然一般查詢儲存在隱含（或系統產生的）資料集中，但通常會以parquet檔案格式匯出。

## 文件

- [Adobe Experience Platform查詢服務說明](https://experienceleague.adobe.com/docs/experience-platform/query/api/getting-started.html?lang=zh-Hant)
- [查詢服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml)

## 查詢服務API

查詢服務API可讓您針對Adobe Experience Platform Data-Lake管理非互動式查詢。

非互動式表示執行查詢的請求將不會導致立即回應。 將會處理查詢，其結果集將儲存在隱含或明確（CTAS：建立表格為選取）的資料集中。

## 範例查詢

作為範例查詢，您將使用[4.3中列出的第一個查詢 — 查詢、查詢、查詢……和流失分析](./ex3.md)：

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

## 查詢

>[!IMPORTANT]
>
>如果您是Adobe員工，請依照這裡的指示使用[PostBuster](./../../../postbuster.md)。

在電腦上開啟Postman。 在模組2.1中，您已建立Postman環境並匯入Postman集合。 請依照[練習2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md)中的指示操作，以防您尚未執行該操作。

在您匯入的Postman集合中，您會看到資料夾&#x200B;**3。 查詢服務**。 如果沒有看見此資料夾，請重新下載[Postman集合](./../../../assets/postman/postman_profile.zip)，並依照[練習2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md)中的指示，在Postman中重新匯入該集合。

![QS](./images/pm3.png)

>[!NOTE]
>
>此時僅資料夾&#x200B;**1。 查詢**&#x200B;包含要求。 其他請求將會在圖層階段新增。

開啟該資料夾並瞭解查詢服務API呼叫，以執行、監控和下載查詢結果集。

對具有下列裝載的[/query/queries]的POST呼叫將觸發我們查詢的執行；

### 建立查詢

按一下名為&#x200B;**1.1 QS — 建立查詢**&#x200B;的要求，並移至&#x200B;**標頭**。 然後您會看到以下內容：

![區段](./images/s1_call.png)

讓我們專注於此標題欄位：

| 索引鍵 | 值 |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>您必須指定正在使用的Adobe Experience Platform沙箱名稱。 標頭欄位&#x200B;**x-sandbox-name**&#x200B;應為`--aepSandboxName--`。

移至此請求的&#x200B;**內文**&#x200B;區段。 在此請求的&#x200B;**內文**&#x200B;中，您會看到下列內容：

![區段](./images/s1_bodydtl.png)

```sql
{
    "name" : "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"description": "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "--aepSandboxName--:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

注意：請更新下列要求中的變數&#x200B;**name**，將&#x200B;**ldap**&#x200B;取代為您的特定&#x200B;**—aepUserLdap—**。

新增您的特定&#x200B;**ldap**&#x200B;之後，Body應該看起來類似這樣：

```json
{
    "name" : "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "tech-insiders:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

>[!NOTE]
>
>上述JSON內文中的索引鍵&#x200B;**dbName**&#x200B;參考您Adobe Experience Platform執行個體中使用的沙箱。 若您使用PROD沙箱，dbName應為&#x200B;**prod：all**；若您使用其他沙箱（例如&#x200B;**tech-insidets**），dbName應等於&#x200B;**tech-insidets：all**。

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

### 取得查詢

按一下名為&#x200B;**1.2 QS — 取得查詢**&#x200B;並移至&#x200B;**標頭**。 然後您會看到以下內容：

![區段](./images/s2_call.png)

讓我們專注於此標題欄位：

| 索引鍵 | 值 |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>您必須指定正在使用的Adobe Experience Platform沙箱名稱。 標頭欄位&#x200B;**x-sandbox-name**&#x200B;應為`--aepSandboxName--`。

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
            "sessionType": "HTTP_SESSION",
            "request": {
                "dbName": "tech-insiders:all",
                "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
                "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
                "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
            },
            "computeMetrics": null,
            "clientId": "b7d8a1fc396242889bb31dc83644e91d",
            "state": "IN_PROGRESS",
            "rowCount": 0,
            "isService": false,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "a535234e-dc0c-42ea-bcad-eb09c5997d76",
            "elapsedTime": 8088,
            "updated": "2024-12-04T14:17:10.627Z",
            "client": "API",
            "effectiveSQL": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
            "userId": "8CD31E54673C49EE0A495E05@techacct.adobe.com",
            "isParentLevel": true,
            "created": "2024-12-04T14:14:22.637Z",
                "version": 1,
    "_links": {
        "next": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries?orderby=-created&start=2024-11-22T00:32:04.505Z"
        },
        "prev": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries?orderby=-created&start=2024-12-04T14:14:22.637Z&isPrevLink=true"
        }
    }
}
```

當狀態為&#x200B;**SUCCESS**&#x200B;時，請繼續下一個要求。

### 取得查詢狀態

按一下名為&#x200B;**1.3 QS — 取得查詢狀態**&#x200B;並移至&#x200B;**標頭**。 然後您會看到以下內容：

![區段](./images/s3_call.png)

讓我們專注於此標題欄位：

| 索引鍵 | 值 |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>您必須指定正在使用的Adobe Experience Platform沙箱名稱。 標頭欄位&#x200B;**x-sandbox-name**&#x200B;應為`--aepSandboxName--`。

接著，按一下藍色的&#x200B;**傳送**&#x200B;按鈕以建立區段並檢視其結果。

![區段](./images/s3_bodydtl_results.png)

成功後，請求將傳回與以下內容類似的回應。

```json
{
    "isInsertInto": false,
    "sessionType": "HTTP_SESSION",
    "request": {
        "dbName": "tech-insiders:all",
        "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
        "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
        "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
    },
    "computeMetrics": {
        "executorVMSeconds": 138,
        "clusterCpuSeconds": 3312,
        "clusterVMHours": 0.07666666805744171,
        "driverVMSeconds": 138,
        "clusterVMSeconds": 276
    },
    "clientId": "b7d8a1fc396242889bb31dc83644e91d",
    "state": "SUCCESS",
    "rowCount": 1,
    "isService": false,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "a535234e-dc0c-42ea-bcad-eb09c5997d76",
    "elapsedTime": 199219,
    "updated": "2024-12-04T14:17:41.856Z",
    "client": "API",
    "effectiveSQL": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
    "userId": "8CD31E54673C49EE0A495E05@techacct.adobe.com",
    "isParentLevel": true,
    "created": "2024-12-04T14:14:22.637Z",
    "_links": {
        "self": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/a535234e-dc0c-42ea-bcad-eb09c5997d76",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/a535234e-dc0c-42ea-bcad-eb09c5997d76",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "referenced_datasets": [
            {
                "id": "672a10b1074ceb2af0aa7034",
                "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/672a10b1074ceb2af0aa7034"
            }
        ]
    }
}
```

當查詢達到&#x200B;**SUCCESS**&#x200B;的狀態時，回應也會指出查詢透過&#x200B;**rowCount**&#x200B;屬性擷取的列數。 在我們的範例中，查詢會傳回10列。 讓我們在下一節中瞭解如何擷取10列。

### 擷取查詢結果

上述&#x200B;**SUCCESS**&#x200B;回應包含&#x200B;**referenced_datasets**&#x200B;屬性，其指向儲存查詢結果的隱含資料集。 若要存取結果，我們會使用其&#x200B;**href**&#x200B;或&#x200B;**id**&#x200B;屬性。

按一下名為&#x200B;**1.4 QS — 取得查詢結果**&#x200B;並移至&#x200B;**標頭**。 然後您會看到以下內容：

![區段](./images/s4_call.png)

讓我們專注於此標題欄位：

| 索引鍵 | 值 |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>您必須指定正在使用的Adobe Experience Platform沙箱名稱。 標頭欄位&#x200B;**x-sandbox-name**&#x200B;應為`--aepSandboxName--`。

接著，按一下藍色的&#x200B;**傳送**&#x200B;按鈕以建立區段並檢視其結果。

![區段](./images/s4_bodydtl_results.png)

此請求的回應將指向資料集檔案：

```json
{
    "672a10b1074ceb2af0aa7034": {
        "name": "Demo System - Event Dataset for Website (Global v1.1)",
        "description": "Demo System - Event Dataset for Website (Global v1.1)",
        "enableErrorDiagnostics": false,
        "tags": {
            "adobe/siphon/partition/definition": [
                "day(timestamp, _ACP_DATE)",
                "identity(_ACP_BATCHID)"
            ],
            "adobe/siphon/meta": [
                "acpBufferedFlag::false"
            ],
            "aep/siphon/partitions": [
                "_ACP_DATE",
                "_ACP_BATCHID"
            ],
            "acp_granular_plugin_validation_flags": [
                "identity:enabled",
                "profile:disabled"
            ],
            "adobe/pqs/table": [
                "demo_system_event_dataset_for_website_global_v1_1"
            ],
            "acp_granular_validation_flags": [
                "requiredFieldCheck:enabled"
            ],
            "aep/siphon/cleanup/trash/timestamp": [
                "1733302532212"
            ],
            "acp_validationContext": [
                "enabled"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ],
            "unifiedProfile": [
                "enabled:true",
                "enabledAt:2024-11-05 12:33:59"
            ],
            "aep/siphon/cleanup/meta/timestamp": [
                "1733302532287"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "state": "ACTIVE",
        "imsOrg": "907075E95BF479EC0A495C73@AdobeOrg",
        "sandboxId": "79e3c8b2-0609-4564-a3c8-b20609a5648c",
        "extensions": {
            "adobe_lakeHouse": {
                "metrics": {
                    "storageSize": 810709,
                    "rowCount": 1141,
                    "asOf": 1732494676514
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "1.0.21",
        "created": 1730810034023,
        "updated": 1733302532348,
        "createdClient": "d75039d36ca543c78612f7aac18e6c2b",
        "createdUser": "53FB1E5E66CDC87D0A495FC0@techacct.adobe.com",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "672a10b2074ceb2af0aa7035",
        "fileDescription": {
            "format": "parquet"
        },
        "files": "@/dataSetFiles?dataSetId=672a10b1074ceb2af0aa7034",
        "schemaRef": {
            "id": "https://ns.adobe.com/experienceplatform/schemas/d9b88a044ad96154637965a97ed63c7b20bdf2ab3b4f642e",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

下一步： [摘要與優點](./summary.md)

[返回模組5.1](./query-service.md)

[返回所有模組](../../../overview.md)
