---
title: 建立方案
description: 建立方案
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 25d77367-046d-46bd-9640-60fbcea263da
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# 建立方案

如中所述 [建構您的資料](../structuring-your-data.md)，傳送至Adobe Experience Platform的資料必須採用XDM格式。 更具體地說，您的資料必須符合 _綱要_. 結構描述基本上是資料外觀的說明。 它說明欄位的名稱以及它們在資料中的位置。 它也說明每個欄位應具有的值型別（例如，布林值、長度為12個字元的字串、數字陣列）。

Adobe Experience Platform提供業界常見的一些現成建置區塊，稱為欄位群組。 例如，對於金融服務業，有餘額轉帳和貸款申請的欄位群組。 對於旅遊業和酒店業，有航班和住宿預訂的欄位群組。

建立結構描述時，建議您儘可能使用內建欄位群組。 我們也瞭解您可能需要貴公司專屬的欄位。 因此，您可以建立自己的自訂欄位群組，以便在您建立的結構描述中使用。

讓我們逐步建立典型電子商務網站的結構描述。

首先，導覽至 [!UICONTROL 結構描述] 在Adobe Experience Platform中檢視。

![結構描述檢視](../../../assets/implementation-strategy/schemas-view.png)

選取 [!UICONTROL 建立結構描述] 右上角。 隨即顯示功能表。 選取 [!UICONTROL XDM ExperienceEvent].

此時，應該會顯示一個對話方塊，詢問您要將哪些欄位群組新增到結構描述中。 您應選取的第一個欄位群組是名為的欄位群組 [!UICONTROL AEP Web SDK ExperienceEvent]. 此欄位群組新增一組欄位，可容納由Adobe Experience Platform Web SDK自動收集的資料。

![AEP Web SDK mixin](../../../assets/implementation-strategy/aep-web-sdk-mixin.png)

由於本教學課程的網站是電子商務網站，因此您也應選取 [!UICONTROL 商務詳細資料] 欄位群組。 此群組可讓您傳送一般商業資料，例如正在檢視、新增至購物車及購買哪些產品。

![商務詳細資料mixin](../../../assets/implementation-strategy/commerce-details-mixin.png)

按一下 [!UICONTROL 新增欄位群組] 按鈕。 此時，您應該會看到結構描述的結構。

![具有Mixin的結構描述](../../../assets/implementation-strategy/schema-with-mixins.png)

左側會列出您新增的欄位群組。 選取欄位群組會醒目顯示右側由該欄位群組提供的欄位。 請花點時間探索可用的欄位。

最後，選取 [!UICONTROL 未命名的結構描述] 在熒幕左側，在熒幕右側提供名稱和說明，然後按一下 [!UICONTROL 儲存].

![具有名稱和說明的結構描述](../../../assets/implementation-strategy/schema-name-description.png)

已建立您的結構描述。 接下來，讓我們瞭解如何建立資料集來儲存您的資料。

如需建立結構描述的詳細資訊，請參閱 [建立結構描述(UI)](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=zh-Hant).
