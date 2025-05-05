---
title: Audience Activation到Microsoft Azure事件中心 — 定義Azure函式
description: Audience Activation到Microsoft Azure事件中心 — 定義Azure函式
kt: 5342
doc-type: tutorial
exl-id: 2ce9dcfc-4b2c-48b4-b554-8a30abb850f3
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# 2.4.6建立您的Microsoft Azure專案

## 熟悉Azure事件中心功能

Azure Functions可讓您執行小段程式碼（稱為&#x200B;**函式**），而不需擔心應用程式基礎結構。 藉由Azure Functions，雲端基礎結構可提供您維持應用程式大規模執行所需的所有最新伺服器。
函式是由特定型別的事件&#x200B;**觸發**。 支援的觸發器包括回應資料變更、回應訊息（例如事件中樞）、依排程執行或作為HTTP請求的結果。
Azure Functions是一種無伺服器運算服務，可讓您執行事件觸發的程式碼，而不需明確布建或管理基礎結構。
Azure事件中樞會整合Azure Functions以提供無伺服器架構。

## 開啟Visual Studio Code並登入Azure

Visual Studio Code可讓您輕鬆……
- 定義並將Azure函式繫結到事件中樞- 本機測試- 部署至Azure- 遠端記錄函式執行

### 開啟Visual Studio Code

### 登入Azure

當您使用您在上一個練習中用來註冊的Azure帳戶登入時，Visual Studio Code可讓您尋找並繫結所有事件中樞資源。
開啟Visual Studio Code並按一下&#x200B;**Azure**&#x200B;圖示。
接著選取&#x200B;**登入Azure**：
![3-01-vsc-open.png](./images/301vscopen.png)
系統會將您重新導向至瀏覽器以登入。 請記得選取您用來註冊的Azure帳戶。
當您在瀏覽器中看到下列畫面時，表示您已使用Visual Code Studio登入：
![3-03-vsc-login-ok.png](./images/303vscloginok.png)
返回Visual Code Studio （您將會看到Azure訂閱的名稱，例如&#x200B;**Azure訂閱1**）：
![3-04-vsc-logged-in.png](./images/304vscloggedin.png)

## 建立Azure專案

按一下&#x200B;**建立函式專案……**：
![3-05-vsc-create-project.png](./images/vsc2.png)
選取或建立您選擇的本機資料夾以儲存專案，然後按一下[選取] **&#x200B;**：
![3-06-vsc-select-folder.png](./images/vsc3.png)
您現在將輸入專案建立精靈。 按一下&#x200B;**Javascript**&#x200B;作為專案的語言：
![3-07-vsc-select-language.png](./images/vsc4.png)
然後選取&#x200B;**模型v4**。
![3-07-vsc-select-language.png](./images/vsc4a.png)
選取&#x200B;**Azure事件中心觸發程式**&#x200B;作為專案的第一個函式範本：
![3-08-vsc-function-template.png](./images/vsc5.png)
輸入函式的名稱，使用下列格式`--aepUserLdap---aep-event-hub-trigger`，然後按Enter鍵：
![3-09-vsc-function-name.png](./images/vsc6.png)
選取&#x200B;**建立新的本機應用程式設定**：
![3-10-vsc-function-local-app-setting.png](./images/vsc7.png)
按一下以選取您先前建立的名為`--aepUserLdap---aep-enablement`的事件中心名稱空間。
![3-11-vsc-function-select-namespace.png](./images/vsc8.png)
接著，按一下以選取您先前建立的事件中樞，其名稱為`--aepUserLdap---aep-enablement-event-hub`。
![3-12-vsc-function-select-eventhub.png](./images/vsc9.png)
按一下以選取&#x200B;**RootManageSharedAccessKey**&#x200B;作為您的事件中心原則：
![3-13-vsc-function-select-eventhub-policy.png](./images/vsc10.png)
選取&#x200B;**新增至工作區**，瞭解如何開啟您的專案：
![3-15-vsc-project-add-to-workspace.png](./images/vsc12.png)
您可能會收到類似以下的訊息。 在這種情況下，請按一下&#x200B;**是，我信任作者**。
![3-15-vsc-project-add-to-workspace.png](./images/vsc12a.png)
建立專案後，在編輯器中開啟檔案`--aepUserLdap---aep-event-hub-trigger.js`：
![3-16-vsc-open-index-js.png](./images/vsc13.png)
Adobe Experience Platform傳送至事件中心的裝載看起來會像這樣：

