---
title: 設定資料流
description: 瞭解如何啟用資料串流並設定Experience Cloud解決方案。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
feature: Web SDK,Tags,Datastreams
exl-id: ca28374a-9fe0-44de-a7ac-0aa046712515
source-git-commit: 9f75ef042342e1ff9db6039e722159ad96ce5e5b
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 4%

---

# 設定資料流


>[!CAUTION]
>
>我們預計於2024年3月15日星期五發佈本教學課程的重大變更。 在那之後，許多練習將會變更，您可能需要從頭開始重新啟動教學課程，才能完成所有課程。

瞭解如何啟用資料串流並設定Experience Cloud解決方案。

資料串流會告訴Adobe Experience Platform Edge Network要將由Platform Web SDK收集的資料傳送至何處。 在資料串流設定中，您可以啟用Experience Cloud應用程式、Experience Platform帳戶和事件轉送。 請參閱 [設定資料串流的基礎知識](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=zh-Hant) 以取得更多詳細資訊。

## 學習目標

在本課程結束時，您將能夠：

* 建立資料串流
* 啟用您的Experience Cloud應用程式
* 啟用Experience Platform

## 先決條件

在設定資料流之前，您必須先完成下列課程：

* [設定許可權](configure-permissions.md)
* [設定結構描述](configure-schemas.md)
* [設定身分名稱空間](configure-identities.md)

## 建立資料串流

現在您可以建立資料串流，告訴Platform Edge Network要將Web SDK收集的資料傳送至何處。

**若要建立資料串流：**

1. 開啟 [資料收集介面](https://launch.adobe.com/tw/){target="_blank"}
1. 確定您在正確的沙箱中

   >[!NOTE]
   >
   >如果您是Real-Time CDP等平台型應用程式的客戶，我們建議您在本教學課程中使用開發沙箱。 如果沒有，請使用 **[!UICONTROL Prod]** 沙箱。

1. 前往 **[!UICONTROL 資料串流]** 在左側導覽列中
1. 選取 **[!UICONTROL 新增資料串流]** 在熒幕的右側。
1. 輸入 `Luma Web SDK` 作為 **[!UICONTROL 名稱]**. 稍後當您在標籤屬性中設定Web SDK擴充功能時，會參考此名稱。
1. 選取您的 `Luma Web Event Data` 作為 **[!UICONTROL 事件結構描述]**
1. 選取 **[!UICONTROL 儲存]**

   ![建立資料串流](assets/datastream-create-datastream.png)

   >[!AVAILABILITY]
   >
   >日後會將對應功能合併至本教學課程中。




在下一個畫面中，您可以將Adobe應用程式等服務新增至資料流，但此時您無法在教學課程中新增任何服務。 您將在稍後的課程中執行此動作 [設定Experience Platform](setup-experience-platform.md)， [設定Analytics](setup-analytics.md)， [設定Audience Manager](setup-audience-manager.md)， [設定目標](setup-target.md)，或 [事件轉送](setup-event-forwarding.md).

>[!NOTE]
>
>在您自己的網站上實作Platform Web SDK時，您應該建立三個資料串流以對應至您的三個標籤環境（開發、預備和生產）。 如果您使用Platform Web SDK搭配Adobe Real-time Customer Data Platform或Adobe Journey Optimizer等平台式應用程式，請務必在適當的Platform沙箱中建立這些資料串流。

您現在已準備好在標籤屬性中安裝Platform Web SDK擴充功能！

[下一步： ](install-web-sdk.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
