---
title: 使用 Web SDK 教學課程實作 Adobe Experience Cloud
description: 了解如何使用 Adobe Experience Platform Web SDK 實施 Experience Cloud 應用程式。
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 6488faee86a53585bdbf03e069c4d6cf7e81d096
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 使用 Web SDK 教學課程實作 Adobe Experience Cloud

了解如何使用 Adobe Experience Platform Web SDK 實施 Experience Cloud 應用程式。

Experience PlatformWeb SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud的客戶透過Adobe Experience Platform邊緣網路與Adobe應用程式和協力廠商服務互動。 請參閱 [Adobe Experience Platform Web SDK概述](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html) 以取得詳細資訊。

本教學課程會引導您完成Platform Web SDK在名為Luma的範例零售網站上的實作。 [](https://luma.enablementadobe.com/content/luma/us/en.html)Luma 網站具有豐富的資料層和功能，可讓您建置逼真的實施。完成本教學課程後，您應已準備好開始透過Platform Web SDK在您自己的網站上實作所有行銷解決方案。

[![Luma 網站](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## 學習目標

完成本教學課程後，您將能：

* 設定資料串流

* 建立XDM結構

* 新增下列Adobe Experience Cloud應用程式：
   * **[Adobe Experience Platform](setup-experience-platform.md)** (以及建置在平台上的應用程式，例如Adobe Real-time Customer Data Platform、Adobe Journey Optimizer和Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* 建立標籤規則和XDM物件資料元素，將資料傳送至Adobe應用程式

* 使用Adobe Experience Platform Debugger驗證實作

* 擷取使用者同意

* 透過事件轉送將資料轉送至第三方

>[!NOTE]
>
>提供類似的多重解決方案教學課程 [行動SDK](../tutorial-mobile-sdk/overview.md).

## 先決條件

所有Experience Cloud客戶皆可使用Platform Web SDK。 不需要授權Real-time Customer Data Platform或Journey Optimizer等平台型應用程式才能使用Web SDK。

在這些課程中，假設您有Adobe帳戶，且 [必要權限](configure-permissions.md) 來完成課程。 否則，您必須聯絡您的Experience Cloud管理員以要求存取權。

此外，我們假設您已熟悉 HTML 和 JavaScript 等前端開發語言。您不需要是這些語言的專家，但如果您能閱讀和了解程式碼，可從本教學課程中學到更多。

我們開始吧！

[下一個： ](configure-permissions.md)

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
