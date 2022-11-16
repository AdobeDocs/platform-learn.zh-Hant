---
title: 建立方案
description: 建立方案
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 25d77367-046d-46bd-9640-60fbcea263da
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# 建立方案

如 [建立資料結構](../structuring-your-data.md)，傳送至Adobe Experience Platform的資料必須位於XDM中。 更具體來說，您的資料必須符合 _綱要_. 結構基本上是資料應呈現的說明。 它說明欄位的名稱，以及資料中應放置的位置。 它也說明每個欄位應具有的值類型（例如，布林值、長度為12個字元的字串、數字陣列）。

Adobe Experience Platform提供業界通用的一些現成可用的建置區塊，稱為欄位群組。 例如，對於金融服務業，有用於餘額轉移和貸款申請的外地組。 對於旅行和旅宿業，有外地團隊，負責航班和住宿預訂。

建議您在建立架構時盡可能使用內建欄位群組。 我們也了解您可能需要屬於您自己公司的欄位。 因此，您可以建立自己的自訂欄位群組，以在您建立的結構中使用。

讓我們逐步建立典型電子商務網站的結構描述。

首先，導覽至 [!UICONTROL 結構] 在Adobe Experience Platform內檢視。

![結構檢視](../../../assets/implementation-strategy/schemas-view.png)

選擇 [!UICONTROL 建立結構] 在右上角。 畫面隨即顯示。 選擇 [!UICONTROL XDM ExperienceEvent].

此時應會顯示對話方塊，詢問您要新增至架構的欄位群組。 您應選取的第一個欄位群組是名為 [!UICONTROL AEP Web SDK ExperienceEvent]. 此欄位群組會新增一組欄位，以因應Adobe Experience Platform Web SDK自動收集的資料。

![AEP Web SDK mixin](../../../assets/implementation-strategy/aep-web-sdk-mixin.png)

由於本教學課程的網站是電子商務網站，因此您也應選取 [!UICONTROL 商務詳細資訊] 欄位群組。 此群組可讓您傳送一般商務資料，例如正在檢視、新增至購物車和購買的產品。

![商務詳細資訊Mixin](../../../assets/implementation-strategy/commerce-details-mixin.png)

按一下 [!UICONTROL 新增欄位群組] 按鈕。 此時，您應該會看到架構的結構。

![具有混合的架構](../../../assets/implementation-strategy/schema-with-mixins.png)

您新增的欄位群組會列在左側。 選取欄位群組會醒目顯示該欄位群組提供之右側的欄位。 請花點時間探索可用欄位。

最後，選取 [!UICONTROL 無標題結構] 在畫面左側，提供畫面右側的名稱和說明，然後按一下 [!UICONTROL 儲存].

![具有名稱和說明的架構](../../../assets/implementation-strategy/schema-name-description.png)

您的架構已建立。 接下來，我們來了解如何建立資料集以存放資料。

如需建立結構的詳細資訊，請參閱 [建立結構(UI)](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=zh-Hant).
