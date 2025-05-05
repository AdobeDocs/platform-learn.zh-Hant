---
title: 建立資料集
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 建立資料集
description: 在本課程中，您將建立資料集以接收資料。
role: Data Architect, Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 6%

---

# 建立資料集

<!--15min-->

在本課程中，您將建立資料集以接收資料。 您一定會很高興知道這是本教學課程中最短的課程！

所有成功內嵌至Adobe Experience Platform的資料都會以資料集的形式保留在資料湖中。 資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。

**資料架構師**&#x200B;需要在本教學課程之外建立資料集。

在開始練習之前，請觀看此短片，以進一步瞭解資料集：
>[!VIDEO](https://video.tv.adobe.com/v/27269?learn=on&enablevpops)

## 需要的許可權

在[設定許可權](configure-permissions.md)課程中，您已設定完成本課程所需的所有存取控制。

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## 在UI中建立資料集

在本練習中，我們將在UI中建立資料集。 讓我們從忠誠度資料開始：

1. 移至Platform使用者介面左側導覽中的&#x200B;**[!UICONTROL 資料集]**
1. 選取&#x200B;**[!UICONTROL 建立資料集]**&#x200B;按鈕
   ![建立資料集](assets/datasets-createDataset.png)

1. 在下一個畫面中，選取&#x200B;**從結構描述建立資料集**
1. 在下一個畫面中，選取您的`Luma Loyalty Schema`，然後選取&#x200B;**[!UICONTROL 下一步]**&#x200B;按鈕
   ![選取資料集](assets/datasets-selectSchema.png)

1. 為資料集命名`Luma Loyalty Dataset`並選取&#x200B;**[!UICONTROL 完成]**&#x200B;按鈕
   ![命名資料集](assets/datasets-nameDataset.png)
1. 資料集儲存後，您將會看到類似以下的畫面：
   ![已建立資料集](assets/datasets-created.png)

完成了！我告訴過您這會很快完成。 使用相同的步驟建立以下其他資料集：

1. 您的`Luma Offline Purchase Events Schema`的`Luma Offline Purchase Events Dataset`
1. 您的`Luma Web Events Schema`的`Luma Web Events Dataset`
1. 您的`Luma Product Catalog Schema`的`Luma Product Catalog Dataset`


## 使用API建立資料集

現在使用API建立`Luma CRM Dataset`。

>[!NOTE]
>
>如果您要略過API練習，並在使用者介面中建立`Luma CRM Dataset`，則沒問題。 將其命名為`Luma CRM Dataset`並使用`Luma CRM Schema`。

### 取得要在資料集中使用的結構描述ID

首先，我們需要取得`Luma CRM Schema`的`$id`：

1. 開啟[!DNL Postman]
1. 如果您沒有存取權杖，請開啟要求&#x200B;**[!DNL OAuth: Request Access Token]**，然後選取&#x200B;**傳送**&#x200B;來要求新的存取權杖，就像您在[!DNL Postman]課程中所做的一樣。
1. 開啟請求&#x200B;**[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. 選取&#x200B;**傳送**&#x200B;按鈕
1. 您應該會收到200回應
1. 檢視`Luma CRM Schema`專案的回應並複製`$id`值
   ![複製$id](assets/dataset-crm-getSchemaId.png)

### 建立資料集

現在您可以建立資料集：

1. 將[目錄服務API.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json)下載至您的`Luma Tutorial Assets`資料夾。
1. 將集合匯入[!DNL Postman]
1. 選取要求&#x200B;**[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. 將下列內容貼上為請求的&#x200B;**內文**，***將ID值取代為您自己的***：

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

1. 選取&#x200B;**傳送**&#x200B;按鈕
1. 您應該會收到包含新資料集ID的「201已建立」回應！
   ![使用API建立的資料集，您的自訂$id用於內文中](assets/datasets-crm-created.png)

>[!TIP]
>
> 提出此請求的常見問題以及可能的修正：
>
> * `400: There was a problem retrieving xdm schema`。確定您已使用您自己的`Luma CRM Schema`識別碼取代上述範例中的識別碼
> * 無驗證權杖：執行&#x200B;**OAuth：要求存取權杖**&#x200B;要求以產生新權杖
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`：將&#x200B;**CONTAINER_ID**&#x200B;環境變數從`global`更新為`tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`：在Admin Console中驗證您的使用者許可權


您可以回到Platform使用者介面中的&#x200B;**[!UICONTROL 資料集]**&#x200B;畫面，您可以驗證所有五個資料集的建立是否成功！
![五個資料集完成](assets/datasets-allComplete.png)


## 其他資源

* [資料集檔案](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=zh-Hant)
* [資料集API （目錄服務的一部分）參考](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

現在我們所有的結構描述、身分和資料集都已準備就緒，我們可以[為即時客戶個人檔案啟用它們](enable-profiles.md)。
