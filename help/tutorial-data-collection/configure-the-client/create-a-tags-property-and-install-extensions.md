---
title: 建立Adobe Experience Platform標籤屬性並安裝擴充功能
description: 建立Adobe Experience Platform標籤屬性並安裝擴充功能
exl-id: d0fe82b5-a036-4e13-bae1-d1fee78d0084
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# 建立Adobe Experience Platform [!DNL Tags] 屬性和安裝擴充功能

現在頁面程式碼正在將資料和事件推送至資料層，行銷人員可以開始從資料層讀取資料，並將這些資料傳送至Adobe Experience Platform。 這通常需要兩個JavaScript程式庫：

* Adobe客戶端資料層：在先前步驟中，您建立資料層陣列，並將物件推送至陣列。 若要存取此資料，您必須載入Adobe用戶端資料層JavaScript程式庫。 此程式庫提供事件和資料層變更的通知，以及資料的簡單存取。
* Adobe Experience Platform Web SDK:此JavaScript程式庫會與 [Adobe Experience Platform Edge Network](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). SDK可處理身分、同意、資料收集、個人化、對象等。

雖然您可以將這些個別程式庫載入網站並直接使用，但建議您使用 [Adobe Experience Platform標籤](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html). 透過「標籤」，您可以將單一指令碼內嵌至HTML，並使用「標籤」使用者介面來部署Adobe用戶端資料層和Adobe Experience Platform Web SDK。 標籤也可讓您建立傳送資料的規則，以及其他。 本教學課程會針對此目的使用標籤，並假設您基本了解標籤的運作方式。

## 在標籤中建立屬性

1. [在標籤中建立屬性](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## 安裝Adobe用戶端資料層擴充功能

安裝Adobe用戶端資料層擴充功能：

1. 選擇 **[!UICONTROL 擴充功能]** 在您用於本教學課程的「標籤」屬性的左側導覽中。
1. 選取 **[!UICONTROL 目錄]** 連結，然後搜尋「資料層」。
1. 在結果中顯示Adobe用戶端資料層後，按一下 **[!UICONTROL 安裝]** 按鈕。 您應該會看到設定畫面。 在本教學課程中，不需要變更預設值。
1. 按一下「**[!UICONTROL 儲存]**」。
   ![Adobe用戶端資料層擴充功能安裝](../assets/acdl-extension-installation.png)


## 安裝Adobe Experience Platform Web SDK擴充功能

接下來，安裝Adobe Experience Platform Web SDK擴充功能：

1. 在擴充功能目錄中搜尋擴充功能，然後按一下個別的 **[!UICONTROL 安裝]** 按鈕。 您應該會看到設定畫面：
   ![Adobe Experience Platform Web SDK擴充功能安裝](../assets/web-sdk-extension-installation.png)
1. 在 [!UICONTROL 資料流] 欄位，選取您先前建立的資料流。 您會看到與 [建立資料流](../configure-the-server/create-a-datastream.md).
   ![資料流選擇](../assets/web-sdk-datastream-selection.png)
1. 進一步在設定畫面中，尋找並取消勾選 **[!UICONTROL 啟用點按資料收集]**. 依預設，SDK會自動追蹤您的連結。 不過，在本教學課程中，我們示範如何使用自訂連結資訊來追蹤您自己的連結點按次數。
1. 按一下 **[!UICONTROL 儲存]** 按鈕完成Adobe Experience Platform Web SDK擴充功能的安裝。

>[!TIP]
>
>資料集環境與「標籤」環境有關係。 假設您已完成Adobe Experience Platform Web SDK擴充功能的安裝，請建立包含擴充功能的標籤程式庫，然後將程式庫發佈至標籤開發環境。 當標籤程式庫載入至您的網頁，且Adobe Experience Platform Web SDK擴充功能向Edge Network提出請求時，擴充功能會包含 [!UICONTROL 開發環境] 資料流環境ID。 Edge Network則會使用該ID來讀取 [!UICONTROL 開發環境] 資料流環境，並將資料轉送至適當的Adobe產品。
>
>目前，您只有一個開發資料流環境、一個中繼資料流環境和一個生產資料流環境。 您可以使用datastream使用者介面來建立多個資料流開發環境（一個供您使用，另一個則供您的同事使用）。 如果您有多個開發資料流環境，則可以選取要用於此標籤屬性的環境。


已安裝適當的擴充功能。 是時候建立規則和資料元素了。

[下一個： ](create-rules-for-tracking-page-view-and-commerce-events.md)

>[!NOTE]
>
>感謝您花時間學習資料收集。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
