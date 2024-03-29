---
title: 使用Experience Platform保證驗證Web SDK實作
description: 瞭解如何使用Adobe Experience Platform保證驗證您的Platform Web SDK實作。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
feature: Web SDK,Tags,Assurance
source-git-commit: fd366a4848c2dd9e01b727782e2f26005a440725
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 2%

---

# 使用Experience Platform保證驗證Web SDK實作

Adobe Experience Platform保證是Adobe Experience Cloud的產品，可協助您檢查、證明、模擬及驗證您如何收集資料或提供體驗。 深入瞭解 [Adobe保證](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).


## 學習目標

在本課程結束時，您將能夠：

* 啟動保證工作階段
* 檢視傳送至Platform Edge Network及從中傳送的請求

## 先決條件

您熟悉資料收集標籤和 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 並完成本教學課程中的先前課程：

* [設定XDM結構描述](configure-schemas.md)
* [設定身分名稱空間](configure-identities.md)
* [設定資料流](configure-datastream.md)
* [安裝在標籤屬性中的Web SDK擴充功能](install-web-sdk.md)
* [建立資料元素](create-data-elements.md)
* [建立身分](create-identities.md)
* [建立標籤規則](create-tag-rule.md)
* [使用Debugger進行驗證](validate-with-debugger.md)


## 開始並檢視保證工作階段

有幾種方式可以啟動保證工作階段。

### 在Debugger中啟動保證工作階段

每次在Adobe Experience Platform Debugger中啟用邊緣追蹤時，保證工作階段都會在背景啟動。

在Debugger課程中檢閱我們的做法：

1. 前往 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 並使用除錯工具 [將網站上的tag屬性切換為您自己的開發屬性](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 在左側導覽列中 **[!UICONTROL Experience Platform偵錯工具]** 選取 **[!UICONTROL 記錄檔]**
1. 選取 **[!UICONTROL Edge]** 標籤，然後選取 **[!UICONTROL 連線]**

   ![連線邊緣追蹤](assets/analytics-debugger-edgeTrace.png)
1. 啟用Edge Trace後，您會在頂端看到外寄連結圖示。 選取圖示以開啟「保證」。 您的瀏覽器中會開啟新標籤。

   ![啟動保證工作階段](assets/validate-debugger-start-assurnance.png)


### 從保證介面啟動保證工作階段

1. 開啟 [資料收集介面](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. 在左側導覽中選取保證
1. 選取建立工作階段
1. 選取開始
1. 為工作階段命名，例如， `Luma Web SDK validation`
1. 作為 **[!UICONTROL 基礎URL]** 進入 `https://luma.enablementadobe.com/`
1. 在下一個畫面，選取 **[!UICONTROL 複製連結]**
1. 選取圖示以將連結複製到剪貼簿
1. 在瀏覽器中貼上URL，這會使用特殊的URL引數開啟Luma網站 `adb_validation_sessionid` 並啟動工作階段
1. 在Assurance介面中，您應該會看到一則訊息，指出您已成功連線至工作階段，而且您應該會看到在Assurance介面中擷取的事件。

## 驗證Web SDK實作的目前狀態

在實施的這個階段，可檢視的資訊有限。 我們可以看到您在Platform Edge Network上產生的Experience CloudID (ECID)值：

1. 選取事件名稱為「Adobe回應控制代碼」的列。
1. 功能表會顯示在右側。 選取 `+` 在「 」旁邊簽署 `[!UICONTROL ACPExtensionEvent]`
1. 選取「 」以向下展開 `[!UICONTROL payload > 0 > payload > 0 > namespace]`. 顯示在最後一個 `0` 對應至 `ECID`. 透過下方顯示的值，您知道這一點 `namespace` 比對 `ECID`

   ![保證驗證ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >由於視窗的寬度，您可能會看到截斷的ECID值。 只要選取介面中的操作框列，然後向左拖曳即可檢視整個ECID。

在未來的課程中，您會使用「保證」，驗證到達在資料流中啟用的Adobe應用程式的完全處理負載。

現在頁面上會引發XDM物件，且您已瞭解如何驗證您的資料收集，您就可以使用Platform Web SDK設定個別Adobe應用程式了。

[下一步： ](setup-experience-platform.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)