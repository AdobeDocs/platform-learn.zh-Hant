---
title: AJO翻譯服務快速入門
description: AJO翻譯服務快速入門
kt: 5342
doc-type: tutorial
exl-id: ee0b8650-a59f-4888-8228-4caafe4143e4
source-git-commit: 3b3c62499bfed86ab13a657a816424879cab4f42
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 2%

---

# 3.2.1翻譯提供者

## 3.2.1.1設定Microsoft Azure Translator

移至[https://portal.azure.com/#home](https://portal.azure.com/#home)。

![翻譯](./images/transl1.png)

在搜尋列中輸入`translators`。 然後，按一下&#x200B;**+建立**。

![翻譯](./images/transl2.png)

選取&#x200B;**建立轉譯器**。

![翻譯](./images/transl3.png)

選擇您的&#x200B;**訂閱識別碼**&#x200B;和&#x200B;**資源群組**。
將**區域**&#x200B;設定為&#x200B;**全域**。
將**訂價層**&#x200B;設定為&#x200B;**免費F0**。

選取&#x200B;**檢閱+建立**。

![翻譯](./images/transl4.png)

選取「**建立**」。

![翻譯](./images/transl5.png)

選取&#x200B;**移至資源**。

![翻譯](./images/transl6.png)

在左側功能表中，移至&#x200B;**資源管理** > **金鑰與端點**。 按一下以複製您的金鑰。

![翻譯](./images/transl7.png)

## 3.2.1.2地區設定字典

移至[https://experience.adobe.com/](https://experience.adobe.com/)。 按一下&#x200B;**Journey Optimizer**。

![翻譯](./images/ajolp1.png)

在左側功能表中，移至&#x200B;**翻譯**，然後移至&#x200B;**地區設定字典**。 如果您看到此訊息，請按一下&#x200B;**新增預設語言環境**。

![翻譯](./images/locale1.png)

您應該會看到此訊息。

![翻譯](./images/locale2.png)

## 3.2.1.3在AJO中設定翻譯提供者

移至[https://experience.adobe.com/](https://experience.adobe.com/)。 按一下&#x200B;**Journey Optimizer**。

![翻譯](./images/ajolp1.png)

在左側功能表中，移至&#x200B;**翻譯**，然後移至&#x200B;**提供者**。 按一下&#x200B;**新增提供者**。

![翻譯](./images/transl8.png)

在&#x200B;**提供者**&#x200B;底下，選取&#x200B;**Microsoft轉譯器**。 勾選核取方塊以啟用翻譯提供者的使用。 貼上您從Microsoft Azure翻譯人員複製的金鑰。 然後，按一下&#x200B;**驗證認證**。

![翻譯](./images/transl9.png)

然後應該會成功驗證您的認證。 如果是，請向下捲動以選取要翻譯的語言。

![翻譯](./images/transl10.png)

請務必選取`[en-US] English`、`[es] Spanish`、`[fr] French`、`[nl] Dutch`。

![翻譯](./images/transl11.png)

向上捲動並按一下&#x200B;**儲存**。

![翻譯](./images/transl12.png)

您的&#x200B;**翻譯提供者**&#x200B;現已準備就緒，可供使用。

![翻譯](./images/transl13.png)

## 3.2.1.4設定翻譯專案

移至[https://experience.adobe.com/](https://experience.adobe.com/)。 按一下&#x200B;**Journey Optimizer**。

![翻譯](./images/ajolp1.png)

在左側功能表中，移至&#x200B;**翻譯**，然後移至&#x200B;**地區設定字典**。 如果您看到此訊息，請按一下[建立專案]。****

![翻譯](./images/ajoprovider1.png)

輸入名稱`--aepUserLdap-- - Translations`，將&#x200B;**Source地區設定**&#x200B;設定為`[en-US] English - United States`，並勾選核取方塊以啟用&#x200B;**自動發佈核准的翻譯**。 接著，按一下&#x200B;**+新增地區設定**。

![翻譯](./images/ajoprovider1a.png)

搜尋`fr`，啟用`[fr] French`的核取方塊，然後啟用&#x200B;**Microsoft Translator**&#x200B;的核取方塊。 按一下&#x200B;**+新增地區設定**。

![翻譯](./images/ajoprovider2.png)

搜尋`es`，啟用`[es] Spanish`的核取方塊，然後啟用&#x200B;**Microsoft Translator**&#x200B;的核取方塊。 按一下&#x200B;**+新增地區設定**。

![翻譯](./images/ajoprovider3.png)

搜尋`nl`，啟用`[nl] Spanish`的核取方塊，然後啟用&#x200B;**Microsoft Translator**&#x200B;的核取方塊。 按一下&#x200B;**+新增地區設定**。

![翻譯](./images/ajoprovider6.png)

按一下&#x200B;**儲存**。

![翻譯](./images/ajoprovider8.png)

您的&#x200B;**翻譯**&#x200B;專案現已準備就緒，可供使用。

![翻譯](./images/ajoprovider9.png)

您已完成此練習。

## 後續步驟

移至[3.2.2建立您的行銷活動](./ex2.md)

返回[模組3.2](./ajotranslationsvcs.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}