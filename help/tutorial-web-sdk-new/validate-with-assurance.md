---
title: 使用Experience Platform保證驗證Web SDK實作
description: 瞭解如何使用Adobe Experience Platform保證驗證您的Platform Web SDK實作。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
feature: Web SDK,Tags,Assurance
source-git-commit: 4361d8e688ff2c2f3b5472f2cfff246efa627c7f
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# 使用Experience Platform保證驗證Web SDK實作


## 啟動保證工作階段

Adobe Experience Platform保證是Adobe Experience Cloud的產品，可協助您檢查、證明、模擬及驗證您如何收集資料或提供體驗。

深入瞭解 [Adobe保證](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).

每次啟用Edge Trace時，系統都會在背景啟動保證工作階段。

若要檢視保證工作階段，

1. 啟用Edge Trace後，您會在頂端看到外寄連結圖示。 選取圖示以開啟「保證」。 您的瀏覽器中會開啟新標籤。

   ![啟動保證工作階段](assets/validate-debugger-start-assurnance.png)

1. 選取事件名稱為「Adobe回應控制代碼」的列。
1. 功能表會顯示在右側。 選取 `+` 在「 」旁邊簽署 `[!UICONTROL ACPExtensionEvent]`
1. 選取「 」以向下展開 `[!UICONTROL payload > 0 > payload > 0 > namespace]`. 顯示在最後一個 `0` 對應至 `ECID`. 透過下方顯示的值，您知道這一點 `namespace` 比對 `ECID`

   ![保證驗證ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >由於視窗的寬度，您可能會看到截斷的ECID值。 只要選取介面中的操作框列，然後向左拖曳即可檢視整個ECID。

在未來的課程中，您會使用「保證」，驗證到達在資料流中啟用的Adobe應用程式的完全處理負載。

現在頁面上會引發XDM物件，且您已瞭解如何驗證您的資料收集，您就可以使用Platform Web SDK設定個別Adobe應用程式了。