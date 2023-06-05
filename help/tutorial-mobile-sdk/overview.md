---
title: 在行動應用程式教學課程中實作Adobe Experience Cloud概述
description: 瞭解如何實作Adobe Experience Cloud行動應用程式。 本教學課程會引導您實施範例Swift應用程式中的Experience Cloud應用程式。
recommendations: noDisplay,catalog
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: 4bccc95ff94e9377b65771268e82b1900c003fc1
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 11%

---

# 在行動應用程式教學課程中實作 Adobe Experience Cloud

了解如何透過 Adobe Experience Platform Mobile SDK 在行動應用程式中實作 Adobe Experience Cloud 應用程式。

Experience Platform Mobile SDK是使用者端SDK，可讓Adobe Experience Cloud客戶透過Adobe Experience Platform Edge Network與Adobe應用程式和協力廠商服務互動。 請參閱 [Adobe Experience Platform Mobile SDK檔案](https://developer.adobe.com/client-sdks/documentation/) 以取得更多詳細資訊。

![建置設定](assets/data-collection-mobile-sdk.png)


本教學課程會逐步引導您在名為Luma的範例零售應用程式中實作Platform Mobile SDK。 此 [Luma應用程式](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) 具備可讓您建置逼真實作的功能。 完成本教學課程後，您應已準備好開始在自己的行動應用程式中透過Platform Mobile SDK實作所有行銷解決方案。

這些課程專為iOS設計且以Swift語言撰寫，但許多概念也適用於Android™。

完成本教學課程後，您將能夠：

* 使用標準和自訂欄位群組建立結構描述。
* 設定資料流.
* 設定行動標籤屬性。
* 設定Experience Platform資料集（選用）。
* 在應用程式中安裝並實作標籤擴充功能。
* 新增下列Adobe Experience Cloud應用程式/擴充功能：
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [生命週期資料收集](lifecycle-data.md)
   * [透過XDM的Adobe Analytics](analytics.md)
   * [同意](consent.md)
   * [身分](identity.md)
   * [設定檔](profile.md)
   * [Adobe Experience Platform](platform.md)
   * [使用Journey Optimizer推送訊息](journey-optimizer-push.md)
* 正確將Experience Cloud引數傳遞至 [webview](web-views.md).
* 使用驗證實施 [Adobe Experience Platform保證](assurance.md).

>[!NOTE]
>
>類似的多重解決方案教學課程適用於 [Web SDK](../tutorial-web-sdk/overview.md).

## 必要條件

這些課程假設您擁有 Adobe ID 和完成練習所需的權限。如果沒有，您應該聯絡您的Adobe管理員以請求存取權。

* 在「資料收集」中，您必須具備：
   * **[!UICONTROL 平台]** — 許可權專案 **[!UICONTROL 行動]**
   * **[!UICONTROL 屬性權利]** — 許可權專案至 **[!UICONTROL 開發]**， **[!UICONTROL 核准]**， **[!UICONTROL 發佈]**， **[!UICONTROL 管理擴充功能]**、和 **[!UICONTROL 管理環境]**.
   * **[!UICONTROL 公司權利]** — 許可權專案至 **[!UICONTROL 管理屬性]** 此外，如果完成選用的推播訊息課程， **[!UICONTROL 管理應用程式設定]**

      如需標籤許可權的詳細資訊，請參閱 [標籤的使用者許可權](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=zh-Hant){target="_blank"} 產品檔案內。
* 在Experience Platform中，您必須具有：
   * **[!UICONTROL 資料模型]** — 管理和檢視結構描述的許可權專案。
   * **[!UICONTROL Identity Management]** — 管理和檢視身分名稱空間的許可權專案。
   * **[!UICONTROL 資料彙集]** — 管理及檢視資料串流的許可權專案。

   * 如果您是平台型應用程式(例如Real-Time CDP、Journey Optimizer或Customer Journey Analytics)的客戶，您也應擁有：
      * **[!UICONTROL 資料管理]** — 管理和檢視資料集的許可權專案，以完成 _選用的平台練習_ （需要平台式應用程式的授權）。
      * 開發 **沙箱** 供您在本教學課程中使用。
* 針對Adobe Analytics，您必須知道哪些 **報告套裝** 您可以使用完成本教學課程。

所有Experience Cloud客戶都應該有權存取部署Mobile SDK所需的功能。

此外，我們假設您熟悉 [!DNL Swift]. 您不需要成為專家就能完成課程，但如果您熟悉且瞭解程式碼，將能從中學到更多。

## 下載Luma應用程式

範例應用程式有兩個版本可供下載。

1. [空白](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}  — 沒有任何Experience Cloud程式碼的版本，以完成本教學課程中的實作練習
1. [完整實作](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}  — 具有完整Experience Cloud實作的版本，以供參考。

我們開始吧！


下一步： **[建立XDM結構描述](create-schema.md)**

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Mobile SDK。 若您有任何疑問、想分享一般意見或對未來內容有任何建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)