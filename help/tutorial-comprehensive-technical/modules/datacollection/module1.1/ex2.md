---
title: 基礎 — Adobe Experience Platform資料收集與Web SDK擴充功能的設定 — Edge Network、資料串流和伺服器端資料收集
description: 基礎 — Adobe Experience Platform資料收集與Web SDK擴充功能的設定 — Edge Network、資料串流和伺服器端資料收集
kt: 5342
doc-type: tutorial
exl-id: e97d40b5-616d-439c-9d6b-eaa4ebf5acb0
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 1.1.2Edge Network、資料串流和伺服器端資料收集

## 內容

在本練習中，您將建立&#x200B;**資料流**。 **資料串流**&#x200B;會通知Adobe Edge伺服器，在Web SDK收集資料後，要將資料傳送至何處。 例如，您要將資料傳送至Adobe Experience Platform嗎？ Adobe Analytics？ Adobe Audience Manager？ Adobe Target？

資料串流一律在Adobe Experience Platform資料收集使用者介面中進行管理，對於使用Web SDK進行Adobe Experience Platform資料收集至關重要。 即使您使用非Adobe標籤管理解決方案實作Web SDK，您仍需在Adobe Experience Platform資料收集使用者介面中建立資料流。

在下一個練習中，您將在瀏覽器上實施Web SDK。 然後您會更清楚知道正在收集的資料是什麼樣子。 目前，我們只是告訴Datastream將資料轉送至何處。

## 建立資料串流

在[快速入門](./../../../modules/gettingstarted/gettingstarted/ex2.md)中，您已建立資料串流，但我們並未討論資料串流的背景和原因。

Satastream會告訴Adobe Edge伺服器，在Web SDK收集資料後，應將資料傳送至何處。 例如，您要將資料傳送至Adobe Experience Platform嗎？ Adobe Analytics？ Adobe Audience Manager？ Adobe Target？ 資料串流在Adobe Experience Platform資料收集使用者介面中進行管理，並且對於使用Web SDK進行資料收集至關重要，無論您是否透過Adobe Experience Platform資料收集實施Web SDK。

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
- 依預設，所有設定檔資料都會收集到資料集&#x200B;**示範系統 — 網站的設定檔資料集（全域v1.1）** （Web SDK目前尚不支援以Web SDK原生擷取設定檔資料）
- 如果您要針對此資料流使用&#x200B;**Offer decisioning**&#x200B;應用程式服務，您必須勾選Offer decisioning方塊。 （這將是[模組3.3](./../../../modules/ajo-b2c/module3.3/offer-decisioning.md)的一部分）
- **Edge分段**&#x200B;預設為啟用，這表示在擷取傳入流量時，將會在邊緣評估合格對象
- 若要使用&#x200B;**Personalization目的地**，您必須勾選Personalization目的地的方塊。
- 
   - 若要在此資料流中使用&#x200B;**Adobe Journey Optimizer**&#x200B;的功能，您必須勾選Adobe Journey Optimizer的方塊。


目前，您的資料流不需要其他設定。

下一步： [1.1.3 Adobe Experience Platform資料彙集簡介](./ex3.md)

[返回模組1.1](./data-ingestion-launch-web-sdk.md)

[返回所有模組](./../../../overview.md)
