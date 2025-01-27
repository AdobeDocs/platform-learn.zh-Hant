---
title: 前期工作
description: 前期工作
doc-type: multipage-overview
source-git-commit: 7b76e7714d2a390d84393ce21a19063b56508ac1
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# PostBuster

>[!IMPORTANT]
>
>以下指示僅適用於Adobe員工。

## 安裝PostBuster

移至[https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542)。

按一下以下載&#x200B;**PostBuster**&#x200B;的最新版本。

![PostBuster](./assets/images/pb1.png)

下載作業系統的正確版本。

![PostBuster](./assets/images/pb2.png)

下載完成並安裝後，請開啟PostBuster。 您應該會看到此訊息。 按一下&#x200B;**匯入**。

![PostBuster](./assets/images/pb3.png)

下載[postbuster.json.zip](./assets/postman/postbuster.json.zip)並在您的案頭上解壓縮。

![PostBuster](./assets/images/pbpb.png)

按一下&#x200B;**選擇檔案**。

![PostBuster](./assets/images/pb4.png)

選取檔案&#x200B;**postbuster.json**。 按一下&#x200B;**「開啟」**。

![PostBuster](./assets/images/pb5.png)

您應該會看到此訊息。 按一下&#x200B;**掃描**。

![PostBuster](./assets/images/pb6.png)

按一下&#x200B;**匯入**。

![PostBuster](./assets/images/pb7.png)

您應該會看到此訊息。 按一下以開啟匯入的集合。

![PostBuster](./assets/images/pb8.png)

現在您可以看到您的集合。 您仍需要設定環境以保留一些環境變數。

![PostBuster](./assets/images/pb9.png)

按一下「**基本環境**」，然後按一下「**編輯**」圖示。

![PostBuster](./assets/images/pb10.png)

您應該會看到此訊息。

![PostBuster](./assets/images/pb11.png)

複製下列環境預留位置，並將其貼到&#x200B;**基本環境**&#x200B;中。

```json
{
	"CLIENT_SECRET": "",
	"API_KEY": "",
	"ACCESS_TOKEN": "",
	"SCOPES": [
		"openid",
		"AdobeID",
		"ff_apis",
		"firefly_api"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"AZURE_STORAGE_URL": "",
	"AZURE_STORAGE_CONTAINER": "",
	"AZURE_STORAGE_SAS_READ": "",
	"AZURE_STORAGE_SAS_WRITE": ""
}
```

然後您應該擁有此專案。

![PostBuster](./assets/images/pb12.png)

完成&#x200B;**Firefly服務**&#x200B;模組之後，您的環境應該如下所示。 您現在不需要執行此動作，我們將在稍後階段解決此問題。

![PostBuster](./assets/images/pb13.png)

>[!NOTE]
>
>![技術內部人士](./assets/images/techinsiders.png){width="50px" align="left"}
>
>如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。

[返回所有模組](./overview.md)
