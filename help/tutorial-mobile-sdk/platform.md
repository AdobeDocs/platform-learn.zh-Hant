---
title: 透過Platform Mobile SDK傳送資料至Experience Platform
description: 瞭解如何將資料傳送至Experience Platform。
solution: Data Collection,Experience Platform
feature: Mobile SDK,Data Ingestion
jira: KT-14637
exl-id: fdd2c90e-8246-4d75-a6db-df3ef31946c4
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 3%

---

# 傳送資料至Experience Platform

瞭解如何將行動應用程式資料傳送至Adobe Experience Platform。

本選擇性課程與Real-Time Customer Data Platform (Real-Time CDP)、Journey Optimizer和Customer Journey Analytics的所有客戶有關。 Experience Platform是Experience Cloud產品的基礎，是開放系統，可將您的所有資料(Adobe和非Adobe)轉換為強大的客戶設定檔。 這些客戶設定檔會即時更新，並使用AI導向的深入分析來協助您跨每個管道提供適當的體驗。

您收集並在先前課程中傳送至Platform Edge Network的[事件](events.md)、[生命週期](lifecycle-data.md)和[身分](identity.md)資料會轉送至您在資料流中設定的服務，包括Adobe Experience Platform。

![架構](assets/architecture-aep.png){zoomable="yes"}


## 先決條件

您的組織必須布建並授與Adobe Experience Platform的許可權。

如果您沒有存取權，可以[略過本課程](install-sdks.md)。

## 學習目標

在本課程中，您將會：

* 建立Experience Platform資料集。
* 設定您的資料串流以將資料轉送至Experience Platform。
* 驗證資料集中的資料。
* 為Real-time Customer Profile啟用您的結構描述和資料集。
* 驗證即時客戶個人檔案中的資料。
* 驗證身分圖表中的資料。


## 建立資料集

所有成功內嵌至Adobe Experience Platform的資料都會以資料集的形式保留在資料湖中。 資料集是資料集合（通常是表格）的儲存和管理結構，其中包含結構（欄）和欄位（列）。 資料集也包含中繼資料，可說明其儲存資料的各個層面。 如需詳細資訊，請參閱[文件](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/catalog/datasets/overview)。

1. 導覽至Experience Platform UI。 從右上角的「應用程式&#x200B;**[!UICONTROL 應用程式]**」功能表中選取![Experience Platform](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg)。


1. 從左側導覽功能表中選取&#x200B;**[!UICONTROL 資料集]**。

1. 選取![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 建立資料集]**。

1. 選取&#x200B;**[!UICONTROL 從結構描述]**&#x200B;建立資料集。
   ![資料集首頁](assets/dataset-create.png){zoomable="yes"}

1. 搜尋您的結構描述。 例如在搜尋欄位中使用`Luma Mobile`。
1. 選取您的結構描述，例如&#x200B;**[!DNL Luma Mobile App Event Schema]**。

1. 選取&#x200B;**[!UICONTROL 下一步]**。
   ![資料集設定](assets/dataset-configure.png){zoomable="yes"}

1. 提供&#x200B;**[!UICONTROL 名稱]**，例如`Luma Mobile App Events Dataset`和&#x200B;**[!UICONTROL 描述]**。

1. 選取「**[!UICONTROL 完成]**」。
   ![資料集完成時間](assets/dataset-finish.png){zoomable="yes"}


## 新增Adobe Experience Platform資料流服務

若要將您的XDM資料從Edge Network傳送到Adobe Experience Platform，請將Adobe Experience Platform服務新增到您設定的資料流，作為[建立資料流](create-datastream.md)的一部分。

>[!IMPORTANT]
>
>您只能在建立事件資料集後啟用Adobe Experience Platform服務。

1. 在資料收集UI中，選取&#x200B;**[!UICONTROL 資料串流]**&#x200B;和您的資料串流。

1. 然後選取![新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL 新增服務]**。

1. 從&#x200B;**[!UICONTROL 服務]**&#x200B;清單中選取[!UICONTROL Adobe Experience Platform]。

1. 透過將&#x200B;**[!UICONTROL 已啟用]**&#x200B;切換為開啟來啟用服務。

1. 選取您先前建立的&#x200B;**[!UICONTROL 事件資料集]**，例如&#x200B;**[!DNL Luma Mobile App Event Dataset]**。

1. 選取「**[!UICONTROL 儲存]**」。

   ![將Adobe Experience Platform新增為資料流服務](assets/datastream-service-aep.png){zoomable="yes"}
1. 最終設定看起來應該像這樣。

   ![資料流設定](assets/datastream-settings.png){zoomable="yes"}


## 驗證資料集中的資料

現在您已建立資料集並更新資料流以將資料傳送至Experience Platform，所有傳送至Platform Edge Network的XDM資料都會轉送至Platform並進入資料集。

