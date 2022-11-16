---
title: 設定權限
seo-title: Configure permissions | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 設定權限
description: 在本課程中，您將使用Adobe Experience Platform的AdobeAdmin Console來設定使用者權限。
role: Data Architect, Data Engineer
feature: Access Control
kt: 4348
thumbnail: 4348-configure-permissions.jpg
exl-id: ca01f99e-f10c-4bf0-bef2-b011ac29a565
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 2%

---

# 設定權限

<!--30min-->

在本課程中，您將使用 [!DNL Adobe's Admin Console].

存取控制是Experience Platform中的關鍵隱私權功能，我們建議將權限限制在人員執行其工作功能所需的最低限度。 請參閱 [存取控制檔案](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=zh-Hant) 以取得更多資訊。

資料架構師和資料工程師是Adobe Experience Platform的強大使用者，您需要許多權限才能完成本教學課程，並在稍後的日常工作中完成。 資料架構師可能參與 *其他Platform使用者* 在他們的公司，例如行銷人員、分析師和資料科學家。 完成本課程後，請思考如何使用這些功能來管理公司的其他使用者。

**資料架構師** 通常會在本教學課程之外為其他使用者設定權限。

>[!IMPORTANT]
>
>Adobe Experience Cloud產品的系統管理員必須完成本課程中的部分步驟，這些步驟會在章節標題中說明。 如果您不是系統管理員，請聯繫貴公司的人員，要求他們完成這些任務。

## 關於Admin Console

此 [!DNL Admin Console] 是用來管理所有Adobe Experience Cloud產品使用者存取權的介面。 請參閱 [Adobe Admin Console檔案](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 以取得詳細資訊。 以下是一些鍵 [!DNL Admin Console] 概念：

* A **產品設定檔** 是權限、角色和沙箱環境的組合，系結至特定Adobe產品。 可為單一Adobe產品建立多個產品設定檔。 例如，「行銷人員」設定檔可將權限限制為一般行銷人員完成生產平台環境中的關鍵工作所需的權限，而「資料架構師」設定檔則可用來授與多個平台環境中的不同權限。 在本課程中，您將建立「Luma教學課程」產品設定檔，其中包含資料架構師和資料工程師在沙箱環境中完成本教學課程所需的所有權限。
* 安 **整合** 是與 *專案* 在Adobe Developer Console中。 Adobe Developer主控台是AdobeAPI驗證和設定的核心。 您將在開發人員控制台中設定整合，並 [!DNL Postman] 教訓。

以下是Platform現有角色的快速摘要：

* **使用者** 產品設定檔的可以根據產品設定檔中指派的權限，在Platform的使用者介面中完成工作。
* **開發人員** 產品設定檔的可以根據產品設定檔中的權限，使用Platform的API來完成工作。
* **產品設定檔管理員** 可編輯 *那個特定的* 權限，並新增使用者、開發人員和其他設定檔管理員。
* **產品管理員** 可管理 *所有產品設定檔* 適用於Platform並新增產品設定檔。
* **系統管理員** 可以新增產品管理員，基本上管理所有Adobe Experience Cloud產品的任何權限。

## 建立Experience Platform產品設定檔（需要系統管理員或產品管理員）

在本練習中，您或您公司的系統管理員將建立Adobe Experience Platform的產品設定檔，並將您新增為該產品設定檔的管理員。

>[!NOTE]
>
>如果您是系統管理員協助同事參加本教學課程，請考慮將同事新增為 *產品管理員* Adobe Experience Platform。 身為產品管理員，他們將能自行完成這些步驟，並在未來管理其他Experience Platform使用者。

若要建立產品設定檔：

1. 登入 [Adobe Admin Console](https://adminconsole.adobe.com)
1. 選擇 **[!UICONTROL 產品]** 在頂端導覽列上
1. 選擇 **[!UICONTROL Adobe Experience Platform]** 在左側導覽器上(您可能需要展開 **[!UICONTROL Experience Cloud]** 小節)
1. 您的Experience Platform例項中可能已有數個設定檔。 選取 **[!UICONTROL 新設定檔]** 按鈕以添加其他
   ![選擇添加新配置檔案](assets/adminconsole-newProfile.png)
1. 為設定檔命名 `Luma Tutorial Platform` （如果貴公司有多人參加本教學課程，請將教學課程參與者的姓名新增至結尾）並選取 **[!UICONTROL 下一個]** 按鈕
   ![為設定檔命名Luma教學課程平台](assets/adminconsole-nameProfile.png)
1. 視您的產品授權詳細資訊而定，您可能會或不會看到此秒 **[!UICONTROL 服務]** 螢幕。 在本教學課程中，我們不會使用任何這些服務，因此請取消核取 **[!UICONTROL 啟用所有服務]** to *移除* 所有服務和選擇 **[!UICONTROL 儲存]**.
   ![禁用服務](assets/adminconsole-createProfile-services.png)

現在，將教學課程參與者新增為新建立產品設定檔的管理員。 若 *you* 是教學課程參與者，請跳到 [設定Experience Platform產品設定檔](#configure-experience-platform-product-profile):

1. 選取 `Luma Tutorial Platform` 產品設定檔：

   ![開啟設定檔](assets/adminconsole-newProfileInList.png)

1. 選取 **[!UICONTROL 管理員]** 標籤，然後選取 **[!UICONTROL 新增管理員]** 按鈕：

   ![前往「管理員」標籤，然後選取「新增管理員」](assets/adminconsole-addAdmin.png)

1. 完成工作流程以將教學課程參與者新增為管理員。

完成這些步驟後，您應會看到 `Luma Tutorial Platform` 設定檔由一個管理員設定。
![已建立平台配置檔案](assets/adminconsole-platform-profileCreated.png)

## 設定Experience Platform產品設定檔

現在您是 `Luma Tutorial Platform` 產品設定檔您可以設定完成本教學課程所需的權限和角色。

### 新增權限

現在您會將個別權限項目新增至設定檔：

1. 開啟 `Luma Tutorial Platform` 產品設定檔
1. 選取 **[!UICONTROL 權限]** 標籤
1. 在 **[!UICONTROL 沙箱]**，新增 **[!UICONTROL 生產]** 沙箱至設定檔。 必須能存取 [!DNL Prod] 沙箱，以建立其他沙箱。 在下堂課新增教學課程沙箱後，我們將移除 [!DNL Prod] 產品設定檔中的沙箱。
1. 在 [!UICONTROL 資料擷取]，新增 [!UICONTROL 管理來源] 和 [!UICONTROL 查看源] 權限項目。
1. 為下列項目新增所有權限項目：
   1. [!UICONTROL 資料模型製作]
   1. [!UICONTROL 資料管理]
   1. [!UICONTROL 設定檔管理]
   1. [!UICONTROL Identity Management]
   1. [!UICONTROL 沙箱管理]
   1. [!UICONTROL 查詢服務]
   1. [!UICONTROL 資料收集]
   1. [!UICONTROL 資料控管]
   1. [!UICONTROL 儀表板]
   1. [!UICONTROL 警示]

1. 新增所有權限項目後，請務必選取 **[!UICONTROL 儲存]** 按鈕

### 將自己新增為使用者

此時，如果 `Luma Tutorial Platform` 是你 *僅限* Experience Platform產品設定檔，您仍無法登入Experience Platform的使用者介面。 要做到這一點，你必須成為 *使用者* 在產品設定檔中。 幸運的是，既然你是 *管理員* 產品設定檔中，您可以將自己新增為 *使用者*!

1. 前往 **[!UICONTROL 使用者]** 標籤
1. 選取 **[!UICONTROL 添加用戶]** 按鈕
   ![選擇添加用戶](assets/adminconsole-addUser.png)
1. 完成工作流程，將您自己新增為產品設定檔的使用者

### 將自己新增為開發人員

若要使用Platform API，請將自己新增為開發人員：

1. 前往 **[!UICONTROL 開發人員]** 標籤
1. 選取 **[!UICONTROL 新增開發人員]** 按鈕
   ![選擇添加用戶](assets/adminconsole-addDeveloper.png)
1. 完成工作流程，將自己新增為產品設定檔的開發人員

## 建立資料收集產品設定檔（需要系統管理員或產品管理員）

在本練習中，您或您公司的系統管理員將建立資料收集的產品設定檔(舊稱Adobe Experience Platform Launch)，並將您新增為產品設定檔管理員。

>[!NOTE]
>
>如果您是系統管理員，協助同事處理本教學課程，請考慮將他們新增為 *產品管理員* （用於資料收集）。 身為產品管理員，他們將能自行完成這些步驟，並在未來管理資料收集的其他使用者。

若要建立產品設定檔：

1. 在 [!DNL Adobe Admin Console] 前往Adobe Experience Platform資料收集產品
1. 新增名為的新設定檔 `Luma Tutorial Data Collection` （如果貴公司有多人參加本教學課程，請將教學課程參與者的名稱新增至結尾）
1. 關閉 **[!UICONTROL 屬性]** > **[!UICONTROL 自動包含]** 設定
1. 此時不指派任何屬性或權限
1. 將教學課程參與者新增為此設定檔的管理員

完成這些步驟後，您應會看到 `Luma Tutorial Data Collection` 設定檔由一個管理員設定。
![已建立資料收集設定檔](assets/adminconsole-dc-profileCreated.png)

## 設定資料收集產品設定檔

現在您是 `Luma Tutorial Data Collection` 產品設定檔您可以設定完成本教學課程所需的權限和角色。

### 新增權限

現在您會將個別權限項目新增至設定檔：

1. 在 [Adobe Admin Console](https://adminconsole.adobe.com)，前往 **[!UICONTROL 產品]** > **[!UICONTROL 資料收集]**
1. 開啟 `Luma Tutorial Data Collection` 設定檔
1. 前往 **[!UICONTROL 權限]** 標籤
1. 開啟 **[!UICONTROL 平台]**
1. 請確定已選取所有可用平台（您可能會根據您的授權看到不同的選項）
1. **[!UICONTROL 儲存]** 任何變更
   ![新增平台](assets/adminconsole-launch-addPlatforms.png)
1. 開啟 **[!UICONTROL 屬性]**
1. 請確定 **[!UICONTROL 自動包含]** 將切換為「關閉」，以便您沒有任何屬性的存取權（稍後將新增）
1. **[!UICONTROL 儲存]** 任何變更
   ![移除屬性](assets/adminconsole-launch-removeProperties.png)
1. 開啟 **[!UICONTROL 屬性權利]**
1. 選擇 **[!UICONTROL 全部新增]** 新增所有屬性權限的方式
1. **[!UICONTROL 儲存]**
   ![移除屬性](assets/adminconsole-launch-addPropertyRights.png)
1. 開啟 **[!UICONTROL 公司權利]**
1. 新增 **[!UICONTROL 管理屬性]**
1. 選擇 **[!UICONTROL 儲存]**

   ![移除屬性](assets/adminconsole-launch-companyRights.png)


### 將自己新增為使用者

現在，將您自己新增為資料收集設定檔的使用者：

1. 前往 **[!UICONTROL 使用者]** 標籤
1. 選取 **[!UICONTROL 添加用戶]** 按鈕
   ![選擇添加用戶](assets/adminconsole-launch-addUser.png)
1. 完成工作流程，將您自己新增為產品設定檔的使用者

您不需要將自己新增為資料收集的開發人員。

現在您幾乎擁有完成本教學課程所需的所有權限！ 只有另外兩個調整 [!DNL Adobe Admin Console]，包括您之後的 [建立沙箱](create-a-sandbox.md)!
