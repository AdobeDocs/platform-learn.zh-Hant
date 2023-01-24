---
title: Bootcamp — 即時客戶個人檔案 — 從未知到網站上已知 — 巴西
description: Bootcamp — 即時客戶個人檔案 — 從未知到網站上已知 — 巴西
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 1%

---

# 1.1從網站上的未知到已知

## 內容

從未知到已知的歷程是現今品牌中最重要的主題之一，客戶從贏取到保留的歷程亦然。

Adobe Experience Platform在這段歷程中扮演著重要角色。 平台是溝通的大腦， **體驗記錄系統**.

Platform是一種環境，在這種環境中，客戶一詞比已知客戶更廣。 從Platform的角度來看，網站上的未知訪客也是客戶，因此，作為未知訪客的所有行為也會傳送至Platform。 有了這種方法，當此訪客最終成為已知客戶時，品牌也可以將那一刻之前發生的情形加以視覺化。 這從歸因和體驗最佳化的觀點來說，有所幫助。

## 客戶歷程流程

前往 [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). 按一下 **允許全部**.

![DSN](./images/web8.png)

按一下螢幕左上角的Adobe標誌圖示，開啟「設定檔檢視器」。

![示範](./images/pv1.png)

查看「設定檔檢視器」面板和「即時客戶設定檔」，其中 **Experience CloudID** 作為此目前未知客戶的主要識別碼。

![示範](./images/pv2.png)

您也可以查看根據客戶行為收集的所有體驗事件。 清單目前為空白，但很快就會變更。

![示範](./images/pv3.png)

前往 **應用程式服務** 選項，然後按一下產品 **Real-Time CDP**.

![示範](./images/pv4.png)

然後您會看到產品詳細資料頁面。 類型的體驗事件 **產品檢視** 現已透過您在模組1中檢閱的Web SDK實作，傳送至Adobe Experience Platform。 開啟「設定檔檢視器」面板，並查看您的 **體驗事件**.

![示範](./images/pv5.png)

前往 **應用程式服務** 選項，然後按一下產品 **Adobe Journey Optimizer**. 已將另一個體驗事件傳送至Adobe Experience Platform。

![示範](./images/pv7.png)

開啟「配置檔案查看器」面板。 您現在會看到2個類型的體驗事件 **產品檢視**. 雖然行為為匿名，但每次點按都會受到追蹤並儲存在Adobe Experience Platform中。 一旦匿名客戶成為已知客戶，我們就能自動將所有匿名行為合併到已知的設定檔。

![示範](./images/pv8.png)

現在來分析您的客戶設定檔，然後使用您的行為來個人化您的網站上的客戶體驗。

下一步： [1.2將您自己的即時客戶設定檔視覺化 — UI](./ex2.md)

[返回用戶流1](./uc1.md)

[返回所有模組](../../overview.md)
