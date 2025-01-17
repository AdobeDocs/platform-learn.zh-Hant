---
title: 資料收集 — 同盟對象構成
description: 資料收集 — 同盟對象構成
kt: 5342
doc-type: tutorial
exl-id: cc2ac85e-e902-4bb7-ab54-aa39980f97aa
source-git-commit: 9099ba1d57d59a95958f29bf226f329f057b6c0c
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# 3.1同盟對象構成

在本單元中，目標是瞭解使用同盟對象構成建立對象的所有相關資訊。

Experience Platform中的同盟對象構成(FAC)可讓您透過企業資料倉儲中的對應高價值屬性存取及建立對象，這些屬性會豐富及補充Experience Platform中的即時客戶設定檔和對象，以改進分段、鎖定目標、啟動及傳送具影響力的客戶體驗。 使用同盟對象構成，透過中繼資料連結遠端資料庫來建立虛擬資料庫。 此方法可簡化存取、減少重複，並增強一般使用者體驗。 團隊在組裝參與工作流程的對象時，可以靈活地直接將資料集擷取到Experience Platform或存取資料倉儲中的資料集。 此方法充分利用Data Warehouse投資和資產，以補充Real-Time CDP和Journey Optimizer。 同盟受眾構成可讓客戶在各種關鍵的新使用案例模式中，運用並結合批次和即時功能：

- 同盟受眾細分：團隊可在Real-Time CDP和Journey Optimizer中，使用行銷人員友善的拖放受眾構成UI，但透過推送至資料倉儲的查詢，在倉儲中保留敏感的基礎資料，避免重複並提供對基本資料集的彈性存取，來製作受眾。
- 對象擴充：在Real-Time CDP和Journey Optimizer中建置的對象可以透過其他企業資料擴充，以其他不會在Adobe Experience Platform中儲存的設定檔和非設定檔資料集改善定位和個人化。 例如，零售品牌可能會以頂級實體位置清單來補充近期線上購買者的對象，以建立跨管道線上和店內促銷的對象。
- 設定檔擴充：團隊可以從Data Warehouse選取設定檔屬性，這些設定檔屬性對於將即時體驗保留在Real-Time CDP中的可操作客戶設定檔中至關重要，並且可透過Journey Optimizer存取。 之後，這些額外的資料點可用於下游細分和由事件行為觸發的個人化，具體取決於使用者操作和客戶使用案例。 這將允許隨同同盟對象一起提供的屬性可用於即時細分和個人化，以及客戶設定檔中保留的其他屬性和行為訊號。

同盟受眾構成可讓Real-Time CDP和Journey Optimizer客戶靈活決定要在何時使用哪些資料，並有助於避免不必要的重複資料集或整合模式。 這是運用企業資料來組織對象和高價值屬性的同盟方法的獨特組合，並結合針對當下跨管道參與最佳化的系統。 這導致資料移動較少，但也會帶來新的機會，以利用高價值受眾和屬性來跨頻道持續地低延遲啟動。

## 學習目標

- 瞭解如何連結Snowflake與Adobe Experience Platform
- 瞭解如何在Adobe Experience Platform中為您的同盟資料建立資料模型
- 瞭解如何在Adobe Experience Platform中建立同盟受眾組合

## 先決條件

- 存取Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 存取Snowflake資料倉儲

## 練習

[3.1.1設定您的Snowflake環境](./ex1.md)

在本練習中，您將設定您的Snowflake試用帳戶，並將其連結至Adobe Experience Platform

[3.1.2建立結構描述、資料模型和連結](./ex2.md)

在本練習中，您將會在AEP中設定同盟資料的資料模型。

[3.1.3建立同盟組合](./ex3.md)

在本練習中，您將會在AEP中設定同盟資料的資料模型。

[摘要和優點](./summary.md)

本單元摘要和優點概觀。

![技術內部人士](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。

[返回所有模組](../../../overview.md)
