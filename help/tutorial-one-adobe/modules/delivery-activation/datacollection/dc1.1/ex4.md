---
title: 基礎 — Adobe Experience Platform Data Collection設定和Web SDK擴充功能 — 使用者端Web Data Collection
description: 基礎 — Adobe Experience Platform Data Collection設定和Web SDK擴充功能 — 使用者端Web Data Collection
kt: 5342
doc-type: tutorial
exl-id: 6ba82c35-1087-45c5-85a3-8bca7408cfec
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 1.1.4使用者端Web資料收集

## 驗證請求中的資料

### 安裝Adobe Experience Platform Debugger

Experience Platform Debugger是適用於Chrome和Firefox瀏覽器的擴充功能，可協助您檢視在網頁中實作的Adobe技術。 安裝您偏好瀏覽器的版本：

- [Firefox擴充功能](https://addons.mozilla.org/zh-TW/firefox/addon/adobe-experience-platform-dbg/)

- [Chrome擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

如果您從未使用過Debugger，而且此版本與舊版Adobe Experience Cloud Debugger不同，建議您觀看此5分鐘概觀影片：

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

鑑於您將會以無痕模式載入示範網站，您必須確定Experience Platform Debugger也可在無痕模式中使用。 若要這麼做，請在瀏覽器中前往&#x200B;**chrome://extensions**，然後開啟Experience Platform Debugger擴充功能。

確認已啟用這2個設定：

- 開發人員模式
- 允許無痕存取

![EXP新聞首頁](./images/ext1.png)

### 開啟示範網站

移至[https://dsn.adobe.com](https://dsn.adobe.com)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案上的3個點&#x200B;**...**，然後按一下&#x200B;**執行**&#x200B;以開啟它。

![DSN](./images/web8.png)

然後您會看到示範網站已開啟。 選取URL並將其複製到剪貼簿。

![DSN](./../../../getting-started/gettingstarted/images/web3.png)

開啟新的無痕瀏覽器視窗。

![DSN](./../../../getting-started/gettingstarted/images/web4.png)

貼上您在上一步中複製的示範網站URL。 接著，系統會要求您使用Adobe ID登入。

![DSN](./../../../getting-started/gettingstarted/images/web5.png)

選取您的帳戶型別並完成登入程式。

![DSN](./../../../getting-started/gettingstarted/images/web6.png)

接著，您會在無痕瀏覽器視窗中看到您的網站已載入。 對於每個示範，您都需要使用全新的無痕瀏覽器視窗來載入您的示範網站URL。

![DSN](./../../../getting-started/gettingstarted/images/web7.png)

### 使用Experience Platform Debugger檢視前往Edge的呼叫

請確定您已開啟示範網站，然後按一下Experience Platform Debugger擴充功能圖示。

![EXP新聞首頁](./images/ext2.png)

Debugger將會開啟，顯示在Adobe Experience Platform資料收集屬性中建立的實作詳細資料。 請記住，您正在偵錯剛編輯的擴充功能和規則。

按一下右上角的&#x200B;**[!UICONTROL 登入]**&#x200B;按鈕以進行驗證。 如果您已有使用Adobe Experience Platform資料收集介面開啟的瀏覽器索引標籤，驗證步驟將自動完成，您不必再次輸入使用者名稱和密碼。

![AEP偵錯工具](./images/validate2.png)

接著，您就會登入Debugger。

![AEP偵錯工具](./images/validate2ab.png)

按一下示範網站上的重新載入按鈕，將偵錯工具連線至該特定標籤。

![AEP偵錯工具](./images/validate2a.png)

確認Debugger已&#x200B;**[!UICONTROL 連線至首頁]** （如上圖所示），然後按一下&#x200B;**[!UICONTROL 鎖定]**&#x200B;圖示將Debugger鎖定至示範網站。 若您未這麼做，Debugger會持續切換，以公開任何焦點瀏覽器標籤的實作詳細資料，而造成混淆。 鎖定偵錯工具後，圖示將變更為&#x200B;**解除鎖定**。

![AEP偵錯工具](./images/validate3.png)

接著，移至示範網站上的任何頁面，例如&#x200B;**計畫**&#x200B;類別頁面。

![AEP Debugger AEP Web SDK擴充功能](./images/validate4.png)

現在請按一下左側導覽中的&#x200B;**[!UICONTROL Experience Platform Web SDK]**，檢視&#x200B;**[!UICONTROL 網路要求]**。

每個要求都包含一個&#x200B;**[!UICONTROL 事件]**&#x200B;列。

![AEP Debugger AEP Web SDK擴充功能](./images/validate5.png)

按一下以開啟&#x200B;**[!UICONTROL 事件]**&#x200B;列。 請注意您如何檢視&#x200B;**web.webpagedetails.pageViews**&#x200B;事件，以及其他遵循&#x200B;**Web SDK ExperienceEvent XDM**&#x200B;格式的現成變數。

![事件值](./images/validate8.png)

這些型別的請求詳細資訊也會顯示在網路標籤中。 篩選與&#x200B;**互動**&#x200B;的請求，以找出網頁SDK傳送的請求。 您可以在「裝載」區段中找到XDM裝載的所有詳細資訊：

![網路標籤](./images/validate9.png)

## 後續步驟

移至[1.1.5實作Adobe Analytics和Adobe Audience Manager](./ex5.md){target="_blank"}

返回[設定Adobe Experience Platform Data Collection和Web SDK標籤擴充功能](./data-ingestion-launch-web-sdk.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
