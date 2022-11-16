---
title: 使用Adobe Experience Cloud Debugger切換標籤環境
description: 了解如何使用Experience Cloud Debugger載入不同的標籤內嵌程式碼。 本課程屬於「在網站中實作Experience Cloud」教學課程的一部分。
exl-id: 29972a00-e5e0-4fe0-a71c-c2ca106938be
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 36%

---

# 使用Experience Cloud Debugger切換標籤環境

在本課程中，您將使用 [Adobe Experience Cloud Debugger擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) 取代 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 擁有您自己的屬性。

此技術稱為環境切換，日後當您在自己的網站上使用標籤時，此技巧將有所幫助。 您可以在瀏覽器中載入生產網站，但透過 *開發* 標籤環境。 這可讓您安心地變更及驗證標籤，而不受一般程式碼發行的影響。  畢竟，將行銷標籤發行與一般程式碼發行分開，是客戶最初使用標籤的主要原因之一！

>[!NOTE]
>
>Adobe Experience Platform Launch已整合至Adobe Experience Platform，為資料收集技術的套件。 介面中已推出數個術語變更，在使用此內容時應注意：
>
> * platform launch（用戶端）現在為 **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)**
> * platform launch伺服器端現在是 **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * 現在提供邊緣設定 **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**


## 學習目標

在本課程結束時，您將能夠：

* 使用Debugger載入替代標籤環境
* 使用Debugger驗證您已載入替代標籤環境

## 取得開發環境的 URL

1. 在您的標籤屬性中，開啟 `Environments` 頁面

1. 在&#x200B;**[!UICONTROL 開發]**&#x200B;列中，按一下「安裝」圖示 ![「安裝」圖示](images/launch-installIcon.png)，開啟強制回應視窗

1. 按一下「複製」圖示 ![「複製」圖示](images/launch-copyIcon.png)，將內嵌程式碼複製到剪貼簿

1. 按一下&#x200B;**[!UICONTROL 關閉]**&#x200B;以關閉強制回應視窗

   ![「安裝」圖示](images/launch-copyInstallCode.png)

## 取代Luma示範網站上的標籤URL

1. 在 Chrome 瀏覽器中開啟 [Luma 示範網站](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 按一下 [Debugger 圖示](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) 圖示，開啟 ![Experience Cloud Debugger 擴充功能](images/icon-debugger.png)

   ![按一下 Experience Cloud Debugger 圖示](images/switchEnvironments-openDebugger.png)

1. 請注意，目前實作的標籤屬性會顯示在「摘要」標籤上

   ![Debugger中顯示的標籤環境](images/switchEnvironments-debuggerOnWeRetail-prod.png)

1. 前往「工具」標籤
1. 捲動至&#x200B;**[!UICONTROL 取代 Launch 內嵌程式碼]**&#x200B;區段
1. 確認顯示Luma網站的Chrome分頁在Debugger後面顯示（而非顯示本教學課程的分頁或顯示資料收集介面的分頁）。  將剪貼簿中的內嵌程式碼貼入輸入欄位中
1. 開啟「在luma.enablementadobe.com之間套用」功能，讓Luma網站上的所有頁面都對應至您的標籤屬性
1. 按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;按鈕

   ![Debugger中顯示的標籤環境](images/switchEnvironments-debugger-save.png)

1. 重新載入 Luma 網站並查看 Debugger 的「摘要」標籤。在 Launch 區段底下，現在應該會看到目前使用的是開發屬性。確認屬性名稱與您的屬性名稱一致，而且環境顯示為「開發」。

   ![Debugger中顯示的標籤環境](images/switchEnvironments-debuggerOnWeRetail.png)

>[!NOTE]
>
>每當您回到Luma網站，Debugger都會儲存此設定並取代標籤內嵌程式碼。 它不會影響您在其他已開啟的分頁中所造訪的其他網站。若要禁止 Debugger 取代內嵌程式碼，請在 Debugger 的「工具」標籤中按一下內嵌程式碼旁的&#x200B;**[!UICONTROL 移除]**&#x200B;按鈕。

繼續本教學課程時，您將會使用此技巧，將Luma網站對應至您自己的標籤屬性，以驗證您的標籤實作。 當您開始在生產網站上使用標籤時，可以使用相同的技巧來驗證變更。

[下堂課「新增 Adobe Experience Platform Identity Service」>](id-service.md)
