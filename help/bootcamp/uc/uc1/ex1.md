---
title: Bootcamp — 即時客戶設定檔 — 從未知到網站上已知
description: Bootcamp — 即時客戶設定檔 — 從未知到網站上已知
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 32a084a3-4c04-4367-947e-f7151fdad73b
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---

# 1.1從未知到網站上已知

## 內容

從未知到已知的歷程是這些天品牌最重要的主題之一，就像從贏取到保留的客戶歷程一樣。

Adobe Experience Platform在此歷程中扮演著重要的角色。 Platform是溝通的大腦， **體驗記錄系統**.

Platform是一種環境，其中客戶一詞的含義比已知客戶更為廣泛。 在網站上的未知訪客也是平台觀點的客戶，因此，作為未知訪客的所有行為也會傳送到Platform。 由於這種方法，當此訪客最終成為已知客戶時，品牌也可以將此時之前發生的事情視覺化。 從歸因和體驗最佳化的角度來看，這很有幫助。

## 客戶歷程流程

前往 [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). 按一下 **全部允許**.

![DSN](./images/web8.png)

按一下畫面左上角的Adobe標誌圖示，開啟設定檔檢視器。

![示範](./images/pv1.png)

請檢視設定檔檢視器面板和即時客戶設定檔，其中包含 **EXPERIENCE CLOUDID** 作為此目前未知客戶的主要識別碼。

![示範](./images/pv2.png)

您也可以檢視根據客戶行為收集的所有體驗事件。 清單目前是空的，但很快就會變更。

![示範](./images/pv3.png)

前往 **應用程式服務** 功能表選項並按一下產品 **Real-Time CDP**.

![示範](./images/pv4.png)

然後您會看到產品詳細資訊頁面。 型別的體驗事件 **產品檢視** 現在已使用您在模組1中檢閱的Web SDK實作傳送至Adobe Experience Platform。 開啟「設定檔檢視器」面板，並檢視 **體驗事件**.

![示範](./images/pv5.png)

前往 **應用程式服務** 功能表選項並按一下產品 **Adobe Journey Optimizer**. 另一個體驗事件已傳送至Adobe Experience Platform。

![示範](./images/pv7.png)

開啟「設定檔檢視器」面板。 您現在會看到2個型別的體驗事件 **產品檢視**. 雖然行為是匿名的，但每次點選都會受到追蹤並儲存在Adobe Experience Platform中。 一旦知道匿名客戶，我們就可以自動將所有匿名行為合併到已知設定檔。

![示範](./images/pv8.png)

現在來分析您的客戶設定檔，然後使用您的行為在網站上個人化您的客戶體驗。

下一步： [1.2將您自己的即時客戶設定檔視覺化 — UI](./ex2.md)

[返回使用者流程1](./uc1.md)

[返回所有模組](../../overview.md)
