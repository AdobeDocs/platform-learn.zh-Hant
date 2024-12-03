---
title: 概觀
description: 讓資料工程師、資料分析師、資料架構師、資料科學家、協調工程師和行銷人員開始瞭解Adobe Experience Platform及其所有應用程式服務的完整商業價值。
doc-type: multipage-overview
source-git-commit: 8270f69dd04714e217ddbb4d125157799cba2940
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 2%

---

# Adobe Experience Platform 的完整技術教學課程

## 概觀

本教學課程是資料工程師、資料分析師、資料架構師、資料科學家、協調工程師和行銷人員的完美起點，可全面瞭解Adobe Experience Platform及其所有應用程式服務的商業價值。 每個課程都著重於企業在當今複雜的個人化生態系統中所面臨的真實挑戰，並細分Experience Platform如何解決各種實作練習中的挑戰。

本教學課程差異很大，為下列應用程式提供清楚的深入分析：

- Adobe Experience Platform
- Adobe Experience Platform 資料彙集
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics

本教學課程不只專注於Adobe應用程式，也考慮品牌營運的更廣泛生態系統。 為了做到這一點，在某些課程中，重點是&#x200B;_非Adobe_&#x200B;應用程式如何與Adobe Experience Platform整合。 因此，您將深入瞭解以下應用程式如何與Adobe Experience Platform搭配運作：

- Amazon： AWS Lambda、AWS S3、AWS Kinesis
- Google： Google Cloud Platform、Google BigQuery、Google Display&amp;Video 360、Google AdWords
- Microsoft：Power BI、Azure EventHub、Azure Blob儲存體
- Salesforce： Tableau
- Apache Kafka
- Postman
- ...

完成本教學課程中的練習後，您將能夠：

- 設定結構描述、欄位群組、資料集和身分
- 設定Adobe Experience Platform資料收集屬性，並在Adobe Experience Platform資料收集中設定新的Web SDK擴充功能
- 使用Adobe Experience Platform資料收集將資料即時串流到Adobe Experience Platform
- 使用工作流程或使用擷取、轉換、載入(ETL)應用程式，將資料批次擷取至Adobe Experience Platform
- 在Adobe Experience Platform中將即時客戶個人檔案視覺化及使用
- 建立客群
- 使用多個Adobe Experience Platform API
- 使用SQL在Adobe Experience Platform中查詢資料
- 設定並執行即時、觸發式歷程
- 使用Real-time CDP啟用不同目的地的受眾以採取行動
- 使用Customer Journey Analytics報告來自各種來源的全通路客戶資料，包括Google BigQuery

## 先決條件

如果您想使用自己的Adobe Experience Platform執行個體來參加此教學課程，請依照[這裡](./setup.md)的指示，為教學課程準備您的組織。

