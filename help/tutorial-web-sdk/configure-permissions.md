---
title: 設定教學課程的許可權
description: 瞭解如何請求Experience PlatformWeb SDK的存取權，並設定完成「使用Web SDK實作Adobe Experience Cloud」教學課程所需的許可權。
feature: Web SDK,Tags,Access Control
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 3%

---

# 設定教學課程的許可權

瞭解如何要求Experience Platform Web SDK的存取權，以及設定完成本教學課程所需的許可權。 若要使用資料收集介面中的標籤來實作Platform Web SDK，您必須擁有中設定的適當使用者許可權 [Admin Console](https://adminconsole.adobe.com).

## 資料收集

* 具有下列專案的許可權： **[!UICONTROL 開發]**， **[!UICONTROL 編輯]**， **[!UICONTROL 核准]**， **[!UICONTROL 發佈]**， **[!UICONTROL 管理擴充功能]**， **[!UICONTROL 管理環境]**、和 **[!UICONTROL 管理屬性]**. 如需有關標籤許可權的詳細資訊，請參閱 [說明檔案](https://experienceleague.adobe.com/en/docs/experience-platform/tags/admin/user-permissions).
* 如果您要完成選用的事件轉送課程，請取得產品授權，包括邊緣轉送和許可權專案 **[!UICONTROL 平台]** > **[!UICONTROL Edge]**

## Experience Platform

這些功能應該可供所有Experience Cloud客戶使用，即使您並非Real-Time CDP等平台型應用程式的客戶。

* 存取 **預設生產**， **&quot;Prod&quot;** 沙箱。
* 存取目標 **[!UICONTROL 管理結構描述]** 和 **[!UICONTROL 檢視結構描述]** 在 **[!UICONTROL 資料模式]**.
* 存取目標 **[!UICONTROL 管理身分識別名稱空間]** 和 **[!UICONTROL 檢視身分識別名稱空間]** 在 **[!UICONTROL Identity Management]**.
* 存取目標 **[!UICONTROL 管理資料串流]** 和 **[!UICONTROL 檢視資料串流]** 在 **[!UICONTROL 資料彙集]**.
* 如果您是平台式應用程式的客戶，並將完成 [設定Experience Platform](setup-experience-platform.md) 課程，您也應該有：
   * 存取 **開發** 沙箱。
   * 下的所有許可權專案 **[!UICONTROL 資料管理]**、和 **[!UICONTROL 設定檔管理]**：


如需有關Platform存取控制的詳細資訊，請參閱 [說明檔案](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home).

## Adobe Analytics

若要參加選用的Adobe Analytics課程，您必須擁有 [管理員對報表套裝設定、處理規則和Analysis Workspace的存取權](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-console/home)

## Adobe Target

若要參加選用的Adobe Target課程，您必須擁有 [編輯者或核准者](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 存取。

## Adobe Audience Manager

* 針對選用的Audience Manager課程，您必須有權建立、讀取和寫入特徵、區段和目的地。 如需詳細資訊，請參閱以下教學課程： [Audience Manager的角色型存取控制](https://experienceleague.adobe.com/en/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control).

現在您已準備好開始初始設定步驟。

[下一步： ](configure-schemas.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