```json
{
  "identityMap": {
    "ecid": [
      {
        "id": "36281682065771928820739672071812090802"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "94db5aed-b90e-478d-9637-9b0fad5bba11": {
        "createdAt": 1732129904025,
        "lastQualificationTime": "2024-11-21T07:33:52Z",
        "mappingCreatedAt": 1732130611000,
        "mappingUpdatedAt": 1732130611000,
        "name": "vangeluw - Interest in Plans",
        "status": "realized",
        "updatedAt": 1732129904025
      }
    }
  }
}
```

使用下列程式碼更新您Visual Studio Code `--aepUserLdap---aep-event-hub-trigger.js`中的程式碼。 每次Real-time CDP將對象資格傳送至事件中心目的地時，都會執行此程式碼。 在此範例中，程式碼只是關於顯示傳入裝載，但您可以想像任何種類的額外功能，以即時處理對象資格，並在資料管道生態系統更下游使用。
檔案`--aepUserLdap---aep-event-hub-trigger.js`中的第11行目前顯示如下：

```javascript
context.log('Event hub message:', message);
```

將`--aepUserLdap---aep-event-hub-trigger.js`中的第11行變更為如下所示：

```javascript
context.log('Event hub message:', JSON.stringify(message));
```

總裝載隨後應如下所示：

```javascript
const { app } = require('@azure/functions');

app.eventHub('--aepUserLdap---aep-event-hub-trigger', {
    connection: '--aepUserLdap--aepenablement_RootManageSharedAccessKey_EVENTHUB',
    eventHubName: '--aepUserLdap---aep-enablement-event-hub',
    cardinality: 'many',
    handler: (messages, context) => {
        if (Array.isArray(messages)) {
            context.log(`Event hub function processed ${messages.length} messages`);
            for (const message of messages) {
                context.log('Event hub message:', message);
            }
        } else {
            context.log('Event hub function processed message:', messages);
        }
    }
});
```


結果應如下所示：
![3-16b-vsc-edit-index-js.png](./images/vsc1.png)

## 執行Azure專案

現在該執行您的專案了。 目前階段，我們不會將專案部署到Azure。 我們將在偵錯模式中在本機執行。 選取「執行」圖示，按一下綠色箭頭。
![3-17-vsc-run-project.png](./images/vsc14.png)
第一次以偵錯模式執行專案時，您必須附加Azure儲存體帳戶，請按一下[選取儲存體帳戶]。**&#x200B;**
![3-17-vsc-run-project.png](./images/vsc14a.png)
然後選取您先前建立的儲存體帳戶，名為`--aepUserLdap--aepstorage`。
![3-17-vsc-run-project.png](./images/vsc14b.png)
您的專案現在已啟動且執行中，並列出事件中心中的事件。 在下個練習中，您將會在CitiSignal示範網站上示範行為，以符合您的受眾資格。 因此，您將在事件中心觸發函式的終端機中收到對象資格裝載。
![3-24-vsc-application-stop.png](./images/vsc18.png)

## 停止Azure專案

若要停止您的專案，請移至VSC中的lenu **CALL STACK**，按一下執行中專案上的箭頭，然後按一下&#x200B;**停止**。
![3-24-vsc-application-stop.png](./images/vsc17.png)

## 後續步驟

移至[2.4.7端對端案例](./ex7.md){target="_blank"}
返回[Real-Time CDP： Audience Activation到Microsoft Azure事件中心](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}
返回[所有模組](./../../../../overview.md){target="_blank"}
