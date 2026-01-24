---
title: 規劃移轉 — 將行動應用程式中的Adobe Target實作移轉至Offer Decisioning和Target擴充功能
description: 瞭解at.js與Platform Web SDK之間的主要差異，以及如何規劃您的移轉作業。
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 規劃移轉

從Target擴充功能移轉至Offer Decisioning和Target擴充功能的工作量等級，取決於您目前實作和所使用Target功能的複雜性。

無論您的實作有多麼簡單或複雜，移轉前都必須充分瞭解您目前的狀態。 本指南可協助您劃分目前實作的元件，並制訂管理得宜的計畫來移轉每個專案。

移轉程式包含下列重要步驟：

1. 評估您目前的實施，並決定移轉方法
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


接下來，檢閱Target擴充功能與Offer Decisioning和Target擴充功能[的詳細](detailed-comparison.md)比較，以更清楚瞭解技術差異，並找出需要額外關注的領域。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Offer Decisioning和Target擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=zh-Hant#M625)中張貼以告知我們。
