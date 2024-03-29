---
title: 設定資料流
description: 瞭解如何啟用資料串流並設定Experience Cloud解決方案。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
feature: Web SDK,Datastreams
source-git-commit: ef3d374f800905c49cefba539c1ac16ee88c688b
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 3%

---

# 設定資料流

瞭解如何啟用資料串流及設定Experience Cloud應用程式。

資料串流會告訴Adobe Experience Platform Edge Network要將由Platform Web SDK收集的資料傳送至何處。 在資料串流設定中，您可以啟用Experience Cloud應用程式、Experience Platform帳戶和事件轉送。 請參閱 [設定資料串流的基礎知識](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=zh-Hant) 以取得更多詳細資訊。


![Web SDK、資料串流和Edge網路圖表](assets/dc-websdk-datastreams.png)

## 學習目標

在本課程結束時，您將能夠：

* 建立資料串流
* 開始使用資料流覆寫

## 先決條件

在設定資料流之前，您必須先完成下列課程：

* [設定結構描述](configure-schemas.md)
* [設定身分名稱空間](configure-identities.md)

## 建立資料串流

現在您可以建立資料串流，告訴Platform Edge Network要將Web SDK收集的資料傳送至何處。

**若要建立資料串流：**

1. 開啟 [資料收集介面](https://launch.adobe.com/tw/){target="_blank"}
1. 確定您在正確的沙箱中

   >[!NOTE]
   >
   >如果您是Real-Time CDP或Journey Optimizer等平台型應用程式的客戶，我們建議您在本教學課程中使用開發沙箱。 如果沒有，請使用 **[!UICONTROL Prod]** 沙箱。

1. 前往 **[!UICONTROL 資料串流]** 在左側導覽列中
1. 選取 **[!UICONTROL 新增資料串流]** 在熒幕的右側。
1. 輸入 `Luma Web SDK: Development Environment` 作為 **[!UICONTROL 名稱]**. 稍後當您在標籤屬性中設定Web SDK擴充功能時，會參考此名稱。
1. 選取您的 `Luma Web Event Data` 作為 **[!UICONTROL 事件結構描述]**
1. 選取 **[!UICONTROL 儲存]**

   ![建立資料串流](assets/datastream-create-new-datastream.png)

在下一個畫面中，您可以將Adobe應用程式等服務新增至資料流，但此時您無法在教學課程中新增任何服務。 您將在稍後的課程中執行此動作 [設定Experience Platform](setup-experience-platform.md)， [設定Analytics](setup-analytics.md)， [設定Audience Manager](setup-audience-manager.md)， [設定目標](setup-target.md)，或 [事件轉送](setup-event-forwarding.md).

>[!NOTE]
>
>在您自己的網站上實作Platform Web SDK時，您應該建立三個資料串流以對應至您的三個標籤環境（開發、預備和生產）。 如果您使用Platform Web SDK搭配Adobe Real-time Customer Data Platform或Adobe Journey Optimizer等平台式應用程式，請務必在適當的Platform沙箱中建立這些資料串流。

## 覆寫資料流

「資料流覆寫」可讓您為資料流定義其他設定，然後在實施的某些條件下覆寫預設設定。


資料流設定覆寫分為兩個步驟：

1. 首先，您需在資料流設定中定義資料流覆寫。 您必須針對要覆寫的Adobe應用程式執行此動作。
1. 接著，您會透過Web SDK傳送事件動作或Web SDK標籤擴充功能中的設定，將覆寫傳送至Edge Network。

在 [設定Adobe Analytics](setup-analytics.md) 課程會使用Platform Web SDK傳送事件動作覆寫頁面的報表套裝。

請參閱 [資料流設定會覆寫檔案](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overrides.html?lang=en) 以取得有關如何覆寫資料流設定的詳細說明。

您現在已準備好在標籤屬性中安裝Platform Web SDK擴充功能！

[下一步： ](install-web-sdk.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
