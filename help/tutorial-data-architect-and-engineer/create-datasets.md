---
title: 建立資料集
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 建立資料集
description: 在本課程中，您將建立資料集以接收資料。
role: Data Architect, Data Engineer
feature: Data Management
kt: 4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 8%

---

# 建立資料集

<!--15min-->

在本課程中，您將建立資料集以接收資料。 您會很高興知道，這是本教學課程中最短的課程！

成功擷取至Adobe Experience Platform的所有資料都會以資料集形式保存在資料湖中。 資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。 

**資料架構師** 需要在本教學課程之外建立資料集。

開始練習之前，請觀看此短片，以深入了解資料集：
>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)

## 需要權限

在 [設定權限](configure-permissions.md) 課程中，您設定了完成本課程所需的所有訪問控制。

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## 在UI中建立資料集

在本練習中，我們將在UI中建立資料集。 讓我們從忠誠度資料開始：

1. 前往 **[!UICONTROL 資料集]** 在Platform使用者介面的左側導覽中
1. 選取 **[!UICONTROL 建立資料集]** 按鈕
   ![建立資料集](assets/datasets-createDataset.png)

1. 在下一個畫面中，選取 **從結構建立資料集**
1. 在下一個畫面中，選取您的 `Luma Loyalty Schema` ，然後選取 **[!UICONTROL 下一個]** 按鈕
   ![選取資料集](assets/datasets-selectSchema.png)

1. 為資料集命名 `Luma Loyalty Dataset` ，然後選取 **[!UICONTROL 完成]** 按鈕
   ![為資料集命名](assets/datasets-nameDataset.png)
1. 資料集儲存後，畫面會顯示如下：
   ![已建立資料集](assets/datasets-created.png)

完成了！我告訴過你這會很快的。 使用相同步驟建立下列其他資料集：

1. `Luma Offline Purchase Events Dataset` 為 `Luma Offline Purchase Events Schema`
1. `Luma Web Events Dataset` 為 `Luma Web Events Schema`
1. `Luma Product Catalog Dataset` 為 `Luma Product Catalog Schema`


## 使用API建立資料集

現在，請建立 `Luma CRM Dataset` 使用API。

>[!NOTE]
>
>如果您想略過API練習並建立 `Luma CRM Dataset` 在使用者介面中，沒問題。 為其命名 `Luma CRM Dataset` 並使用 `Luma CRM Schema`.

### 取得要在資料集中使用的結構ID

首先，我們要 `$id` 的 `Luma CRM Schema`:

1. 開啟 [!DNL Postman]
1. 如果您在過去24小時內未提出請求，則您的授權Token可能已過期。 開啟請求 **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** 選取 **傳送** 請求新的JWT和存取權杖，就像您在 [!DNL Postman] 教訓。
1. 開啟請求 **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. 選取 **傳送** 按鈕
1. 您應會收到200個回應
1. 查看 `Luma CRM Schema` 項目並複製 `$id` value
   ![複製$id](assets/dataset-crm-getSchemaId.png)

### 建立資料集

現在您可以建立資料集：

1. 下載 [目錄服務API.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json) 至 `Luma Tutorial Assets` 檔案夾。
1. 將集合匯入 [!DNL Postman]
1. 選擇請求 **[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. 將下列項目貼上為 **主體** 請求， ***將id值取代為您自己的***:

   ```json
   {
       "name": "Luma CRM Dataset",
   
       "schemaRef": {
           "id": "REPLACE_WITH_YOUR_OWN_ID",
           "contentType": "application/vnd.adobe.xed-full+json;version=1"
       },
       "fileDescription": {
           "persisted": true,
           "containerFormat": "parquet",
           "format": "parquet"
       }
   }
   ```

1. 選取 **傳送** 按鈕
1. 您應該會收到包含新資料集ID的「201已建立」回應！
   ![使用API建立的資料集，內文中使用的自訂$id](assets/datasets-crm-created.png)

>[!TIP]
>
> 提出此要求的常見問題和可能的修正：
>
> * `400: There was a problem retrieving xdm schema`。請確定您已將上述範例中的id取代為您自己的id `Luma CRM Schema`
> * 無驗證令牌：執行 **IMS:JWT透過使用者代號產生+驗證** 產生新代號的呼叫
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`:更新 **CONTAINER_ID** 環境變數來源 `global` to `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`:驗證Admin Console中的使用者權限



您可以返回 **[!UICONTROL 資料集]** 螢幕上顯示的所有資料集，您可以確認是否已成功建立所有五個資料集！
![完成五個資料集](assets/datasets-allComplete.png)


## 其他資源

* [資料集檔案](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=zh-Hant)
* [資料集API（屬於目錄服務一部分）參考](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

現在，我們的所有結構、身分和資料集都已就緒，我們可以 [啟用即時客戶個人檔案](enable-profiles.md).