- 存取Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 存取Adobe Experience Platform資料彙集： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 存取示範系統： [https://dsn.adobe.com/](https://dsn.adobe.com/)

## 影片

您可在我們的[Experience Makers社群YouTube頻道](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw)的Tech Academy網路研討會、訓練營等影片中找到許多有趣的影片。

## 完成與認證

本教學課程是Adobe認證課程的一部分。 您可以連同本教學課程一起註冊此課程，方法是前往[https://certification.adobe.com](https://certification.adobe.com)。

使用下列教學課程完成的每個模組，都需要提交完成證明，如[此處](./completion.md)所示。

## 內容

[0.快速入門](./modules/gettingstarted/gettingstarted/getting-started.md)

在此基本單元中，您將設定所有專案，以便存取和使用示範環境。

**時間投資：** 30分鐘

### 1.資料收集

[1.1 Foundation - Adobe Experience Platform Data Collection &amp; Web SDK設定](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

在此基本單元中，您將瞭解Adobe Experience Platform資料收集和新的Web SDK擴充功能。

**時間投資：** 30分鐘

[1.2 Foundation — 資料擷取](./modules/datacollection/module1.2/data-ingestion.md)

在此基本單元中，您會將來自各種來源的資料擷取至Adobe Experience Platform

**時間投資：** 120分鐘

[1.3同盟對象構成](./modules/datacollection/module1.3/fac.md)

在本單元中，您將瞭解如何設定同盟受眾模型，並使用同盟資料產生受眾。

**時間投資：** 90分鐘

### 2. Real-Time CDP B2C

[2.1 Foundation — 即時客戶個人檔案](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

在此基本單元中，您將利用UI和API探索Adobe Experience Platform中的即時客戶個人檔案。

**時間投資：** 90分鐘

[2.2智慧型服務](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

在本單元中，您將瞭解如何設定、設定和使用Adobe Experience Platform Intelligent Services。

**時間投資：** 60分鐘

[2.3 Real-Time CDP — 建立受眾並採取行動](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

在本單元中，您將設定對象並將對象啟動至數個目的地，包括Google DV360、Adobe Target和AWS S3。

**時間投資：** 90分鐘

[2.4 Real-Time CDP：Audience Activation至Microsoft Azure事件中心](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

在此單元中，您將設定Microsoft Azure EventHub目的地為Adobe Experience Platform Real-time CDP的即時目的地。 您也會設定和部署Azure函式，每當Adobe Experience Platform將對象裝載傳遞至Azure EventHub目的地時，就會即時觸發。 您即將觸發的Azure函式將會顯示Adobe Experience Platform Real-time CDP啟用功能的機制。
在此單元中，您也會瞭解什麼會觸發Real-time CDP將裝載實際傳送至指定目的地。 我們也會討論對象資格的狀態，以及它與啟用之間的關係。

**時間投資：** 90分鐘

[2.5 Real-Time CDP連線：事件轉送](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

在此單元中，您將使用先前設定的資料集、結構描述和Adobe Experience Platform資料收集屬性來收集資料，然後將該資料伺服器端轉送至數個端點，例如Google Cloud Platform Pub/Sub和AWS Kinesis。

**時間投資：** 90分鐘

[2.6將Apache Kafka的資料串流至Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

在本單元中，您將瞭解如何設定您自己的Apache Kafka叢集、定義主題、製作者和消費者，並使用Kafka Connect的Adobe Experience Platform Sink Connector將資料串流到Adobe Experience Platform。

**時間投資：** 90分鐘

### 3. Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer：協調流程](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

在此單元中，您將使用Adobe Journey Optimizer來建置觸發式歷程。

**時間投資：** 60分鐘

[3.2 Adobe Journey Optimizer：外部資料來源和自訂動作](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

在此單元中，您將使用Adobe Journey Optimizer來線上及離線監聽客戶行為，並透過各種管道以智慧、情境式及即時方式回應。

**時間投資：** 90分鐘

[3.3 Adobe Journey Optimizer：Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

在此單元中，您將以實作方式使用Adobe Experience Platform - Offers/Decisioning應用程式服務來設定個人化優惠方案和您自己的優惠方案活動。

**時間投資：** 120分鐘

[3.4 Adobe Journey Optimizer：事件型歷程](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

在本單元中，您將瞭解Journey Optimizer的所有須知事項，其可幫助公司為其客戶設計和提供連結、情境式和個人化的體驗。

**時間投資：** 120分鐘

### 4.Adobe Customer Journey Analytics

[4.1Customer Journey Analytics：在Adobe Experience Platform之上使用Analysis Workspace建置控制面板](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

在此單元中，您可以設定包含全通路資料（例如網站互動、行動應用程式互動、客服中心互動、商店內互動等）的儀表板，以獲得線上到離線深入分析。

**時間投資：** 120分鐘

[4.2Customer Journey Analytics：使用BigQuery Source Connector在Adobe Experience Platform中擷取和分析Google Analytics資料](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

在本單元中，您將設定自己的Google Cloud Platform執行個體、在Google Cloud Platform中載入示範資料，然後使用BigQuery Source Connector將該資料從Google Cloud Platform擷取到Adobe Experience Platform。 最後，您可以使用Customer Journey Analytics將該資料視覺化。

**時間投資：** 120分鐘

### 5.資料Distiller

[5.1查詢服務](./modules/datadistiller/module5.1/query-service.md)

在本單元中，您將學習如何使用Adobe Experience Platform查詢服務。

**時間投資：** 90分鐘