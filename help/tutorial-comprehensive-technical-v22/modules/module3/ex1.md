---
title: Foundation — 即時客戶設定檔 — 從網站上的未知到已知
description: Foundation — 即時客戶設定檔 — 從網站上的未知到已知
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 065d79c5-8979-4992-afb1-4da47bbff74b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 2%

---

# 3.1從網站上的未知到已知

## 內容

從未知到已知的歷程是現今品牌中最重要的主題之一，客戶從贏取到保留的歷程亦然。

Adobe Experience Platform在這段歷程中扮演著重要角色。 平台是溝通的大腦，「經驗記錄系統」。

Platform是一種環境，在這種環境中，客戶一詞比已知客戶更廣。 從Platform的角度來看，網站上的未知訪客也是客戶，因此，作為未知訪客的所有行為也會傳送至Platform。 有了這種方法，當此訪客最終成為已知客戶時，品牌也可以將那一刻之前發生的情形加以視覺化。 這從歸因和體驗最佳化的觀點來說，有所幫助。

## 客戶歷程流程

前往 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). 使用您的Adobe ID登入後，您會看到這個。 按一下您的網站專案以開啟。

![DSN](../module0/images/web8.png)

在 **Screens** 頁面，按一下 **執行**.

![DSN](../module1/images/web2.png)

然後，您會看到示範網站已開啟。 選取URL並複製到剪貼簿。

![DSN](../module0/images/web3.png)

開啟新的無痕瀏覽器窗口。

![DSN](../module0/images/web4.png)

貼上您在上一步複製的示範網站URL。 然後系統會要求您使用Adobe ID登入。

![DSN](../module0/images/web5.png)

選取您的帳戶類型並完成登入程式。

![DSN](../module0/images/web6.png)

然後，您會在無痕瀏覽器視窗中看到您的網站載入。 對於每個演示，您都需要使用全新的無痕瀏覽器窗口來載入演示網站URL。

![DSN](../module0/images/web7.png)

按一下螢幕左上角的Adobe標誌圖示，開啟「設定檔檢視器」。

![示範](../module2/images/pv1.png)

查看「設定檔檢視器」面板和「即時客戶設定檔」，其中 **Experience CloudID** 作為此目前未知客戶的主要識別碼。

![示範](../module2/images/pv2.png)

您也可以查看根據客戶行為收集的所有體驗事件。 清單目前為空白，但很快就會變更。

![示範](../module2/images/pv3.png)

前往 **男性** 產品類別。 下一步，按一下產品 **蒙大拿風衣**.

![示範](../module2/images/pv4.png)

然後您會看到產品詳細資料頁面。 類型的體驗事件 **產品檢視** 現已透過您在模組1中檢閱的Web SDK實作，傳送至Adobe Experience Platform。

![示範](../module2/images/pv5.png)

開啟「Provile Viewer（配置查看器）」面板，並查看您的 **體驗事件**.

![示範](../module2/images/pv6.png)

返回 **女性** 類別頁面，然後按一下其他產品。 已將另一個體驗事件傳送至Adobe Experience Platform。

![示範](../module2/images/pv7.png)

開啟「配置檔案查看器」面板。 您現在會看到2個類型的體驗事件 **產品檢視**. 雖然行為是匿名的，但我們可以追蹤每次點按，並將其儲存在Adobe Experience Platform中。 一旦匿名客戶成為已知客戶，我們就能自動將所有匿名行為合併到已知的設定檔。

![示範](../module2/images/pv8.png)

前往註冊/登入頁面。 按一下 **建立帳戶**.

![示範](../module2/images/pv9.png)

填寫詳細資訊，然後按一下 **註冊** 之後，系統會將您重新導向至上一頁。

![示範](../module2/images/pv10.png)

開啟「設定檔檢視器」面板，然後前往「即時客戶設定檔」。 在「設定檔檢視器」面板上，您應該會看到所有個人資料顯示，例如新新增的電子郵件和電話識別碼。

![示範](../module2/images/pv11.png)

在「設定檔檢視器」面板上，前往「體驗事件」。 您會在「設定檔檢視器」面板上看到之前檢視的2項產品。 這兩個事件現在也會連線至您的「已知」設定檔。

![示範](../module2/images/pv12.png)

您現在已將資料內嵌至Adobe Experience Platform，並將該資料連結至ECID和電子郵件地址之類的識別碼。 其目標是要了解您要做的事情的商業背景。 在下一個練習中，您將開始設定所有必要項目，讓所有資料擷取皆可進行。

### 導覽行動應用程式

成為已知客戶後，該開始使用行動應用程式了。 在iPhone上開啟行動應用程式，然後登入應用程式。

如果您尚未安裝應用程式，或者您不記得如何安裝應用程式，請查看以下內容： [0.5使用行動應用程式](../module0/ex5.md)

依照指示安裝應用程式後，您會看到載入了Luma品牌的應用程式登陸頁面。 按一下畫面左上角的帳戶圖示。

![示範](./images/app_hp.png)

在「登入」畫面中，使用您在案頭網站上使用的電子郵件地址登入。 按一下「**登入**」。

![示範](./images/app_acc.png)

前往應用程式的主畫面，然後按一下以開啟任何產品。

![示範](./images/app_hp.png)

然後您會看到產品詳細資料頁面。

![示範](./images/app_carst.png)

前往應用程式的主畫面，然後向左滑動畫面以檢視「設定檔檢視器」面板。 之後，您就會在 **體驗事件** 區段，以及之前網站工作階段中的所有產品檢視。

![示範](./images/app_after_carst.png)

現在，返回您的台式電腦並重新整理首頁，之後您也會看到產品出現在該處。

![示範](./images/lb_x_aftermobile.png)

您現在已將資料內嵌至Adobe Experience Platform，並將該資料連結至ECID和電子郵件地址之類的識別碼。 本練習的目的是了解您要做的事情的商業背景。 您現在已有效建立即時的跨裝置客戶個人檔案。 在下一個練習中，您將在Adobe Experience Platform中將您的設定檔視覺化。

下一步： [3.2將您自己的即時客戶設定檔視覺化 — UI](./ex2.md)

[返回模組3](./real-time-customer-profile.md)

[返回所有模組](../../overview.md)
