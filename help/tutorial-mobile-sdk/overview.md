---
title: 在行動應用程式教學課程中實作Adobe Experience Cloud概述
description: 瞭解如何實作Adobe Experience Cloud行動應用程式。 本教學課程將指導您在一個範例Swift應用程式中實施Experience Cloud應用程式。
recommendations: noDisplay,catalog
last-substantial-update: 2023-11-29T00:00:00Z
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: c08671ae28955ff090baa7aa5a47246b2196ba20
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 4%

---

# 在行動應用程式教學課程中實作Adobe Experience Cloud

了解如何透過 Adobe Experience Platform Mobile SDK 在行動應用程式中實作 Adobe Experience Cloud 應用程式。

Experience Platform Mobile SDK是使用者端的SDK，可讓Adobe Experience Cloud的客戶透過Adobe Experience Platform Edge Network與Adobe應用程式和協力廠商服務互動。 如需更多詳細資訊，請參閱[Adobe Experience Platform Mobile SDK檔案](https://developer.adobe.com/client-sdks/home/)。

![架構](assets/architecture.png)


本教學課程會引導您在名為Luma的範例零售應用程式中實施Platform Mobile SDK。 [Luma應用程式](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App)具備的功能可讓您建置逼真的實施。 完成本教學課程後，您應已準備好開始透過Experience Platform Mobile SDK在您自己的行動應用程式中實施所有行銷解決方案。

這些課程是專為iOS設計且使用Swift/SwiftUI撰寫，但許多概念也適用於Android™。

完成本教學課程之後，您將能夠：

* 使用標準和自訂欄位群組建立結構描述。
* 設定資料串流。
* 設定行動標籤屬性。
* 設定Experience Platform資料集（選用）。
* 在應用程式中安裝及實作標籤擴充功能。
* 正確傳遞Experience Cloud引數至[webview](web-views.md)。
* 使用[Adobe Experience Platform Assurance](assurance.md)驗證實作。
* 新增下列Adobe Experience Cloud應用程式/擴充功能：
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [生命週期資料集合](lifecycle-data.md)
   * [同意](consent.md)
   * [身分識別](identity.md)
   * [輪廓](profile.md)
   * [地點](places.md)
   * [Analytics](analytics.md)
   * [Experience Platform](platform.md)
   * [使用Journey Optimizer推送訊息](journey-optimizer-push.md)
   * [使用Journey Optimizer的應用程式內傳訊](journey-optimizer-inapp.md)
   * [使用Journey Optimizer進行決策管理](journey-optimizer-offers.md)
   * [Target](target.md)


>[!NOTE]
>
>[網頁SDK](../tutorial-web-sdk/overview.md)有類似的多解決方案教學課程。

## 權限

這些課程假設您擁有Adobe ID和完成練習所需的使用者層級許可權。 如果沒有，您應該聯絡Adobe管理員以要求存取權。

* 在資料收集中，您必須擁有：
   * **[!UICONTROL 平台]** — 許可權專案&#x200B;**[!UICONTROL 行動裝置]**
   * **[!UICONTROL 屬性權利]** — 許可權專案： **[!UICONTROL 開發]**、**[!UICONTROL 核准]**、**[!UICONTROL 發佈]**、**[!UICONTROL 管理擴充功能]**&#x200B;和&#x200B;**[!UICONTROL 管理環境]**。
   * **[!UICONTROL 公司權利]** — 用於&#x200B;**[!UICONTROL 管理屬性]**&#x200B;的許可權專案

     如需有關標籤許可權的詳細資訊，請參閱產品檔案中的[標籤](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=zh-Hant){target="_blank"}的使用者許可權。
* 在Experience Platform中，您必須擁有：
   * **[!UICONTROL 資料模型]** — 管理和檢視結構描述的許可權專案。
   * **[!UICONTROL Identity Management]** — 管理和檢視身分識別名稱空間的許可權專案。
   * **[!UICONTROL 資料彙集]** — 管理和檢視資料串流的許可權專案。

   * 如果您是Real-Time CDP、Journey Optimizer或Customer Journey Analytics等平台型應用程式的客戶，並將進行相關課程，您也應該有：
      * **[!UICONTROL 資料管理]** — 管理和檢視資料集的許可權專案。
      * 您可以在本教學課程中使用的開發&#x200B;**沙箱**。

   * 若要參加Journey Optimizer課程，您需要設定&#x200B;**推播通知服務**&#x200B;的許可權，以及建立&#x200B;**應用程式介面**、**歷程**、**訊息**&#x200B;和&#x200B;**訊息預設集**&#x200B;的許可權。 針對決定管理，您需要適當的許可權來&#x200B;**管理優惠**&#x200B;和&#x200B;**決定**，如[此處](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=zh-Hant#decisions-permissions)所述。

* 針對Adobe Analytics，您必須知道您可以使用哪些&#x200B;**報表套裝**&#x200B;來完成本教學課程。

* 針對Adobe Target，您必須擁有建立和啟用活動的許可權。


>[!NOTE]
>
>在本教學課程中，您會建立結構描述、資料集、身分等等。 如果有多人在一個沙箱中完成本教學課程，在建立這些物件時，請考慮在命名慣例中附加或附加身分識別。 例如，將` - <your name or initials>`新增至指示您建立的物件名稱。

## 版本記錄

* 2023年11月29日：透過新的範例應用程式和適用於應用程式內訊息、決策管理和Adobe Target的新課程進行重大檢修。
* 2022年3月9日：首次發佈

## 下載Luma應用程式

範例應用程式有兩個版本可供下載。 兩個版本均可從[Github](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App)下載/複製。 您會找到兩個資料夾：


1. [開始](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}：專案，不含程式碼，或包含您完成本教學課程中實作練習所需的大部分Experience Platform Mobile SDK程式碼的預留位置程式碼。
1. [完成](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}：具有完整實作以供參考的版本。

>[!NOTE]
>
>您使用iOS作為平台，[!DNL Swift]作為程式設計語言，[!DNL SwiftUI]作為UI架構，[!DNL Xcode]作為整合式開發環境(IDE)。 不過，許多所說明的實作概念與其他開發平台類似。 許多人已經成功完成本教學課程，很少或沒有先前的iOS/Swift(UI)體驗。 您不需要成為專家就能完成課程，但如果您熟悉且瞭解程式碼，將能從中學到更多。


您可以從App Store下載應用程式的最終產品化版本。

[![下載](assets/download-app.svg)](https://apps.apple.com/us/app/luma-app/id6466588487)


我們開始吧！

>[!SUCCESS]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)上分享。

下一步： **[建立XDM結構描述](create-schema.md)**
