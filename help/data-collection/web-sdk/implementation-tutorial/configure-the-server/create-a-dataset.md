---
title: 建立資料集
description: 建立資料集
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 7705d292-a29c-4977-bcc6-f088a51713ea
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 4%

---

# 建立資料集

除了說明您將傳送至Adobe Experience Platform的資料外，您還需要有存放處以保存資料。 在Adobe Experience Platform中，您可以放置資料的貯體稱為資料集。

若要建立資料集，請導覽至 [!UICONTROL 資料集] 在Adobe Experience Platform內檢視。

![資料集檢視](../../../assets/implementation-strategy/datasets-view.png)

按一下 [!UICONTROL 建立資料集] 在右上角。

在資料集建立程式期間，選取 [!UICONTROL 從結構建立資料集] 選取 [您先前建立的架構](create-a-schema.md).

![方案選擇](../../../assets/implementation-strategy/schema-selection.png)

按一下 [!UICONTROL 下一個] 並提供名稱和說明。

![資料集名稱和說明](../../../assets/implementation-strategy/dataset-name-description.png)

按一下[!UICONTROL 完成]。您的資料集已建立，且已準備好接收資料。

開始將資料傳入資料集時，Adobe Experience Platform會驗證您嘗試放入資料集的資料是否符合套用的結構。 如果資料不符合結構，資料會遭拒，且不會放入資料集。 經過此驗證步驟後，資料集(Adobe產品、第三方或您自己的公司)的消費者對於資料集資料的結構和潔淨度可以有一定程度的把握。

如需建立資料集的詳細資訊，請參閱 [資料集UI指南](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=zh-Hant).
