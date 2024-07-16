---
title: 簡介 | 將Target從at.js 2.x移轉至Web SDK
description: 瞭解如何將Adobe Target實作從at.js 2.x移轉至Adobe Experience Platform Web SDK。 主題包括載入JavaScript程式庫、傳送引數、轉譯活動以及其他值得注意的圖說文字。
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 4%

---

# 將Target從at.js 2.x移轉至Platform Web SDK

本指南適用於經驗豐富的Adobe Target實作人員，以瞭解如何將at.js實作移轉至Adobe Experience Platform Web SDK。

Adobe Experience Platform Web SDK是使用者端的JavaScript資料庫，可讓Adobe Experience Cloud客戶透過Adobe Experience PlatformEdge Network與Experience Cloud服務互動。 這個新程式庫將個別Adobe應用程式庫的功能結合為單一輕量型套件，可充分運用Adobe Experience Platform的新功能。

## 主要優點

與獨立at.js程式庫相比，Platform Web SDK的一些優點包括：

* 更快共用[Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=zh-Hant)的對象
* 整合Target與Journey Optimizer以支援[Offer decisioning傳遞](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* 能夠使用[第一方ID](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html)產生ECID以識別持續較長的訪客
* 跨Adobe應用程式整合網路呼叫
* 更小的佔用空間，以提升頁面速度量度
* 與Adobe Analytics更緊密整合，不仰賴拼接來自個別網路呼叫的資訊
* 為開發人員提供額外的實作彈性

可以說移轉對Target客戶最大的好處是與Real-time Customer Data Platform整合。 Real-Time CDP根據擷取到Experience Platform的所有資料及其即時客戶設定檔功能，提供龐大的受眾建立功能。 內建的資料控管架構，可自動負責使用這些資料。 Customer AI可讓您輕鬆使用機器學習模型來建構傾向性和流失模型，而模型的輸出可分享回Adobe Target。 最後，選購的Healthcare及Privacy &amp; Security Shield附加元件的客戶可使用同意執行功能，輕鬆強制執行個別客戶的同意偏好設定。 若要在您的Web Channel中使用這些RTCDP功能，必須使用Platform Web SDK。

## 學習目標

在本教學課程結束時，您將能:

* 瞭解at.js和平台Web SDK之間的Target實作差異
* 設定Target功能的初始設定
* 將at.js程式庫升級至Platform Web SDK
* 呈現表單式和視覺化體驗撰寫器活動
* 傳遞引數至Target
* 追蹤轉換事件
* 啟用跨網域支援
* 更新對象和個人資料指令碼
* 驗證實作
* Debug Target體驗傳送


## 先決條件

若要完成本教學課程，您應該首先：

* 從技術角度瞭解您目前的Target at.js實作
* 確定您擁有Target執行個體的[編輯者或發佈者角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80)，這樣您就可以嘗試自己的範例
* 瞭解如何在Adobe Target中設定活動。 如果您需要複習程式，下列教學課程和指南對本課程很有幫助：
   * [使用 Visual Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [使用表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [建立體驗鎖定目標活動](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

準備就緒後，成功移轉的第一步就是[瞭解移轉程式](migration-overview.md)以及at.js和平台Web SDK的差異。

>[!NOTE]
>
>我們致力協助您成功將Target從at.js移轉至Web SDK。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
