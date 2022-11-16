---
title: 在行動應用程式中實作Adobe Experience Cloud教學課程概觀
description: 了解如何實作Adobe Experience Cloud行動應用程式。 本教學課程將引導您在範例Swift應用程式中實施Experience Cloud應用程式。
recommendation: noDisplay,catalog
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 10%

---

# 在行動應用程式教學課程中實作 Adobe Experience Cloud

了解如何透過 Adobe Experience Platform Mobile SDK 在行動應用程式中實作 Adobe Experience Cloud 應用程式。

Experience PlatformMobile SDK是用戶端SDK，可讓Adobe Experience Cloud的客戶透過Adobe Experience Platform邊緣網路與Adobe應用程式和協力廠商服務互動。 請參閱 [Adobe Experience Platform Mobile SDK檔案](https://aep-sdks.gitbook.io/docs/) 以取得詳細資訊。

![建置設定](assets/data-collection-mobile-sdk.png)


本教學課程會引導您完成Platform Mobile SDK在名為Luma的範例零售應用程式中的實作。 此 [Luma應用程式](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) 功能可讓您建置逼真的實作。 完成本教學課程後，您應已準備好開始在自己的行動應用程式中透過Platform Mobile SDK實作所有行銷解決方案。

這些課程是為iOS設計並在Swift中撰寫的，但許多概念也適用於Android™。

完成本教學課程後，您將能：

* 使用標準和自訂欄位群組建立結構。
* 設定資料流。
* 設定行動標籤屬性。
* 設定Experience Platform資料集（選用）。
* 在應用程式中安裝並實作標籤擴充功能。
* 新增下列Adobe Experience Cloud應用程式/擴充功能：
   * [Adobe Experience Platform Edge(XDM)](events.md)
   * [生命週期資料收集](lifecycle-data.md)
   * [Adobe Analytics（透過XDM）](analytics.md)
   * [同意](consent.md)
   * [身分](identity.md)
   * [設定檔](profile.md)
   * [Adobe Experience Platform](platform.md)
   * [使用Journey Optimizer推送訊息](journey-optimizer-push.md)
* 正確將Experience Cloud參數傳遞至 [webview](web-views.md).
* 使用驗證實作 [Adobe Experience Platform保障](assurance.md).

>[!NOTE]
>
>提供類似的多重解決方案教學課程 [Web SDK](../tutorial-web-sdk/overview.md).

## 必要條件

這些課程假設您擁有 Adobe ID 和完成練習所需的權限。否則，請洽詢您的Adobe管理員以要求存取權。

* 在資料收集中，您必須：
   * **[!UICONTROL 平台]** — 權限項目 **[!UICONTROL 行動]**
   * **[!UICONTROL 屬性權利]** — 權限項目 **[!UICONTROL 開發]**, **[!UICONTROL 核准]**, **[!UICONTROL 發佈]**, **[!UICONTROL 管理擴充功能]**，和 **[!UICONTROL 管理環境]**.
   * **[!UICONTROL 公司權利]** — 權限項目 **[!UICONTROL 管理屬性]** 和，如果您已完成選用推送訊息課程， **[!UICONTROL 管理應用程式設定]**

      如需標籤權限的詳細資訊，請參閱 [標籤的使用者權限](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=zh-Hant)產品檔案中的{target=&quot;_blank&quot;}。
* 在Experience Platform中，您必須：
   * **[!UICONTROL 資料模型]** — 管理和檢視結構的權限項目。
   * **[!UICONTROL Identity Management]** — 管理和檢視身分識別命名空間的權限項目。
   * **[!UICONTROL 資料收集]** — 管理和檢視資料流的權限項目。

   * 如果您是Platform型應用程式(如Real-time CDP、Journey Optimizer或Customer Journey Analytics)的客戶，您也應該有：
      * **[!UICONTROL 資料管理]** — 管理和檢視資料集以完成的權限項目 _可選平台練習_ （需要平台型應用程式的授權）。
      * 發展 **沙箱** 這可供本教學課程使用。
* 對於Adobe Analytics，你必須知道 **報表套裝** 您可以使用來完成本教學課程。

所有Experience Cloud客戶皆應可存取部署行動SDK所需的必要功能。

此外，我們假設您熟悉 [!DNL Swift]. 您不需要是專家就能完成這些課程，但如果您熟悉且了解程式碼，將能從中學到更多。

## 下載Luma應用程式

範例應用程式的兩個版本可供下載。

1. [空白](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} — 不含任何Experience Cloud程式碼的版本，可完成本教學課程中的實作練習
1. [已完全實施](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} — 版本，提供完整Experience Cloud實作以供參考。

我們開始吧！


下一個： **[建立XDM結構](create-schema.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)