---
title: 設定資料流
description: 了解如何啟用資料流和設定Experience Cloud解決方案。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
feature: Datastreams
exl-id: ca28374a-9fe0-44de-a7ac-0aa046712515
source-git-commit: 762195148f7594e30b361546941dfcd8076ab7b1
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 3%

---

# 設定資料流

了解如何啟用資料流和設定Experience Cloud解決方案。

資料流會告訴Adobe Experience Platform Edge Network，要將Platform Web SDK收集的資料傳送至何處。 在資料流設定中，您可以啟用Experience Cloud應用程式、Experience Platform帳戶及事件轉送。 請參閱 [設定資料流的基本知識](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en) 以取得詳細資訊。

## 學習目標

在本課程結束時，您將能夠：

* 建立資料流
* 啟用您的Experience Cloud應用程式
* 啟用Experience Platform

## 先決條件

設定資料流之前，您必須已完成下列課程：

* [設定權限](configure-permissions.md)
* [設定結構](configure-schemas.md)
* [設定身分命名空間](configure-identities.md)

## 建立資料流

現在您可以建立資料流，告知Platform Edge Network要將Web SDK收集的資料傳送至何處。

**若要建立資料流：**

1. 開啟 [資料收集介面](https://launch.adobe.com/tw/){target=&quot;_blank&quot;}
1. 請確定您位在正確的沙箱中

   >[!NOTE]
   >
   >如果您是Platform型應用程式（例如即時CDP）的客戶，建議您在本教學課程中使用開發沙箱。 若非如此，請使用 **[!UICONTROL 生產]** 沙箱。

1. 前往 **[!UICONTROL 資料流]** 在左側導覽列中
1. 選擇 **[!UICONTROL 新資料流]** 在螢幕的右側。
1. 輸入 `Luma Web SDK` 作為 **[!UICONTROL 名稱]**. 您稍後在標籤屬性中設定Web SDK擴充功能時，會參照此名稱。
1. 選取 `Luma Web Event Data` 作為 **[!UICONTROL 事件結構]**
1. 選擇 **[!UICONTROL 儲存]**

   ![建立資料流](assets/datastream-create-datastream.png)

   >[!AVAILABILITY]
   >
   >日後將將對應功能整合到本教學課程中。




在下一個畫面中，您可以將Adobe應用程式等服務新增至資料流，不過您目前不會在教學課程中新增任何服務。 您稍後將在課程中進行 [設定Experience Platform](setup-experience-platform.md), [設定Analytics](setup-analytics.md), [設定Audience Manager](setup-audience-manager.md), [設定目標](setup-target.md)，或 [事件轉送](setup-event-forwarding.md).

>[!NOTE]
>
>在您自己的網站上實作Platform Web SDK時，您應建立三個資料流，以對應至您的三個標籤環境（開發、預備和生產）。 如果您使用Platform Web SDK搭配Adobe Real-time Customer Data Platform或Adobe Journey Optimizer等以平台為基礎的應用程式，請務必在適當的Platform沙箱中建立這些資料流。

您現在已準備好在標籤屬性中安裝Platform Web SDK擴充功能！

[下一個： ](install-web-sdk.md)

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
