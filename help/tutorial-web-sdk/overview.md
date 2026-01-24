---
title: 使用 Web SDK 教學課程實作 Adobe Experience Cloud
description: 了解如何使用 Adobe Experience Platform Web SDK 實施 Experience Cloud 應用程式。
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 7%

---

# 使用 Web SDK 教學課程實作 Adobe Experience Cloud

了解如何使用 Adobe Experience Platform Web SDK 實施 Experience Cloud 應用程式。

Experience Platform Web SDK是使用者端的JavaScript資料庫，可讓Adobe Experience Cloud的客戶透過Adobe Experience Platform Edge Network與Adobe應用程式和協力廠商服務互動。 如需詳細資訊，請參閱[Adobe Experience Platform Web SDK概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/edge/home)。

![Experience Platform Web SDK架構](assets/dc-websdk.png)

本教學課程會引導您在名為Luma的範例零售網站上實作Platform Web SDK。 [Luma網站](https://luma.enablementadobe.com/content/luma/us/en.html)具有豐富的資料層和功能，可讓您建置逼真的實施。 在本教學課程中，您可以：

* 使用適用於Luma網站的Platform Web SDK實作，在您自己的帳戶中建立自己的標籤屬性。
* 設定Web SDK實作的所有資料收集功能，例如資料串流、結構描述和身分識別名稱空間。
* 新增下列Adobe Experience Cloud應用程式：
   * **[Adobe Experience Platform](setup-experience-platform.md)** (以及以Adobe Real-Time Customer Data Platform、Adobe Journey Optimizer和Adobe Customer Journey Analytics等平台建置的應用程式)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* 實作事件轉送功能，將Web SDK收集的資料傳送至Adobe以外的目的地。
* 使用Experience Platform Debugger和Assurance驗證您自己的Platform Web SDK實作。

完成本教學課程後，您應已準備好開始透過Platform Web SDK在您自己的網站上實作所有的行銷應用程式！


>[!NOTE]
>
>[行動SDK](../tutorial-mobile-sdk/overview.md)也提供類似的多解決方案教學課程。

## 先決條件

所有Experience Cloud客戶都可以使用Platform Web SDK。 授權Real-Time Customer Data Platform或Journey Optimizer等平台型應用程式使用Web SDK並非必要條件。

這些課程假設您擁有Adobe帳戶和完成課程所需的許可權。 如果沒有，您必須聯絡貴公司的Experience Cloud管理員以取得存取權。

* 針對&#x200B;**資料彙集**，您必須擁有：
   * **[!UICONTROL 平台]** — 對&#x200B;**[!UICONTROL Web]**&#x200B;的許可權，如果授權，**[!UICONTROL Edge]**
   * **[!UICONTROL 屬性權利]** — 許可權&#x200B;**[!UICONTROL 核准]**、**[!UICONTROL 開發]**、**[!UICONTROL 編輯屬性]**、**[!UICONTROL 管理環境]**、**[!UICONTROL 管理擴充功能]**&#x200B;以及&#x200B;**[!UICONTROL 發佈]**，
   * **[!UICONTROL 公司權利]** — 使用&#x200B;**[!UICONTROL 管理屬性]**&#x200B;的許可權

     如需有關標籤許可權的詳細資訊，請參閱[檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/tags/admin/user-permissions)。

* 針對&#x200B;**Experience Platform**，您必須擁有：

   * 存取&#x200B;**預設生產**，**「生產」**&#x200B;沙箱。
   * 存取&#x200B;**[!UICONTROL 資料模型化]**&#x200B;下的&#x200B;**[!UICONTROL 管理結構描述]**&#x200B;和&#x200B;**[!UICONTROL 檢視結構描述]**。
   * 存取&#x200B;**[!UICONTROL Identity Management]**&#x200B;下的&#x200B;**[!UICONTROL 管理識別名稱空間]**&#x200B;和&#x200B;**[!UICONTROL 檢視識別名稱空間]**。
   * 存取&#x200B;**[!UICONTROL 資料彙集]**&#x200B;下的&#x200B;**[!UICONTROL 管理資料串流]**&#x200B;和&#x200B;**[!UICONTROL 檢視資料串流]**。
   * 如果您是平台式應用程式的客戶，且即將完成[設定Experience Platform](setup-experience-platform.md)課程，您也應該有：
      * 存取&#x200B;**開發**&#x200B;沙箱。
      * **[!UICONTROL 資料管理]**&#x200B;和&#x200B;**[!UICONTROL 設定檔管理]**&#x200B;下的所有許可權專案：

     所有Experience Cloud客戶都應該可以使用所需的功能，即使您並非Real-Time CDP等平台型應用程式的客戶。

     如需有關Platform存取控制的詳細資訊，請參閱[檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/access-control/home)。

* 針對選用的&#x200B;**Adobe Analytics**&#x200B;課程，您必須擁有[報表套裝設定、處理規則和Analysis Workspace的管理員存取權](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-console/home)

* 對於選用的&#x200B;**Adobe Target**&#x200B;課程，您必須擁有[編輯者或核准者](https://experienceleague.adobe.com/zh-hant/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80)存取權。

* 對於選用的&#x200B;**Audience Manager**&#x200B;課程，您必須有權建立、讀取和寫入特徵、區段和目的地。 如需詳細資訊，請參閱有關[Audience Manager角色型存取控制](https://experienceleague.adobe.com/zh-hant/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control)的教學課程。


>[!NOTE]
>
>我們假設您熟悉HTML和JavaScript等前端開發語言。 您不需要精通這些語言，但如果您能閱讀並瞭解程式碼，可進一步瞭解本教學課程。

## 更新

* 2024年4月24日：重大更新，包括新增設定變數/更新變數、分割個人化和分析請求、Journey Optimizer課程

## 載入Luma網站

在個別的瀏覽器分頁中載入[Luma網站](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}，並將它加入書籤，以便在教學課程期間視需要輕鬆載入。 除了能夠載入我們的託管生產網站，您不需要任何其他存取Luma的許可權。

[![Luma網站](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

我們開始吧！

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=zh-Hant)上分享
