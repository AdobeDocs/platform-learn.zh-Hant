---
title: 使用資料收集標籤實作Brand Concierge
description: 使用資料收集標籤實作Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: 3704abb57e9fa64c2ff6d6914b6da8b46a5f44aa
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 3%

---

# 1.4.3使用資料收集標籤實作Brand Concierge

>[!IMPORTANT]
>
>此練習正在進行中，尚未完成。

## 資料收集標籤屬性

Brand Concierge需要將資料傳送至Adobe Experience Platform。 若要這麼做，需要將網頁SDK （或alloy.js）部署至您的網站。

若要這麼做，您現在需要建立資料收集標籤屬性。

移至[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 開啟&#x200B;**資料彙集**。

![Brand Concierge](./images/aep101.png)

按一下&#x200B;**新增屬性**。

![Brand Concierge](./images/aep102.png)

輸入名稱： `--aepUserLdap-- - CitiSignal Website + Brand Concierge`，並輸入您網站的網域。

按一下&#x200B;**儲存**。

![Brand Concierge](./images/aep103.png)

搜尋您的屬性，然後開啟它。

![Brand Concierge](./images/aep104.png)

前往&#x200B;**擴充功能**，然後前往&#x200B;**目錄**。

![Brand Concierge](./images/aep105.png)

搜尋`web sdk`，然後按一下擴充功能&#x200B;**Adobe Experience Platform Web SDK**。 按一下&#x200B;**安裝**。

![Brand Concierge](./images/aep106.png)

您應該會看到此訊息。 您只需在此提供資料流的詳細資料。 若要這麼做，請向下捲動一點。

![Brand Concierge](./images/aep107.png)

針對所有3個環境&#x200B;**生產**、**暫存**&#x200B;和&#x200B;**開發**，請選取下列專案：

- **沙箱**： `--aepUserLdap-- - bc`
- **資料流**： `--aepUserLdap-- - Brand Concierge`

按一下&#x200B;**儲存**。

![Brand Concierge](./images/aep108.png)

您應該會看到此訊息。 移至&#x200B;**規則**。

![Brand Concierge](./images/aep108a.png)

按一下&#x200B;**「建立新規則」**。

![Brand Concierge](./images/aep109.png)

輸入名稱： `Homepage`。 然後，按一下&#x200B;**「事件」**&#x200B;下的&#x200B;**+「新增」**。

![Brand Concierge](./images/aep110.png)

選取下列選項：

- **延伸模組**： **核心**
- **事件型別**： **載入的程式庫（頁面頂端）**

按一下&#x200B;**保留變更**。

![Brand Concierge](./images/aep111.png)

您應該會看到此訊息。 按一下&#x200B;**條件**&#x200B;下的&#x200B;**+新增**。

![Brand Concierge](./images/aep112.png)

選取下列選項：

- **邏輯型別**： **一般**
- **延伸模組**： **核心**
- **條件型別**： **路徑不含查詢字串**
- **路徑等於……**：輸入您的網站網域，在此案例中為`https://vangeluw.adobedemosystem.com/`

按一下&#x200B;**保留變更**。

![Brand Concierge](./images/aep113.png)

您應該會看到此訊息。 按一下&#x200B;**「動作」**&#x200B;下的&#x200B;**+「新增」**。

![Brand Concierge](./images/aep114.png)

選取下列選項：

- **延伸模組**： **核心**
- **動作型別**： **自訂程式碼**
- **語言**： **JavaScript**

按一下&#x200B;**開啟編輯器**。

![Brand Concierge](./images/aep115.png)

貼上下列程式碼：

```javascript
window["alloy"]("sendEvent", {
        conversation: {fetchConversationalExperience: true}
    }).then(result=> {
        console.log("Conversation experience fetched", result);
        window["alloy"]("bootstrapConversationalExperience", {
            selector: "#brand-concierge-mount",
						// src: "main.js",
            src: "https://experience-stage.adobe.net/solutions/experience-platform-brand-concierge-web-agent/static-assets/main.js",
            stylingConfigurations: window.styleConfiguration,
						stickySession: true
        })
    });
```

按一下&#x200B;**儲存**。

![Brand Concierge](./images/aep116.png)

您應該會看到此訊息。 按一下&#x200B;**保留變更**。

![Brand Concierge](./images/aep117.png)

您應該會看到此訊息。 按一下&#x200B;**儲存**。

![Brand Concierge](./images/aep118.png)

移至&#x200B;**發佈流程**。 按一下&#x200B;**新增資料庫**。

![Brand Concierge](./images/aep119.png)

輸入名稱： `Dev`，為環境選取&#x200B;**開發（開發）**，然後按一下&#x200B;**新增所有變更的資源**。

按一下&#x200B;**「儲存並為開發建立」**。

![Brand Concierge](./images/aep120.png)

幾分鐘後，您的程式庫就會建置。 請稍候片刻，直到您看到&#x200B;**Dev**&#x200B;旁的&#x200B;**綠色點**。 接著，移至&#x200B;**環境**。

![Brand Concierge](./images/aep121.png)

按一下&#x200B;**開發**&#x200B;環境的&#x200B;**安裝**&#x200B;圖示。

![Brand Concierge](./images/aep122.png)

然後您應該會看到此訊息。 按一下「**複製**」按鈕，以復製程式庫的路徑。 您必須在網站上實作此專案。

程式庫路徑應如下所示：
`<script src="https://assets.adobedtm.com/XXXXXXX/XXXXXXXX/launch-XXXXXXXXX-development.min.js" async></script>`

![Brand Concierge](./images/aep123.png)

返回[Brand Concierge](./brandconcierge.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}