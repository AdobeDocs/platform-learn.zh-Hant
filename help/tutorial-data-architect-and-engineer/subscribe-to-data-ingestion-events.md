---
title: 訂閱資料擷取事件
seo-title: Subscribe to data ingestion events | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 訂閱資料擷取事件
description: 在本課程中，您將使用Adobe Developer主控台和線上webhook開發工具設定webhook ，以訂閱資料擷取事件。 在後續的課程中，您將使用這些事件來監控資料擷取工作的狀態。
role: Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-subscribe-to-data-ingestion-events.jpg
exl-id: f4b90832-4415-476f-b496-2f079b4fcbbc
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# 訂閱資料擷取事件

<!--25min-->

在本課程中，您將使用Adobe Developer主控台和線上webhook開發工具設定webhook ，以訂閱資料擷取事件。 在後續的課程中，您將使用這些事件來監控資料擷取工作的狀態。

**資料工程師** 將會想要訂閱本教學課程以外的資料擷取事件。
**資料架構師** _可以略過本課程_ 並前往 [批次擷取課程](ingest-batch-data.md).

## 需要的許可權

在 [設定許可權](configure-permissions.md) 課程，您可以設定完成本課程所需的所有存取控制項，尤其是：

<!--* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

>[!IMPORTANT]
>
> 這些由資料擷取事件觸發的通知將套用至 _您的所有沙箱_，而不僅僅是 `Luma Tutorial`. 您也可能會在帳戶中看到源自其他資料擷取事件的通知。


## 設定webhook

在本練習中，我們將使用名為webhook.site的線上工具來建立webhook （您可以隨意取代您偏好使用的任何其他webhook開發工具）：

1. 在另一個瀏覽器標籤中，開啟網站 [https://webhook.site/](https://webhook.site/)
1. 系統已為您指派一個唯一的URL，當您稍後在資料擷取課程中返回該URL時，您應該將該URL加入書籤：

   ![Webhook.site](assets/ioevents-webhook-home.png)
1. 選取 **編輯** 頂端導覽列中的按鈕
1. 回應內文請輸入 `$request.query.challenge$`. 我們在本課程稍後設定的Adobe I/O事件通知會向webhook傳送挑戰，並要求將其包含在回應本文中。
1. 選取 **儲存** 按鈕

   ![編輯回應](assets/ioevents-webhook-editResponse.png)

## 設定

1. 在另一個瀏覽器標籤中，開啟 [Adobe Developer主控台](https://console.adobe.io/)
1. 開啟您的 `Luma Tutorial API Project`
1. 選取 **[!UICONTROL 新增至專案]** 按鈕，然後選取 **[!UICONTROL 事件]**

   ![新增事件](assets/ioevents-addEvents.png)
1. 透過選取以下專案篩選清單 **[!UICONTROL Experience Platform]**
1. 選取 **[!UICONTROL 平台通知]**
1. 選取 **[!UICONTROL 下一個]** 按鈕
   ![新增通知](assets/ioevents-addNotifications.png)
1. 選取所有事件
1. 選取 **[!UICONTROL 下一個]** 按鈕
   ![選取訂閱](assets/ioevents-addSubscriptions.png)
1. 在設定認證的下一個畫面上，選取 **[!UICONTROL 下一個]** 再次按鈕
   ![略過認證畫面](assets/ioevents-clickNext.png)
1. 作為 **[!UICONTROL 事件註冊名稱]**，輸入 `Platform notifications`
1. 向下捲動並選取「 」以開啟 **[!UICONTROL Webhook]** 區段
1. 作為 **[!UICONTROL Webhook URL]**，貼上以下位置的值： **您的唯一URL** webhook.site的欄位
1. 選取 **[!UICONTROL 儲存已設定的事件]** 按鈕
   ![儲存事件](assets/ioevents-addWebhook.png)
1. 等候設定儲存，應該會看到您的 `Platform notifications` 事件為「作用中」，其中包含您的webhook詳細資料且沒有錯誤訊息
   ![設定已儲存](assets/ioevents-webhookConfigured.png)
1. 切換回您的webhook.site標籤，您應該會看到對webhook的第一個請求，該請求是因開發人員控制檯設定驗證而產生：
   ![webhook.site中的第一個要求](assets/ioevents-webhook-firstRequest.png)

目前為止，當您內嵌資料時，您將在下一課程中進一步瞭解這些通知。

## 其他資源

* [Webhook.site](https://webhook.site/)
* [資料擷取通知檔案](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html)
* [Adobe I/O事件快速入門檔案](https://www.adobe.io/apis/experienceplatform/events/docs.html)

好，終於開始了 [擷取資料](ingest-batch-data.md)！
