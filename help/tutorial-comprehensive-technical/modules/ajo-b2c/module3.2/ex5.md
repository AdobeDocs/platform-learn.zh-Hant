---
title: Adobe Journey Optimizer — 外部氣象API、SMS動作等 — 觸發您的協調客戶歷程
description: Adobe Journey Optimizer — 外部氣象API、SMS動作等 — 觸發您的協調客戶歷程
kt: 5342
doc-type: tutorial
source-git-commit: c6ba1f751f18afe39fb6b746a62bc848fa8ec9bf
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---

# 3.2.5觸發您的歷程

在本練習中，您將測試並觸發您在本單元中設定的歷程。

## 3.2.5.1更新您的地理圍欄事件設定

移至[Adobe Experience Platform資料彙集](https://experience.adobe.com/launch/)並選取&#x200B;**標籤**。

這是您之前看到的Adobe Experience Platform資料收集屬性頁面。

![屬性頁面](./../../../modules/datacollection/module1.1/images/launch1.png)

在模組0中，示範系統為您建立了兩個使用者端屬性：一個用於網站，另一個用於行動應用程式。 在&#x200B;**[!UICONTROL 搜尋]**&#x200B;方塊中搜尋`--demoProfileLdap--`以尋找它們。 按一下以開啟&#x200B;**Web**&#x200B;屬性。

![搜尋方塊](./../../../modules/datacollection/module1.1/images/property6.png)

您將會看到此訊息。

![啟動安裝程式](./images/rule1.png)

在左側功能表中，移至&#x200B;**規則**&#x200B;並搜尋規則&#x200B;**地理圍欄事件**。 按一下規則&#x200B;**地理圍欄事件**&#x200B;以開啟它。

![啟動安裝程式](./images/rule2.png)

之後，您將會看到此規則的詳細資料。 按一下以開啟動作&#x200B;**傳送「地理圍欄事件」至AEP — 觸發JO**。

![啟動安裝程式](./images/rule3.png)

之後您會看到，觸發此動作時，會使用特定資料元素來定義XDM資料結構。 您需要更新該資料元素，而且需要定義您在[練習8.1](./ex1.md)中設定之事件的&#x200B;**事件識別碼**。

![啟動安裝程式](./images/rule4.png)

您現在需要更新資料元素&#x200B;**XDM — 地理圍欄事件**。 若要這麼做，請移至&#x200B;**資料元素**。 搜尋&#x200B;**XDM — 地理圍欄事件**，然後按一下以開啟該資料元素。

![啟動安裝程式](./images/rule5.png)

然後您會看到以下內容：

![啟動安裝程式](./images/rule6.png)

瀏覽至欄位`_experience.campaign.orchestration.eventID`。 移除目前的值，並將您的eventID貼到該處。

提醒您，您可以在Adobe Journey Optimizer中的&#x200B;**設定>事件**&#x200B;下找到事件ID，您也可以在事件裝載的範例中找到事件ID，如下所示： `"eventID": "fa42ab7982ba55f039eacec24c1e32e5c51b310c67f0fa559ab49b89b63f4934"`。

![ACOP](./images/payloadeventID.png)

接下來，您應該在此資料元素中定義您的城市。 前往&#x200B;**placeContext >地理>城市**，然後輸入您選擇的城市。 接著，按一下&#x200B;**儲存**&#x200B;或&#x200B;**儲存至資料庫**。

![ACOP](./images/payloadeventIDgeo.png)

最後，您需要發佈變更。 前往左側功能表中的&#x200B;**發佈流程**。

![啟動安裝程式](./images/rule8.png)

按一下[新增所有變更的資源]**，然後按一下[儲存並建置至開發]****。**

![啟動安裝程式](./images/rule9.png)

## 3.2.5.2觸發您的歷程

移至[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案以開啟。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

在&#x200B;**Screens**&#x200B;頁面上按一下&#x200B;**執行**。

![DSN](./../../../modules/datacollection/module1.1/images/web2.png)

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

按一下畫面左上角的Adobe標誌圖示，開啟設定檔檢視器。

![示範](./../../../modules/datacollection/module1.2/images/pv1.png)

請檢視「設定檔檢視器」面板和即時客戶設定檔，並將&#x200B;**Experience CloudID**&#x200B;設為此目前未知客戶的主要識別碼。

![示範](./../../../modules/datacollection/module1.2/images/pv2.png)

前往「註冊/登入」頁面。 按一下&#x200B;**建立帳戶**。

![示範](./../../../modules/datacollection/module1.2/images/pv9.png)

填寫您的詳細資料，然後按一下&#x200B;**註冊**，之後您將會被重新導向到上一頁。

![示範](./../../../modules/datacollection/module1.2/images/pv10.png)

開啟設定檔檢視器面板，然後前往即時客戶設定檔。 在「設定檔檢視器」面板上，您應該會看到所有顯示的個人資料，例如新新增的電子郵件和電話識別碼。

![示範](./../../../modules/datacollection/module1.2/images/pv11.png)

在「設定檔檢視器」面板上，按一下&#x200B;**公用程式**。 輸入`geofenceevent`並按一下&#x200B;**傳送**。

![示範](./images/smsdemo1.png)

幾秒後，您將會收到來自Adobe Journey Optimizer的簡訊。

![示範](./images/smsdemo4.png)

下一步： [摘要與優點](./summary.md)

[返回模組3.2](journey-orchestration-external-weather-api-sms.md)

[返回所有模組](../../../overview.md)
