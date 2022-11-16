---
title: 建立資料集
description: 建立資料集
exl-id: 19a60087-2f78-4510-b127-b1007a6b7a56
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 建立資料集

除了說明您傳送至Adobe Experience Platform的資料外，您還需要有存放處來保存資料。 在Adobe Experience Platform中，您可以放置資料的貯體稱為資料集。

>[!NOTE]
>
>如果您只使用Platform Web SDK將資料傳送至Adobe Analytics、Adobe Target和Adobe Audience Manager，或使用事件轉送，則不需要資料集。 如果您只將Web SDK用於這些用途，可略過本教學課程的頁面。

1. 選擇 **[!UICONTROL 資料集]** 在 [!UICONTROL 資料管理] 從Adobe Experience Platform的左側功能表。
1. 下一步，選取 **[!UICONTROL 建立資料集]** 命令。
   ![資料集檢視](../assets/datasets-view.png)

## 從結構建立資料集

1. 從 [!UICONTROL 工作流程] 介面，選擇第一個表徵圖， **[!UICONTROL 從結構建立資料集]**.
1. 搜尋 [您先前建立的架構](create-a-schema.md) 並加以選取。
   ![方案選擇](../assets/schema-selection.png)
1. 選擇 **[!UICONTROL 下一個]** 並提供名稱和說明。
   ![資料集名稱和說明](../assets/dataset-name-description.png)
1. 選擇 **[!UICONTROL 完成]**. 您的資料集已建立，且已準備好接收資料。

開始將資料傳入資料集時，Adobe Experience Platform會驗證您嘗試放入資料集的資料是否符合套用的結構。 如果資料不符合結構，資料會遭拒，且不會放入資料集。 經過此驗證步驟後，資料集(Adobe產品、第三方或您自己的公司)的消費者對於資料集資料的結構和潔淨度可以有一定程度的把握。

如需建立資料集的詳細資訊，請參閱 [建立資料集並內嵌資料](/help/platform/data-ingestion/create-datasets-and-ingest-data.md).

[下一個： ](create-a-datastream.md)

>[!NOTE]
>
>感謝您花時間學習資料收集。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)

