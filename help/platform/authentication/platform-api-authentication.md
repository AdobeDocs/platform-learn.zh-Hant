---
title: 驗證及存取 Experience Platform API
description: 了解如何存取 Adobe Experience Platform API。
feature: API
role: Developer
level: Beginner
jira: KT-3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 10%

---

# 驗證及存取[!DNL Experience Platform] API

瞭解如何開始使用Adobe Experience Platform API。 本教學課程將引導您完成建立驗證憑證並開始發出Experience Platform API請求的過程。

## 在Adobe Developer Console中建立專案並匯出Postman環境{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/)是協力廠商應用程式，可協助開發人員快速輕鬆地與Adobe Experience Platform API互動。

[Adobe Developer Console的](https://developer.adobe.com/console/home) **Postman匯出詳細資料**&#x200B;功能可讓您輕鬆匯出存取單一Postman環境檔案中的Experience Platform API及與其互動所需的帳戶詳細資料，如此一來，您就不需要從Adobe Developer Console複製並貼上值至Postman。

>[!IMPORTANT]
>
>若要存取[Adobe Developer Console](https://developer.adobe.com/console/home)，您必須是[Adobe Admin Console](https://adminconsole.adobe.com)中的[系統管理員](https://helpx.adobe.com/tw/enterprise/using/admin-roles.html)或[開發人員](https://helpx.adobe.com/tw/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.)。
>
> 建立API認證後，系統管理員必須將該認證與Experience Platform中的角色建立關聯。

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&enablevpops)

## 使用Postman產生存取Token{#generate-an-access-token-with-postman}

使用[Adobe Identity Management Service API](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)取得存取Token，以存取Adobe Experience Platform API。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on&enablevpops)


## 使用Postman與Experience Platform API互動

探索使用[Adobe提供的Adobe Experience Platform API Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)，以[Adobe Developer Console環境變數](#export-integration-details-to-postman)和[產生的存取權杖](#generate-an-access-token-with-postman)為基礎，與Experience Platform API互動。

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on&enablevpops)


## 這些影片中參考的資源

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Adobe Experience Platform Postman範例](https://github.com/adobe/experience-platform-postman-samples)
   * 用於產生存取權杖的[Identity Management System Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [下載Postman](https://www.postman.com/)
