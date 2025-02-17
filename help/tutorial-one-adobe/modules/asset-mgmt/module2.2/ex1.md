---
title: Workfront快速入門
description: Workfront快速入門
kt: 5342
doc-type: tutorial
exl-id: 7ed76d37-5d3e-49c7-b3d3-ebcfe971896d
source-git-commit: dd075b0296c6ba06d72b229145635060c2c6abb1
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# 1.2.1 Workfront快速入門

前往[https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}登入Adobe Workfront。

然後您會看到這個訊息。

![WF](./images/wfb1.png)

## 1.2.1.1設定您的AEM Assets整合

按一下9個點&#x200B;**漢堡**&#x200B;圖示，然後選取&#x200B;**設定**。

![WF](./images/wfb2.png)

在左側功能表中，向下捲動至&#x200B;**檔案**，然後按一下&#x200B;**Experience Manager Assets**。

![WF](./images/wfb3.png)

按一下&#x200B;**+新增Experience Manager整合**。

![WF](./images/wfb4.png)

對於整合的名稱，請使用`--aepUserLdap-- - Citi Signal AEM`。

開啟&#x200B;**Experience Manager存放庫**&#x200B;下拉式清單，然後選取您應命名為`--aepUserLdap-- - Citi Signal`的AEM CS執行個體。

![WF](./images/wfb5.png)

在&#x200B;**中繼資料**&#x200B;下，設定下列對應：

| Workfront欄位 | Experience Manager Assets欄位 |
| --------------- | ------------------------------ | 
| **檔案** > **名稱** | **wm：documentName** |
| **專案** > **描述** | **wm：projectDescription** |
| **任務** > **名稱** | **wm：taskName** |
| **工作** > **描述** | **wm：taskDescription** |

啟用&#x200B;**同步處理物件中繼資料**&#x200B;的開關。

按一下&#x200B;**儲存**。

![WF](./images/wfb6.png)

您從Workfront到AEM Assets CS的整合現已設定完成。

![WF](./images/wfb7.png)

## 1.2.1.2使用AEM Assets設定中繼資料整合

接下來，您需要設定AEM Assets，好讓Workfront中資產的中繼資料欄位能與AEM共用。

