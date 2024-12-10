---
title: 從Adobe Target移轉至Adobe Journey Optimizer - Decisioning行動擴充功能
description: 瞭解如何將您的行動應用程式實作從Adobe Target移轉至Adobe Journey Optimizer - Decisioning擴充功能
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: 485e79e3569052184475fbc49ab5f43cebcac9a6
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 3%

---

# 從Adobe Target移轉至Adobe Journey Optimizer - Decisioning行動擴充功能

本指南適用於經驗豐富的Adobe Target實作人員，協助他們瞭解如何將現有的Adobe Experience Platform Mobile SDK實作從Adobe Target擴充功能移轉至Adobe Journey Optimizer - Decisioning擴充功能。

Adobe Experience Platform Mobile SDK支援行動應用程式中的端對端參與。 Target擴充功能以Mobile SDK為基礎，可協助您使用Adobe Target打造個人化應用程式體驗。 Decisioning擴充功能是在行動應用程式中實施Adobe Target的較新方法，其使用Adobe Experience PlatformEdge Network功能，協助將Target與Real-Time CDP和Journey Optimizer等平台型應用程式整合。

## 主要優點

Decisioning擴充功能的一些優點包括：

* 更快共用[Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=zh-Hant)的對象
* 整合Target與Journey Optimizer以支援[Offer decisioning傳遞](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* 與Adobe Analytics更緊密整合，不仰賴拼接來自個別網路呼叫的資訊
* 為開發人員提供額外的實作彈性

可以說移轉對Target客戶最大的好處是與Real-time Customer Data Platform整合。 Real-Time CDP根據擷取到Experience Platform的所有資料及其即時客戶設定檔功能，提供龐大的受眾建立功能。 內建的資料控管架構，可自動負責使用這些資料。 Customer AI可讓您輕鬆使用機器學習模型來建構傾向性和流失模型，而模型的輸出可分享回Adobe Target。 最後，選購的Healthcare及Privacy &amp; Security Shield附加元件的客戶可使用同意執行功能，輕鬆強制執行個別客戶的同意偏好設定。 若要在您的Web Channel中使用這些Real-Time CDP功能，必須使用Platform Web SDK。

## 學習目標

在本教學課程結束時，您將能:

* 專案符號1
* 專案符號2


## 先決條件

若要完成本教學課程，您應該首先：

* 專案符號1
* 專案符號2


>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
