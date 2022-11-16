---
title: Foundation — 即時客戶設定檔 — 建立區段 — API
description: Foundation — 即時客戶設定檔 — 建立區段 — API
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 3f537efd-7281-4c0c-b809-97f266a2a337
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 3%

---

# 3.5建立區段 — API

在本練習中，您將使用Postman和Adobe I/O，透過Adobe Experience Platform的API來建立區段，並將該區段的結果儲存為資料集。

## Story

在「即時客戶設定檔」中，所有設定檔資料會與事件資料和現有區段成員資格一起顯示。 顯示的資料可以來自任何位置，從Adobe應用程式和外部解決方案。 這是Adobe Experience Platform最強大的觀點，這是有記錄的體驗系統。

## 練習3.5.1 — 透過Platform API建立區段

去Postman。

找出集合： **啟用Adobe Experience Platform(_A)**. 在此集合中，您會看到資料夾 **2. 區段**. 在本練習中，我們將使用這些請求。

![區段](./images/pmdtl.png)

接下來我們將依照所有必要步驟，透過API建立區段。 我們將建立一個簡單的區段：&quot;**ldap**  — 所有女性客戶」。

### 步驟1 — 建立區段定義

按一下名為的請求 **步驟1 — 設定檔：建立區段定義**.

![區段](./images/s1_call.png)

前往 **主體** 部分。

![區段](./images/s1_body.png)

在 **主體** 在此請求中，您會看到下列內容：

![區段](./images/s1_bodydtl.png)

用於此請求的語言稱為「設定檔查詢語言」，或 **PQL**.

您可以找到有關PQL的更多資訊和文檔 [此處](https://experienceleague.adobe.com/docs/experience-platform/segmentation/pql/overview.html?lang=en).


注意：請更新變數 **名稱** 取代 **ldap** 與 **ldap**.

```json
{
    "name" : "ldap - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "ldap",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

新增您的特定 **ldap**，內文看起來應類似以下：

```json
{
    "name" : "vangeluw - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "vangeluw",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

您也應驗證 **標題**  — 請求的欄位。 前往 **標題**. 然後您會看到：

![Postman](./images/s1_h.png)

| 代碼 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>您必須指定您所使用Adobe Experience Platform沙箱的名稱。 您的x-sandbox-name應為 `--aepSandboxId--`.

現在，按一下藍色 **傳送** 按鈕來建立區段並檢視其結果。

![區段](./images/s1_bodydtl_results.png)

在此步驟之後，您可以在Platform UI中檢視區段定義。 若要勾選此項目，請登入Adobe Experience Platform並前往 **區段**.

![區段](./images/s1_segmentdef.png)

### 步驟2 — 建立區段POST工作

在上一個練習中，您建立 _串流_ 區段。 串流區段持續即時評估資格。 你在這裡做的，是 _批次_ 區段。 批次區段可讓您預覽區段在資格方面看起來是什麼樣子，但 _不代表區段實際執行_. 目前， _沒有人符合此區段的資格_. 若要讓人員符合資格，批次區段必須執行，這正是我們將要執行的作業。

現在來POST區段工作。

去Postman。

![區段](./images/pmdtl.png)

在Postman集合中，按一下 **步驟2 -POST區段作業** 來開啟它。

![區段](./images/s2_call.png)

您也應驗證 **標題**  — 請求的欄位。 前往 **標題**. 然後您會看到：

![Postman](./images/s2headers.png)

| 代碼 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>您必須指定您所使用Adobe Experience Platform沙箱的名稱。 您的x-sandbox-name應為 `--aepSandboxId--`.

按一下藍色 **傳送** 按鈕。

您應該會看到類似的結果：

![區段](./images/s2_call_response.png)

此區段作業目前執行中，可能需要一些時間。 在步驟3中，您將能檢查此作業的狀態。


### 步驟3 -GET區段作業狀態

去Postman。

![區段](./images/pmdtl.png)

在Postman集合中，按一下 **步驟3 -GET區段作業狀態**.

![區段](./images/s3_call.png)

您也應驗證 **標題**  — 請求的欄位。 前往 **標題**. 然後您會看到：

![Postman](./images/s3headers.png)

| 代碼 | 值 |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>您必須指定您所使用Adobe Experience Platform沙箱的名稱。 您的x-sandbox-name應為 `--aepSandboxId--`.

按一下藍色 **傳送** 按鈕。

您應該會看到類似的結果：

![區段](./images/s3_status.png)

在此範例中， **狀態** 的 **已排隊**.

按一下藍色 **傳送** 按一下按鈕，直到 **狀態** 設為 **成功**.

![區段](./images/s3_status_succeeded.png)

狀態為 **成功**，您的區段工作即已執行，且客戶現在符合區段資格。

恭喜您，您已成功完成分段練習。 現在來看看如何在整個企業中啟用即時客戶設定檔。

下一步： [3.6請參閱客服中心的「即時客戶個人檔案」實作](./ex6.md)

[返回模組3](./real-time-customer-profile.md)

[返回所有模組](../../overview.md)
