---
title: 設定許可權
seo-title: Configure permissions | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 設定許可權
description: 在本課程中，您將使用Adobe的Admin Console設定Adobe Experience Platform使用者許可權。
role: Data Architect, Data Engineer
feature: Access Control
jira: KT-4348
thumbnail: 4348-configure-permissions.jpg
exl-id: ca01f99e-f10c-4bf0-bef2-b011ac29a565
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 1%

---

# 設定許可權

<!--30min-->

在本課程中，您將使用Platform介面中的[!DNL Adobe's Admin Console]和[!UICONTROL 許可權]畫面來設定Adobe Experience Platform使用者許可權。

存取控制是Experience Platform中的一項關鍵隱私權功能，我們建議將許可權限制在人員執行其工作職能所需的最低許可權。 如需詳細資訊，請參閱[存取控制檔案](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=zh-Hant)。

資料架構師和資料工程師是Adobe Experience Platform的超級使用者，您需要許多許可權才能完成本教學課程以及日後的工作。 資料架構師可能會參與公司中&#x200B;*其他Platform使用者*&#x200B;的管理工作，例如行銷人員、分析人員和資料科學家。 完成本課程後，請思考如何使用這些功能管理公司的其他使用者。

**資料架構師**&#x200B;經常在本教學課程之外設定其他使用者的許可權。

>[!IMPORTANT]
>
>Adobe Experience Cloud產品的系統管理員必須完成本課程中的部分步驟，這會在區段標題中說明。 如果您不是系統管理員，請洽詢您公司的管理員，要求他們完成這些工作。 在[設定Developer Console和Postman](set-up-developer-console-and-postman.md)課程期間，他們還需要完成一項工作。

## 關於Admin Console

[!DNL Admin Console]是用來管理所有Adobe Experience Cloud產品之使用者存取權的介面。 若要存取Platform，必須將使用者或新增到Admin Console中，然後在Adobe Experience Platform的「許可權」畫面中管理其所有精細的許可權專案。


以下是Platform現有的角色快速摘要：

* 產品設定檔的&#x200B;**使用者**&#x200B;可以根據產品設定檔中指派的許可權，在Platform使用者介面中完成工作。
* **開發人員**&#x200B;可以在Adobe Developer Console中建立API認證和專案，以便開始使用Experience PlatformAPI
* **產品管理員**&#x200B;可以在Adobe Admin Console中將使用者和開發人員新增到Adobe Experience Platform產品，並在Platform介面的「許可權」畫面中管理精細的使用者存取。
* **系統管理員**&#x200B;可以新增產品管理員，並管理所有Adobe Experience Cloud產品的基本任何許可權。

## 將使用者和開發人員新增到`AEP-Default-All-Users`產品設定檔（需要系統管理員或產品管理員）

在本練習中，您或系統管理員或產品管理員會將您新增為Adobe Admin Console Adobe Experience Platform產品中的使用者和開發人員。

>[!NOTE]
>
>如果您是協助同事參加本教學課程的系統管理員，請考慮將您的同事新增為Adobe Experience Platform的&#x200B;*產品管理員*。 作為產品管理員，他們將來能夠自行完成這些步驟並管理其他Experience Platform使用者。

若要將教學課程參與者新增為[!UICONTROL 使用者]和[!UICONTROL 開發人員]：

1. 登入[Adobe Admin Console](https://adminconsole.adobe.com)
1. 在頂端導覽中選取&#x200B;**[!UICONTROL 產品]**
1. 選取&#x200B;**Adobe Experience Platform**
   ![選取Adobe Experience Platform](assets/adminconsole-experiencePlatform.png)
1. 您的Experience Platform執行個體中可能已經有多個設定檔。 選取`AEP-Default-All-Users`設定檔
   ![選取新增設定檔](assets/adminconsole-newProfile.png)

1. 前往&#x200B;**[!UICONTROL 使用者]**&#x200B;標籤
1. 選取&#x200B;**[!UICONTROL 新增使用者]**&#x200B;按鈕
   ![選取新增使用者](assets/adminconsole-addUser.png)
1. 完成工作流程，將教學課程參與者作為使用者新增至產品設定檔

1. 移至&#x200B;**[!UICONTROL 開發人員]**&#x200B;標籤
1. 選取&#x200B;**[!UICONTROL 新增開發人員]**&#x200B;按鈕
   ![選取新增使用者](assets/adminconsole-addDeveloper.png)
1. 完成工作流程，將教學課程參與者作為開發人員新增至產品設定檔


## 在Adobe Experience Platform中新增角色（需要系統管理員或產品管理員）

Experience Platform的精細許可權是在Platform介面的許可權畫面中進行管理。 只有系統和產品管理員才能存取此畫面，因此如果您沒有管理員許可權，便需要具備該許可權的人員協助。

許可權在角色中進行管理。 建立教學課程的角色：

1. 登入[Adobe Experience Platform](https://platform.adobe.com)
1. 在左側導覽中選取「**[!UICONTROL 許可權]**」，系統會將您帶至「[!UICONTROL 角色]」畫面
1. 選取&#x200B;**[!UICONTROL 建立角色]**

   ![在Experience Platform](assets/permissions-addRole.png)中建立角色
1. 為角色命名`Luma Tutorial Platform` （如果您公司的多個人員正在參加此教學課程，請將教學課程參與者的名稱加入至結尾）並選取&#x200B;**[!UICONTROL 確認]**

   ![在Experience Platform](assets/permissions-nameRole.png)中建立角色


1. 使用&#x200B;**[!UICONTROL +]**&#x200B;和&#x200B;**[!UICONTROL 全部新增]**，為下列資源新增所有許可權專案：

   1. 資料模型製作
   1. 資料管理
   1. 設定檔管理
   1. Identity Management
   1. 沙箱管理
   1. 查詢服務
   1. 資料收集
   1. 資料治理
   1. 儀表板
   1. 警報

      ![新增許可權專案](assets/permissions-addPermissionItems.png)

1. 在「資料擷取」下方，新增「管理來源」和「檢視來源」許可權專案。

1. 新增所有許可權專案後，請務必選取儲存按鈕
   ![儲存許可權專案](assets/permissions-savePermissions.png)

在[建立沙箱](create-a-sandbox.md)和[設定Developer Console和Postman](set-up-developer-console-and-postman.md)課程之後，您將對此角色進行一些小的更新。

## 建立資料收集產品設定檔（需要系統管理員或產品管理員）

在本練習中，您或您公司的系統管理員將會為資料收集(先前稱為Adobe Experience Platform Launch)建立產品設定檔，並將您新增為產品設定檔管理員。

>[!NOTE]
>
>如果您是協助同事完成本教學課程的系統管理員，請考慮將他們新增為資料收集的&#x200B;*產品管理員*。 作為產品管理員，他們未來能夠自行完成這些步驟並管理資料收集的其他使用者。

若要建立產品設定檔：

1. 在[!DNL Adobe Admin Console]中，前往Adobe Experience Platform資料收集產品
1. 新增名為`Luma Tutorial Data Collection`的設定檔（如果貴公司的多個人員正在參加此教學課程，請將教學課程參與者的名稱新增至結尾）
1. 關閉&#x200B;**[!UICONTROL 屬性]** > **[!UICONTROL 自動包含]**&#x200B;設定
1. 此時不要指派任何屬性或許可權
1. 將教學課程參與者新增為此設定檔的管理員

完成這些步驟後，您應該會看到`Luma Tutorial Data Collection`設定檔已設定為一位管理員。
![已建立資料彙集設定檔](assets/adminconsole-dc-profileCreated.png)

## 設定資料收集產品設定檔

現在您已經是`Luma Tutorial Data Collection`產品設定檔的管理員，您可以設定完成本教學課程所需的許可權和角色。

### 新增許可權

現在您要將個別許可權專案新增至設定檔：

1. 在[Adobe Admin Console](https://adminconsole.adobe.com)中，移至&#x200B;**[!UICONTROL 產品]** > **[!UICONTROL 資料彙集]**
1. 開啟`Luma Tutorial Data Collection`設定檔
1. 前往&#x200B;**[!UICONTROL 許可權]**&#x200B;標籤
1. 開啟&#x200B;**[!UICONTROL 平台]**
1. 請確定已選取所有可用的平台（根據您的授權，您可能會看到不同的選項）
1. **[!UICONTROL 儲存]**&#x200B;任何變更
   ![新增平台](assets/adminconsole-launch-addPlatforms.png)
1. 開啟&#x200B;**[!UICONTROL 屬性]**
1. 請確定&#x200B;**[!UICONTROL 自動包含]**&#x200B;切換為關閉，如此您便無法存取任何屬性（我們將在稍後新增）
1. **[!UICONTROL 儲存]**&#x200B;任何變更
   ![移除屬性](assets/adminconsole-launch-removeProperties.png)
1. 開啟&#x200B;**[!UICONTROL 屬性權利]**
1. 選取&#x200B;**[!UICONTROL 全部新增]**&#x200B;以新增所有屬性許可權
1. **[!UICONTROL 儲存]**
   ![移除屬性](assets/adminconsole-launch-addPropertyRights.png)
1. 開啟&#x200B;**[!UICONTROL 公司權利]**
1. 新增&#x200B;**[!UICONTROL 管理屬性]**
1. 選取&#x200B;**[!UICONTROL 儲存]**
   ![移除屬性](assets/adminconsole-launch-companyRights.png)


### 將您新增為使用者

現在將您新增為資料收集設定檔的使用者：

1. 前往&#x200B;**[!UICONTROL 使用者]**&#x200B;標籤
1. 選取&#x200B;**[!UICONTROL 新增使用者]**&#x200B;按鈕
   ![選取新增使用者](assets/adminconsole-launch-addUser.png)
1. 完成工作流程，將自己新增為產品設定檔的使用者

您不需要將自己新增為資料收集的開發人員。

現在您幾乎擁有完成本教學課程所需的所有許可權！ 您將在[!DNL Adobe Admin Console]內再進行兩次調整，包括在[建立沙箱](create-a-sandbox.md)後進行一次！