若要這麼做，請前往[https://experience.adobe.com/](https://experience.adobe.com/)。 按一下&#x200B;**Experience Manager Assets**。

![WF](./images/wfbaem1.png)

按一下以選取您的AEM Assets環境，應命名為`--aepUserLdap-- - Citi Signal dev`。

![WF](./images/wfbaem2.png)

您應該會看到此訊息。 在左側功能表中，前往&#x200B;**Assets**&#x200B;並按一下&#x200B;**建立資料夾**。

![WF](./images/wfbaem3.png)

為資料夾命名`--aepUserLdap-- - Workfront Assets`並按一下&#x200B;**建立**。

![WF](./images/wfbaem4.png)

接著，前往左側功能表中的&#x200B;**中繼資料Forms**，然後按一下&#x200B;**建立**。

![WF](./images/wfbaem5.png)

使用名稱`--aepUserLdap-- - Metadata Form`並按一下&#x200B;**建立**。

![WF](./images/wfbaem6.png)

新增3個新的&#x200B;**單行文字**&#x200B;欄位至表單，並選取第一個欄位。 然後，按一下&#x200B;**中繼資料屬性**&#x200B;欄位旁的&#x200B;**結構描述**&#x200B;圖示。

![WF](./images/wfbaem7.png)

在搜尋欄位中輸入`wm:project`，然後選取欄位&#x200B;**專案描述**。 按一下&#x200B;**選取**。

![WF](./images/wfbaem8.png)

將欄位標籤變更為&#x200B;**專案描述**。

![WF](./images/wfbaem9.png)

接著，選取第2個&#x200B;**單行文字**&#x200B;欄位，然後再次按一下&#x200B;**中繼資料屬性**&#x200B;欄位旁的&#x200B;**結構描述**&#x200B;圖示。

![WF](./images/wfbaem10b.png)

之後您會再次看到此快顯視窗。 在搜尋欄位中輸入`wm:project`，然後選取欄位&#x200B;**專案識別碼**。 按一下&#x200B;**選取**。

![WF](./images/wfbaem10.png)

將欄位標籤變更為&#x200B;**專案識別碼**。

![WF](./images/wfbaem10a.png)

選取第3個&#x200B;**單行文字**&#x200B;欄位，然後再次按一下&#x200B;**中繼資料屬性**&#x200B;欄位旁的&#x200B;**結構描述**&#x200B;圖示。

![WF](./images/wfbaem11a.png)

之後您會再次看到此快顯視窗。 在搜尋欄位中輸入`wm:project`，然後選取欄位&#x200B;**專案名稱**。 按一下&#x200B;**選取**。

![WF](./images/wfbaem11.png)

將欄位標籤變更為&#x200B;**專案名稱**。 按一下&#x200B;**儲存**。

![WF](./images/wfbaem12.png)

將表單上的&#x200B;**索引標簽名稱**&#x200B;變更為`--aepUserLdap-- - Workfront Metadata`。 按一下&#x200B;**儲存**&#x200B;和&#x200B;**關閉**。

![WF](./images/wfbaem13.png)

您的&#x200B;**中繼資料表單**&#x200B;現已設定。

![WF](./images/wfbaem14.png)

接下來，您需要將中繼資料表單指派給您之前建立的資料夾。 勾選中繼資料表單的核取方塊，然後按一下&#x200B;**指派至資料夾**。

![WF](./images/wfbaem15.png)

選取應命名為`--aepUserLdap-- - Workfront Assets`的資料夾。 按一下&#x200B;**指派**。

![WF](./images/wfbaem16.png)

中繼資料表單現在已成功指派至您的資料夾。

![WF](./images/wfbaem17.png)

## 1.2.1.2設定您的AEM Sites整合

>[!NOTE]
>
>此外掛程式目前處於&#x200B;**搶先存取**&#x200B;模式，尚未普遍可用。
>
>此外掛程式可能已安裝在您使用的Workfront執行個體中。 如果已安裝，您可以檢閱下列指示，但不需要變更設定中的任何專案。

移至[https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor){target="_blank"}。

確定此外掛程式的&#x200B;**切換**&#x200B;設定為&#x200B;**已啟用**。 然後，按一下&#x200B;**齒輪**&#x200B;圖示。

![WF](./images/wfb8.png)

您會看到&#x200B;**擴充功能組態**&#x200B;快顯視窗。 設定下列欄位以使用此外掛程式。

| 索引鍵 | 值 |
| --------------- | ------------------------------ | 
| **`IMS_ENV`** | **PROD** |
| **`WORKFRONT_INSTANCE_URL`** | **https://experienceplatform.my.workfront.com** |
| **`SHOW_CUSTOM_FORMS`** | **&#39;{&quot;previewUrl&quot;： true， &quot;publishUrl&quot;： true}&#39;** |

按一下&#x200B;**儲存**。

![WF](./images/wfb8.png)

返回您的Workfront UI，然後按一下9個點&#x200B;**漢堡**&#x200B;圖示。 選取&#x200B;**安裝程式**。

![WF](./images/wfb9.png)

在左側功能表中，移至&#x200B;**自訂Forms**&#x200B;並選取&#x200B;**表單**。 按一下&#x200B;**+新增自訂表單**。

![WF](./images/wfb10.png)

選取&#x200B;**工作**&#x200B;並按一下&#x200B;**繼續**。

![WF](./images/wfb11.png)

然後您會看到空的自訂表單。 輸入表單名稱`Content Fragment & Integration ID`。

![WF](./images/wfb12.png)

將新的&#x200B;**單行文字**&#x200B;欄位拖放到畫布上。

![WF](./images/wfb13.png)

設定新欄位，如下所示：

- **標籤**： **內容片段**
- **名稱**： **`aem_workfront_integration_content_fragment`**

![WF](./images/wfb14.png)

將新的&#x200B;**單行文字**&#x200B;欄位新增到畫布上，並設定新欄位，如下所示：

- **標籤**： **整合識別碼**
- **名稱**： **`aem_workfront_integration_id`**

按一下&#x200B;**套用**。

![WF](./images/wfb15.png)

您現在需要設定第二個自訂表單。 按一下&#x200B;**+新增自訂表單**。

![WF](./images/wfb10.png)

選取&#x200B;**工作**&#x200B;並按一下&#x200B;**繼續**。

![WF](./images/wfb11.png)

然後您會看到空的自訂表單。 輸入表單名稱`Preview & Publish URL`。

![WF](./images/wfb16.png)

將新的&#x200B;**單行文字**&#x200B;欄位拖放到畫布上。

![WF](./images/wfb17.png)

設定新欄位，如下所示：

- **標籤**： **預覽URL**
- **名稱**： **`aem_workfront_integration_preview_url`**

![WF](./images/wfb18.png)

將新的&#x200B;**單行文字**&#x200B;欄位新增到畫布上，並設定新欄位，如下所示：

- **標籤**： **發佈URL**
- **名稱**： **`aem_workfront_integration_publish_url`**

按一下&#x200B;**套用**。

![WF](./images/wfb19.png)

之後，您應該有2個可用的自訂表格。

![WF](./images/wfb20.png)

下一步： [使用Workfront校訂1.2.2](./ex2.md){target="_blank"}

使用Adobe Workfront](./workfront.md){target="_blank"}返回[工作流程管理

[返回所有模組](./../../../overview.md){target="_blank"}
