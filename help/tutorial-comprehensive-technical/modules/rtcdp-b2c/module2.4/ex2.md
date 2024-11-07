---
title: Microsoft Azure事件中樞的區段啟用 — 在Adobe Experience Platform中設定事件中樞RTCDP目的地
description: Microsoft Azure事件中樞的區段啟用 — 在Adobe Experience Platform中設定事件中樞RTCDP目的地
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# 2.4.2在Adobe Experience Platform中設定Azure事件中樞目的地

## 2.4.2.1識別必要的Azure連線引數

若要在Adobe Experience Platform中定義事件中心目的地，您需要執行下列作業：

- 事件中樞名稱空間
- 事件中樞
- Azure SAS金鑰名稱
- Azure SAS金鑰

已在先前的練習中定義事件中心和EventHub名稱空間： [練習1 — 在Azure中設定事件中心](./ex1.md)

### 事件中樞名稱空間

若要在Azure入口網站中查詢上述資訊，請導覽至[https://portal.azure.com/#home](https://portal.azure.com/#home)。 請確定您使用正確的Azure帳戶。

選取Azure入口網站中的&#x200B;**所有資源**：

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### 事件中樞

尋找資源型別為&#x200B;**事件中樞名稱空間**&#x200B;的資源，如果您遵循上一個練習中所使用的命名慣例，事件中樞名稱空間將為`--aepUserLdap---aep-enablement`。 記下它，您將在下一個練習中用到它。

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

按一下「事件中樞名稱空間」名稱以取得詳細資料：

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

選取&#x200B;**事件中樞**&#x200B;以取得事件中樞名稱空間中定義的事件中樞清單，如果您遵循上一個練習中所使用的命名慣例，您將會找到名為`--aepUserLdap---aep-enablement-event-hub`的事件中樞。 記下它，您將在下一個練習中用到它。

![2-04-event-hub-selected.png](./images/2-04-event-hub-selected.png)

### SAS金鑰名稱

為您的&#x200B;**事件中樞名稱空間**&#x200B;選取&#x200B;**共用存取原則**

![2-05-select-sas.png](./images/2-05-select-sas.png)

您將會看到共用存取原則清單。 我們正在尋找的SAS金鑰是&#x200B;**RootManageSharedAccessKey**。 這是SAS金鑰名稱。 寫下來。

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### SAS金鑰值

按一下&#x200B;**RootManageSharedAccessKey**&#x200B;以取得SAS金鑰值。 然後按&#x200B;**複製到剪貼簿**&#x200B;圖示複製&#x200B;**主索引鍵**：

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### 目的地值摘要

此時，您應該已找出在Adobe Experience Platform Real-time CDP中定義Azure事件中心目的地所需的所有值。

| 目的地屬性名稱 | 目的地屬性值 | 範例值 |
|---|---|---|
| sasKeyName | SAS金鑰名稱 | RootManageSharedAccessKey |
| sasKey | SAS金鑰值 | srREx9ShJG1Rv7f/... |
| 名稱空間 | 事件中樞名稱空間 | `--aepUserLdap---aep-enablement` |
| eventHubName | 事件中樞 | `--aepUserLdap---aep-enablement-event-hub` |

## 2.4.2.2在Adobe Experience Platform中建立Azure事件中心目的地

前往此URL登入Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./../../../modules/datacollection/module1.2/images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--aepSandboxName--``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的沙箱後，您會看到畫面變更，現在您已進入專屬沙箱。

![資料擷取](./../../../modules/datacollection/module1.2/images/sb1.png)

前往&#x200B;**目的地**，然後前往&#x200B;**目錄**。

![資料擷取](./images/sb2a.png)

選取&#x200B;**雲端儲存空間**&#x200B;並移至&#x200B;**Azure事件中樞**，然後按一下&#x200B;**[設定]**&#x200B;或&#x200B;**[設定]**：

![2-08-list-destinations.png](./images/2-08-list-destinations.png)

填入您在上一個練習中所收集的目的地值。 接著，按一下&#x200B;**連線到目的地**。

![2-09-destination-values.png](./images/2-09-destination-values.png)

如果認證正確，您將會看到確認： **已連線**。

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

您現在需要以`--aepUserLdap---aep-enablement`格式輸入名稱和描述。 輸入&#x200B;**eventHubName** （請參閱上一個練習，看起來像這樣： `--aepUserLdap---aep-enablement-event-hub`），然後按一下&#x200B;**下一步**。

![2-10-create-destination.png](./images/2-10-create-destination.png)

按一下&#x200B;**儲存並結束**。

![2-11-save-exit-activation.png](./images/2-11-save-exit-activation.png)

您的目的地現在已建立，並可在Adobe Experience Platform中使用。

![2-12-destination-created.png](./images/2-12-destination-created.png)

下一步： [2.4.3建立區段](./ex3.md)

[返回模組2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模組](./../../../overview.md)
