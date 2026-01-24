---
title: 將您的行動應用程式從Adobe Target移轉至Offer Decisioning和Target擴充功能
description: 瞭解如何將您的行動應用程式實作從Adobe Target移轉至Offer Decisioning和Target擴充功能
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 1%

---

# 將您的行動應用程式從Adobe Target移轉至Offer Decisioning和Target擴充功能

本指南適用於經驗豐富的Adobe Target實作人員，以瞭解如何將現有的Adobe Experience Platform Mobile SDK實作從Adobe Target擴充功能移轉至Offer Decisioning和Target擴充功能。

Adobe Experience Platform Mobile SDK可在您的行動應用程式中強化端對端參與。 Target擴充功能以Mobile SDK為基礎，可協助您使用Adobe Target打造個人化應用程式體驗。 Offer Decisioning和Target擴充功能是在行動應用程式中實作Adobe Target的較新方法，其使用Adobe Experience Platform Edge Network功能，可協助將Target與Real-Time CDP和Journey Optimizer等平台式應用程式整合。

![圖表顯示透過Edge Network使用Offer Decisioning和Target擴充功能連線至Target的行動裝置SDK](assets/datacollection.png)

## 主要優點

相較於Target擴充功能，Adobe Journey Optimizer Offer Decisioning和Target擴充功能的一些優點包括：

* 更快共用[Real-Time Customer Data Platform](https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/destinations/target/next-hit-personalization)的對象
* 將Target與Journey Optimizer整合以支援[Offer Decisioning傳遞](https://experienceleague.adobe.com/zh-hant/docs/target/using/integrate/ajo/offer-decision)
* 與Adobe Analytics更緊密整合，不仰賴拼接來自個別網路呼叫的資訊
* 為開發人員提供額外的實作彈性

可以說移轉對Target客戶最大的好處是與Real-Time Customer Data Platform整合。 Real-Time CDP根據擷取到Experience Platform的所有資料及其即時客戶個人檔案功能，提供龐大的受眾建立功能。 內建的資料控管架構可讓您以負責任的方式自動使用這些資料。 Customer AI可讓您輕鬆使用機器學習模型來建構傾向性和流失模型，而模型的輸出可分享回Adobe Target。 最後，選購的Healthcare和Privacy &amp; Security Shield附加元件的客戶可使用同意執行功能來強制實施個別客戶的同意偏好設定。 若要在行動裝置頻道中使用這些Real-Time CDP功能，必須使用Platform Mobile SDK和Offer Decisioning and Target擴充功能。

## 移轉步驟

從Target擴充功能移轉至Offer Decisioning和Target擴充功能的工作量等級，取決於您目前實作和所使用Target功能的複雜性。

無論您的實作有多麼簡單或複雜，移轉前都必須充分瞭解您目前的狀態。 本指南可協助您劃分目前實作的元件，並制訂管理得宜的計畫來移轉每個專案。

移轉程式包含下列重要步驟：

1. 評估您目前的實施，包括：
   1. 所有使用的Target SDK API
   1. 修改Target的全域設定
   1. 與 Adobe Analytics 整合
   1. mbox、設定檔和實體引數的使用
   1. 使用設定檔指令碼和對象
   1. 實作特有的自訂程式碼
1. 設定初始元件以連線至Adobe Experience Platform Edge Network
1. 更新基本實施，以Offer Decisioning和Target擴充功能取代Target擴充功能
1. 針對您的特定使用案例增強「最佳化SDK」實作。 這可能涉及傳遞其他引數、使用回應Token等。
1. 更新Target介面中的物件，例如設定檔指令碼、活動和對象定義
1. 在生產應用程式中進行切換之前，請驗證最終實施


>[!INFO]
>
>在Adobe Experience Platform Mobile SDK生態系統內，擴充功能會由匯入應用程式（名稱可能不同）的SDK實作：
>
> * **目標SDK**&#x200B;實作&#x200B;**Adobe Target擴充功能**
> * **最佳化SDK**&#x200B;實作&#x200B;**Offer Decisioning和Target擴充功能**

接下來，檢閱Target擴充功能與Offer Decisioning和Target擴充功能[的詳細](comparison.md)比較，以更清楚瞭解技術差異，並找出需要額外關注的領域。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Offer Decisioning和Target擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=zh-Hant#M625)中張貼以告知我們。
