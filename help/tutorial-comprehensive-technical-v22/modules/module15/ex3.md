---
title: 在Adobe Experience Platform中設定HTTP API端點
description: 在Adobe Experience Platform中設定HTTP API端點
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 3346c57b-3a78-40b1-a891-053fc8781659
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 8%

---

# 15.3在Adobe Experience Platform中設定HTTP API串流端點

在Kafka中設定Adobe Experience Platform Sink連接器之前，您需要先在Adobe Experience Platform中建立HTTP API來源連接器。 設定Adobe Experience Platform Sink Connector時需要HTTP API串流端點URL。

若要建立HTTP API來源連接器，請前往此URL登入Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

登入後，您會登陸Adobe Experience Platform首頁。

![資料擷取](../module2/images/home.png)

繼續之前，您需要選取 **沙箱**. 要選取的沙箱已命名 ``--aepSandboxId--``. 您可以按一下文字 **[!UICONTROL 生產產品]** 在螢幕上方的藍線。 選取適當的沙箱後，畫面會變更，現在您就位於專用的沙箱中。

![資料擷取](../module2/images/sb1.png)

在左側功能表中，前往 **來源** 並向下捲動 **源目錄** 直到你看到 **HTTP API**. 按一下 **新增資料**.

![資料擷取](./images/kaep1.png)

按一下 **新帳戶**. 使用 `--demoProfileLdap-- - Kafka` 作為HTTP API連線的名稱，在此案例中為 **萬熱盧 — 卡夫卡**. 啟用 **XDM相容**. 按一下 **連接到源**.

![資料擷取](./images/kaep2.png)

然後您會看到，按一下 **下一個**.

![資料擷取](./images/kaep3.png)

選擇 **現有資料集**，開啟下拉式功能表。 搜尋並選取資料集 **示範系統 — 客服中心（全域v1.1）的事件資料集**.

![資料擷取](./images/kaep4.png)

按&#x200B;**「下一步」**。

![資料擷取](./images/kaep6.png)

按&#x200B;**「下一步」**。

![資料擷取](./images/kaep7.png)

按一下&#x200B;**完成**。

![資料擷取](./images/kaep8.png)

接著，您就會看到剛建立的HTTP API來源連接器概觀。

![資料擷取](./images/kaep9.png)

您需要複製 **串流端點** URL，如下所示，因為您在下一個練習中會需要它。

`https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`

您已完成本練習。

下一步： [15.4安裝並配置Kafka Connect和Adobe Experience Platform Sink Connector](./ex4.md)

[返回模組15](./aep-apache-kafka.md)

[返回所有模組](../../overview.md)
