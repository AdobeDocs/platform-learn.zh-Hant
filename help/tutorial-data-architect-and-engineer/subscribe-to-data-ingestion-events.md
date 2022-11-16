---
title: 訂閱資料擷取事件
seo-title: Subscribe to data ingestion events | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 訂閱資料擷取事件
description: 在本課程中，您將透過Adobe Developer主控台和線上Webhook開發工具來設定Webhook，以訂閱資料擷取事件。 在後續課程中，您將使用這些事件來監控資料擷取作業的狀態。
role: Data Engineer
feature: Data Management
kt: 4348
thumbnail: 4348-subscribe-to-data-ingestion-events.jpg
exl-id: f4b90832-4415-476f-b496-2f079b4fcbbc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# 訂閱資料擷取事件

<!--25min-->

在本課程中，您將透過Adobe Developer主控台和線上Webhook開發工具來設定Webhook，以訂閱資料擷取事件。 在後續課程中，您將使用這些事件來監控資料擷取作業的狀態。

**資料工程師** 會想要訂閱本教學課程以外的資料擷取事件。
**資料架構師** _可以略過本課程_ 然後前往 [批次擷取課程](ingest-batch-data.md).

## 需要權限

在 [設定權限](configure-permissions.md) 課程中，您設定了完成本課程所需的所有訪問控制，具體來說：

<!--* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

>[!IMPORTANT]
>
> 資料擷取事件所觸發的這些通知將套用至 _所有沙箱_，而不只是您的 `Luma Tutorial`. 您可能也會看到來自帳戶中其他資料擷取事件的通知。


## 設定網頁鈎

在本練習中，我們將使用名為webhook.site的線上工具建立Webhook（您可以隨意替換您喜歡使用的任何其他Webhook開發工具）:

1. 在其他瀏覽器標籤中，開啟網站 [https://webhook.site/](https://webhook.site/)
1. 您稍後會在資料擷取課程中返回時，會獲派一個應將之加入書籤的唯一URL:

   ![Webhook.site](assets/ioevents-webhook-home.png)
1. 選取 **編輯** 按鈕
1. 作為回應內文，請輸入 `$request.query.challenge$`. 我們在本課程稍後設定的Adobe I/O事件通知會傳送挑戰給Webhook，並要求將其包含在回應內文中。
1. 選取 **儲存** 按鈕

   ![編輯回應](assets/ioevents-webhook-editResponse.png)

## 設定

1. 在其他瀏覽器標籤中，開啟 [Adobe Developer Console](https://console.adobe.io/)
1. 開啟 `Luma Tutorial API Project`
1. 選取 **[!UICONTROL 新增至專案]** 按鈕，然後選取 **[!UICONTROL 事件]**

   ![新增事件](assets/ioevents-addEvents.png)
1. 選取 **[!UICONTROL Experience Platform]**
1. 選擇 **[!UICONTROL 平台通知]**
1. 選取 **[!UICONTROL 下一個]** 按鈕
   ![新增通知](assets/ioevents-addNotifications.png)
1. 選取所有事件
1. 選取 **[!UICONTROL 下一個]** 按鈕
   ![選取訂閱](assets/ioevents-addSubscriptions.png)
1. 在設定認證的下一個畫面中，選取 **[!UICONTROL 下一個]** 再次
   ![跳過憑據螢幕](assets/ioevents-clickNext.png)
1. 作為 **[!UICONTROL 事件註冊名稱]**，輸入 `Platform notifications`
1. 向下捲動並選取以開啟 **[!UICONTROL Webhook]** 節
1. 作為 **[!UICONTROL Webhook URL]**，從 **您的唯一URL** webhook.site中的欄位
1. 選取 **[!UICONTROL 儲存已設定的事件]** 按鈕
   ![儲存事件](assets/ioevents-addWebhook.png)
1. 等候設定儲存，您應會看到 `Platform notifications` 事件對您的WebHook詳細資訊處於活動狀態，且沒有錯誤訊息
   ![已儲存的設定](assets/ioevents-webhookConfigured.png)
1. 切換回webhook.site標籤，您應該會看到對Webhook的第一個請求，這是因為驗證了您的開發人員控制台配置：
   ![webhook.site中的第一個要求](assets/ioevents-webhook-firstRequest.png)

目前已完成，您在擷取資料時，將在下堂課中進一步了解這些通知。

## 其他資源

* [Webhook.site](https://webhook.site/)
* [資料擷取通知檔案](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html)
* [Adobe I/O事件快速入門檔案](https://www.adobe.io/apis/experienceplatform/events/docs.html)

好了，我們最後開始 [擷取資料](ingest-batch-data.md)!
