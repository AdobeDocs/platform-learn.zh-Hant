---
title: Microsoft Azure事件中樞的區段啟用 — 動作
description: Microsoft Azure事件中樞的區段啟用 — 動作
kt: 5342
doc-type: tutorial
source-git-commit: c6ba1f751f18afe39fb6b746a62bc848fa8ec9bf
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# 2.4.6端對端案例

## 2.4.6.1啟動Azure事件中樞觸發程式

若要顯示Adobe Experience Platform Real-time CDP在區段資格後傳送至Azure事件中樞的裝載，我們需要啟動簡單的Azure事件中樞觸發函式。 此函式將簡單地將裝載「傾印」到Visual Studio Code中的主控台。 但請記住，此函式可透過任何方式，擴充至使用專用API和通訊協定與各種環境進行介面。

### 啟動Visual Studio Code並啟動專案

請確定已開啟並執行Visual Studio Code專案

若要在Visual Studio Code中啟動/停止/重新啟動Azure函式，請參閱下列練習：

- [練習13.5.4 — 啟動Azure專案](./ex5.md)
- [練習13.5.5 — 停止Azure專案](./ex5.md)

您的Visual Studio Code的&#x200B;**終端機**&#x200B;應該提及類似以下的專案：

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 2.4.6.2載入您的Luma網站

移至[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案以開啟。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

您現在可以依照以下流程存取網站。 按一下&#x200B;**整合**。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web1.png)

在&#x200B;**整合**&#x200B;頁面上，您必須選取在練習0.1中建立的資料收集屬性。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web2.png)

然後您會看到示範網站已開啟。 選取URL並將其複製到剪貼簿。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

開啟新的無痕瀏覽器視窗。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

貼上您在上一步中複製的示範網站URL。 接著，系統會要求您使用Adobe ID登入。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

選取您的帳戶型別並完成登入程式。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

接著，您會在無痕瀏覽器視窗中看到您的網站已載入。 對於每個示範，您都需要使用全新的無痕瀏覽器視窗來載入您的示範網站URL。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

## 2.4.6.3符合您對裝置區段的興趣

導覽至&#x200B;**裝置**&#x200B;頁面一次，且&#x200B;**不要重新載入或重新整理**。 此動作應可讓您符合`--demoProfileLdap-- - Interest in Equipment`區段的資格。

![6-04-luma-telco-nav-sports.png](./images/luma1.png)

若要確認，請開啟「設定檔檢視器」面板。 您現在應該是`--demoProfileLdap-- - Interest in Equipment`的成員。 如果您的區段會籍尚未在設定檔檢視器面板中更新，請按一下重新載入按鈕。

![6-05-luma-telco-nav-broadband.png](./images/luma2.png)

切換回Visual Studio Code並檢視您的&#x200B;**TERMINAL**&#x200B;標籤，您應該會看到特定&#x200B;**ECID**&#x200B;的區段清單。 只要您符合`--demoProfileLdap-- - Interest in Equipment`區段的資格，就會將此啟用裝載傳送至您的事件中樞。

當您進一步瞭解區段承載時，可以看到`--demoProfileLdap-- - Interest in Equipment`處於&#x200B;**已實現**&#x200B;狀態。

**已實現**&#x200B;的區段狀態表示我們的設定檔剛進入區段。 雖然&#x200B;**existing**&#x200B;狀態表示我們的設定檔會繼續位於區段中。

![6-06-vsc-activation-realized.png](./images/luma3.png)

## 2.4.6.4再次造訪「裝置」頁面

執行&#x200B;**裝置**&#x200B;頁面的硬重新整理。

![6-07-back-to-sports.png](./images/luma1.png)

現在，切換回Visual Studio Code並驗證您的&#x200B;**終端機**&#x200B;索引標籤。 您會看到我們仍有您的區段，但目前的狀態為&#x200B;**existing**，表示我們的設定檔會繼續位於區段中。

![6-08-vsc-activation-existing.png](./images/luma4.png)

## 2.4.6.5第三次造訪「運動」頁面

如果您第三次重新造訪&#x200B;**Sports**&#x200B;頁面，將不會進行啟用，因為從區段檢視的角度來看，狀態不會變更。

區段啟用只會在區段的狀態變更時發生：

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

下一步： [摘要與優點](./summary.md)

[返回模組2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模組](./../../../overview.md)
