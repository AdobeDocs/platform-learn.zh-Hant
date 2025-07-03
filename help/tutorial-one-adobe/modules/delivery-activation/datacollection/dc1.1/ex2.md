---
title: 基礎 — Adobe Experience Platform Data Collection設定和Web SDK擴充功能 — Edge Network、資料串流和伺服器端資料收集
description: 基礎 — Adobe Experience Platform Data Collection設定和Web SDK擴充功能 — Edge Network、資料串流和伺服器端資料收集
kt: 5342
doc-type: tutorial
exl-id: f805b2a6-c813-4734-8a78-f8588ecd0683
source-git-commit: 31466040336580e9e4b2308801347dc387be4da5
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# 1.1.2 Edge Network、資料串流和伺服器端資料收集

## 內容

在本練習中，您將建立&#x200B;**資料串流**。 **資料串流**&#x200B;會通知Adobe Edge Network伺服器，在Web SDK收集資料後，要將資料傳送至何處。 例如，您要將資料傳送至Adobe Experience Platform嗎？ Adobe Analytics？ Adobe Audience Manager？ Adobe Target？

資料串流一律在Experience Platform資料收集使用者介面中進行管理，對於使用[網頁SDK](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/web-sdk/home)進行Experience Platform資料收集至關重要。 即使您使用非Adobe標籤管理解決方案實作Web SDK，仍需要建立資料串流。

在下一個練習中，您將在瀏覽器上實作Web SDK。 然後您會更清楚知道正在收集的資料是什麼樣子。 目前，我們只是告訴資料流將資料轉送至何處。

## 建立資料串流

您在[快速入門](./../../../../modules/getting-started/gettingstarted/ex2.md)中已建立資料流，但我們並未討論您建立資料流的背景和原因。

[資料串流](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/datastreams/overview)會通知Edge Network伺服器，在網頁SDK收集資料後，要將資料傳送至何處。 如需透過資料流傳送資料的完整詳細資訊，請參閱[新增服務至資料流](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/datastreams/configure#add-services)的檔案。

資料串流在Experience Platform資料收集使用者介面中管理，且對於透過Web SDK進行資料收集至關重要，無論您是否透過Adobe Experience Platform資料收集實作Web SDK。

讓我們檢閱您的&#x200B;**[!UICONTROL 資料流]**：

移至[https://experience.adobe.com/launch/](https://experience.adobe.com/launch/)。

按一下左側功能表中的&#x200B;**[!UICONTROL 資料串流]**。

![按一下左側導覽中的[資料流]圖示](./images/edgeconfig1.png)

開啟名為`--aepUserLdap-- - Demo System Datastream`的資料流。

![命名資料流並儲存](./images/edgeconfig2.png)

之後，您將會看到資料流的詳細資料。

![命名資料流並儲存](./images/edgecfg1.png)

按一下&#x200B;**Adobe Experience Platform**&#x200B;旁的&#x200B;**...**，然後按一下&#x200B;**編輯**。

![命名資料流並儲存](./images/edgecfg1a.png)

您將會看到此訊息。 目前您僅啟用Adobe Experience Platform。 您的設定將與以下設定類似。 (根據您的環境和Adobe Experience Platform執行個體，沙箱名稱可能會不同)

![命名資料流並儲存](./images/edgecfg2.png)

您應將以下欄位解譯如下：

針對此資料流……

- 所有收集的資料都會儲存在Adobe Experience Platform的`--aepSandboxName--`沙箱中
- 預設會將所有體驗事件資料收集到資料集&#x200B;**示範系統 — 網站的事件資料集（全域v1.1）**&#x200B;中
- 依預設，所有設定檔資料都會收集到資料集&#x200B;**示範系統 — 網站的設定檔資料集（全域v1.1）** (Web SDK目前尚不支援以原生方式擷取Web SDK的設定檔資料)
- **Edge分段**&#x200B;預設為啟用，這表示在擷取傳入流量時，將會在邊緣評估合格對象
- 若要使用[個人化目的地](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/destinations/catalog/personalization/overview)，請勾選&#x200B;**Personalization目的地**&#x200B;的方塊。
- 若要在此資料流中使用&#x200B;**Adobe Journey Optimizer**&#x200B;的功能，您必須勾選&#x200B;**Adobe Journey Optimizer**&#x200B;的方塊。

目前，您的資料流不需要其他設定。

## 後續步驟

移至[1.1.3 Adobe Experience Platform資料彙集簡介](./ex3.md){target="_blank"}

返回[設定Adobe Experience Platform Data Collection和Web SDK標籤擴充功能](./data-ingestion-launch-web-sdk.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
