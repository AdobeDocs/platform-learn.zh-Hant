---
title: Microsoft Azure事件中樞的區段啟用 — Azure中的設定事件中樞
description: Microsoft Azure事件中樞的區段啟用 — Azure中的設定事件中樞
kt: 5342
doc-type: tutorial
exl-id: 0c2e94ec-00e8-4f47-add7-ca3a08151225
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 1%

---

# 2.4.2設定您的Microsoft Azure EventHub環境

Azure事件中樞是一種高度可擴充的發佈 — 訂閱服務，每秒可以擷取數百萬個事件，並將它們串流到多個應用程式中。 如此一來，您就可以處理和分析連線裝置和應用程式所產生的大量資料。

## 什麼是Azure事件中樞？

Azure事件中樞是巨量資料串流平台和事件擷取服務。 其每秒可接收及處理數百萬個事件。 傳送到事件中樞的資料可以使用任何即時分析提供者或批次/儲存配接卡進行轉換和儲存。

事件中樞代表事件管道的&#x200B;**前門**，在解決方案架構中通常稱為事件擷取器。 事件擷取器是位於事件發佈者(例如Adobe Experience Platform RTCDP)和事件消費者之間的元件或服務，以將事件資料流的產生與這些事件的消費分離。 事件中樞提供具有時間保留緩衝的統一串流平台，將事件製作者與事件消費者分離。

## 建立事件中樞名稱空間

移至[https://portal.azure.com/#home](https://portal.azure.com/#home)並選取&#x200B;**建立資源**。

![1-01-open-azure-portal.png](./images/101openazureportal.png)

在資源畫面中，在搜尋列中輸入&#x200B;**Event**。 尋找&#x200B;**事件中樞**&#x200B;卡，按一下&#x200B;**建立**，然後按一下&#x200B;**事件中樞**。

![1-02-search-event-hubs.png](./images/102searcheventhubs.png)

如果這是您第一次在Azure中建立資源，則需要建立新的&#x200B;**資源群組**。 如果您已經有資源群組，您可以選取它（或建立新資源群組）。

按一下&#x200B;**建立新的**&#x200B;並命名您的群組`--aepUserLdap---aep-enablement`，按一下&#x200B;**確定**。

![1-04-create-resource-group.png](./images/104createresourcegroup.png)

依照指示完成其餘欄位：

- 名稱空間：定義您的名稱空間，必須是唯一的，請使用以下模式`--aepUserLdap---aep-enablement`
- 位置：選擇任何位置
- 訂價層： **基本**
- 輸送量單位： **1**

按一下&#x200B;**檢閱+建立**。

![1-05-create-namespace.png](./images/105createnamespace.png)

按一下&#x200B;**建立**。

![1-07-namespace-create.png](./images/107namespacecreate.png)

資源群組的部署可能需要1-2分鐘，部署成功後，您將會看到下列畫面：

![1-08-namespace-deploy.png](./images/108namespacedeploy.png)

## 在Azure中設定您的事件中樞

移至[https://portal.azure.com/#home](https://portal.azure.com/#home)並選取&#x200B;**所有資源**。

![1-09-all-resources.png](./images/109allresources.png)

從資源清單中，按一下您的`--aepUserLdap---aep-enablement`事件中樞名稱空間：

![1-10-list-resources.png](./images/110listresources.png)

在`--aepUserLdap---aep-enablement`詳細資訊畫面中，移至&#x200B;**實體**&#x200B;並按一下&#x200B;**事件中樞**：

![1-11-eventhub-namespace.png](./images/111eventhubnamespace.png)

按一下&#x200B;**+事件中樞**。

![1-12-add-event-hub.png](./images/112addeventhub.png)

使用`--aepUserLdap---aep-enablement-event-hub`作為名稱，然後按一下&#x200B;**檢閱+建立**。

![1-13-create-event-hub.png](./images/113createeventhub.png)

按一下&#x200B;**建立**。

![1-13-create-event-hub.png](./images/113createeventhub1.png)

在事件中心名稱空間下的&#x200B;**事件中心**&#x200B;中，您現在會看到&#x200B;**事件中心**&#x200B;已列出。

![1-14-event-hub-list.png](./images/114eventhublist.png)

## 設定您的Azure儲存體帳戶

若要在稍後的練習中偵錯Azure事件中樞功能，您必須提供Azure儲存體帳戶，作為Visual Studio Code專案設定的一部分。 您現在將建立該Azure儲存體帳戶。

移至[https://portal.azure.com/#home](https://portal.azure.com/#home)並選取&#x200B;**建立資源**。

![1-15-event-hub-storage.png](./images/115eventhubstorage.png)

在搜尋中輸入&#x200B;**儲存體帳戶**，尋找&#x200B;**儲存體帳戶**&#x200B;的卡片，然後按一下&#x200B;**儲存體帳戶**。

![1-16-event-hub-search-storage.png](./images/116eventhubsearchstorage.png)

指定您的&#x200B;**資源群組** （在本練習開始時建立），使用`--aepUserLdap--aepstorage`作為儲存體帳戶名稱並選取&#x200B;**本機備援儲存體(LRS)**，然後按一下&#x200B;**檢閱+建立**。

![1-18-event-hub-create-review-storage.png](./images/118eventhubcreatereviewstorage.png)

按一下&#x200B;**建立**。

![1-19-event-hub-submit-storage.png](./images/119eventhubsubmitstorage.png)

建立我們的儲存帳戶將需要幾秒鐘的時間：

![1-20-event-hub-deploy-storage.png](./images/120eventhubdeploystorage.png)

完成後，您的畫面將會顯示&#x200B;**前往資源**&#x200B;按鈕。

按一下&#x200B;**首頁**。

![1-21-event-hub-deploy-ready-storage.png](./images/121eventhubdeployreadystorage.png)

您的存放裝置帳戶現在會顯示在&#x200B;**最近使用的資源**&#x200B;下。

![1-22-event-hub-deploy-resources-list.png](./images/122eventhubdeployresourceslist.png)

下一步： [2.4.3在Adobe Experience Platform中設定Azure事件中心目的地](./ex3.md)

[返回模組2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模組](./../../../overview.md)
