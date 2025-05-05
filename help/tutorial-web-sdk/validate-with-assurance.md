---
title: 使用Experience Platform保證驗證Web SDK實作
description: 了解如何使用 Adob​​e Experience Platform Assurance 驗證您的 Platform Web SDK 實施。本課程是「使用 Web SDK 實施 Adob​​e Experience Cloud」教學課程的一部分。
feature: Web SDK,Tags,Assurance
jira: KT-15406
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 7%

---

# 使用Experience Platform保證驗證Web SDK實作

Adobe Experience Platform保證功能可協助您檢查、證明、模擬及驗證您如何收集資料或提供體驗。 深入瞭解[Adobe保證](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/assurance/home)。


## 學習目標

在本課程結束時，您將能夠：

* 啟動保證工作階段
* 檢視傳送至平台或從平台Edge Network傳送的請求

## 先決條件

您熟悉資料收集標籤和[Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}，並已完成教學課程中先前的課程：

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

每次在Adobe Experience Platform Debugger中啟用Edge追蹤時，保證工作階段都會在背景啟動。

在Debugger課程中檢閱我們的做法：

1. 移至[Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html)，然後使用偵錯工具來[將網站上的標籤屬性切換為您自己的開發屬性](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. 在&#x200B;**[!UICONTROL Experience Platform偵錯工具]**&#x200B;的左側導覽中，選取&#x200B;**[!UICONTROL 記錄檔]**
1. 選取&#x200B;**[!UICONTROL Edge]**&#x200B;索引標籤，然後選取&#x200B;**[!UICONTROL 連線]**

   ![連線Edge追蹤](assets/analytics-debugger-edgeTrace.png)
1. 啟用Edge追蹤後，您會在頂端看到外寄連結圖示。 選取圖示以開啟「保證」。

   ![啟動保證工作階段](assets/validate-debugger-start-assurnance.png)

1. 隨即開啟新的瀏覽器索引標籤，其中包含Assurance介面。

### 從保證介面啟動保證工作階段

1. 開啟[資料收集介面](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. 在左側導覽中選取保證
1. 選取建立工作階段
   ![建立保證工作階段](assets/assurance-create-session.png)
1. 選取開始
1. 為工作階段命名，例如`Luma Web SDK validation`
1. 作為&#x200B;**[!UICONTROL 基底URL]**，請輸入`https://luma.enablementadobe.com/`
   ![命名保證工作階段](assets/assurance-name-session.png)
1. 在下一個畫面中，選取&#x200B;**[!UICONTROL 複製連結]**
1. 選取圖示以將連結複製到剪貼簿
1. 在瀏覽器中貼上URL，這會使用特殊的URL引數`adb_validation_sessionid`開啟Luma網站並啟動工作階段
1. 在Assurance介面中，您應該會看到一則訊息，指出您已成功連線至工作階段，而且您應該會看到在Assurance介面中擷取的事件。
   ![保證工作階段已連線](assets/assurance-success.png)

## 驗證Web SDK實作的目前狀態

在實施的這個階段，可檢視的資訊有限。 我們可以看到您在PlatformEdge Network上產生的Experience CloudID (ECID)值：

1. 選取事件名稱為`Alloy Response Handle`的列。
1. 功能表會顯示在右側。 選取`[!UICONTROL ACPExtensionEventData]`旁邊的`+`符號
1. 選取`[!UICONTROL payload > 0 > payload > 0 > namespace]`以深入研究。 最後`0`下方顯示的ID對應至`ECID`。 您知道值顯示在`namespace`下符合`ECID`

   ![保證驗證ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >由於視窗的寬度，您可能會看到截斷的ECID值。 只要選取介面中的操作框列，然後向左拖曳即可檢視整個ECID。

在未來的課程中，您會使用「保證」，驗證到達在資料流中啟用的Adobe應用程式的完全處理負載。

現在頁面上會引發XDM物件，且您已瞭解如何驗證您的資料收集，您就可以使用Platform Web SDK設定Experience Platform和個別Adobe應用程式了。

[下一步： ](setup-experience-platform.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)上分享
