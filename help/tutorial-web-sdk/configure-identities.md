---
title: 設定身分命名空間
description: 了解如何設定身分識別命名空間以與Adobe Experience Platform Web SDK搭配使用。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
feature: Identities
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 6%

---

# 設定身分命名空間

了解如何設定身分識別命名空間以與Adobe Experience Platform Web SDK搭配使用。

此 [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html) 設定所有Adobe解決方案的通用訪客ID，以便支援Experience Cloud功能，例如解決方案之間的受眾共用。 您也可以將自己的客戶ID傳送至服務，以啟用跨裝置鎖定目標以及與其他系統(例如您的客戶關係管理(CRM)系統)的整合。

如果您的網站已在網站上使用Experience CloudID服務(透過訪客API或Experience CloudID服務標籤擴充功能)，而您想在移轉至Adobe Experience Platform Web SDK時繼續使用，則必須使用最新版的訪客API或Experience CloudID服務標籤擴充功能。 請參閱 [ID移轉](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en) 以取得更多資訊。

>[!NOTE]
>
> 為了示範，本課程中的練習可讓您擷取登入之虛構客戶的身分詳細資料 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 使用憑證， **使用者：test@adobe.com /密碼：測試**. 雖然您可以使用這些步驟建立不同的身分以供您自行使用，但若要了解「資料收集」介面中的「身分對應」功能，建議您先依照這些步驟來擷取範例身分。

## 學習目標

在本課程結束時，您將能夠：

* 了解身分識別命名空間
* 建立自訂身分命名空間以擷取內部CRM ID


## 先決條件

您必須已完成先前的課程：

* [設定權限](configure-permissions.md)
* [配置結構](configure-schemas.md)

>[!IMPORTANT]
>
>此 [Experience CloudID擴充功能](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) 實作Adobe Experience Platform Web SDK時不需要，因為Web SDK JavaScript程式庫包含訪客ID服務功能。

## 建立身分命名空間

在本練習中，您會為Luma的自訂身分欄位建立身分命名空間， `lumaCrmId`. 身分識別命名空間在建立即時客戶設定檔方面扮演關鍵角色，因為相同命名空間中的兩個相符值可讓兩個資料來源形成身分圖表。

開始練習之前，請觀看此短片，以進一步了解Adobe Experience Platform中的身分：
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

現在，為Luma CRM ID建立命名空間：

1. 開啟 [資料收集介面](https://launch.adobe.com/tw/){target=&quot;_blank&quot;}
1. 選取您用於教學課程的沙箱

   >[!NOTE]
   >
   >如果您是Real-Time CDP等以平台為基礎之應用程式的客戶，建議您針對本教學課程使用開發沙箱。 若非如此，請使用 **[!UICONTROL 生產]** 沙箱。

1. 選擇 **[!UICONTROL 身分]** 在左側導覽列中
1. 選擇 **[!UICONTROL 瀏覽]**

   頁面的主介面中會顯示身分識別命名空間清單，其中會顯示其名稱、身分識別符號、上次更新的日期，以及這些命名空間是標準或自訂的命名空間。 右側邊欄包含身分圖表強度的資訊。

1. 選擇 **[!UICONTROL 建立身分命名空間]**

   ![檢視身分](assets/configure-identities-screen.png)

1. 提供詳細資訊，如下所示，並選取 **[!UICONTROL 建立]**.

   | 欄位 | 值 |
   |---------------|-----------|
   | 顯示名稱 | Luma CRM ID |
   | 標識符 | lumaCrmId |
   | 類型 | 跨裝置ID |


   ![建立命名空間](assets/identities-create-namespace.png)


   身分命名空間會填入 **[!UICONTROL 身分]** 螢幕。

   ![建立命名空間](assets/configure-identities-namespace-lumaCrmId.png)


>[!INFO]
>
> 在 [建立資料元素](create-data-elements.md) 課程中，您將學習如何在將身分傳送至Platform Edge Network時使用此命名空間。

## 在生產沙箱中建立身分命名空間

由於Web SDK擴充功能目前有限，您也必須在生產沙箱中建立身分識別命名空間，才能使用命名空間將資料傳送至開發沙箱。 因此，如果您已在本教學課程中使用開發沙箱，請同時建立 `Luma CRM ID` 命名空間。

## 其他資源

* [Identity Service 文件](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hant)
* [Identity服務API](https://www.adobe.io/experience-platform-apis/references/identity-service/)

現在身分已就緒，即可設定資料流。

[下一個： ](configure-datastream.md)

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
