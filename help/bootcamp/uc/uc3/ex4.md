---
title: Bootcamp — 混合實體和數位 — 測試您的歷程
description: Bootcamp — 混合實體和數位 — 測試您的歷程
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 45c77177-9ea9-4c3d-a40e-c04a747938eb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# 3.4測試您的歷程

若要測試您的歷程，必須使用練習3.2中建立之事件的事件ID，如下所示。

![ACOP](./images/payloadeventID.png)

事件ID是必須傳送至Adobe Experience Platform才能觸發歷程的專案。 在此範例中，eventID為：
`e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5`。

開啟行動應用程式，然後前往首頁。 按一下&#x200B;**設定**&#x200B;圖示。

![DSN](./images/appsett.png)

將您的eventID貼到欄位&#x200B;**Beacon EventID**，然後按一下&#x200B;**儲存**。

![DSN](./images/beacon1.png)

繼續之前，請在您的電腦上開啟此網頁： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

然後您會看到以下內容：

![DSN](./images/screen1.png)

接著，返回首頁。 按一下&#x200B;**信標**&#x200B;圖示。

![DSN](./images/app23.png)

您將會看到此訊息。 首先，選取&#x200B;**Bootcamp熒幕信標**，然後按一下&#x200B;**專案**&#x200B;按鈕。 這可讓您模擬信標專案。

![DSN](./images/app21.png)

現在，請檢視店內畫面。 您會在5秒內看到最後檢視的產品。

![DSN](./images/beacon3.png)

您也會收到推播通知。

![DSN](./images/beacon2.png)

您現在已經完成此練習。

[返回使用者流程3](./uc3.md)

[返回所有模組](../../overview.md)
