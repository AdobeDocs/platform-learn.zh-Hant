---
title: 基礎 — 即時客戶設定檔 — 建立區段 — API
description: 基礎 — 即時客戶設定檔 — 建立區段 — API
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 3%

---

# 2.1.5建立區段 — API

在本練習中，您將使用Postman和Adobe I/O，建立區段並運用Adobe Experience Platform的API將該區段的結果儲存為資料集。

## Story

在即時客戶個人檔案中，所有個人檔案資料都會與事件資料和現有區段會籍一起顯示。 顯示的資料可來自任何地方，包括Adobe應用程式和外部解決方案。 這是Adobe Experience Platform中功能最強大的檢視方式，也是體驗記錄系統。

## 2.1.5.1 — 透過平台API建立區段

前往Postman。

找到集合： **_Adobe Experience Platform啟用**。 在此集合中，您會看到資料夾&#x200B;**2。 區段**。 在本練習中，我們將使用這些請求。

![區段](./images/pmdtl.png)

我們接下來要做的就是依照所有必要步驟，透過API建立區段。 我們將建置簡單的區段： &quot;**ldap** — 所有女性客戶&quot;。

### 步驟1 — 建立區段定義

按一下名為&#x200B;**步驟1 — 設定檔：建立區段定義**。

![區段](./images/s1_call.png)

移至此請求的&#x200B;**內文**&#x200B;區段。

![區段](./images/s1_body.png)

在此請求的&#x200B;**內文**&#x200B;中，您會看到下列內容：

![區段](./images/s1_bodydtl.png)

用於此要求的語言稱為Profile Query Language或&#x200B;**PQL**。

您可以在[這裡](https://experienceleague.adobe.com/docs/experience-platform/segmentation/pql/overview.html?lang=en)找到更多有關PQL的資訊和檔案。


注意：請更新下列要求中的變數&#x200B;**名稱**，將&#x200B;**ldap**&#x200B;取代為您的特定&#x200B;**ldap**。

```json
{
    "name" : "ldap - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "ldap",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

新增您的特定&#x200B;**ldap**&#x200B;之後，Body應該看起來類似這樣：

```json
{
    "name" : "vangeluw - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "vangeluw",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

您也應該驗證請求的&#x200B;**標頭** — 欄位。 移至&#x200B;**標頭**。 然後您會看到以下內容：

![Postman](./images/s1_h.png)

| 索引鍵 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>您必須指定正在使用的Adobe Experience Platform沙箱名稱。 您的x-sandbox-name應為`--aepSandboxId--`。

現在，按一下藍色的&#x200B;**傳送**&#x200B;按鈕以建立區段並檢視其結果。

![區段](./images/s1_bodydtl_results.png)

完成此步驟後，您可以在Platform UI中檢視區段定義。 若要檢查此專案，請登入Adobe Experience Platform並移至&#x200B;**區段**。

![區段](./images/s1_segmentdef.png)

### 步驟2 — 建立區段POST工作

在上一個練習中，您已建立&#x200B;_串流_&#x200B;區段。 串流區段會持續即時評估資格。 您正在這裡建立&#x200B;_批次_&#x200B;區段。 批次區段可讓您預覽該區段在資格方面的外觀，但&#x200B;_並不表示該區段實際已執行_。 目前，_沒有任何人符合此區段_&#x200B;的資格。 為了讓人員符合資格，批次區段必須執行，這正是我們在這裡要做的事。

現在來POST區段工作。

前往Postman。

![區段](./images/pmdtl.png)

在Postman集合中，按一下名為&#x200B;**步驟2 -POST區段工作**&#x200B;的要求以開啟。

![區段](./images/s2_call.png)

您也應該驗證請求的&#x200B;**標頭** — 欄位。 移至&#x200B;**標頭**。 然後您會看到以下內容：

![Postman](./images/s2headers.png)

| 索引鍵 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>您必須指定正在使用的Adobe Experience Platform沙箱名稱。 您的x-sandbox-name應為`--aepSandboxId--`。

按一下藍色的&#x200B;**傳送**&#x200B;按鈕。

您應該會看到類似的結果：

![區段](./images/s2_call_response.png)

此區段工作目前正在執行中，這可能需要一些時間。 在步驟3中，您可以檢查此工作的狀態。


### 步驟3 -GET區段作業狀態

前往Postman。

![區段](./images/pmdtl.png)

在您的Postman集合中，按一下名為&#x200B;**步驟3 -GET區段作業狀態**&#x200B;的請求。

![區段](./images/s3_call.png)

您也應該驗證請求的&#x200B;**標頭** — 欄位。 移至&#x200B;**標頭**。 然後您會看到以下內容：

![Postman](./images/s3headers.png)

| 索引鍵 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>您必須指定正在使用的Adobe Experience Platform沙箱名稱。 您的x-sandbox-name應為`--aepSandboxId--`。

按一下藍色的&#x200B;**傳送**&#x200B;按鈕。

您應該會看到類似的結果：

![區段](./images/s3_status.png)

在此範例中，工作的&#x200B;**狀態**&#x200B;設定為&#x200B;**已排入佇列**。

每隔幾分鐘按一下藍色的&#x200B;**傳送**&#x200B;按鈕來重複此要求，直到&#x200B;**狀態**&#x200B;設定為&#x200B;**成功**。

![區段](./images/s3_status_succeeded.png)

一旦狀態為&#x200B;**SUCCEEDED**，表示您的區段工作已執行，客戶現在符合該區段的資格。

恭喜，您已成功完成分段作業。 現在來看看在整個企業內如何啟用即時客戶設定檔。

下一步： [2.1.6在客服中心檢視您使用中的即時客戶設定檔](./ex6.md)

[返回模組2.1](./real-time-customer-profile.md)

[返回所有模組](../../../overview.md)
