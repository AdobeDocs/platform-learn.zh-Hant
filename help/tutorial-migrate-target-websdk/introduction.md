---
title: 簡介 |將Target從at.js 2.x移轉至Web SDK
description: 了解如何將Adobe Target實作從at.js 2.x移轉至Adobe Experience Platform Web SDK。 主題包括載入JavaScript程式庫、傳送參數、轉譯活動和其他值得注意的圖說。
last-substantial-update: 2023-02-23T00:00:00Z
source-git-commit: 4b695b4578f0e725fc3fe1e455aa4886b9cc0669
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 6%

---

# 將Target從at.js 2.x移轉至Platform Web SDK

本指南適用於經驗豐富的Adobe Target實作者，了解如何將at.js實作移轉至Adobe Experience Platform Web SDK。

Adobe Experience Platform Web SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud客戶透過Adobe Experience Platform邊緣網路與Experience Cloud服務互動。 這個新程式庫將個別Adobe應用程式程式庫的功能結合為單一輕量型套件，以充分運用新的Adobe Experience Platform功能。

## 主要優點

Platform Web SDK與獨立at.js程式庫相比，有幾項優點：

* 更快共用受眾，從 [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=zh-Hant)
* 整合Target與Journey Optimizer以支援 [offer decisioning傳送](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* 使用功能 [第一方id](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html) 若要產生持續時間較長的訪客身分識別ECID
* 跨Adobe應用程式整合網路呼叫
* 減少佔用空間以改善頁面速度量度
* 與Adobe Analytics的更緊密整合，不需仰賴將資訊與個別網路呼叫連結
* 為開發人員提供額外的實作彈性

可以說，Target客戶在移轉方面最大的好處是與Real-time Customer Data Platform整合。 Real-Time CDP提供巨大的受眾建立功能，其基礎是擷取至Experience Platform的完整資料及其即時客戶個人檔案功能。 內建的資料控管架構，自動負責任地使用該資料。 Customer AI可讓您輕鬆使用機器學習模型來建構傾向和流失率模型，其輸出可共用回Adobe Target。 最後，可選的醫療保健和隱私與安全防護軟體的客戶可以使用許可強制執行功能來輕鬆強制執行個別客戶的許可首選項。 若要在Web通道中使用這些RTCDP功能，則需要使用Platform Web SDK。

## 學習目標

在本教學課程結束時，您將能:

* 了解at.js和Platform Web SDK之間的Target實作差異
* 設定Target功能的初始設定
* 將at.js程式庫升級至Platform Web SDK
* 轉譯表單式和可視化體驗撰寫器活動
* 傳遞參數至Target
* 追蹤轉換事件
* 啟用跨網域支援
* 更新對象和設定檔指令碼
* 驗證實作
* 除錯Target體驗傳送


## 先決條件

若要完成本教學課程，您應先：

* 對您目前的Target at.js實作有技術上的了解
* 確定您有 [編輯者或發佈者角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 例，讓您可以自行嘗試範例
* 了解如何在Adobe Target中設定活動。 如果您需要重新整理，下列教學課程和指南將有助於本課程：
   * [使用 Visual Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [使用表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [建立體驗鎖定目標活動](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

準備好之後，成功移轉的第一步是 [了解移轉程式](migration-overview.md) 以及at.js和Platform Web SDK的不同之處。

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).