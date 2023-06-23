---
title: 建立資料集
description: 建立資料集
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 7705d292-a29c-4977-bcc6-f088a51713ea
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 4%

---

# 建立資料集

除了說明您會傳送至Adobe Experience Platform的資料外，您還需要一個位置來儲存資料。 在Adobe Experience Platform中，您可以放置資料的這些貯體稱為資料集。

若要建立資料集，請導覽至 [!UICONTROL 資料集] 在Adobe Experience Platform中檢視。

![資料集檢視](../../../assets/implementation-strategy/datasets-view.png)

按一下 [!UICONTROL 建立資料集] 右上角。

在資料集建立過程中，選取 [!UICONTROL 從結構描述建立資料集] 並選取 [您先前建立的結構描述](create-a-schema.md).

![結構描述選擇](../../../assets/implementation-strategy/schema-selection.png)

按一下 [!UICONTROL 下一個] 並提供名稱和說明。

![資料集名稱和說明](../../../assets/implementation-strategy/dataset-name-description.png)

按一下[!UICONTROL 完成]。您的資料集已建立，可以接收資料。

當您開始將資料傳送至資料集時，Adobe Experience Platform會驗證您嘗試放入資料集的資料是否符合套用的結構描述。 如果資料不符合結構描述，資料會遭到拒絕，且不會放入資料集中。 此驗證步驟的結果是，資料集的消費者(Adobe產品、第三方或您自己的公司)對於資料集資料的結構和潔淨度有一定的確定性。

如需建立資料集的詳細資訊，請參閱 [資料集UI指南](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=zh-Hant).
