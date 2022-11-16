---
title: 區段啟動至Microsoft Azure事件中樞 — 在Adobe Experience Platform中設定事件中樞RTCDP目的地
description: 區段啟動至Microsoft Azure事件中樞 — 在Adobe Experience Platform中設定事件中樞RTCDP目的地
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: b42b4ccb-1952-480b-b538-c1bd661e29eb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# 13.2在Adobe Experience Platform中設定您的Azure事件中樞目的地

## 13.2.1標識所需的Azure連接參數

若要在Adobe Experience Platform中定義事件中心目的地，您需要：

- 事件中心命名空間
- 事件中心
- Azure SAS密鑰名稱
- Azure SAS密鑰

在先前的練習中已定義「事件中心」和「EventHub」命名空間： [練習1 — 在Azure中設定事件中心](./ex1.md)

### 事件中心命名空間

若要在Azure入口網站中查閱上述資訊，請導覽至 [https://portal.azure.com/#home](https://portal.azure.com/#home). 請確定您使用正確的Azure帳戶。

選擇 **所有資源** 在Azure門戶中：

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### 事件中心

查找資源類型 **事件中心命名空間**，如果您遵循上一練習中使用的命名慣例，則「事件中心命名空間」將成為 `--demoProfileLdap---aep-enablement`. 請注意，您將在下一個練習中需要它。

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

按一下「事件中心」命名空間名稱以獲取詳細資訊：

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

選擇 **事件中心** 要獲取在「事件中心命名空間」中定義的事件中心清單，如果您遵循了前一個練習中使用的命名慣例，將會找到一個名為 `--demoProfileLdap---aep-enablement-event-hub`. 請注意，您將在下一個練習中需要它。

![2-04-event-hub-selected.png](./images/2-04-event-hub-selected.png)

### SAS密鑰名

選擇 **共用訪問策略** 為 **事件中心命名空間**

![2-05-select-sas.png](./images/2-05-select-sas.png)

您將看到共用訪問策略的清單。 我們要尋找的SAS密鑰是 **RootManageSharedAccessKey**. 這是SAS密鑰名。 寫下來。

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### SAS密鑰值

按一下 **RootManageSharedAccessKey** 獲取SAS密鑰值。 按 **複製到剪貼簿** 圖示來複製 **主鍵**:

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### 目標值摘要

此時，您應已識別在Adobe Experience Platform Real-time CDP中定義Azure Event Hub目的地所需的所有值。

| 目標屬性名稱 | 目標屬性值 | 範例值 |
|---|---|---|
| sasKeyName | SAS密鑰名 | RootManageSharedAccessKey |
| sasKey | SAS密鑰值 | srREx9ShJG1Rv7f/... |
| namespace | 事件中心命名空間 | `--demoProfileLdap---aep-enablement` |
| eventHubName | 事件中心 | `--demoProfileLdap---aep-enablement-event-hub` |

## 13.2.2在Adobe Experience Platform中建立Azure事件中樞目的地

前往此URL登入Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

登入後，您會登陸Adobe Experience Platform首頁。

![資料擷取](../module2/images/home.png)

繼續之前，您需要選取 **沙箱**. 要選取的沙箱已命名 ``--aepSandboxId--``. 您可以按一下文字 **[!UICONTROL 生產產品]** 在螢幕上方的藍線。 選取適當的沙箱後，畫面會變更，現在您就位於專用的沙箱中。

![資料擷取](../module2/images/sb1.png)

前往 **目的地**，然後前往 **目錄**.

![資料擷取](./images/sb2a.png)

選擇 **雲端儲存空間** 然後 **Azure事件中心** 按一下 **設定** 或 **設定**:

![2-08-list-destinations.png](./images/2-08-list-destinations.png)

填寫您在上次練習中收集的目標值。 下一步，按一下 **連接到目標**.

![2-09-destination-values.png](./images/2-09-destination-values.png)

如果您的認證正確，您會看到確認訊息： **已連接**.

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

您現在需要以格式輸入名稱和說明 `--demoProfileLdap---aep-enablement`. 輸入 **eventHubName** (請參閱先前的練習，看起來如下： `--demoProfileLdap---aep-enablement-event-hub`)，然後按一下 **下一個**.

![2-10-create-destination.png](./images/2-10-create-destination.png)

按一下 **儲存並退出**.

![2-11-save-exit-activation.png](./images/2-11-save-exit-activation.png)

您的目的地現在已建立，並可在Adobe Experience Platform中使用。

![2-12-destination-created.png](./images/2-12-destination-created.png)

下一步： [13.3建立區段](./ex3.md)

[返回模組13](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模組](./../../overview.md)
