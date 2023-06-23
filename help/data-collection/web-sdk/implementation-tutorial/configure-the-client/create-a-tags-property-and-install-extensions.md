---
title: 建立Adobe Experience Platform標籤屬性並安裝擴充功能
description: 建立Adobe Experience Platform標籤屬性並安裝擴充功能
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 7403059f-b34c-48e0-9efe-b2db7a9afb27
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# 建立Adobe Experience Platform標籤屬性並安裝擴充功能

現在，頁面上的程式碼正在將資料和事件推送至資料層，行銷人員應該從資料層讀取資料，並將此資料傳送至Adobe Experience Platform。 這通常需要兩個JavaScript程式庫：

* Adobe使用者端資料層：在之前的步驟中，您已建立資料層陣列並將物件推送至該陣列。 若要存取資料，您必須載入Adobe使用者端資料層JavaScript程式庫，此程式庫可提供通知資料層變更和事件的方式，並提供存取資料的簡單方式。
* Adobe Experience Platform Web SDK：此JavaScript程式庫可與Adobe Experience Platform Edge Network通訊。 SDK可處理身分、同意、資料收集、個人化、對象等。

雖然您可以將這些個別程式庫載入您的網站，並直接加以使用，建議您使用 [Adobe Experience Platform標籤](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html). 透過Tags，您可以將單一指令碼內嵌至HTML，並使用Tags使用者介面來部署Adobe使用者端資料層和Adobe Experience Platform Web SDK。 標籤也可讓您建立傳送資料的規則，以及其他功能。 本教學課程使用標籤來達成此目的，並假設您已基本瞭解標籤的運作方式。

## 在標籤內建立屬性

如果您尚未安裝， [在標籤內建立屬性](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## 安裝Adobe使用者端資料層擴充功能

導覽至擴充功能目錄，找出擴充功能，然後按一下個別的「 」，安裝Adobe使用者端資料層擴充功能 [!UICONTROL 安裝] 按鈕。 您應該會看到設定畫面。

![Adobe使用者端資料層擴充功能安裝](../../../assets/implementation-strategy/acdl-extension-installation.png)

在本教學課程中，不需要變更預設值。 按一下[!UICONTROL 儲存]。

## 安裝Adobe Experience Platform Web SDK擴充功能

接下來，請在擴充功能目錄中找到擴充功能，然後按一下個別的「 」，以安裝Adobe Experience Platform Web SDK擴充功能 [!UICONTROL 安裝] 按鈕。 您應該會看到設定畫面。

![Adobe Experience Platform Web SDK擴充功能安裝](../../../assets/implementation-strategy/web-sdk-extension-installation.png)

在 [建立資料串流](../configure-the-server/create-a-datastream.md)，您已建立Adobe Experience Platform Edge Network參考的資料串流，以判斷要將傳入資料傳送至何處。 從Adobe Experience Platform Web SDK向Edge Network提出請求時，您必須指出應參考哪個資料流Edge Network。

若要這麼做，請找到 [!UICONTROL 資料流] 欄位並選取您先前建立的資料流。 您會看到與您在中看到的相同資料流環境 [建立資料串流](../configure-the-server/create-a-datastream.md).

![資料流選擇](../../../assets/implementation-strategy/web-sdk-datastream-selection.png)

如中所述 [建立資料串流](../configure-the-server/create-a-dataset.md)，這些資料集環境與標籤環境有關聯。 假設您完成Adobe Experience Platform Web SDK擴充功能的安裝，接著建立包含擴充功能的標籤程式庫，然後將程式庫發佈至標籤開發環境。 當標籤程式庫載入您的網頁，且Adobe Experience Platform Web SDK擴充功能向Edge Network提出請求時，擴充功能會包含 [!UICONTROL 開發環境] 資料流環境ID。 而Edge Network會使用該ID來讀取 [!UICONTROL 開發環境] 資料流環境，並將資料轉送至適當的Adobe產品。

目前，您只有一個開發資料流環境、一個中繼資料流環境及一個生產資料流環境。 這就是擴充功能設定使用者介面顯示所有預先選取且不可變更的原因。 不過，您可以使用資料流使用者介面來建立多個資料流開發環境（一個供您使用，一個供同事使用）。 如果您有多個開發資料流環境，您可以選取要用於此標籤屬性的環境。

最後，向下捲動並取消勾選 [!UICONTROL 啟用點選資料收集]. 根據預設，SDK會自動追蹤您的連結。 不過，在本教學課程中，我們將示範如何使用自訂連結資訊來追蹤您自己的連結點按。

按一下 [!UICONTROL 儲存] 按鈕以完成安裝Adobe Experience Platform Web SDK擴充功能。

已安裝適當的擴充功能。 是時候建立規則和資料元素了。
