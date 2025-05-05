---
title: 使用Adobe Experience Cloud Debugger切換標籤環境
description: 瞭解如何使用Experience Cloud Debugger載入不同的標籤內嵌程式碼。 本課程屬於「在網站中實作Experience Cloud」教學課程的一部分。
exl-id: 29972a00-e5e0-4fe0-a71c-c2ca106938be
source-git-commit: 2483409b52562e13a4f557fe5bdec75b5afb4716
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 21%

---

# 使用Experience Cloud Debugger切換標籤環境

在本課程中，您將使用[Adobe Experience Platform Debugger擴充功能](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)，將[Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html)上以硬式編碼撰寫的標籤屬性取代為您自己的屬性。

此技巧稱為環境切換，您日後在自己的網站上使用標籤時，此技巧將有所幫助。 您可以在瀏覽器中載入您的生產網站，但搭配您的&#x200B;*開發*&#x200B;標籤環境。 這可讓您安心地變更及驗證標籤，而不受定期程式碼發行的影響。  畢竟，將行銷標籤發行與定期程式碼發行分開，是客戶使用標籤的主要原因之一！

>[!NOTE]
>
>Adobe Experience Platform Launch正在以資料收集技術套裝的形式整合到Adobe Experience Platform中。 此介面已推出幾項術語變更，使用此內容時請務必注意：
>
> * platform launch（使用者端）現在是&#x200B;**[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hant)**
> * platform launch伺服器端現在是&#x200B;**[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=zh-Hant)**
> * Edge設定現在是&#x200B;**[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=zh-Hant)**

## 學習目標

在本課程結束時，您將能夠：

* 使用Debugger載入替代標籤環境
* 使用Debugger驗證您已載入替代標籤環境

## 取得開發環境的 URL

1. 在您的標籤屬性中，開啟`Environments`頁面

1. 在&#x200B;**[!UICONTROL 開發]**&#x200B;列中，按一下「安裝」圖示![安裝圖示](images/launch-installIcon.png)以開啟強制回應視窗

1. 按一下「複製」圖示 ![「複製」圖示](images/launch-copyIcon.png)，將內嵌程式碼複製到剪貼簿

1. 按一下&#x200B;**[!UICONTROL 關閉]**&#x200B;以關閉強制回應視窗

   ![「安裝」圖示](images/launch-copyInstallCode.png)

## 取代Luma示範網站上的標籤URL

1. 在 Chrome 瀏覽器中開啟 [Luma 示範網站](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 按一下![Debugger圖示](images/icon-debugger.png)圖示，開啟[Experience PlatformDebugger擴充功能](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

   ![按一下 Experience Cloud Debugger 圖示](images/switchEnvironments-openDebugger.png)

1. 請注意，目前實作的標籤屬性會顯示在「摘要」標籤上

   Debugger![&#128279;](images/switchEnvironments-debuggerOnWeRetail-prod.png)中顯示的標籤環境

1. 前往「工具」標籤
1. 捲動至&#x200B;**[!UICONTROL 取代Launch內嵌程式碼]**&#x200B;區段
1. 確認顯示Luma網站的Chrome標籤成為Debugger後的焦點（而非顯示本教學課程的標籤或顯示資料收集介面的標籤）。  將剪貼簿中的內嵌程式碼貼入輸入欄位中
1. 開啟「透過luma.enablementadobe.com套用」功能，使Luma網站上的所有頁面都將對應至您的標籤屬性
1. 按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;按鈕

   Debugger![&#128279;](images/switchEnvironments-debugger-save.png)中顯示的標籤環境

1. 重新載入 Luma 網站並查看 Debugger 的「摘要」標籤。在 Launch 區段底下，現在應該會看到目前使用的是開發屬性。確認屬性名稱與您的屬性名稱一致，而且環境顯示為「開發」。

   Debugger![&#128279;](images/switchEnvironments-debuggerOnWeRetail.png)中顯示的標籤環境

>[!NOTE]
>
>每當您回到Luma網站，Debugger都會儲存此設定並取代標籤內嵌程式碼。 它不會影響您在其他已開啟的分頁中所造訪的其他網站。若要禁止Debugger取代內嵌程式碼，請在Debugger的「工具」標籤中按一下內嵌程式碼旁的&#x200B;**[!UICONTROL 移除]**&#x200B;按鈕。

繼續進行教學課程的過程中，您將使用此技巧將Luma網站對應至您自己的標籤屬性，以驗證標籤實施。 當您開始在生產環境網站上使用標籤時，可以使用相同的技巧來驗證變更。

[下堂課「新增Adobe Experience Platform Identity Service」>](id-service.md)
