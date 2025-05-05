---
title: 資料架構師和資料工程師專用Adobe Experience Platform快速入門
description: 資料架構師和資料工程師快速入門Adobe Experience Platform。
breadcrumb-title: 概觀
role: Data Architect, Data Engineer
jira: KT-4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: 63987fb652a653283a05a5f35f7ce670127ae905
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# 資料架構師和資料工程師專用Adobe Experience Platform快速入門

<!--5min-->

_資料架構師和資料工程師的Adobe Experience Platform快速入門_&#x200B;是動手進行Experience Platform的最佳起點。


<!--How do we address ETL-->

## 學習目標

資料架構師和資料工程師必須緊密合作，才能成功Experience Platform部署。 此實作教學課程會教導您&#x200B;_兩個角色_&#x200B;執行的主要工作，讓您瞭解如何開始為自己的企業實作Platform。 您將透過練習逐步瞭解Experience Platform的重要術語、功能、介面和API。 Adobe Experience Cloud應用程式(例如Real-time Customer Data Platform、Customer Journey Analytics和Journey Optimizer)的客戶也會發現此內容很有用，因為Platform服務是這些應用程式的重要基礎。

![Adobe Experience Cloud行銷結構重點說明本教學課程中涵蓋的Platform服務 — 身分、設定檔、分段、擷取、查詢和治理](assets/marketecture.png)

主題包括：

* 設定使用者許可權
* 建立沙箱
* 設定Developer Console專案並使用Platform API
* 資料管理 — 包括建立結構描述、資料集、身分、合併原則和資料控管
* 使用批次和串流模式的資料擷取
* 使用Adobe Experience Platform Web SDK擷取網頁資料
* 建立即時客戶設定檔
* 使用查詢服務來驗證資料並擷取資料
* 建立區段

## 業務案例

Adobe Experience Platform是技術平台，旨在協助您達成行銷目標。 業務使用案例應推動您設計和實作技術的方式。 本教學課程著重於名為Luma的虛構零售品牌。 Luma在多個國家經營實體店，並透過網站和行動應用程式線上上開展業務。 他們投資在Adobe Experience Platform，將忠誠度、CRM、網頁和離線購買資料結合到即時客戶設定檔中，並啟用這些設定檔，將他們的行銷提升到新的境界。 Luma的業務目標可能與貴公司的目標一致，也可能不一致，但您應能將此教學課程中的實作步驟與自己的業務目標建立關聯。

## 先決條件

* 您已觀看Experience League上的[Adobe Experience Platform播放清單簡介](https://experienceleague.adobe.com/zh-hant/playlists/experience-platform-introduction)，並熟悉Platform功能
* 您可以存取透過Adobe Experience Platform (或Real-Time CDP或Journey Optimizer等平台型應用程式)和Data Collection （前身為Launch）布建的帳戶。
* 您是該帳戶的系統管理員，或者可以為您設定一個[使用者許可權](configure-permissions.md)。

## 使用本教學課程

本教學課程結合資料工程師和資料架構師的任務。 由於這是入門級教學課程，您應該能夠完成這兩個角色的工作。 由於許多課程是以先前課程中實作的內容為基礎，因此您應依序逐一瀏覽課程。 我會指出哪些課程可以略過。

在本教學課程中建立各種Platform元素時，請儘量使用我建議的名稱。 不過，如果您的組織有多人同時參加此教學課程，建議您自訂一些高階元素名稱。 例如，您可能會想要將Platform沙箱命名為「Luma Tutorial Platform - Ignatius J Reilly」，而不僅僅是「Luma Tutorial Platform」。

如果您卡住了，請先嘗試重新閱讀指示，然後使用每個頁面側邊欄上的![記錄問題](https://experienceleague.adobe.com/assets/img/feedback.svg?lang=zh-Hant)連結來聯絡我。

## 技術說明

### 沙箱環境

在本教學課程中，您將建立沙箱環境並使用它來完成練習。 沙箱環境可讓您安全地完成練習和實驗，而不用擔心危及您的生產資料。

### API

平台是API優先建置。 雖然所有主要平台工作流程都有介面工作流程存在，並將主要使用，但本教學課程包含一些以API為導向的練習。 我將引導您完成Adobe Developer Console中的基本專案設定，並為您提供[!DNL Postman]環境和集合，以便您開始使用Platform API。 完成本教學課程之後，您可能會發現熟悉平台API並將其用於您自己的部署很有價值。

### 協力廠商技術

雖然在本教學課程中，您將使用多項技術，但您幾乎仍會停留在Adobe生態系統內。 在您自己的Platform實作中，您可能會將Platform與特定的協力廠商技術整合。 為了讓本教學課程適用於所有客戶，我們將使用較通用的實施。

## 教學課程更新

* 2023年6月：更新以包含新的許可權工作流程，並使用OAuth伺服器對伺服器API認證


現在讓我們繼續第一個課程 — [設定許可權](configure-permissions.md)。
