---
title: 設定資料流
description: 瞭解如何在Experience Platform中建立資料串流。
feature: Mobile SDK,Datastreams
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 5%

---

# 建立資料串流

瞭解如何在Experience Platform中建立資料串流。

資料串流是Platform Edge Network上的伺服器端設定。  資料流可確保將傳入Platform Edge Network的資料正確路由至Adobe Experience Cloud應用程式和服務。 如需詳細資訊，請參閱 [檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html) 或這個 [視訊](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html).

## 先決條件

若要建立資料串流，您的組織必須在資料收集介面(先前稱為 [!UICONTROL Launch])且您必須擁有下列專案的使用者許可權： [!UICONTROL Experience Platform] > [!UICONTROL 資料彙集] > **[!UICONTROL 管理資料串流]** 和 **[!UICONTROL 檢視資料串流]**.

## 學習目標

在本課程中，您將會：

* 知道何時使用資料串流。
* 建立資料串流。
* 設定資料流.

## 建立資料串流

資料串流可建立於 [!UICONTROL 資料彙集] 介面使用 [!UICONTROL 資料流] 設定工具。 若要建立資料串流：

1. 確定您處於正確的Platform沙箱中。
1. 選取「**[!UICONTROL 新資料流]**」。

   ![資料串流首頁](assets/mobile-datastream-new.png)

1. 提供名稱，例如 `Luma App`.
1. 選取您在上一堂課中建立的結構描述。
1. 選取「**[!UICONTROL 儲存]**」。

   ![新資料串流](assets/mobile-datastream-name.png)


## 新增服務

接下來，您可以將Experience Cloud服務連線至資料流。 當Platform Mobile SDK傳送資料至Edge Network時，資料流會將資料傳送至下列服務：

1. 新增 **[!UICONTROL Adobe Analytics]** 並提供報表套裝。

1. 啟用 **[!UICONTROL Adobe Audience Manager]** （選擇性）。

1. 啟用 **[!UICONTROL Adobe Experience Platform]** 並提供 **[!UICONTROL 資料集]** （選擇性）。
   * 如果您尚未建立資料集，請依照指示操作 [此處](platform.md).

1. 最終設定看起來應該像這樣。
   ![資料流設定](assets/mobile-datastream-settings.png)


>[!NOTE]
>
>啟用貴組織使用的每項服務，可確保行動應用程式中收集的資料能夠用於任何地方。 如需資料流設定的詳細資訊，請檢閱此檔案 [此處](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

在您自己的網站上實作Platform Mobile SDK時，您應建立三個資料串流以對應至您的三個標籤環境（開發、測試和生產）。 如果您使用Platform Mobile SDK搭配Adobe Real-time Customer Data Platform或Adobe Journey Optimizer等平台式應用程式，請務必在適當的Platform沙箱中建立這些資料串流。

下一步： **[設定標籤](configure-tags.md)**

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Mobile SDK。 若您有任何疑問、想分享一般意見或對未來內容有任何建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
