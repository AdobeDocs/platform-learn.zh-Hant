---
title: 設定Platform Web SDK的資料流
description: 瞭解如何啟用資料串流及設定Experience Cloud解決方案。 本課程是「使用 Web SDK 實施 Adob​​e Experience Cloud」教學課程的一部分。
feature: Web SDK,Datastreams
jira: KT-15399
exl-id: 20f770d1-eb0f-41a9-b451-4069a0a91fc4
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 7%

---

# 設定資料流

了解如何在 Adobe Experience Platform Web SDK 中設定資料流。

[資料串流](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/datastreams/overview)會告訴Adobe Experience Platform Edge Network要將由Platform Web SDK收集的資料傳送至何處。 在資料串流設定中，您可以啟用Experience Cloud應用程式、Experience Platform帳戶和事件轉送。

![網頁SDK、資料串流和Edge Network圖表](assets/dc-websdk-datastreams.png)

## 學習目標

在本課程結束時，您將能夠：

* 建立資料串流
* 開始使用資料流覆寫

## 先決條件

在設定資料流之前，您必須先完成下列課程：

* [設定結構描述](configure-schemas.md)
* [設定身分名稱空間](configure-identities.md)

## 建立資料串流

現在，您可以建立資料串流，告訴Platform Edge Network要將網頁SDK收集的資料傳送至何處。

**若要建立資料流：**

1. 開啟[資料收集介面](https://experience.adobe.com/data-collection/){target="_blank"}
1. 確定您位於正確的沙箱

   >[!NOTE]
   >
   >如果您是Real-Time CDP或Journey Optimizer等平台型應用程式的客戶，我們建議您在本教學課程中使用開發沙箱。 如果沒有，請使用&#x200B;**[!UICONTROL Prod]**&#x200B;沙箱。

1. 前往左側導覽中的&#x200B;**[!UICONTROL 資料串流]**
1. 選取&#x200B;**[!UICONTROL 新資料流]**
1. 輸入`Luma Web SDK: Development Environment`作為&#x200B;**[!UICONTROL 名稱]**。 稍後當您在標籤屬性中設定Web SDK擴充功能時，會參考此名稱。
1. 選取&#x200B;**[!UICONTROL 儲存]**

   ![建立資料流](assets/datastream-create-new-datastream.png)

   >[!NOTE]
   >
   >您不需要選取結構描述。 只有在您使用資料收集的[資料準備](/help/data-collection/edge/data-prep.md)功能時，才需要結構描述選取。

在下一個畫面中，您可以將Adobe應用程式等服務新增至資料流，但此時您不會新增任何服務。 您稍後將會在[設定Experience Platform](setup-experience-platform.md)、[設定Analytics](setup-analytics.md)、[設定Audience Manager](setup-audience-manager.md)、[設定Target](setup-target.md)或[事件轉送](setup-event-forwarding.md)課程中執行此作業。

>[!NOTE]
>
>在您自己的網站上實作Platform Web SDK時，您應該建立三個資料串流來對應至您的三個標籤環境（開發、測試和生產）。 如果您使用Platform Web SDK搭配Adobe Real-Time Customer Data Platform或Adobe Journey Optimizer等平台式應用程式，請務必在適當的Platform沙箱中建立這些資料串流。

## 覆寫資料流

[資料流覆寫](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/datastreams/overrides)可讓您為資料流定義其他設定，然後在特定條件下覆寫您的預設設定。

資料流設定覆寫分為兩個步驟：

1. 首先，您可以在資料流服務設定中定義資料流覆寫。 例如，您可以定義替代的Analytics報表套裝、Target工作區或Platform資料集以用作覆寫。
1. 然後，您會使用Web SDK傳送事件動作，或透過Web SDK標籤擴充功能中的設定，將覆寫傳送至Edge Network。

在[設定Adobe Analytics](setup-analytics.md)課程中，您使用Platform Web SDK傳送事件動作覆寫頁面的報表套裝。

您現在已準備好在標籤屬性中安裝Platform Web SDK擴充功能！

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)上分享
