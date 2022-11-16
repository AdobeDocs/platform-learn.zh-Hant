---
title: 總覽
description: 資料工程師、資料分析師、資料架構師、資料科學家、協調工程師和行銷人員可以從此開始，充分了解Adobe Experience Platform及其所有應用程式服務的業務價值。
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 2%

---

# Adobe Experience Platform 的完整技術教學課程

## 總覽

本教學課程是資料工程師、資料分析師、資料架構師、資料科學家、協調工程師和行銷人員完整了解Adobe Experience Platform及其所有應用程式服務的商業價值的最佳起點。 每個課程都著重於企業在現今複雜的個人化生態系統中所面臨的真正挑戰，並分析Experience Platform如何在各種實際操作練習中解決該挑戰。 請觀看此影片，了解Adobe Experience Platform可協助您解決的問題。

>[!VIDEO](https://video.tv.adobe.com/v/344237?quality=12&enable=on)

本教學課程內容十分豐富，並提供下列應用程式的清晰分析：

- Adobe Experience Platform
- Adobe Experience Platform 資料彙集
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics
- Offer Decisioning

本教學課程不僅著重於Adobe應用程式，也考量到品牌運作的更廣泛生態系統。 為了做到這一點，在一些教訓中，重點是如何 _非Adobe_ 應用程式與Adobe Experience Platform整合。 因此，您將深入了解下列應用程式如何與Adobe Experience Platform搭配運作：

- Amazon:AWS Lambda、AWS S3、AWSKinesis
- Google:Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft:Power BI, Azure EventHub, Azure Blob儲存
- Salesforce:塔布洛
- 阿帕奇卡夫卡
- Postman
- ...

完成本教學課程後，您將能：

- 設定結構、Mixin、資料集和身分
- 設定Adobe Experience Platform資料收集屬性，並在Adobe Experience Platform資料收集中設定新的Web SDK擴充功能
- 使用Adobe Experience Platform資料收集、Google Tag Manager或Amazon Alexa，即時將資料串流至Adobe Experience Platform
- 使用工作流程或使用擷取、轉換、載入(ETL)應用程式將資料批次內嵌至Adobe Experience Platform
- 在Adobe Experience Platform中視覺化及使用即時客戶個人檔案
- 建立區段
- 使用數個Adobe Experience Platform API
- 使用SQL在Adobe Experience Platform中查詢資料
- 在Adobe Experience Platform中設定、訓練和計分機器學習模型
- 使用Journey Orchestration來設定即時、觸發式歷程
- 使用Real-time CDP，針對各種目的地啟動區段以採取行動
- 使用Customer Journey Analytics報告來自各種來源的全通路客戶資料，包括Google BigQuery

## 先決條件

- 存取 Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 存取Adobe Experience Platform資料收集： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 訪問演示系統： [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

>[!IMPORTANT]
>
>本教學課程的建立是為了便於使用特定研討會格式。 它使用您可能沒有存取權的特定系統和帳戶。 即使沒有訪問權，我們仍然認為，通過閱讀這些非常詳細的內容，您仍可以學到很多。 如果您是其中一個研討會的參與者，並需要您的訪問認證，請聯繫您的Adobe代表，他將向您提供所需資訊。

## 關於本教學課程

在這些課程中，您將使用可支援多個產業的示範網站來實作Adobe Experience Platform和應用程式服務。 示範網站和行動應用程式具有豐富的資料層和功能，可讓您建置逼真的實作。 它提供對示範品牌(例如 **盧馬**, **Citi Signal**, **EXP新聞**, **MUTUAL365**, **卡爾韋洛** 還有幾個。 您將在自己的Experience Cloud組織中建立自己的Adobe Experience Platform資料收集用戶端屬性，並將其對應至您的示範網站。 接著便會產生傳送至您自己Adobe Experience Platform例項的資料。

## 架構

開始進行實作練習之前，請先了解本教學課程背後的架構。 如上方概述所示，本教學課程將深入探討Adobe Experience Platform的多項功能，但也將討論跨多種來源和目的地的多重整合。 為了讓您正確了解本教學課程背後的架構，以及Adobe Experience Platform在您的企業生態系統中的整體定位，請從檢閱架構影片和圖表開始。

前往 [架構](./architecture.md).


## 影片

![影片](./assets/images/yt.jpeg)

你可以從我們的技術學院活動中找到很多有趣的視頻，從Bootcamp，還有更多關於我們 [Experience Makers社群YouTube頻道](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

已建立數部影片，展示Adobe Experience Platform與非Adobe應用程式之間的啟用和強大整合元素。 按一下以下連結，以取得這些影片的概觀。

前往 [影片](./videos.md).



## 如何測量您完成Adobe Experience Platform的完整技術教學課程？

如果您是以Adobe合作夥伴或Adobe員工的身分參與本教學課程，則需要在每個啟用模組完成後提交進度。

您可以在此處找到提交完成的要求和流程： [測量完成](./completion.md)

## 內容

[0.快速入門](./modules/module0/getting-started.md)

- **對象：** Adobe Experience Platform全面技術教學課程的所有參與者
- **必要條件：** 下一步存取示範系統、Adobe Experience Platform和Adobe Experience Platform資料收集。 存取Adobe Experience Platform環境的預設設定ID。
- **說明：** 在此基礎模組中，您將設定所有內容，以便存取和使用示範環境。
- **時間投資：** 30分鐘

[1. Foundation — 設定Adobe Experience Platform資料收集與Web SDK](./modules/module1/data-ingestion-launch-web-sdk.md)

- **對象：** 資料工程師，資料架構師
- **必要條件：** 存取Adobe Experience Platform和Adobe Experience Platform資料收集。
- **說明：** 在本基礎模組中，您將了解Adobe Experience Platform資料收集和新的Web SDK擴充功能。
- **時間投資：** 30分鐘

[2.基礎 — 資料擷取](./modules/module2/data-ingestion.md)

- **對象：** 資料工程師，資料架構師
- **必要條件：** 存取Adobe Experience Platform和Adobe Experience Platform資料收集。
- **說明：** 在此基礎模組中，您會將資料從網站內嵌至平台
- **時間投資：** 120分鐘

[3.基礎 — 即時客戶個人檔案](./modules/module3/real-time-customer-profile.md)

- **對象：** 資料工程師，資料架構師，行銷人員
- **必要條件：** 存取Adobe Experience Platform和Postman
- **說明：** 在此基礎模組中，您將善用UI和API，探索Adobe Experience Platform中的即時客戶個人檔案。
- **時間投資：** 90分鐘
- **下載這些資產**:
   - [Postman集合](./assets/postman/postman_profile.zip)

[4.查詢服務](./modules/module4/query-service.md)

- **對象：** 資料工程師，資料架構師，資料分析師，BI專家
- **必要條件：** 存取Adobe Experience Platform、查詢服務、Power BI或Tableau
- **說明：** 在本模組中，您將學習如何使用Adobe Experience Platform Query Service。
- **時間投資：** 90分鐘
- **下載這些資產**:
   - [JSON — 範例資料：示範系統 — 網站的事件資料集](./assets/json/ee.json)
   - [JSON — 範例資料：示範系統 — 客服中心的事件資料集](./assets/json/callcenter.json)
   - [JSON — 範例資料：示範系統 — 忠誠度的設定檔資料集](./assets/json/loyalty.json)

[5. Intelligent Services](./modules/module5/intelligent-services.md)

- **對象：** 資料工程師，資料架構師，資料科學家
- **必要條件：** 存取Adobe Experience Platform、Intelligent Services
- **說明：** 在本模組中，您將學習如何設定、設定和使用Adobe Experience Platform Intelligent Services。
- **時間投資：** 60分鐘

[6. Real-Time CDP — 建立區段並採取行動](./modules/module6/real-time-cdp-build-a-segment-take-action.md)

- **對象：** 資料架構師，協調工程師，行銷人員
- **必要條件：** 存取Adobe Experience Platform、Real-time CDP、Adobe Audience Manager、Adobe Target、AWS S3
- **說明：** 在本模組中，您將設定區段，將其啟用為串流分段，並將區段啟用至數個目的地，包括Google DV360、Google AdWords、Adobe Audience Manager、Adobe Target和S3目的地，例如SalesforceMarketing Cloud。
- **時間投資：** 90分鐘

[7.Adobe Journey Optimizer:協調](./modules/module7/journey-orchestration-create-account.md)

- **對象：** 資料工程師，資料架構師，協調工程師
- **必要條件：** 存取Adobe Experience Platform和Adobe Journey Optimizer
- **說明：** 在本模組中，您將使用Adobe Journey Optimizer來建置觸發式歷程。
- **時間投資：** 60分鐘

[8.Adobe Journey Optimizer:外部資料來源和自訂動作](./modules/module8/journey-orchestration-external-weather-api-sms.md)

- **對象：** 資料工程師、資料架構師、協調工程師、市場營銷人員
- **必要條件：** 存取Adobe Experience Platform、Adobe Journey Optimizer、開放氣象API、Twilio
- **說明：** 在本模組中，您將使用Adobe Journey Optimizer線上和離線監聽客戶行為，並透過各種管道以智慧、情境式和即時的方式回應。
- **時間投資：** 90分鐘

[9.Adobe Journey Optimizer:offer decisioning](./modules/module9/offer-decisioning.md)

- **對象：** 資料工程師、資料架構師、協調工程師、市場營銷人員
- **必要條件：** 存取Adobe Experience Platform和Offer decisioning
- **說明：** 在本模組中，您將以實作方式使用Adobe Experience Platform - Offers/Decisioning應用程式服務，來設定個人化優惠方案和您自己的優惠方案活動。
- **時間投資：** 120分鐘

[10.Adobe Journey Optimizer:事件型歷程](./modules/module10/journeyoptimizer.md)

- **對象：** 電子郵件行銷人員，協調專員，資料工程師，資料架構師，資料分析師
- **必要條件：** 存取Adobe Experience Platform和Journey Optimizer
- **說明：** 在本模組中，您將了解關於Journey Optimizer的所有須知，這可協助公司設計並提供連結、情境式和個人化的體驗給客戶。
- **時間投資：** 120分鐘

[十一、Customer Journey Analytics:在Adobe Experience Platform上使用Analysis Workspace建立控制面板](./modules/module11/customer-journey-analytics-build-a-dashboard.md)

- **對象：** 資料工程師，資料架構師，資料分析師
- **必要條件：** 存取Adobe Experience Platform和Customer Journey Analytics
- **說明：** 在此模組中，您會設定包含全通路資料（例如網站互動、行動應用程式互動、客服中心互動、店內互動等）的控制面板，以取得「離線分析」的線上資訊。
- **時間投資：** 120分鐘

[十二、Customer Journey Analytics:使用BigQuery Source Connector在Adobe Experience Platform中內嵌和分析Google Analytics資料](./modules/module12/customer-journey-analytics-bigquery-gcp.md)

- **對象：** 資料工程師，資料架構師，資料分析師
- **必要條件：** 存取Adobe Experience Platform、Customer Journey Analytics、Google雲端平台、Google BigQuery
- **說明：** 在本模組中，您將設定自己的Google Cloud Platform例項，在Google Cloud Platform中載入示範資料，然後使用BigQuery Source Connector，將該資料從Google Cloud Platform內嵌至Adobe Experience Platform。 最後，您將使用Customer Journey Analytics來視覺化該資料。
- **時間投資：** 120分鐘
- **下載這些資產**:
   - [JSON — 範例資料：示範 — 忠誠度資料](./assets/json/bqLoyalty.json)

[13.Real-Time CDP:區段啟動至Microsoft Azure事件中心](./modules/module13/segment-activation-microsoft-azure-eventhub.md)

- **對象：** 資料工程師，資料架構師，資料分析師
- **必要條件：** 存取Adobe Experience Platform、Real-time CDP和Microsoft Azure
- **說明：** 在此模組中，您將設定Microsoft Azure EventHub目的地，作為Adobe Experience Platform即時CDP的即時目的地。 您也將設定並部署Azure函式，每當Adobe Experience Platform將區段裝載傳送至您的Azure EventHub目的地時，即時觸發此函式。 您將觸發的Azure函式將顯示Adobe Experience Platform Real-time CDP啟用功能的機制。
在此模組中，您也將能了解觸發即時CDP將裝載實際傳送至指定目的地的原因。 我們也將討論區段資格的狀態及其與啟動的相關性。
- **時間投資：** 90分鐘

[十四、Real-Time CDP聯繫：事件轉送](./modules/module14/aep-data-collection-ssf.md)

- **對象：** 資料工程師，資料架構師，資料分析師
- **必要條件：** 存取Real-Time CDP連線、標籤和事件轉送屬性
- **說明：** 在本模組中，您將使用先前設定的資料集、結構描述和Adobe Experience Platform資料收集屬性來收集資料，然後將該資料從伺服器端轉送至您選擇的端點。
- **時間投資：** 90分鐘

[15.將資料從Apache Kafka流入Real-Time CDP](./modules/module15/aep-apache-kafka.md)

- **對象：** 資料分析師，資料工程師，資料架構師
- **必要條件：** 存取Adobe Experience Platform
- **說明：** 在本模組中，您將學習如何使用Adobe Experience Platform Sink Connector for Kafka Connect來設定您自己的Apache Kafka叢集、定義主題、製作者和消費者，以及將資料串流至Adobe Experience Platform。
- **時間投資：** 90分鐘

>[!NOTE]
>
>謝謝你花時間去學習關於Adobe Experience Platform的一切。 如果您有疑問，想要分享對未來內容有建議的一般性反饋，請直接聯繫Wouter Van Geluwe，方法是發送電子郵件至 **vangeluw@adobe.com**.
