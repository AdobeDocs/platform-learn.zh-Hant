---
title: 使用 Web SDK 教學課程實作 Adobe Experience Cloud
description: 瞭解如何使用Adobe Experience Platform Web SDK實作Experience Cloud應用程式。
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 9f75ef042342e1ff9db6039e722159ad96ce5e5b
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 11%

---

# 使用 Web SDK 教學課程實作 Adobe Experience Cloud

>[!CAUTION]
>
>我們預計於2024年3月15日星期五發佈本教學課程的重大變更。 在那之後，許多練習將會變更，您可能需要從頭開始重新啟動教學課程，才能完成所有課程。


瞭解如何使用Adobe Experience Platform Web SDK實作Experience Cloud應用程式。

Experience Platform Web SDK是使用者端的JavaScript資料庫，可讓Adobe Experience Cloud的客戶透過Adobe Experience Platform Edge Network與Adobe應用程式和協力廠商服務互動。 另請參閱 [Adobe Experience Platform Web SDK總覽](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=zh-Hant) 以取得更多詳細資訊。

本教學課程會引導您在名為Luma的範例零售網站上實作Platform Web SDK。 此 [Luma網站](https://luma.enablementadobe.com/content/luma/us/en.html) 具備豐富的資料層和功能，可讓您建置逼真的實施。 完成本教學課程後，您應已準備好開始透過Platform Web SDK在您自己的網站上實作所有行銷解決方案。

[![Luma網站](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## 學習目標

完成本教學課程之後，您將能：

* 設定資料串流

* 建立XDM結構描述

* 新增下列Adobe Experience Cloud應用程式：
   * **[Adobe Experience Platform](setup-experience-platform.md)** (以及以Adobe Real-time Customer Data Platform、Adobe Journey Optimizer和Adobe Customer Journey Analytics等平台建置的應用程式)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* 建立標籤規則和XDM物件資料元素，以將資料傳送至Adobe應用程式

* 使用Adobe Experience Platform Debugger驗證實施

* 擷取使用者同意

* 透過事件轉送將資料轉送給第三方

>[!NOTE]
>
>類似的多重解決方案教學課程適用於 [行動SDK](../tutorial-mobile-sdk/overview.md).

## 先決條件

所有Experience Cloud客戶都可以使用Platform Web SDK。 授權Real-time Customer Data Platform或Journey Optimizer等平台式應用程式使用Web SDK並非必要條件。

這些課程假設您擁有Adobe帳戶，而且 [必要許可權](configure-permissions.md) 以完成課程。 如果沒有，您必須聯絡您的Experience Cloud管理員以請求存取權。

此外，我們假設您已熟悉 HTML 和 JavaScript 等前端開發語言。您不需要精通這些語言，但如果您能閱讀並瞭解程式碼，可進一步瞭解本教學課程。

我們開始吧！

[下一步： ](configure-permissions.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
