---
title: 在Slack中監視事件
description: 瞭解如何透過與Experience Platform App Builder webhook Proxy整合在Slack中接收Adobe通知。
feature: Monitoring
role: Developer, Admin
level: Intermediate
duration: 519
last-substantial-update: 2026-02-24T00:00:00Z
jira: KT-20339
exl-id: 6d4a072c-9eef-4a38-9459-9e1cbd66bfb5
source-git-commit: 4ec7a800ef963f9b1257e2f246428abff32e9b94
workflow-type: tm+mt
source-wordcount: '1539'
ht-degree: 0%

---

# 監視Slack中的Experience Platform事件

瞭解如何透過與Experience Platform App Builder webhook Proxy整合在Slack中接收Adobe通知。 資料工程師和管理員可能會想要在Slack中收到來自Adobe Experience Platform的主動通知，以監控其Platform實施的健康狀況。 本教學課程概述使用Adobe App Builder將Adobe I/O Events連線至Slack的架構和實施步驟。


>[!VIDEO](https://video.tv.adobe.com/v/3480183?learn=on)

## 為何要使用webhook Proxy？

無法將Adobe I/O Events直接連線到Slack傳入Webhook，因為驗證程式中的通訊協定不相符。

* **挑戰**：當您使用Adobe I/O Events註冊webhook時，Adobe會傳送「挑戰」請求（`GET`或`POST`）到您的端點。 您的端點必須成功處理此挑戰，並傳回特定值以確認所有權。

* **限制**： Slack的傳入Webhook僅設計用來擷取JSON裝載以進行傳訊。 他們無法辨識或回應Adobe的驗證挑戰握手的邏輯。

* **解決方案**：使用Adobe App Builder部署中介webhook Proxy。 此Proxy位於Adobe和Slack之間，用於：
   1. 截獲來自Adobe的請求並回應驗證挑戰。
   1. 將裝載格式化為與Slack相容的訊息，並將其轉送至Slack。

* **傳遞方法**：執行階段動作。  執行階段動作會與Adobe App Builder一起封裝。 使用執行階段動作（非Web動作）做為事件處理常式時，Adobe I/O Events會自動處理簽章驗證和質詢回應。 建議使用執行階段動作，因為此方法需要較少的程式碼並提供內建安全性。

## 架構概覽

### 什麼是Adobe Developer Console？

Adobe Developer Console是管理Adobe專案、API和憑證的中央入口網站。 您可以在此處建立專案、設定驗證並註冊Webhook。

### 什麼是App Builder？

Adobe App Builder是一個完整的架構，可讓企業開發人員建置雲端原生應用程式。

* **布建**：預設不會啟用App Builder；必須作為功能為您的組織布建。 確定貴組織擁有&#x200B;**[!DNL App Builder]**&#x200B;權益。

* **專案範本**： App Builder專案是特別使用&#x200B;**[!UICONTROL 中的]** App Builder[!DNL Developer Console]範本所建立(來自範本[!UICONTROL &#x200B; > &#x200B;]App Builder[!UICONTROL 的]專案)。 範本會自動設定必要的工作區和執行階段環境。

* **App Builder快速入門手冊**：請參閱檔案[，以布建範本並建立您的第一個專案](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app){target=_blank}。

### 什麼是Adobe I/O Runtime？

Adobe I/O Runtime是支援App Builder的無伺服器平台。 它可讓開發人員部署程式碼(Functions-as-a-Service)，以便在回應HTTP請求時執行，而不需要管理伺服器基礎結構。

在此實作中，我們使用&#x200B;**動作**。 動作是無狀態函式（以Node.js撰寫），會在Adobe I/O Runtime上執行。 我們的動作可作為Adobe I/O Events交談的公用HTTP端點。

如需詳細資訊，請參閱[Adobe I/O Runtime檔案](https://developer.adobe.com/runtime/){target=_blank}。

## 實作指南

### 先決條件

開始之前，請確定您具備下列條件：

* **Adobe Developer Console存取權**：您必須有權存取已啟用App Builder之組織中的系統管理員或[開發人員角色](../admin/add-developers.md)。

  >[!TIP]
  > 若要驗證App Builder布建，請登入[Adobe Developer Console](https://developer.adobe.com/console/){target=_blank}、確定您是屬於所需組織、選取「**[!UICONTROL 從範本建立專案]**」，並驗證App Builder範本是否可用。 如果不是，請檢閱App Builder常見問題集區段&quot;[如何取得App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/faq#how-to-get-app-builder){target=_blank}&quot;


* **Node.js &amp; npm**：此專案需要Node.js，其中包括NPM （節點封裝管理員）。 NPM可用來安裝Adobe CLI及管理專案相依性。

   * [下載Node.js （建議使用LTS版本）](https://nodejs.org/){target=_blank}
   * [npm快速入門手冊](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm){target=_blank} — 如何確認安裝的指南。

* **`aio CLI`**：已透過您的終端機安裝： `npm install -g @adobe/aio-cli`
* **Slack應用程式設定**：您需要在工作區中設定Slack應用程式，並啟動&#x200B;**傳入的Webhook**。

   * [建立Slack應用程式](https://api.slack.com/apps){target=_blank}
   * [Slack傳入Webhook指南](https://docs.slack.dev/messaging/sending-messages-using-incoming-webhooks/){target=_blank} — 遵循此指南，建立您的應用程式並產生Webhook URL （以`https://hooks.slack.com/`開頭……）。

### 步驟1：在Adobe Developer Console中建立專案

首先，在Adobe Developer Console中使用App Builder範本建立專案：

1. 登入[Adobe Developer Console](https://developer.adobe.com/console)
1. 選取&#x200B;**[!UICONTROL 從範本建立專案]**
1. 選取App Builder範本
1. 輸入專案標題，例如`Slack webhook integration`
1. 選取&#x200B;**[!UICONTROL 儲存]**

### 初始化執行階段環境

在終端機中執行以下命令以建立專案結構：

#### 登入`aio`

```
aio login
```

#### 步驟2：初始化新的App Builder專案

```
aio app init slack-webhook-proxy
```

1. 選取您的組織並按&#x200B;**Enter**
1. 選取您在上一步建立的專案（例如，`Slack webhook integration`），然後按&#x200B;**Enter**
1. 選取&#x200B;**[!UICONTROL 僅我的組織支援的範本]**&#x200B;選項
1. 按&#x200B;**Enter**&#x200B;跳過範例區段
1. 出現提示時，請確定已選取下列元件（應填入圓形），然後按&#x200B;**Enter**：
   1. **[!UICONTROL 動作：部署執行階段動作]**
   1. **[!UICONTROL 事件：發佈至Adobe I/O Events]**
   1. **[!UICONTROL 網頁Assets：部署至裝載的靜態資產]**
1. 使用您的「向上」和「向下」箭頭，瀏覽傳入清單並選擇&#x200B;**[!UICONTROL Adobe Experience Platform：即時客戶個人檔案]**&#x200B;並按&#x200B;**Enter**
1. **[!UICONTROL 一般]**&#x200B;動作會自動產生
1. 為UI選擇&#x200B;**[!UICONTROL 純HTML/JS]**，然後按&#x200B;**Enter**
1. 保留&#x200B;**[!UICONTROL 一般]**&#x200B;作為範例動作，以展示如何存取外部API名稱，並按&#x200B;**Enter**
1. 保留&#x200B;**[!UICONTROL publish-events]**&#x200B;作為範例動作名稱，以使用雲端事件格式建立訊息，然後按&#x200B;**Enter**

應用程式初始化應完成。

#### 導覽至專案目錄

```
cd slack-webhook-proxy
```

#### 新增網頁動作

```
aio app add action
```

1. 選擇&#x200B;**[!UICONTROL 僅我的組織支援的範本]**，然後按&#x200B;**Enter**
2. 在呈現的表格中檢視&#x200B;**[!UICONTROL publish-events]**&#x200B;動作；按下&#x200B;**空格**&#x200B;以選取動作。 如果名稱旁邊的圓圈已填滿，如影片教學課程中所示，請按&#x200B;**Enter**
3. 命名動作`webhook-proxy`

### 步驟3：更新Proxy動作代碼

在IDE或文字編輯器中，使用下列程式碼建立/修改檔案`actions/webhook-proxy/index.js`。 此實作會將事件轉送至Slack。 使用執行階段動作註冊時，會自動進行簽章驗證和挑戰處理。

```javascript
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
 
/**
 * Adobe I/O Events to Slack Runtime Proxy
 *
 * Receives events from Adobe I/O Events and forwards them to Slack.
 * Signature verification and challenge handling are automatic when
 * using Runtime Action registration (non-web action).
 */
async function main(params) {
  const logger = Core.Logger("webhook-proxy", { level: params.LOG_LEVEL || "info" });
 
  try {
    logger.info(`Event received: ${JSON.stringify(params)}`);
 
    // Forward to Slack
    return forwardToSlack(params, params.SLACK_WEBHOOK_URL, logger);
 
  } catch (error) {
    logger.error(`Error: ${error.message}`);
    return { statusCode: 500, body: { error: "Internal server error" } };
  }
}
 
/**
 * Forwards the event payload to Slack
 */
async function forwardToSlack(payload, webhookUrl, logger) {
  if (!webhookUrl) {
    logger.error("SLACK_WEBHOOK_URL not configured");
    return { statusCode: 500, body: { error: "Server configuration error" } };
  }
 
  // Extract Adobe headers passed to runtime action
  const headers = {
    "x-adobe-event-code": payload["x-adobe-event-code"],
    "x-adobe-event-id": payload["x-adobe-event-id"],
    "x-adobe-provider": payload["x-adobe-provider"]
  };
 
  const slackMessage = buildSlackMessage(payload, headers);
 
  const response = await fetch(webhookUrl, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(slackMessage)
  });
 
  if (!response.ok) {
    const errorText = await response.text();
    logger.error(`Slack API error: ${response.status} - ${errorText}`);
    return { statusCode: response.status, body: { error: errorText } };
  }
 
  logger.info("Event forwarded to Slack");
  return { statusCode: 200, body: { success: true } };
}
 
/**
 * Builds a Slack Block Kit message from the event payload
 */
function buildSlackMessage(payload, headers) {
  // Adobe passes event code as x-adobe-event-code header (available in params for runtime actions)
  const eventType = headers["x-adobe-event-code"] ||
                    payload["x-adobe-event-code"] ||
                    payload.event_code ||
                    payload.type ||
                    payload.event_type ||
                    "Adobe Event";
  const eventId = headers["x-adobe-event-id"] || payload["x-adobe-event-id"] || payload.event_id || payload.id || "N/A";
  const eventData = payload.data || payload.event || payload;
 
  return {
    blocks: [
      {
        type: "header",
        text: { type: "plain_text", text: `Event: ${eventType}`, emoji: true }
      },
      {
        type: "section",
        fields: formatDataFields(eventData)
      },
      { type: "divider" },
      {
        type: "context",
        elements: [{
          type: "mrkdwn",
          text: `*Event ID:* ${eventId}  |  *Time:* ${new Date().toISOString()}`
        }]
      }
    ]
  };
}
 
/**
 * Formats event data as Slack mrkdwn fields
 */
function formatDataFields(data, maxFields = 10) {
  if (typeof data !== "object" || data === null) {
    return [{ type: "mrkdwn", text: `*Payload:*\n${String(data)}` }];
  }
 
  const entries = Object.entries(data);
  if (entries.length === 0) {
    return [{ type: "mrkdwn", text: "_No data provided_" }];
  }
 
  return entries.slice(0, maxFields).map(([key, value]) => ({
    type: "mrkdwn",
    text: `*${key}:*\n${typeof value === "object" ? `\`\`\`${JSON.stringify(value)}\`\`\`` : value}`
  }));
}
 
exports.main = main;
```

### 步驟4：設定動作

`app.config.yaml`中的動作設定是關鍵的。 使用Web：否，建立可在Developer Console中註冊為「執行階段動作」的非Web動作。

```yaml
application:
  runtimeManifest:
    packages:
      slack-webhook-proxy:
        license: Apache-2.0
        actions:
          webhook-proxy:
            function: actions/webhook-proxy/index.js
            web: no
            runtime: nodejs:22
            inputs:
              LOG_LEVEL: info
              SLACK_WEBHOOK_URL: $SLACK_WEBHOOK_URL
            annotations:
              require-adobe-auth: false
              final: true
```

#### 為什麼`web: no?`

當您使用非Web動作並透過Developer Console中的「執行階段動作」選項註冊時，Adobe I/O Events會自動執行下列動作：

* 處理挑戰驗證（包括`GET`和`POST`）
* 在叫用您的動作之前驗證數位簽章
* 將簽名驗證器動作鏈結在動作前

這表示您的程式碼只需要處理商業邏輯(轉送至Slack)。

### 步驟4：更新環境變數

為了安全地管理認證，我們使用環境變數。 在專案的根目錄中建立/修改`.env`檔案，以新增Slack webhook URL。 如果您沒有看到`.env`檔案，請確定在您的系統上顯示隱藏的檔案：

```
# ... other .env file content ...
 
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### 步驟5：部署動作

設定環境變數後，請部署動作。 在終端機中執行此命令時，請確定位於專案的根目錄中，也就是`slack-webhook-proxy`。

```
aio app deploy
```

您的動作已部署至Adobe I/O Runtime，並可在Developer Console中註冊使用。

### 步驟6：在Adobe Developer Console中註冊動作

現在您的動作已部署，請將其註冊為Adobe事件的目的地。

1. 導覽至[Adobe Developer Console](https://developer.adobe.com/console){target=_blank}並開啟您的App Builder專案。
1. 選擇您的&#x200B;**[!UICONTROL Workspace]**
1. 選取&#x200B;**[!UICONTROL 新增服務]**&#x200B;並選取&#x200B;**[!UICONTROL 事件]**。
1. 選取&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;作為產品。
1. 選取&#x200B;**[!UICONTROL 平台通知]**&#x200B;作為事件型別。
1. 選取您想要在Slack中收到通知的特定事件（或全部），然後選取「**[!UICONTROL 下一步]**」。
1. 選取或[建立您的OAuth認證](https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/api/platform-api-authentication){target=_blank}。
1. 設定&#x200B;**[!UICONTROL 事件註冊詳細資料]**：
   1. **[!UICONTROL 註冊名稱]**：為您的註冊提供描述性名稱。
   1. **[!UICONTROL 註冊說明]**：請確定此說明是明確的，以便其他貢獻者能夠瞭解其作用。
   1. 選取&#x200B;**[!UICONTROL 下一步]**
   1. **[!UICONTROL 傳遞方法]**：選取&#x200B;**[!UICONTROL 執行階段動作]** （不是「Webhook」）。
   1. **[!UICONTROL 執行階段動作]**：從下拉式清單中選擇`webhook-proxy` （如果沒有看到頁面，請重新整理頁面）。
1. 選取&#x200B;**[!UICONTROL 儲存已設定的事件]**。


### 步驟7：使用範例事件進行驗證

您可以按一下任何已設定事件旁的「傳送範例事件」圖示，以端對端測試整個流程。

範例事件會透過您在建立Slack應用程式和建立webhook時設定的頻道傳送；您應會看到類似以下內容：

![Slack中的監視事件範例](../assets/slack-monitor.png)

恭喜，您已成功將Slack與Experience Platform活動整合！

### 常見問題

以下是您在設定Proxy時可能會遇到的一些問題，以及一些解決這些問題的可能方法。

* **無法檢視IMS組織**：如果在執行`aio app init`時沒有看到您的IMS組織清單，請嘗試下列操作。 在您的「終端機」中執行`aio logout`，在您的預設網頁瀏覽器上登出Experience Cloud，然後再次執行`aio login`。
* **動作未出現在下拉式清單中**：請確定`web: no`設定在`app.config.yaml`中。 只有非Web動作會出現在執行階段動作下拉式清單中。 部署後重新整理Developer Console頁面。
* **簽章驗證失敗**：如果您在啟動記錄檔中看到此訊息，表示Adobe的內建驗證器已拒絕要求。 合法Adobe事件不應發生這種情況。 檢查事件註冊是否已正確設定。
* **Slack未接收訊息**：請檢查您的`SLACK_WEBHOOK_URL`檔案中是否已正確設定`.env`，以及Slack應用程式是否已啟用Incoming Webhook。
* **動作逾時**：執行階段動作有60秒的逾時。 如果您的動作需要更長的時間，請考慮改用日誌方法。