開啟應用程式，並導覽至您正在追蹤事件的畫面。 您也可以觸發生命週期量度。

在Platform介面中開啟資料集。 您應該會看到資料批次到達資料集。 資料通常每15分鐘會以微批次的形式送達，因此您可能無法立即看到資料。

![驗證資料登陸Platform資料集批次](assets/platform-dataset-batches.png){zoomable="yes"}

您也應該看到使用&#x200B;**[!UICONTROL 預覽資料集]**&#x200B;功能的範例記錄和欄位：
![驗證傳送至Platform資料集的生命週期](assets/lifecycle-platform-dataset.png){zoomable="yes"}

驗證資料的更強大工具是Platform的[查詢服務](https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/queries/explore-data)。

## 啟用即時客戶個人檔案

Experience Platform的即時客戶設定檔可讓您建立每個個別客戶的整體檢視，該檢視會結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 設定檔可讓您將不同的客戶資料整合為統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

### 啟用結構

1. 開啟您的結構描述，例如&#x200B;**[!DNL Luma Mobile App Event Schema]**。
1. 啟用&#x200B;**[!UICONTROL 設定檔]**。
1. 選取&#x200B;**[!UICONTROL 此結構描述的資料在identityMap欄位中包含主要身分。對話方塊中的]**。
1. **[!UICONTROL 儲存]**&#x200B;結構描述。

   ![啟用設定檔](assets/platform-profile-schema.png){zoomable="yes"}的結構描述

### 啟用資料集

1. 開啟您的資料集，例如&#x200B;**[!DNL Luma Mobile App Event Dataset]**。
1. 啟用&#x200B;**[!UICONTROL 設定檔]**。

   ![啟用設定檔](assets/platform-profile-dataset.png){zoomable="yes"}的資料集

### 驗證設定檔中的資料

開啟應用程式，並導覽至您正在追蹤事件的畫面，例如：登入Luma應用程式並進行購買。

使用Assurance尋找在identityMap中傳遞的其中一個身分（電子郵件、lumaCrmId或ECID），例如CRM ID。

![抓取識別值](assets/platform-identity.png){zoomable="yes"}

在平台介面中，

1. 導覽至&#x200B;**[!UICONTROL 設定檔]**，然後從頂端列選取&#x200B;**[!UICONTROL 瀏覽]**。
1. 指定您剛才擷取的身分詳細資料，例如`Luma CRM ID`身分名稱空間&#x200B;**[!UICONTROL 的]**&#x200B;以及您為&#x200B;**[!UICONTROL 身分值]**&#x200B;複製的值。 然後選取&#x200B;**[!UICONTROL 檢視]**。
1. 若要檢視詳細資訊，請選取設定檔。

![查詢身分值](assets/platform-profile-lookup.png){zoomable="yes"}

在&#x200B;**[!UICONTROL 詳細資料]**&#x200B;畫面上，您可以看到使用者的基本資訊，包括&#x200B;**[!UICONTROL **&#x200B;連結的身分&#x200B;**]**：
![設定檔詳細資料](assets/platform-profile-details.png){zoomable="yes"}

在&#x200B;**[!UICONTROL 事件]**&#x200B;上，您可以看到從您的行動應用程式實作為此使用者收集的事件：

![設定檔事件](assets/platform-profile-events.png){zoomable="yes"}


從設定檔詳細資訊畫面：

1. 若要檢視身分圖表，請按一下連結或導覽至&#x200B;**[!UICONTROL 身分圖表]**，然後從上方列選取&#x200B;**[!UICONTROL 身分圖表]**。
1. 若要查詢識別值，請指定`Luma CRM ID`做為&#x200B;**[!UICONTROL 識別名稱空間]**，並將複製的值做為&#x200B;**[!UICONTROL 識別值]**。 然後選取&#x200B;**[!UICONTROL 檢視]**。

   此視覺效果會顯示設定檔中連結在一起的身分及其來源。 以下是身分圖表範例，它是由完成此Mobile SDK教學課程(Data Source 2)和[Web SDK教學課程](https://experienceleague.adobe.com/zh-hant/docs/platform-learn/implement-web-sdk/overview) (Data Source 1)所收集的資料所建構：

   ![抓取識別值](assets/platform-profile-identitygraph.png){zoomable="yes"}


## 後續步驟

行銷人員和分析人員還可以處理Experience Platform中擷取的資料，包括在Customer Journey Analytics中分析資料以及在Real-Time Customer Data Platform中建立區段。 您有一個良好的開端！


>[!SUCCESS]
>
>您現在已設定應用程式，不僅將資料傳送至Edge Network，也傳送至Adobe Experience Platform。<br>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=zh-Hant)上分享。
>

下一步： **[建立並傳送推播通知](journey-optimizer-push.md)**
