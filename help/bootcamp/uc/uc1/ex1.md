---
title: Bootcamp — 即時客戶設定檔 — 從未知到網站上已知
description: Bootcamp — 即時客戶設定檔 — 從未知到網站上已知
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 32a084a3-4c04-4367-947e-f7151fdad73b
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# 1.1從未知到網站上已知

## 內容

從未知到已知的歷程是這些天品牌中最重要的主題之一，就像客戶從贏取到保留的歷程。

Adobe Experience Platform在此歷程中擔當著重要角色。 Platform是通訊的大腦，亦即&#x200B;**記錄體驗系統**。

Platform是一種環境，其中客戶一詞的含義比已知客戶更為廣泛。 在網站上的未知訪客也是Platform視角下的客戶，因此，作為未知訪客的所有行為也會傳送到Platform。 由於這種方法，當此訪客最終成為已知客戶時，品牌也可以將當下所發生的事情視覺化。 從歸因和體驗最佳化的角度來看，這很有幫助。

## 客戶歷程流程

移至[https://bootcamp.aepdemo.net](https://publish9122.adobedemo.com/content/aep-bootcamp-experience/language-masters/en.html)。 按一下&#x200B;**全部允許**。

![DSN](./images/web8.png)

按一下畫面左上角的Adobe標誌圖示，開啟設定檔檢視器。

![示範](./images/pv1.png)

請檢視「設定檔檢視器」面板，以及將&#x200B;**Experience CloudID**&#x200B;作為目前未知客戶主要識別碼的即時客戶設定檔。

![示範](./images/pv2.png)

您也可以檢視根據客戶行為收集的所有體驗事件。 清單目前是空的，但很快就會變更。

![示範](./images/pv3.png)

移至&#x200B;**應用程式服務**&#x200B;功能表選項，然後按一下產品&#x200B;**Real-Time CDP**。

![示範](./images/pv4.png)

然後您會看到產品詳細資料頁面。 型別&#x200B;**產品檢視**&#x200B;的體驗事件現在已使用您在模組1中檢閱的Web SDK實作傳送至Adobe Experience Platform。 開啟「設定檔檢視器」面板，並檢視您的&#x200B;**體驗事件**。

![示範](./images/pv5.png)

移至&#x200B;**應用程式服務**&#x200B;功能表選項，然後按一下產品&#x200B;**Adobe Journey Optimizer**。 另一個體驗事件已傳送至Adobe Experience Platform。

![示範](./images/pv7.png)

開啟設定檔檢視器面板。 您現在會看到2個型別為&#x200B;**產品檢視**&#x200B;的體驗事件。 雖然行為是匿名的，但每次點按都會受到追蹤並儲存在Adobe Experience Platform中。 一旦知道匿名客戶，我們就可以自動將所有匿名行為合併到知道的設定檔。

![示範](./images/pv8.png)

現在來分析您的客戶設定檔，然後使用您的行為來個人化您在網站上的客戶體驗。

下一步： [1.2視覺化您自己的即時客戶設定檔 — UI](./ex2.md)

[返回使用者流程1](./uc1.md)

[返回所有模組](../../overview.md)
