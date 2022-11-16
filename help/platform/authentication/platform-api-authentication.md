---
title: 驗證及存取 Experience Platform API
description: 了解如何存取 Adobe Experience Platform API。
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 10%

---

# 驗證和存取 [!DNL Experience Platform] API

若要呼叫Adobe Experience Platform API，您必須先取得Experience Platform開發人員帳戶的存取權。

如需說明如何取得開發人員帳戶存取權的逐步指示，請造訪 [Experience PlatformAPI驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en).

## 建立Experience PlatformAPI並匯出至Postman

[Postman](https://www.getpostman.com/) 是一種工具，可讓開發人員快速輕鬆地與Adobe Experience Platform API互動。

Adobe Developer Console **Postman的匯出詳細資料** 功能可讓您輕鬆將存取及與單一Postman環境檔案中的Experience PlatformAPI互動所需的所有帳戶詳細資訊，移除將值從Adobe Developer Console複製及貼到Postman的需求。

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

## 使用Postman產生存取權杖

使用 [AdobeIdentity Management服務API](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) 取得存取權杖，以存取非生產用途的Adobe Experience Platform API

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

>[!WARNING]
>
> 如Adobe I/O存取權杖產生Postman集合中所述，表示的產生方法適用於非生產用途。 本機簽署會從第三方主機載入JavaScript程式庫，而遠端簽署會將私密金鑰傳送至Adobe擁有且運作的Web服務。 雖然Adobe不會儲存此私密金鑰，但生產金鑰絕不應與任何人共用。

## 使用Postman與Adobe I/OAPI互動

探索如何與Adobe I/OAPI互動，使用 [Adobe提供的Experience PlatformAPI Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)，在 [Adobe I/O環境變數](#export-adobe-io-integration-details-to-postman) 和 [產生存取權杖](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)

請注意，並非每個AdobeAPI都有Adobe I/O提供的Postman集合，不過提供的 [Experience PlatformAPI Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform) 可用來作為指南，說明如何為這些使用案例定義自己的Postman集合。

## 其他資源

* [Adobe I/O主控台](https://console.adobe.io)
* [Adobe Experience Platform Postman範例](https://github.com/adobe/experience-platform-postman-samples)
   * [Adobe I/O存取權杖產生Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [下載Postman](https://www.getpostman.com/)
