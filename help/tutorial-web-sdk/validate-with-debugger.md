---
title: 使用Experience Platform偵錯工具驗證Web SDK實作
description: 了解如何使用Adobe Experience Platform Debugger驗證您的Platform Web SDK實作。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
feature: Debugger
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 5%

---

# 使用Experience Platform偵錯工具驗證Web SDK實作

了解如何使用Adobe Experience Platform Debugger驗證您的Platform Web SDK實作。

Experience Platform偵錯工具是適用於Chrome和Firefox瀏覽器的擴充功能，可協助您查看網頁中實作的Adobe技術。 下載您偏好瀏覽器的版本：

* [Firefox擴充功能](https://addons.mozilla.org/zh-TW/firefox/addon/adobe-experience-platform-dbg/)
* [Chrome擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

如果您以前從未使用過除錯程式(而且此版本與舊版Adobe Experience Cloud Debugger不同)，您可能會想要觀看此5分鐘的概述影片：

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

在本課程中，您將使用 [Adobe Experience Cloud Debugger擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) 取代 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 擁有您自己的屬性。

此技術稱為環境切換，日後當您在自己的網站上使用標籤時，此技巧將有所幫助。 您可以在瀏覽器中載入生產網站，但透過 *開發* 標籤環境。 此功能可讓您安心地變更及驗證標籤，而不受定期程式碼發行的影響。 畢竟，將行銷標籤發行與一般程式碼發行分開，是客戶最初使用標籤的主要原因之一！

## 學習目標

在本課程結束時，您將能使用除錯工具：

* 載入替代標籤程式庫
* 驗證XDM物件是否正如預期的邊緣網路擷取和傳送資料

## 先決條件

您熟悉資料收集標籤，以及 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;}，並已完成本教學課程中的下列先前課程：

* [設定權限](configure-permissions.md)
* [設定XDM結構](configure-schemas.md)
* [設定身分命名空間](configure-identities.md)
* [設定資料流](configure-datastream.md)
* [Web SDK擴充功能已安裝在標籤屬性中](install-web-sdk.md)
* [建立資料元素](create-data-elements.md)
* [建立標籤規則](create-tag-rule.md)


## 使用Debugger載入替代標籤程式庫

本教學課程使用公開托管的 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html). 開啟首頁並將其加入書籤。

![Luma首頁](assets/validate-luma-site.png)

Experience Platform偵錯工具有一項酷炫功能，可讓您將現有的標籤程式庫取代為其他標籤程式庫。 此技巧對驗證很實用，可讓我們略過本教學課程中的許多實作步驟。

1. 請確定您已開啟Luma網站，並選取Experience Platform偵錯工具擴充功能圖示
1. Debugger將會開啟並顯示硬式編碼實作的部分詳細資料，這與本教學課程無關（開啟Debugger後，您可能需要重新載入Luma網站）
1. 確認Debugger為「**[!UICONTROL 已連線至Luma]**&quot; ，然後選取「**[!UICONTROL 鎖]**」圖示，將Debugger鎖定至Luma網站。
1. 選取 **[!UICONTROL 登入]** 按鈕，然後使用您的AdobeID登入Adobe Experience Cloud。
1. 現在，請前往 **[!UICONTROL Experience Platform標籤]** 在左側導覽列中

   ![除錯工具標籤畫面](assets/validate-launch-screen.png)

1. 選取 **[!UICONTROL 設定]** 標籤
1. 右邊顯示 **[!UICONTROL 頁面內嵌程式碼]**，開啟 **[!UICONTROL 動作]** 下拉式清單，然後選取 **[!UICONTROL 取代]**

   ![選擇操作>替換](assets/validate-switch-environment.png)

1. 由於您已通過驗證，因此Debugger將提取您可用的標籤屬性和環境。 選取 `Web SDK Course` 屬性
1. 選取 `Development` 環境
1. 選取 **[!UICONTROL 套用]** 按鈕

   ![選擇替代標籤屬性](assets/validate-switch-selection.png)

1. Luma網站現在會重新載入 _搭配您的標籤屬性_.

   ![已取代標籤屬性](assets/validate-switch-success.png)

繼續本教學課程時，您會使用此技巧，將Luma網站對應至您自己的標籤屬性，以驗證您的Platform Web SDK實作。 當您開始在生產網站上使用標籤時，可以使用相同的技巧來驗證變更。

## 在Experience Platform偵錯工具中驗證實施

您可以使用Debugger驗證您的Platform Web SDK實作，並檢視傳送至Platform邊緣網路的資料：

1. 前往 **[!UICONTROL 摘要]** 在左側導覽中，查看標籤屬性的詳細資訊

   ![摘要索引標籤](assets/validate-summary.png)

1. 現在，請前往 **[!UICONTROL Experience PlatformWeb SDK]** 在左側導覽中，查看 **[!UICONTROL 網路請求]**
1. 開啟 **[!UICONTROL 事件]** 列（不要擔心此螢幕截圖顯示的請求數是否超過您的請求數，它包含來自未來課程的請求，您現在可以忽略）

   ![Adobe Experience Platform Web SDK要求](assets/validate-aep-screen.png)

1. 請注意，我們如何看到 `web.webpagedetails.pageView` 我們在 [!UICONTROL 傳送事件] 動作，以及其他現成可用的變數。 `AEP Web SDK ExperienceEvent Mixin` 格式

   ![事件詳細資料](assets/validate-event-pageViews.png)

1. 向下捲動至 `web` 對象，選擇以開啟它並檢查 `webPageDetails.name`, `webPageDetails.server`，和 `webPageDetails.siteSection`. 它們應符合首頁上對應的digitalData資料層變數

   ![網路標籤](assets/validate-xdm-content.png)

您也可以驗證「身分對應」詳細資訊：

1. 使用 `test@adobe.com`/`test` 憑證登入 Luma 網站

1. 返回 [Luma 首頁](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 開啟 **[!UICONTROL Experience PlatformWeb SDK]** 區段

   ![Debugger中的Web SDK](assets/identity-debugger-websdk-dark.png)

1. 選取 **[!UICONTROL 事件]** 開啟快顯視窗中的詳細資訊的列

   ![Debugger中的Web SDK](assets/identity-deugger-websdk-event-dark.png)

1. 搜尋 **identityMap** 在快顯視窗中。 在這裡，您應該看到 `lumaCrmId` 使用authenticatedState、id和primary的三個索引鍵：
   ![Debugger中的Web SDK](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)


## 使用瀏覽器開發工具進行驗證

瀏覽器的網頁開發人員工具中也會顯示這些類型的請求詳細資料 **網路** 標籤（假設網站載入您的標籤庫）。

1. 開啟瀏覽器的網頁開發人員工具 **網路** 標籤並重新載入頁面。 篩選呼叫，並搭配 `/ee` 若要找出呼叫，請選取該呼叫，然後查看 **標題** 標籤，和 **裝載** 標籤

   ![網路標籤](assets/validate-dev-console.png)

1. 前往 **回應** 標籤，並注意回應中ECID值的包含方式。 複製此值，如同您將在下一個練習中使用它來驗證設定檔資訊一樣

   ![網路標籤](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   >    您可能看不到與上方螢幕擷取中相同的裝載請求數量。 這種差距是因為未來 [設定Target](setup-target.md) 在螢幕截圖拍攝時完成。 你暫時可以忽略這一差異。

現在頁面上會觸發XDM物件，且您熟悉如何驗證資料收集，因此可以使用Platform Web SDK設定個別Adobe應用程式。

[下一個： ](setup-experience-platform.md)

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
