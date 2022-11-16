---
title: 設定教學課程的權限
description: 了解如何要求存取Experience PlatformWeb SDK，以及設定完成「使用Web SDK實作Adobe Experience Cloud」教學課程所需的權限。
feature: Access Control
exl-id: d7c4f2c3-cf3c-4587-88f8-82113d250084
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 6%

---

# 設定教學課程的權限

了解如何要求存取Experience PlatformWeb SDK，以及設定完成本教學課程所需的權限。 若要使用資料收集介面中的標籤來實作Platform Web SDK，您必須在 [Admin Console](https://adminconsole.adobe.com).

## 資料彙集

* 擁有 **[!UICONTROL 開發]**, **[!UICONTROL 編輯]**, **[!UICONTROL 核准]**, **[!UICONTROL 發佈]**, **[!UICONTROL 管理擴充功能]**，和 **[!UICONTROL 管理環境]** 標籤屬性。 如需標籤權限的詳細資訊，請參閱 [檔案](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* 如果您要完成選用事件轉送課程，請取得產品授權，其中包含邊緣轉送和權限項目 **[!UICONTROL 平台]** > **[!UICONTROL Edge]**

## Experience Platform

即使您不是Lear-time CDP等基於平台的應用程式的Experience Cloud，這些功能也應可供所有客戶使用。

* 存取 **預設生產** 沙箱。
* 存取 **[!UICONTROL 管理結構]** 和 **[!UICONTROL 檢視結構]** 在 **[!UICONTROL 資料模型]**
* 存取 **[!UICONTROL 管理身分識別命名空間]** 和 **[!UICONTROL 檢視身分識別命名空間]** 在 **[!UICONTROL Identity Management]**
* 存取 **[!UICONTROL 管理資料流]** 和 **[!UICONTROL 檢視資料流]** 在 **[!UICONTROL 資料收集]**
* 如果您是平台型應用程式的客戶，且將完成 [設定Experience Platform](setup-experience-platform.md) 課程中，您也應該有：
   * 存取 **開發** 沙箱。
   * 下的所有權限項目 **[!UICONTROL 資料管理]**，和 **[!UICONTROL 設定檔管理]**:


如需Platform存取控制的詳細資訊，請參閱 [檔案](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=zh-Hant).

## Adobe Analytics

對於選用的Adobe Analytics課程，您必須 [報表套裝設定、處理規則和Analysis Workspace的管理員存取權](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html?lang=zh-Hant)

## Adobe Target

對於選用的Adobe Target課程，您必須 [編輯者或核准者](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 存取權。

## Adobe Audience Manager

* 對於選用的Audience Manager課程，您必須擁有建立、讀取和寫入特徵、區段和目的地的存取權。 如需詳細資訊，請參閱 [Audience Manager的基於角色的訪問控制](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).

現在，您可以開始初始配置步驟了。

[下一個： ](configure-schemas.md)

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
