---
title: 建立及設定資料串流
description: 瞭解如何建立和設定新的資料流，以將您的網站資料路由至Adobe Analytics。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16757
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---


# 建立及設定資料串流

瞭解如何建立和設定新的資料流，以將您的網站資料路由至Adobe Analytics。

在本課程中，您將瞭解如何建立及設定系統，讓您的資料從網站傳輸至Adobe Edge，然後從那裡路由至Adobe Analytics。

![架構圖](assets/architecture_diagram.jpg)

## 建立新的開發資料流

1. 開啟Adobe資料收集介面
   1. 在瀏覽器中導覽至https://experience.adobe.com
   1. 確定在頁面頂端選取了正確的組織(例如，下圖中的Adobe生產 — 技術行銷示範)
   1. 按一下「九個點」（亦即應用程式切換器），然後選取&#x200B;**資料收集**

      ![瀏覽至資料彙集](assets/navigate-to-data-collection.jpg)

1. 前往左側導覽中的&#x200B;**[!UICONTROL 資料串流]**
1. 選取&#x200B;**[!UICONTROL 新資料流]**
1. 輸入所需的&#x200B;**[!UICONTROL Name]**，並加入將用於網頁SDK開發環境的指標。 例如，您可以在網站後面命名此名稱，如下所示。 記下該名稱，因為當您稍後在標籤屬性中設定Web SDK擴充功能時，會參照此名稱。 視需要輸入說明。

   >[!NOTE]
   >
   >如果您使用資料收集的[資料準備](https://experienceleague.adobe.com/zh-hant/docs/platform-learn/data-collection/edge-network/data-prep)功能，您只需要選取結構描述，我們在本教學課程中不會這麼做。 請瀏覽連結以瞭解更多資訊。

1. 選取&#x200B;**[!UICONTROL 儲存]**

   ![建立資料流](assets/create-new-datastream.jpg)

1. 儲存資料流後，新畫面會隨即顯示，通知您尚未設定任何服務。 換言之，您的資料將傳送至Edge伺服器，但不會傳送至任何應用程式，直到我們新增服務為止。 我們現在會設定資料串流，將資料傳送至Adobe Analytics。 按一下&#x200B;**[!UICONTROL 新增服務]**。
   ![新增服務](assets/datastream-add-service.jpg)
1. 在服務下拉式功能表中，選取&#x200B;**[!UICONTROL Adobe Analytics]**。
1. 在報表套裝ID欄位中，輸入您在[建立驗證報表套裝](create-a-validation-report-suite.md)活動中建立的驗證報表套裝的ID （不是標題，而是報表套裝ID）。 按一下&#x200B;**[!UICONTROL 儲存]**。

## 中繼和生產資料串流

您現在要&#x200B;**再次執行相同的步驟**&#x200B;兩次：一次用於您的中繼環境，另一次用於您的生產環境。 當您設定這些額外的兩個資料串流時，以下是一些附註。

### 中繼資料串流

* 為資料串流命名時（以及新增說明時），您可以/應該使用相同的名稱，只不過新增「staging」而非「development」不同。
* 新增Adobe Analytics服務（就像您之前做的那樣），並將報表套裝設定為相同的開發報表套裝。
* 如果您想要更簡潔的環境，以便在Adobe Analytics報表中檢視測試編號，您可以建立僅用於測試的新報表套裝，然後確定您已在此資料流的Analytics服務中指向該報表套裝。

### 生產資料流

* 為資料串流命名時（以及新增說明時），您可以或應該使用相同的名稱，只不過新增「生產」而非「開發」不同。
* 選擇要對應資料的報表套裝，而非選擇開發報表套裝或甚至是新的報表套裝，您就可以將此資料串流對應至AppMeasurement實作所饋送的&#x200B;**目前**&#x200B;生產報表套裝。 如此一來，當您完成移轉並經過測試且對數字感到滿意後，就可以移除舊的AppMeasurement程式碼、將標籤程式庫傳送至生產環境，而且您會將新的生產資料饋送至相同的生產報表套裝，以便在舊實作與新實作之間保持連續性。
