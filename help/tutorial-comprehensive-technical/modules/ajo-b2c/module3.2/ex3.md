---
title: Adobe Journey Optimizer — 外部氣象API、SMS動作等 — 定義自訂動作
description: Adobe Journey Optimizer — 外部氣象API、SMS動作等 — 定義自訂動作
kt: 5342
doc-type: tutorial
exl-id: d9bdc4c6-7539-4646-9b75-f397b792479f
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 3%

---

# 3.2.3定義自訂動作

在本練習中，您將建立自訂動作以傳送訊息至Slack頻道。

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。 然後您就會進入沙箱`--aepSandboxName--`的&#x200B;**首頁**&#x200B;檢視。

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

您現在將使用現有的Slack頻道，並傳送訊息至該Slack頻道。 Slack有一個簡單易用的API，您將使用Adobe Journey Optimizer來觸發其API。

![示範](./images/slack.png)

在左側功能表中，向下捲動並按一下&#x200B;**組態**。 接著，按一下&#x200B;**動作**&#x200B;下的&#x200B;**管理**&#x200B;按鈕。

![示範](./images/menuactions.png)

然後您會看到&#x200B;**動作**&#x200B;清單。 按一下&#x200B;**建立動作**。

![示範](./images/acthome.png)

您會看到空白的「動作」快顯視窗。

![示範](./images/emptyact.png)

作為動作的名稱，請使用`--aepUserLdap--TextSlack`。

設定描述為： `Send Message to Slack`。

對於&#x200B;**URL組態**，請使用這個：

- URL： `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- 方法： **POST**

>[!NOTE]
>
>上述URL會參考AWS Lambda函式，該函式隨後會將您的請求轉送至上述Slack頻道。 這麼做是為了保護Adobe擁有的Slack頻道的存取權。 如果您有自己的Slack頻道，您應該透過[https://api.slack.com/](https://api.slack.com/)建立Slack應用程式，然後您必須在該Slack應用程式中建立內送Webhook，然後將上述URL取代為內送Webhook URL。

![示範](./images/slackname.png)

您不需要變更標題欄位。

![示範](./images/slackurl.png)

**驗證**&#x200B;應該設定為&#x200B;**無驗證**。

![示範](./images/slackauth.png)

在&#x200B;**承載**&#x200B;之下，您需要定義哪些欄位應該傳送給Slack。 邏輯上，您想要Adobe Journey Optimizer和Adobe Experience Platform成為個人化的大腦，所以要傳送給Slack的文字應該由Adobe Journey Optimizer定義，然後傳送給Slack執行。

若為&#x200B;**要求**，請按一下&#x200B;**編輯裝載**&#x200B;圖示。

![示範](./images/slackmsgp.png)

然後您會看到一個空白的快顯視窗。

![示範](./images/slackmsgpopup.png)

複製下列文字並貼到空白的彈出式視窗中。

```json
{
 "text": {
  "toBeMapped": true,
  "dataType": "string",
  "label": "textToSlack"
 }
}
```

然後您會看到以下內容：

![示範](./images/slackmsgpopup1.png)

向上捲動並再按一次&#x200B;**儲存**&#x200B;以儲存您的動作。

![示範](./images/slackmsgpopup3.png)

您的自訂動作現在是&#x200B;**動作**&#x200B;清單的一部分。

![示範](./images/slackdone.png)

您已定義事件、外部資料來源和動作。 現在，讓我們將所有這些整合到一個歷程中。

下一步： [3.2.4建立您的歷程與訊息](./ex4.md)

[返回模組3.2](journey-orchestration-external-weather-api-sms.md)

[返回所有模組](../../../overview.md)
