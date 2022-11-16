---
title: 建立方案
description: 建立方案
exl-id: 0256b358-0c2c-4c59-ab23-5fe0d38880d6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# 建立方案

如 [建立資料結構](../structuring-your-data.md)，傳送至Adobe Experience Platform的資料必須位於XDM中。 更具體來說，您的資料必須符合 _綱要_. 結構基本上是資料應呈現的說明。 它說明欄位的名稱，以及資料中應放置的位置。 它也說明每個欄位應具有的值類型（例如，布林值、長度為12個字元的字串、數字陣列）。

Adobe Experience Platform提供業界通用的一些現成可用的建置區塊，稱為欄位群組。 例如，對於金融服務業，有用於餘額轉移和貸款申請的外地組。 對於旅行和旅宿業，有外地團隊，負責航班和住宿預訂。

建議您在建立架構時盡可能使用內建欄位群組。 我們也了解您可能需要屬於您自己公司的欄位。 因此，您可以建立自己的自訂欄位群組，以在您建立的結構中使用。

讓我們逐步建立典型電子商務網站的結構描述。

1. 選擇 **[!UICONTROL 結構]** 在 [!UICONTROL 資料管理] 從Adobe Experience Platform介面的左側功能表。
1. 選擇 **[!UICONTROL 建立結構]** 在右上角， **[!UICONTROL XDM ExperienceEvent]** 從下拉式功能表。

您現在位於結構產生器畫布上。
![結構檢視](../assets/schemas-view.png)

## 新增欄位群組

1. 在 **[!UICONTROL 欄位群組]** 區段 **[!UICONTROL 結構]** ，選擇 **[!UICONTROL +新增]** 連結。 此時會顯示一個強制回應，以選擇要新增至您結構的欄位群組。
1. 首先，選取名為的欄位群組 **[!UICONTROL AEP Web SDK ExperienceEvent]**. 此欄位群組會新增一組欄位，以因應Adobe Experience Platform Web SDK自動收集的資料。
   ![AEP Web SDK mixin](../assets/aep-web-sdk-mixin.png)
1. 接下來，由於本教學課程的網站是電子商務網站，請選取 **[!UICONTROL 商務詳細資訊]** 欄位群組。 此欄位群組可讓您傳送一般商務資料，例如正在檢視、新增至購物車和購買的產品。
1. 選取 **[!UICONTROL 新增欄位群組]** 按鈕。
   ![商務詳細資訊Mixin](../assets/commerce-details-mixin.png)
1. 此時，您應該會看到架構的結構。
   ![具有混合的架構](../assets/schema-with-mixins.png)

## 儲存結構

1. 最後，在螢幕右側提供名稱和說明，然後選取 **[!UICONTROL 儲存]**.
   ![具有名稱和說明的架構](../assets/schema-name-description.png)

您的架構已建立。 接下來，我們來了解如何建立資料集來儲存您的資料。

如需建立結構的詳細資訊，請參閱 [建立結構](/help/platform/schemas/create-schemas.md).

[下一個： ](create-a-dataset.md)

>[!NOTE]
>
>感謝您花時間學習資料收集。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
