---
title: 驗證及存取 Experience Platform API
description: 了解如何存取 Adobe Experience Platform API。
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 60f509ef55ce121f572466a8f13953dba982a0ce
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 15%

---

# 驗證和存取 [!DNL Experience Platform] API

若要向Adobe Experience Platform API提出請求，您必須擁有Experience Platform開發人員帳戶。

## 在Adobe Developer主控台中建立專案並匯出Postman環境

[[!DNL Postman]](https://www.postman.com/) 是可讓開發人員快速輕鬆地與Adobe Experience Platform API互動的工具。

Adobe Developer Console的 **Postman的匯出詳細資料** 功能可讓您輕鬆地匯出存取單一Postman環境檔案中的Experience PlatformAPI及與之互動所需的所有帳戶詳細資訊，免除將值從Adobe Developer主控台複製並貼到Postman的需求。

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

>[!IMPORTANT]
>
>建立API認證後，您公司的系統管理員必須將認證與Experience Platform角色相關聯。


## 使用Postman產生存取Token

使用 [AdobeIdentity Management服務API](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) 以取得存取Token來存取Adobe Experience Platform API。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## 使用Postman與Experience Platform API互動

探索使用與Adobe Experience Platform API互動 [Adobe提供的Experience PlatformAPI Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)，建立在 [Adobe Developer主控台環境變數](#export-adobe-io-integration-details-to-postman) 和 [產生的存取權杖](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## 其他資源

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Adobe Experience Platform Postman範例](https://github.com/adobe/experience-platform-postman-samples)
   * [用於產生存取權杖的Identity Management System Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [下載Postman](https://www.postman.com/)
