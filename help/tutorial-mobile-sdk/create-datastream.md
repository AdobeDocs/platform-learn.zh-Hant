---
title: 設定Platform Mobile SDK實作的資料流
description: 了解如何在 Experience Platform 中建立資料流。
feature: Mobile SDK,Datastreams
jira: KT-14625
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 5%

---

# 建立資料串流

了解如何在 Experience Platform 中建立資料流。

資料串流是PlatformEdge Network上的伺服器端設定。 資料流可確保將傳入PlatformEdge Network的資料正確路由至Adobe Experience Cloud應用程式和服務。 如需詳細資訊，請參閱[檔案](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hant)或此[影片](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=zh-Hant)。

![架構](assets/architecture.png)

## 先決條件

若要建立資料串流，您的組織必須在資料收集介面（先前稱為[!UICONTROL Launch]）中布建此功能，而且您必須擁有使用者許可權管理及檢視資料串流。

## 學習目標

在本課程中，您將會：

* 瞭解何時使用資料流。
* 建立資料串流。
* 設定資料串流。

## 建立資料串流

可以使用[!UICONTROL 資料串流]組態工具，在[!UICONTROL 資料彙集]介面中建立資料串流。 若要建立資料串流：

1. 當資料串流定義在沙箱層級時，請確保您處於正確的Experience Platform沙箱中。
1. 在左側邊欄中選取&#x200B;**[!UICONTROL 資料串流]**。
1. 選取&#x200B;**[!UICONTROL 新資料流]**。

   ![資料串流首頁](assets/datastream-new.png)

1. 提供&#x200B;**[!UICONTROL 名稱]** （例如`Luma Mobile App`）和&#x200B;**[!UICONTROL 描述]** （例如`Datastream for Luma Mobile App`）。

   >[!NOTE]
   >
   >最終提醒：如果您正在閱讀本教學課程，但有一個沙箱容納多個人員，或者您使用共用帳戶，請考慮在命名慣例中附加或附加身分識別。 例如，使用`Luma Mobile App Event Dataset - Joe Smith`，而非`Luma Mobile App Event Dataset`。 另請參閱[總覽](overview.md)中的備註。

1. 從&#x200B;**事件結構描述**&#x200B;清單中選取您在上一堂課中建立的結構描述。
1. 選取「**[!UICONTROL 儲存]**」。

   ![新資料串流](assets/datastream-name.png)


## 新增服務

當您在本教學課程中完成（選擇性） [Analytics](analytics.md)和[Experience Platform](platform.md)課程時，您會將服務新增至資料流，以便將傳送至PlatformEdge Network的資料轉送至這些應用程式。

<!--

### Adobe Analytics

1. Select **[!UICONTROL Add Service]**.

1. Add **[!UICONTROL Adobe Analytics]** from the [!UICONTROL Service] list, 

1. Enter the name of the report site that you want to use in **[!UICONTROL Report Suite ID]**.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Analytics as datastream service](assets/datastream-service-aa.png)


### Adobe Experience Platform

You might also want to enable the Adobe Experience Platform service. 

>[!IMPORTANT]
>
>You can only enable the Adobe Experience Platform service when having created an event dataset. If you don't already have an event dataset created, follow the instructions [here](platform.md).

1. Click ![Add](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Add Service]** to add another service.

1. Select **[!UICONTROL Adobe Experience Platform]** from the [!UICONTROL Service] list.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select the **[!UICONTROL Event Dataset]** that you created as part of the [Create a dataset](platform.md#create-a-dataset) instructions, for example **Luma Mobile App Event Dataset**

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Experience Platform as a datastream service](assets/datastream-service-aep.png)
1. The final configuration should look something like this.
   
   ![datastream settings](assets/datastream-settings.png)

-->


>[!NOTE]
>
>啟用貴組織使用的每項服務，可確保行動應用程式中收集的資料能夠用於任何地方。 如需有關資料流設定的詳細資訊，請在[這裡](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hant)檢閱檔案。

在您自己的應用程式中實作Platform Mobile SDK時，您最終應建立三個資料串流以對應至您的三個標籤環境（開發、預備和生產）。 如果您使用Platform Mobile SDK搭配Adobe Real-time Customer Data Platform或Adobe Journey Optimizer等平台式應用程式，請務必在適當的沙箱中建立這些資料串流。

>[!SUCCESS]
>
>您現在有資料串流可用於教學課程的其餘部分。
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享

下一步： **[設定標籤屬性](configure-tags.md)**
