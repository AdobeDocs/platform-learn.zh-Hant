---
title: 基礎 — 即時客戶設定檔 — 從未知到網站上已知
description: 基礎 — 即時客戶設定檔 — 從未知到網站上已知
kt: 5342
doc-type: tutorial
exl-id: f33a7448-e1b9-47e7-97c7-509ad36cf991
source-git-commit: 2264f26a0778c2570c36abe1bae4d6a1dc3a465c
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# 2.1.1從未知到網站上已知

## 內容

從未知到已知的歷程是這些天品牌中最重要的主題之一，就像客戶從贏取到保留的歷程。

Adobe Experience Platform在此歷程中擔當著重要角色。 Platform是溝通的大腦，「體驗記錄系統」。

Platform是一種環境，其中客戶一詞的含義比已知客戶更為廣泛。 在網站上的未知訪客也是Platform視角下的客戶，因此，作為未知訪客的所有行為也會傳送到Platform。 由於這種方法，當此訪客最終成為已知客戶時，品牌也可以將當下所發生的事情視覺化。 從歸因和體驗最佳化的角度來看，這很有幫助。

## 客戶歷程流程

移至[https://dsn.adobe.com](https://dsn.adobe.com)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案上的3個點&#x200B;**...**，然後按一下&#x200B;**執行**&#x200B;以開啟它。

![DSN](./../../datacollection/dc1.1/images/web8.png)

然後您會看到示範網站已開啟。 選取URL並將其複製到剪貼簿。

![DSN](../../../getting-started/gettingstarted/images/web3.png)

開啟新的無痕瀏覽器視窗。

![DSN](../../../getting-started/gettingstarted/images/web4.png)

貼上您在上一步中複製的示範網站URL。 接著，系統會要求您使用Adobe ID登入。

![DSN](../../../getting-started/gettingstarted/images/web5.png)

選取您的帳戶型別並完成登入程式。

![DSN](../../../getting-started/gettingstarted/images/web6.png)

接著，您會在無痕瀏覽器視窗中看到您的網站已載入。 每次練習都需要使用全新的無痕瀏覽器視窗，才能載入您的示範網站URL。

![DSN](../../../getting-started/gettingstarted/images/web7.png)

按一下畫面左上角的Adobe標誌圖示，開啟設定檔檢視器。

![示範](../../datacollection/dc1.2/images/pv1.png)

請檢視「設定檔檢視器」面板和「即時客戶設定檔」，將&#x200B;**Experience Cloud ID**&#x200B;設為此目前未知客戶的主要識別碼。

![示範](../../datacollection/dc1.2/images/pv2.png)

您也可以檢視根據客戶行為收集的所有體驗事件。 清單目前是空的，但很快就會變更。

![示範](../../datacollection/dc1.2/images/pv3.png)

移至&#x200B;**電話和裝置**&#x200B;產品類別。 接著，按一下產品&#x200B;**iPhone 16 Pro**。

![示範](../../datacollection/dc1.2/images/pv4.png)

然後您會看到產品詳細資料頁面。 型別&#x200B;**產品檢視**&#x200B;的事件現在已使用您在模組1中檢閱的Web SDK實作傳送至Adobe Experience Platform。

![示範](../../datacollection/dc1.2/images/pv5.png)

開啟[設定檔檢視器]面板，並檢視您的&#x200B;**事件**。

![示範](../../datacollection/dc1.2/images/pv6.png)

返回&#x200B;**電話和裝置**&#x200B;類別頁面，然後按一下其他產品。 另一個體驗事件已傳送至Adobe Experience Platform。 開啟設定檔檢視器面板。 您現在會看到2個型別為&#x200B;**產品檢視**&#x200B;的事件。 雖然行為是匿名的，但在獲得適當同意後，您仍可追蹤每次點按，並將其儲存在Adobe Experience Platform中。 一旦知道匿名客戶，我們就可以自動將所有匿名行為合併到知道的設定檔。

按一下&#x200B;**登入**。

![示範](../../datacollection/dc1.2/images/pv7.png)

按一下&#x200B;**建立帳戶**。

![示範](../../datacollection/dc1.2/images/pv8.png)

填寫您的詳細資料，然後按一下&#x200B;**註冊**，之後您將會被重新導向到上一頁。

![示範](../../datacollection/dc1.2/images/pv9.png)

開啟設定檔檢視器面板，然後前往即時客戶設定檔。 在「設定檔檢視器」面板上，您應該會看到所有顯示的個人資料，例如新新增的電子郵件和電話識別碼。

![示範](../../datacollection/dc1.2/images/pv10.png)

在「設定檔檢視器」面板上，前往「體驗事件」。 您將會在「設定檔檢視器」面板上看到先前檢視過的2項產品。 這兩個事件現在也都連線到您的「已知」設定檔。

![示範](../../datacollection/dc1.2/images/pv11.png)

您現在已將資料內嵌至Adobe Experience Platform，且已將該資料連結至ECID和電子郵件地址等識別碼。 此課程的目標是瞭解您打算進行的業務內容。 在下一個練習中，您將開始設定所需的一切，以讓所有資料擷取成為可能。

### 瀏覽行動應用程式

成為已知客戶後，您就可以開始使用行動應用程式。 在iPhone上開啟行動應用程式，然後登入應用程式。

如果您尚未安裝應用程式，或忘記如何安裝，請在這裡檢視： [使用行動應用程式](../../../getting-started/gettingstarted/ex5.md)

依照指示安裝應用程式後，您會看到已載入Citi Signal品牌的應用程式登陸頁面。 按一下畫面左上方的帳戶圖示。

![示範](./images/app_hpz.png)

在「登入」畫面上，使用您在案頭網站上使用的電子郵件地址登入。 按一下&#x200B;**登入**。

![示範](./images/app_acc.png)

之後，您將會收到您已登入的確認。

![示範](./images/app_acc1.png)

前往應用程式的主畫面，然後前往頁面&#x200B;**手機和裝置**。

![示範](./images/app_hp1.png)

按一下頁面上的任何產品。

![示範](./images/app_hp2.png)

然後您會看到產品詳細資料頁面。

![示範](./images/app_galaxy.png)

前往應用程式內的首頁，然後按一下Adobe圖示以檢視「設定檔檢視器」面板。 您之後會看到&#x200B;**設定檔屬性**&#x200B;檢視，其中現在會顯示您的網頁與行動應用程式活動的合併檢視。 前往&#x200B;**活動**

![示範](./images/app_hp3.png)

然後您將會在&#x200B;**體驗事件**&#x200B;區段中看到您剛才檢視的產品，以及之前網站工作階段中的所有產品檢視。

>[!NOTE]
>
>您可能需要幾分鐘時間，才會在應用程式和網站上看到整合檢視。

![示範](./images/app_after_galaxy.png)

現在返回您的桌上型電腦並重新整理首頁，之後您也會看到產品出現在那裡。

>[!NOTE]
>
>您可能需要幾分鐘時間，才會在應用程式和網站上看到整合檢視。

![示範](./images/web_x_aftermobile.png)

您現在已將資料內嵌至Adobe Experience Platform，且已將該資料連結至ECID和電子郵件地址等識別碼。 此練習的目標是瞭解您打算做什麼的業務環境。 您現在已有效建立即時、跨裝置客戶設定檔。 在下一個練習中，您將會繼續並在Adobe Experience Platform中視覺化您的設定檔。

## 後續步驟

移至[2.1.2視覺化您自己的即時客戶設定檔 — UI](./ex2.md){target="_blank"}

返回[即時客戶個人檔案](./real-time-customer-profile.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
