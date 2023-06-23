---
title: Bootcamp — 混合實體和數位 — 使用行動應用程式並觸發信標專案
description: Bootcamp — 混合實體和數位 — 使用行動應用程式並觸發信標專案
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: c33c973b-db8a-49ce-bd6c-a6c4fbe579a0
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# 3.1使用行動應用程式並觸發信標專案

## 安裝行動應用程式

安裝應用程式之前，您需要啟用 **追蹤** 在您的iOS裝置上。 若要這麼做，請前往 **設定** > **隱私權與安全性** > **追蹤** 並確保選項 **允許應用程式要求追蹤**.

![DSN](./../uc3/images/app4.png)

前往Apple App Store並搜尋 `aepmobile-bootcamp`. 按一下 **安裝** 或 **下載**.

![DSN](./../uc3/images/app1.png)

安裝應用程式後，按一下 **開啟**.

![DSN](./../uc3/images/app2.png)

按一下&#x200B;**「確定」**。

![DSN](./../uc3/images/app9.png)

按一下 **允許**.

![DSN](./../uc3/images/app3.png)

按一下 **我同意**.

![DSN](./../uc3/images/app7.png)

按一下 **使用應用程式時允許**.

![DSN](./../uc3/images/app8.png)

按一下 **允許**.

![DSN](./../uc3/images/app5.png)

您現在位於應用程式的首頁上，可以開始瀏覽客戶歷程。

![DSN](./../uc3/images/app12.png)

## 客戶歷程流程

首先，您必須登入。 按一下「**登入**」。

![DSN](./images/app13.png)

在先前練習中建立您的帳戶後，您已在網站上看到此內容。 您現在需要重複使用您在應用程式中建立之帳戶的電子郵件地址來登入。

![示範](./images/pv1.png)

在此處輸入您在網站上使用的電子郵件地址，然後按一下 **登入**.

![DSN](./images/app14.png)

之後，您將會收到您已登入的確認訊息，而您將會收到推播通知。

![DSN](./images/app15.png)

返回應用程式中的首頁，您會看到其他功能出現。

![DSN](./images/app17.png)

首先，前往 **產品**. 在此範例中，按一下任何產品 **咖啡待用**.

![DSN](./images/app19.png)

您將會看到 **咖啡待用** 產品頁面。

![DSN](./images/app20.png)

您現在會在離線存放區位置中模擬信標專案事件。 模擬此情形的目標是在店內熒幕上個人化客戶體驗。 為了將店內體驗視覺化，已建立一個頁面，該頁面會動態顯示與剛進入商店的客戶相關的資訊。

繼續之前，請在您的電腦上開啟此網頁： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

然後您會看到以下內容：

![DSN](./images/screen1.png)

接著，返回首頁。 按一下 **beacon** 圖示。

![DSN](./images/app23.png)

然後您會看到此內容。 首先，選取 **Bootcamp畫面信標** 然後按一下 **登入** 按鈕。 這可讓您模擬信標專案。

![DSN](./images/app21.png)

現在，請檢視店內畫面。 您會在5秒內看到最後檢視的產品。

![DSN](./images/screen2.png)

然後，返回 **產品**. 在此範例中，按一下任何產品 **沙灘毯棕褐色**.

![DSN](./images/app22.png)

接著，返回首頁。 按一下 **beacon** 圖示。

![DSN](./images/app23.png)

然後您會看到此內容。 首先，選取 **Bootcamp畫面信標** 然後按一下 **登入** 按鈕。 這可讓您模擬信標專案。

![DSN](./images/app21.png)

現在，請再次檢視店內畫面。 您會在5秒內看到最後檢視的產品。

![DSN](./images/screen3.png)

我們也來瀏覽一下您網站上的設定檔檢視器。 您會看到許多新增的事件，其中只顯示系統已收集和儲存客戶的任何互動，並放入Adobe Experience Platform。

![DSN](./images/screen4.png)

在下個練習中，您將設定並測試自己的Beacon進入歷程。

下一步： [3.2建立您的活動](./ex2.md)

[返回使用者流程3](./uc3.md)

[返回所有模組](../../overview.md)
