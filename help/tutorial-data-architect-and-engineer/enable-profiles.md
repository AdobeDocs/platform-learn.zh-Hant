---
title: 啟用即時客戶個人檔案
seo-title: Enable Real-Time Customer Profiles | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 啟用即時客戶個人檔案
description: 在本課程中，您將為Real-time Customer Profile啟用結構描述和資料集。
role: Data Architect
feature: Profiles
jira: KT-4348
thumbnail: 4348-enable-profiles.jpg
exl-id: b05f1af1-a599-42f2-8546-77453a578b92
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 0%

---

# 啟用即時客戶個人檔案

<!-- 15min-->
在本課程中，您將為Real-time Customer Profile啟用結構描述和資料集。

好的，我說資料集課程是本教學課程中最短的一課時，我撒謊了 — 這個課程應該花更少的時間！ 實際上，您所要做的就是進行一些切換。 但是，當您翻轉這些開關時，會發生什麼事情&#x200B;_真的_&#x200B;很重要，所以我想專注一整頁。

透過即時客戶個人檔案，您可以檢視結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。 設定檔可讓您將不同的客戶資料整合為統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

雖然聽起來很神奇，但您不需要為設定檔啟動&#x200B;*您的所有資料*。 實際上，您應該只啟用啟用啟用使用案例所需的資料。 啟用您想要用於行銷使用案例、客服中心整合等的資料，以便快速存取強大的客戶設定檔。 如果您上傳的資料僅供分析，則可能不應為設定檔啟用此功能。

