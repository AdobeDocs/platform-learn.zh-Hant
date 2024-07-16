---
title: 設定身分名稱空間
description: 瞭解如何設定身分識別名稱空間以搭配Adobe Experience Platform Web SDK使用。 本課程是「使用 Web SDK 實施 Adob​​e Experience Cloud」教學課程的一部分。
feature: Web SDK,Identities
jira: KT-15400
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 1a4f2e3813a6db4bef77753525c8a7d40692a4b2
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 12%

---

# 設定身分名稱空間

了解如何設定身分命名空間，以配合 Adob&#x200B;&#x200B;e Experience Platform Web SDK 使用。

[Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/en/docs/id-service/using/home)會設定跨SDKAdobe應用程式的一般訪客ID (ECID)，以強化Experience Cloud功能，例如應用程式之間的受眾共用。 您也可以將自己的客戶ID傳送至此服務，以啟用跨裝置目標鎖定及與其他系統(例如客戶關係管理(CRM)系統)的整合。

[Adobe Experience Platform Identity服務](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) （是的，有兩個！） 使用ECID和客戶ID來產生身分圖表，好讓您將屬性和行為合併到即時客戶個人檔案中。

>[!NOTE]
>
>自訂身分名稱空間是&#x200B;_不需要_，才能使用Web SDK實作Adobe Analytics、Adobe Target或Adobe Audience Manager （可以在`data`物件中傳遞已驗證的身分，而非您稍後看到的`xdm`物件中）。 Journey Optimizer、Real-time Customer Data Platform、Customer Journey Analytics等平台原生應用程式需要身分識別名稱空間。 雖然您可以決定在自己的實作中不使用身分名稱空間，但您應在本教學課程中這樣做。

>[!NOTE]
>
> 為了示範，本課程中的練習會讓您使用認證，**使用者： `test@adobe.com` /密碼： test**，擷取登入[Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html)之虛擬客戶的身分詳細資訊。

## 學習目標

在本課程結束時，您將能夠：

* 瞭解身分名稱空間
* 建立自訂身分名稱空間以擷取內部CRM ID


## 先決條件

您必須已完成先前的課程：

* [設定結構描述](configure-schemas.md)

>[!IMPORTANT]
>
>實作Adobe Experience Platform Web SDK時不需要[Experience CloudID擴充功能](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension)，因為Web SDK JavaScript程式庫包含訪客ID服務功能。
>
> 如果您的網站已透過訪客API或Experience CloudID服務標籤擴充功能在網站上使用Experience CloudID服務，而且您要在移轉至Adobe Experience Platform Web SDK時繼續使用該服務，您必須使用最新版本的訪客API或Experience CloudID服務標籤擴充功能。 如需詳細資訊，請參閱[ID移轉](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview)。

## 建立身分名稱空間

在本練習中，您將為Luma的自訂身分欄位`lumaCrmId`建立身分名稱空間。 身分識別命名空間在建立即時客戶設定檔方面扮演關鍵角色，因為相同命名空間中的兩個相符值可讓兩個資料來源形成身分識別圖表。

在開始練習之前，請觀看此短片，進一步瞭解Adobe Experience Platform中的身分識別：

>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on)

現在，為Luma CRM ID建立名稱空間：

1. 開啟[資料收集介面](https://launch.adobe.com/tw/){target="_blank"}
1. 選取您用於教學課程的沙箱

   >[!NOTE]
   >
   >如果您是Real-Time CDP或Journey Optimizer等平台型應用程式的客戶，我們建議您在本教學課程中使用開發沙箱。 如果沒有，請使用&#x200B;**[!UICONTROL Prod]**&#x200B;沙箱。

1. 在左側導覽中選取&#x200B;**[!UICONTROL 身分]**
1. 選取&#x200B;**[!UICONTROL 瀏覽]**

   身分名稱空間清單會顯示在頁面的主要介面中，顯示其名稱、身分符號、上次更新日期，以及是否為標準或自訂名稱空間。 右邊欄包含有關[!UICONTROL 身分圖表強度]的資訊。

1. 選取&#x200B;**[!UICONTROL 建立身分名稱空間]**

   ![檢視身分](assets/configure-identities-screen.png)

1. 提供下列詳細資料，並選取&#x200B;**[!UICONTROL 建立]**。

   | 欄位 | 值 |
   |---------------|-----------|
   | 顯示名稱 | Luma CRM ID |
   | 身分符號 | lumaCrmId |
   | 類型 | 個人跨裝置 ID |


   ![建立命名空間](assets/identities-create-namespace.png)


   身分名稱空間會填入&#x200B;**[!UICONTROL 身分]**&#x200B;畫面中。

   ![建立命名空間](assets/configure-identities-namespace-lumaCrmId.png)


>[!NOTE]
>
> 在[建立身分](create-identities.md)課程中，您將瞭解在傳送身分給PlatformEdge Network時如何使用此名稱空間。

現在身分已準備就緒，可以設定資料流。

[下一步： ](configure-datastream.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)上分享
