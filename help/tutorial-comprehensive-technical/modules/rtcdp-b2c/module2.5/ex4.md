---
title: 資料收集和即時伺服器端轉送 — 建立和設定Google雲端功能
description: 建立及設定Google雲端功能
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 0%

---

# 2.5.4建立及設定Google雲端功能

## 2.5.4.1建立您的Google Cloud函式

移至[https://console.cloud.google.com/](https://console.cloud.google.com/)。 移至&#x200B;**雲端函式**。

![GCP](./images/gcp1.png)

您將會看到此訊息。 按一下&#x200B;**建立函式**。

![GCP](./images/gcp2.png)

您將會看到此訊息。

![GCP](./images/gcp6.png)

進行下列選擇：

- **函式名稱**： `--aepUserLdap---event-forwarding`
- **地區**：選取任何地區
- **觸發器型別**：選取&#x200B;**HTTP**
- **驗證**：選取&#x200B;**允許未驗證的呼叫**

您現在應該擁有此專案。 按一下&#x200B;**儲存**。

![GCP](./images/gcp7.png)

按一下&#x200B;**下一步**。

![GCP](./images/gcp8.png)

然後您會看到以下內容：

![GCP](./images/gcp9.png)

進行下列選擇：

- **執行階段**：選取&#x200B;**Node.js 16** （或更新版本）
- **進入點**：輸入&#x200B;**helloAEP**

按一下&#x200B;**啟用API**&#x200B;以啟用&#x200B;**雲端建置API**。 然後您會看到新視窗。 在該新視窗中，再按一下&#x200B;**啟用**。

![GCP](./images/gcp10.png)

您將會看到此訊息。 按一下&#x200B;**啟用**。

![GCP](./images/gcp11.png)

啟用&#x200B;**Cloud Build API**&#x200B;後，您將會看到此訊息。

![GCP](./images/gcp12.png)

返回您的&#x200B;**雲端函式**。
在雲端函式內嵌編輯器中，確認您有下列程式碼：

```javascript
/**
 * Responds to any HTTP request.
 *
 * @param {!express:Request} req HTTP request context.
 * @param {!express:Response} res HTTP response context.
 */
exports.helloAEP = (req, res) => {
  let message = req.query.message || req.body.message || 'Hello World!';
  res.status(200).send(message);
};
```

接著，按一下&#x200B;**部署**。

![GCP](./images/gcp13.png)

您將會看到此訊息。 正在建立您的雲端功能。 這可能需要幾分鐘的時間。

![GCP](./images/gcp14.png)

您的函式建立並執行後，您就會看到此訊息。 按一下函式名稱以開啟。

![GCP](./images/gcp15.png)

您將會看到此訊息。 移至&#x200B;**觸發器**。 然後您會看到&#x200B;**觸發程式URL**，您將用來定義Launch Server Side中的端點。

![GCP](./images/gcp16.png)

複製觸發程式URL，如下所示： **https://europe-west1-dazzling-pillar-273812.cloudfunctions.net/vangeluw-event-forwarding**。

在接下來的步驟中，您將設定Adobe Experience Platform資料收集伺服器，將有關&#x200B;**頁面檢視**&#x200B;的特定資訊串流到您的Google雲端功能。 除了直接轉送完整的裝載原樣，您只會將&#x200B;**ECID**、**時間戳記**&#x200B;和&#x200B;**頁面名稱**&#x200B;之類的傳送至您的Google雲端功能。

以下是您需要剖析以篩選掉上述變數的裝載範例：

```json
{
  "events": [
    {
      "xdm": {
        "eventType": "web.webpagedetails.pageViews",
        "web": {
          "webPageDetails": {
            "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC",
            "name": "vangeluw-OCUC",
            "viewName": "vangeluw-OCUC",
            "pageViews": {
              "value": 1
            }
          },
          "webReferrer": {
            "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC/equipment"
          }
        },
        "device": {
          "screenHeight": 1080,
          "screenWidth": 1920,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1920,
            "viewportHeight": 451
          }
        },
        "placeContext": {
          "localTime": "2022-02-23T06:51:07.140+01:00",
          "localTimezoneOffset": -60
        },
        "timestamp": "2022-02-23T05:51:07.140Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy/reactor",
          "version": "2.8.0+2.9.0",
          "environment": "browser"
        },
        "_experienceplatform": {
          "identification": {
            "core": {
              "ecid": "08346969856929444850590365495949561249"
            }
          },
          "demoEnvironment": {
            "brandName": "vangeluw-OCUC"
          },
          "interactionDetails": {
            "core": {
              "channel": "web"
            }
          }
        }
      },
      "query": {
        "personalization": {
          "schemas": [
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
          ],
          "decisionScopes": [
            "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0YzA1MjM4MmUxYjY1MDUiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTRiZjA5ZGM0MTkwZWJiYSJ9",
            "__view__"
          ]
        }
      }
    }
  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  },
  "meta": {
    "state": {
      "domain": "adobedemo.com",
      "cookiesEnabled": true,
      "entries": [
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_identity",
          "value": "CiYwODM0Njk2OTg1NjkyOTQ0NDg1MDU5MDM2NTQ5NTk0OTU2MTI0OVIPCPn66KfyLxgBKgRJUkwx8AH5-uin8i8="
        },
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_consent_check",
          "value": "1"
        },
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_consent",
          "value": "general=in"
        }
      ]
    }
  }
}
```

這些欄位包含需要剖析的資訊：

- ECID： **events.xdm。_experienceplatform.identification.core.ecid**
- 時間戳記： **timestamp**
- 頁面名稱： **events.xdm.web.webPageDetails.name**

現在請前往Adobe Experience Platform資料收集伺服器，設定資料元素，讓此功能成為可能。

## 2.5.4.2更新您的事件轉送屬性：資料元素

移至[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)並移至&#x200B;**事件轉送**。 搜尋您的「事件轉送」屬性，然後按一下以開啟。

![Adobe Experience Platform Data Collection SSF](./images/prop1.png)

在左側功能表中，移至&#x200B;**資料元素**。 按一下&#x200B;**新增資料元素**。

![Adobe Experience Platform Data Collection SSF](./images/de1gcp.png)

然後，您會看到要設定的新資料元素。

![Adobe Experience Platform Data Collection SSF](./images/de2gcp.png)

進行下列選取：

- 以&#x200B;**Name**&#x200B;的身分，輸入&#x200B;**customerECID**。
- 選取&#x200B;**核心**&#x200B;作為&#x200B;**延伸模組**。
- 作為&#x200B;**資料元素型別**，請選取&#x200B;**路徑**。
- 作為&#x200B;**路徑**，請輸入`arc.event.xdm.--aepTenantId--.identification.core.ecid`。 若輸入此路徑，您將會從網站或行動應用程式傳送至Adobe Edge的事件裝載中，篩選掉欄位&#x200B;**ecid**。

>[!NOTE]
>
>在上方及下方路徑中，已對&#x200B;**arc**&#x200B;產生參考。 **arc**&#x200B;代表Adobe資源內容，**arc**&#x200B;永遠代表伺服器端內容中可用的最高物件。 可以使用Adobe Experience Platform資料收集伺服器功能將擴充與轉換新增至該&#x200B;**arc**&#x200B;物件。
>
>在上方及下方路徑中，已參考&#x200B;**事件**。 **event**&#x200B;代表不重複事件，Adobe Experience Platform Data Collection Server一律會個別評估每個事件。 有時您可能會在Web SDK Client Side傳送的裝載中看到&#x200B;**事件**&#x200B;的參考，但在Adobe Experience Platform Data Collection Server中，每個事件都會個別評估。

您現在已擁有此專案。 按一下&#x200B;**儲存**。

![Adobe Experience Platform Data Collection SSF](./images/gcdpde1.png)

按一下&#x200B;**新增資料元素**。

![Adobe Experience Platform Data Collection SSF](./images/addde.png)

然後，您會看到要設定的新資料元素。

![Adobe Experience Platform Data Collection SSF](./images/de2gcp.png)

進行下列選取：

- 作為&#x200B;**Name**，請輸入&#x200B;**eventTimestamp**。
- 選取&#x200B;**核心**&#x200B;作為&#x200B;**延伸模組**。
- 作為&#x200B;**資料元素型別**，請選取&#x200B;**路徑**。
- 以&#x200B;**路徑**&#x200B;的形式，輸入&#x200B;**arc.event.xdm.timestamp**。 輸入此路徑後，您將會從網站或行動應用程式傳送至Adobe Edge的事件裝載中，篩選掉欄位&#x200B;**timestamp**。

您現在已擁有此專案。 按一下&#x200B;**儲存**。

![Adobe Experience Platform Data Collection SSF](./images/gcdpde2.png)

按一下&#x200B;**新增資料元素**。

![Adobe Experience Platform Data Collection SSF](./images/addde.png)

然後，您會看到要設定的新資料元素。

![Adobe Experience Platform Data Collection SSF](./images/de2gcp.png)

進行下列選取：

- 以&#x200B;**Name**&#x200B;的身分，輸入&#x200B;**pageName**。
- 選取&#x200B;**核心**&#x200B;作為&#x200B;**延伸模組**。
- 作為&#x200B;**資料元素型別**，請選取&#x200B;**路徑**。
- 以&#x200B;**Path**&#x200B;身分，輸入&#x200B;**arc.event.xdm.web.webPageDetails.name**。 輸入此路徑後，您將會從網站或行動應用程式傳送到Adobe Edge的事件裝載中，篩選掉欄位&#x200B;**name**。

您現在已擁有此專案。 按一下&#x200B;**儲存**。

![Adobe Experience Platform Data Collection SSF](./images/gcdpde3.png)

您現在已建立下列資料元素：

![Adobe Experience Platform Data Collection SSF](./images/de3gcp.png)

## 2.5.4.3更新您的事件轉送屬性：更新規則

在左側功能表中，移至&#x200B;**規則**。 在上一個練習中，您已建立規則&#x200B;**所有頁面**。 按一下該規則以開啟。

![Adobe Experience Platform Data Collection SSF](./images/rl1gcp.png)

到時您會看到這個。 按一下「**動作**」下的「**+**」圖示以新增動作。

![Adobe Experience Platform Data Collection SSF](./images/rl2gcp.png)

您將會看到此訊息。

![Adobe Experience Platform Data Collection SSF](./images/rl4gcp.png)

進行下列選取：

- 選取&#x200B;**擴充功能**： **Adobe雲端聯結器**。
- 選取&#x200B;**動作型別**： **進行擷取呼叫**。

應該會提供此&#x200B;**名稱**： **Adobe雲端聯結器 — 進行擷取呼叫**。 您現在應該會看到：

![Adobe Experience Platform Data Collection SSF](./images/rl5gcp.png)

接著，設定下列專案：

- 將要求通訊協定從GET變更為&#x200B;**POST**
- 輸入您在前一個步驟中建立的Google雲端函式URL，如下所示： **https://europe-west1-dazzling-pillar-273812.cloudfunctions.net/vangeluw-event-forwarding**

您現在應該擁有此專案。 接著，移至&#x200B;**內文**。

![Adobe Experience Platform Data Collection SSF](./images/rl6gcp.png)

您將會看到此訊息。 按一下&#x200B;**JSON**&#x200B;的選項按鈕。

![Adobe Experience Platform Data Collection SSF](./images/rl7gcp.png)

設定&#x200B;**主體**，如下所示：

| 索引鍵 | 值 |
|--- |--- |
| customerECID | {{customerECID}} |
| pageName | {{pageName}} |
| eventTimestamp | {{eventTimestamp}} |

您將會看到此訊息。 按一下&#x200B;**保留變更**。

![Adobe Experience Platform Data Collection SSF](./images/rl9gcp.png)

您將會看到此訊息。 按一下&#x200B;**儲存**。

![Adobe Experience Platform Data Collection SSF](./images/rl10gcp.png)

您現在已在Adobe Experience Platform資料收集伺服器屬性中更新現有規則。 移至&#x200B;**發佈流程**&#x200B;以發佈您的變更。 按一下指示的&#x200B;**編輯**，開啟您的開發程式庫&#x200B;**主要**。

![Adobe Experience Platform Data Collection SSF](./images/rl12gcp.png)

按一下&#x200B;**新增所有變更的資源**&#x200B;按鈕，之後您會看到您的規則和資料元素出現在此程式庫中。 接著，按一下&#x200B;**儲存並建置以供開發**。 正在部署您的變更。

![Adobe Experience Platform Data Collection SSF](./images/rl13gcp.png)

幾分鐘後，您會看到部署已完成並準備好進行測試。

![Adobe Experience Platform Data Collection SSF](./images/rl14.png)

## 2.5.3.4測試您的設定

移至[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案以開啟。

![DSN](../../gettingstarted/gettingstarted/images/web8.png)

您現在可以依照以下流程存取網站。 按一下&#x200B;**整合**。

![DSN](../../gettingstarted/gettingstarted/images/web1.png)

在&#x200B;**整合**&#x200B;頁面上，您必須選取在練習0.1中建立的資料收集屬性。

![DSN](../../gettingstarted/gettingstarted/images/web2.png)

然後您會看到示範網站已開啟。 選取URL並將其複製到剪貼簿。

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

開啟新的無痕瀏覽器視窗。

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

貼上您在上一步中複製的示範網站URL。 接著，系統會要求您使用Adobe ID登入。

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

選取您的帳戶型別並完成登入程式。

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

接著，您會在無痕瀏覽器視窗中看到您的網站已載入。 對於每個示範，您都需要使用全新的無痕瀏覽器視窗來載入您的示範網站URL。

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

當您開啟瀏覽器開發人員檢視時，可以如下所示檢查網路要求。 使用篩選器&#x200B;**互動**&#x200B;時，您會看到Adobe Experience Platform資料收集使用者端傳送給Adobe Edge的網路要求。

![Adobe Experience Platform資料彙集設定](./images/hook1.png)

將檢視切換至您的Google雲端功能，並移至&#x200B;**記錄檔**。 您現在應該有與此類似的檢視，其中會顯示許多記錄專案。 每次您看到&#x200B;**函式執行開始**&#x200B;時，就表示您的Google雲端函式已接收傳入流量。

![Adobe Experience Platform資料彙集設定](./images/hook3gcp.png)

讓我們稍微更新您的函式，以便處理傳入的資料，並顯示從Adobe Experience Platform資料收集伺服器收到的資訊。 移至&#x200B;**SOURCE**&#x200B;並按一下&#x200B;**編輯**。

![Adobe Experience Platform資料彙集設定](./images/hook4gcp.png)

在下一個畫面中，按一下&#x200B;**下一步**。

![Adobe Experience Platform資料彙集設定](./images/gcf1.png)

更新您的程式碼，如下所示：

```javascript
/**
 * Responds to any HTTP request.
 *
 * @param {!express:Request} req HTTP request context.
 * @param {!express:Response} res HTTP response context.
 */
exports.helloAEP = (req, res) => {
  console.log('>>>>> Function has started. The following information was received from Event Forwarding:');
  console.log(req.body);

  let message = req.query.message || req.body.message || 'Hello World!';
  res.status(200).send(message);
};
```

您就會擁有此專案。 按一下&#x200B;**部署**。

![Adobe Experience Platform資料彙集設定](./images/gcf2.png)

幾分鐘後，您的函式將再次部署。 按一下您的函式名稱以開啟。

![Adobe Experience Platform資料彙集設定](./images/gcf3.png)

在您的示範網站上，導覽至產品，例如&#x200B;**DEIRDRE RELAXED-FIT CAPRI**。

![Adobe Experience Platform資料彙集設定](./images/gcf3a.png)

將檢視切換至您的Google雲端功能，並移至&#x200B;**記錄檔**。 您現在應該有與此類似的檢視，其中會顯示許多記錄專案。

現在，您應該會在示範網站的每個頁面檢視中，在Google雲端功能的記錄檔中看到新的記錄專案快顯視窗，其中顯示收到的資訊。

![Adobe Experience Platform資料彙集設定](./images/gcf4.png)

您現在已成功將Adobe Experience Platform資料收集收集的資料即時傳送至Google雲端函式端點。 從該位置，該資料可供任何Google雲端平台應用程式使用，例如用於儲存和報表或機器學習使用案例的BigQuery。

下一步： [2.5.5向AWS生態系統轉送事件](./ex5.md)

[返回模組2.5](./aep-data-collection-ssf.md)

[返回所有模組](./../../../overview.md)