對於即時客戶設定檔資料[&#128279;](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)有重要的護欄，在決定您自己的哪些資料應該啟用設定檔時，您應該檢閱這些護欄。

<!--is this accurate. Are there other considerations to point out? -->

**資料架構師**&#x200B;需要在本教學課程之外啟用即時客戶個人檔案。

在開始練習之前，請觀看此短片，以進一步瞭解即時客戶個人檔案：
>[!VIDEO](https://video.tv.adobe.com/v/27251?learn=on&enablevpops)

## 需要的許可權

在[設定許可權](configure-permissions.md)課程中，您已設定完成本課程所需的所有存取控制。


<!--* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## 使用Platform使用者介面啟用即時客戶個人檔案的結構描述

讓我們從啟用結構的簡單工作開始：

1. 在Platform使用者介面中，開啟&#x200B;**Luma忠誠度結構描述**
1. 在&#x200B;**[!UICONTROL 結構描述屬性]**&#x200B;中，切換&#x200B;**設定檔**&#x200B;引數
1. 在確認模式中，按下&#x200B;**[!UICONTROL 啟用]**&#x200B;按鈕以確認
1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;按鈕以儲存您的變更

   >[!IMPORTANT]
   >
   >為設定檔啟用結構描述後，就無法停用或刪除它。 此外，此時之後無法從結構描述中移除欄位。 當您在生產環境中使用自己的資料時，請務必牢記這些含意。 在本教學課程中，您應該使用開發沙箱，您可以隨時將其刪除。
   >
   >在本教學課程的受控環境中，您將會在擷取任何資料之前&#x200B;_啟用設定檔的結構描述和資料集_。 使用您自己的資料時，我們建議您依照下列順序操作：
   >
   > 1. 首先，將一些資料內嵌到資料集中。
   > 1. 解決資料擷取程式期間發生的任何問題（例如資料驗證或對應問題）。
   > 1. 為設定檔啟用資料集和結構描述
   > 1. 擷取資料


   ![設定檔切換](assets/profile-loyalty-enableSchema.png)

輕鬆嗎？ 針對這些其他結構描述重複上述步驟：

1. Luma產品目錄結構描述
1. Luma離線購買事件結構描述
1. Luma Web事件結構（在確認模式中，勾選「此結構的資料將在identityMap欄位中包含主要身分」方塊）

## 使用平台API啟用即時客戶個人檔案的結構描述

現在該使用API啟用`Luma CRM Schema`了。 如果您想略過此練習，並在使用者介面中將其啟用，請直接進行。

### 取得結構描述的meta：altId

首先取得`Luma CRM Schema`的`meta:altId`：

1. 開啟[!DNL Postman]
1. 如果您沒有存取權杖，請開啟要求&#x200B;**[!DNL OAuth: Request Access Token]**，然後選取&#x200B;**傳送**&#x200B;來要求新的存取權杖，就像您在[!DNL Postman]課程中所做的一樣。
1. 開啟請求&#x200B;**[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. 選取&#x200B;**傳送**&#x200B;按鈕
1. 您應該會收到200回應
1. 檢視`Luma CRM Schema`專案的回應並複製`meta:altId`值
   ![複製meta：altIid](assets/profile-crm-getMetaAltId.png)

### 啟用結構

現在我們有了結構描述的meta：altId，可以為設定檔啟用它：

1. 開啟請求&#x200B;**[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. 在&#x200B;**引數**&#x200B;中，將您的`meta:altId`值貼上為`SCHEMA_ID`引數值
1. 在&#x200B;**內文**&#x200B;索引標籤中，貼上下列程式碼

   ```json
   [{
       "op": "add",
       "path": "/meta:immutableTags",
       "value": ["union"]
   }]
   ```

1. 選取&#x200B;**傳送**&#x200B;按鈕
1. 您應該會收到200回應

   ![啟用設定檔的CRM結構描述，並將您的自訂meta：altIid用作SCHEMA_ID引數](assets/profile-crm-enableProfile.png)

您應該能夠在使用者介面中看到設定檔已啟用所有五個結構描述（您可能需要使用SHIFT-Reload才能看到`Luma CRM Schema`已啟用）：
![所有已啟用的結構描述](assets/profile-allSchemasEnabled.png)


## 使用Platform使用者介面啟用即時客戶個人檔案的資料集

也必須為設定檔啟用資料集，流程會更簡單：

1. 在平台使用者介面中，開啟`Luma Loyalty Dataset`
1. 切換&#x200B;**[!UICONTROL 設定檔]**&#x200B;引數
1. 在確認模式中，按下&#x200B;**[!UICONTROL 啟用]**&#x200B;按鈕以確認

   ![設定檔切換](assets/profile-loyalty-enableDataset.png)

對其他資料集重複上述步驟：

1. Luma產品目錄資料集
1. Luma離線購買事件資料集
1. Luma Web事件資料集

>[!NOTE]
>
>與結構描述不同，您可以從設定檔停用資料集，但所有先前擷取的資料將保留在設定檔中。

## 使用平台API啟用即時客戶個人檔案的資料集

現在您將使用API為設定檔啟用資料集。 同樣地，如果您想透過使用者介面使用上述方法將其啟用，這也沒問題。

### 取得資料集的id

首先，我們需要取得`Luma CRM Dataset`的`id`：

1. 開啟[!DNL Postman]
1. 如果您沒有存取權杖，請開啟要求&#x200B;**[!DNL OAuth: Request Access Token]**，然後選取&#x200B;**傳送**&#x200B;來要求新的存取權杖，就像您在[!DNL Postman]課程中所做的一樣。
1. 開啟請求&#x200B;**[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]**
1. 選取&#x200B;**傳送**&#x200B;按鈕
1. 您應該會收到200回應
1. 檢視`Luma CRM Dataset`專案的回應並複製ID：
   ![複製ID](assets/profile-crm-copyDatasetId.png)

### 啟用資料集

現在我們有資料集的ID了，可以為設定檔啟用它：

1. 開啟請求&#x200B;**[!DNL Catalog Service API > Datasets > Update one or more attributes of a dataset specified by ID.]**
1. 在&#x200B;**引數**&#x200B;中，將`DATASET_ID`值更新為您自己的值
1. 在&#x200B;**內文**&#x200B;索引標籤中，貼上下列程式碼。 請注意，前兩個值是先前回應中顯示的現有標籤。 除了要新增的兩個新標籤之外，這些標籤也需要納入內文中：

   ```json
   {
       "tags":{
           "adobe/pqs/table":["luma_crm_dataset"],
           "adobe/siphon/table/format":["parquet"],
           "unifiedProfile":["enabled:true"],
           "unifiedIdentity":["enabled:true"]
           }
   }
   ```

1. 選取&#x200B;**傳送**&#x200B;按鈕
1. 您應該會收到200回應

   ![為設定檔啟用CRM資料集，確定使用您的自訂資料集ID做為DATASET_ID引數](assets/profile-crm-enableDataset.png)

您也可以確認使用者介面會顯示資料集已啟用：
![確認](assets/profile-crm-confirmEnabled.png)

>[!IMPORTANT]
>
> 如果您在啟用設定檔的結構描述和資料集之前擷取資料，則後續需要重新擷取該資料。

## 其他資源

* [即時客戶個人檔案檔案](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=zh-Hant)
* [即時客戶設定檔API參考](https://www.adobe.io/experience-platform-apis/references/profile/)


**資料工程師**&#x200B;應該繼續進行[訂閱資料擷取事件](subscribe-to-data-ingestion-events.md)課程。
**資料架構師** _可以略過前面_，並前往[批次擷取課程](ingest-batch-data.md)。
