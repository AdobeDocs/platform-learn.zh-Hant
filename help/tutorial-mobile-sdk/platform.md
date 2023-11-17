---
title: 傳送資料至Adobe Experience Platform
description: 瞭解如何將資料傳送至Adobe Experience Platform。
solution: Data Collection,Experience Platform
feature: Mobile SDK,Data Ingestion
exl-id: fdd2c90e-8246-4d75-a6db-df3ef31946c4
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 8%

---

# 傳送資料至Adobe Experience Platform

瞭解如何將資料傳送至Adobe Experience Platform。

>[!INFO]
>
> 在2023年11月下旬，此教學課程將由使用新範例行動應用程式的新教學課程取代

此選擇性課程與Real-time Customer Data Platform (Real-Time CDP)、Journey Optimizer和Customer Journey Analytics的所有客戶有關。 Experience Platform是Experience Cloud產品的基礎，是開放系統，可將您的所有資料(Adobe和非Adobe)轉換為健全的客戶設定檔，即時更新，並使用AI驅動的深入分析，協助您跨每個管道提供正確的體驗。

此 [事件](events.md)， [生命週期](lifecycle-data.md)、和 [身分](identity.md) 您在先前的課程中收集並傳送至Platform Edge Network的資料，會轉送至您在資料流中設定的服務，包括Adobe Experience Platform。


## 先決條件

您的組織必須布建並授與Adobe Experience Platform的許可權。

如果您沒有存取權，可以 [略過本課程](install-sdks.md).

## 學習目標

在本課程中，您將會：

* 建立Experience Platform資料集。
* 驗證資料集中的資料。
* 為Real-time Customer Profile啟用您的結構描述和資料集。
* 驗證即時客戶個人檔案中的資料。
* 驗證身分圖表中的資料。


## 建立資料集

所有成功內嵌至Adobe Experience Platform的資料都會以資料集的形式保留在資料湖中。 資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。 請參閱 [檔案](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=zh-Hant) 以取得相關資訊。

1. 從右上方的3x3功能表選取Experience Platform介面，導覽至該介面。
   ![資料集功能表](assets/mobile-dataset-menu.png)

1. 選取 **[!UICONTROL 資料集]** 從左側導覽功能表。

1. **[!UICONTROL 建立資料集]**.
   ![資料集首頁](assets/mobile-dataset-home.png)

1. 選取&#x200B;**[!UICONTROL 「從結構建立資料集」]**。
   ![資料集首頁](assets/mobile-dataset-create.png)

1. 搜尋您的結構描述並選取。

1. 選取&#x200B;**[!UICONTROL 「下一步」]**。
   ![資料集設定](assets/mobile-dataset-configure.png)

1. 提供 **[!UICONTROL 名稱]**， **[!UICONTROL 說明]**，並選取 **[!UICONTROL 完成]**.
   ![資料集完成時間](assets/mobile-dataset-finish.png)

## 更新資料流

建立資料集後，請務必 [更新您的資料流](create-datastream.md) 以新增Adobe Experience Platform。 此更新可確保資料流入Platform。

## 驗證資料集中的資料

現在您已建立資料集並更新資料流以將資料傳送至Experience Platform，所有傳送至Platform Edge Network的XDM資料都會轉送至Platform並進入資料集。

開啟應用程式，並導覽至您正在追蹤事件的畫面。 您也可以觸發生命週期量度。

在Platform介面中開啟資料集。 您應該會看到資料批次到達資料集

![驗證資料登陸Platform資料集批次](assets/mobile-platform-dataset-batches.png)

您也應該能夠檢視範例記錄和使用 **[!UICONTROL 預覽資料集]** 功能：
![驗證傳送至Platform資料集的生命週期](assets/mobile-lifecycle-platform-dataset.png)

驗證資料更強大的工具是Platform [查詢服務](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=zh-Hant).

## 啟用即時客戶個人檔案

Experience Platform的即時客戶設定檔可讓您建立每個個別客戶的整體檢視，該檢視會結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 設定檔可讓您將不同的客戶資料整合為統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

### 啟用結構

1. 開啟您的結構描述
1. 啟用 **[!UICONTROL 個人資料]**
1. 選取 **[!UICONTROL 此結構描述的資料將在identityMap欄位中包含主要身分。]** 在強制回應視窗中
1. **[!UICONTROL 儲存]** 結構描述

   ![為設定檔啟用結構描述](assets/mobile-platform-profile-schema.png)

### 啟用資料集

1. 開啟您的資料集
1. 啟用 **[!UICONTROL 個人資料]**

   ![為設定檔啟用資料集](assets/mobile-platform-profile-dataset.png)

### 驗證設定檔中的資料

開啟應用程式，並導覽至您正在追蹤事件的畫面。 登入Luma應用程式並進行購買。

使用Assurance尋找在identityMap中傳遞的其中一個身分（電子郵件、lumaCrmId或ECID）：

>[!TIP]
>
>   的值 `lumaCrmId` 是 `112ca06ed53d3db37e4cea49cc45b71e`


![抓取身分值](assets/mobile-platform-identity.png)

在Platform介面中，瀏覽至 **[!UICONTROL 設定檔]** > **[!UICONTROL 瀏覽]**，查詢您剛才擷取的身分值，並開啟設定檔：

![查詢身分值](assets/mobile-platform-profile-lookup.png)

在 **[!UICONTROL 詳細資料]** 熒幕您可以看到有關使用者的基本資訊，包括 **[!UICONTROL **&#x200B;連結的身分&#x200B;**]**：
![設定檔詳細資料](assets/mobile-platform-profile-details.png)

在 **[!UICONTROL 活動]**，您可以檢視針對此使用者從行動應用程式實施收集的事件：

![設定檔事件](assets/mobile-platform-profile-events.png)


在設定檔詳細資訊畫面中，按一下連結以檢視身分圖表或導覽至 **[!UICONTROL 身分]** > **[!UICONTROL 身分圖表]** 和查詢身分值。 此視覺效果會顯示設定檔中連結在一起的所有身分及其來源。 以下是身分圖表範例，由完成此Mobile SDK教學課程（資料來源2）和 [Web SDK教學課程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hant) （資料來源1）：

![抓取身分值](assets/mobile-platform-profile-identitygraph.png)

行銷人員和Analytics處理在Experience Platform中擷取的資料的能力更強，包括在Customer Journey Analytics中分析資料以及在Real-time Customer Data Platform中建立區段。 您有一個良好的開端！

下一步： **[使用Journey Optimizer推送訊息](journey-optimizer-push.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
