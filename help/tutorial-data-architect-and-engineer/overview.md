---
title: 資料架構師與資料工程師專用Adobe Experience Platform快速入門
description: 資料架構師與資料工程師專用Adobe Experience Platform快速入門。
breadcrumb-title: 總覽
role: Data Architect, Data Engineer
kt: 4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 1%

---

# 資料架構師與資料工程師專用Adobe Experience Platform快速入門

<!--5min-->

_資料架構師與資料工程師專用Adobe Experience Platform快速入門_ 是實踐Experience Platform的最佳起點。


<!--How do we address ETL-->

## 學習目標

資料架構師和資料工程師必須密切合作，才能成功部署Experience Platform。 本實作教學課程會說明由執行的主要工作 _兩個角色_ 讓您了解如何開始為自己的業務實作Platform。 您將參閱相關練習，了解重要的術語、功能、介面和Experience PlatformAPI。 Real-time Customer Data Platform、Customer Journey Analytics和Journey Optimizer等Adobe Experience Cloud應用程式的客戶也會發現此內容很實用，因為Platform服務是這些應用程式的關鍵基礎。

![Adobe Experience Cloud行銷架構，重點說明本教學課程所涵蓋的Platform服務：身分、設定檔、細分、擷取、查詢和控管](assets/marketecture.png)

主題包括：

* 設定使用者權限
* 建立沙箱
* 設定開發人員控制台專案並使用平台API
* 資料管理 — 包括建立結構、資料集、身分、合併原則及資料控管
* 使用批次和串流模式擷取資料
* 使用Adobe Experience Platform Web SDK擷取Web資料
* 建立即時客戶設定檔
* 使用Query Service驗證資料及擷取資料
* 建立區段

## 業務方案

Adobe Experience Platform是技術平台，旨在協助您達成行銷目標。 業務使用案例應推動您設計和實施技術的方式。 本教學課程主要探討虛構的零售品牌Luma。 Luma在多個國家經營實體店，還擁有一個網站和移動應用的線上業務。 他們正在投資Adobe Experience Platform，將忠誠度、CRM、網路和離線購買資料結合為即時客戶設定檔，並啟用這些設定檔，將其行銷提升至全新境界。 Luma的業務目標可能與貴公司的目標一致，也可能不符合，但您應能將本教學課程中的實際操作步驟與您自己的業務目標聯繫起來。

## 先決條件

* 您已完成 [Adobe Experience Platform課程簡介](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2020.1) Experience League，並熟悉Platform功能
* 您可以存取已布建Adobe Experience Platform(或Platform型應用程式，例如即時CDP或Journey Optimizer)和Data Collection（先前稱為Launch）的帳戶。
* 您是該帳戶的系統管理員，或可以有 [設定使用者權限](configure-permissions.md) 為了你。

## 使用本教學課程

本教學課程結合資料工程師和資料架構師的工作。 由於這是入門級教學課程，因此您應該能夠完成這兩個角色的工作。 由於許多課程都以先前課程中所實施的內容為基礎，因此您應該按順序逐步總結這些課程。 我會說明可以略過哪些課程。

在本教學課程中，當您建立各種Platform元素時，請嘗試盡可能依照我建議的名稱操作。 不過，如果您的組織中有多人同時參加本教學課程，可能會想要自訂一些高階元素名稱。 例如，您可將平台沙箱命名為「Luma教學課程平台 — Ignatius J Reilly」，而非「Luma教學課程平台」。

如果卡住，請先嘗試重新閱讀指示，然後使用 ![記錄問題](https://experienceleague.adobe.com/assets/img/feedback.svg) 連結到每個頁面的側欄，與我聯繫。

## 技術說明

### 沙箱環境

在教學課程中，您將建立沙箱環境，並使用它來完成練習。 沙箱環境可讓您安全地完成練習和實驗，而不必擔心影響生產資料。

### API

平台是先建置API的。 雖然所有主要平台工作流程皆有介面工作流程，且將主要使用，但教學課程包含一些API導向的練習。 我會引導您完成Adobe Developer Console中的基本專案設定，並提供 [!DNL Postman] 環境和集合，以開始使用Platform API。 完成本教學課程後，您可能會發現熟悉Platform API，並將其用於您自己的部署中，這是很有價值的作法。

### 第三方技術

雖然您將在本教學課程中使用多種技術，但您幾乎仍停留在Adobe生態系統中。 在您自己的Platform實作中，您可能會將Platform與特定的協力廠商技術整合。 為了讓本教學課程與所有客戶保持相關，我們將使用更通用的實作。

現在，我們繼續講第一課……[設定權限](configure-permissions.md).
