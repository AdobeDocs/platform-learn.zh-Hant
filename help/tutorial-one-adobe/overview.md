---
title: 概覽 — 完整技術教學課程 — One Adobe
description: 完整技術教學課程 — One Adobe
doc-type: multipage-overview
exl-id: 5bc0d621-0662-4d94-80a0-b6c173c0ac9e
source-git-commit: f25c1705ae6813dc744945e8a4ee9858513f7374
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 2%

---

# 完整技術教學課程 — One Adobe

![技術內部人士](./assets/images/techinsiders.png){width="50px" align="left"}

## 概觀

本教學課程是您的最佳起點

本教學課程差異很大，為下列應用程式提供清楚的深入分析：

- Adobe Firefly服務
- Adobe Photoshop
- Adobe Workfront與Adobe Workfront Fusion
- Adobe Experience Manager Cloud Service、Sites、Assets和Edge Delivery Services
- Adobe Experience Platform
- Adobe Real-Time CDP
- Adobe Journey Optimizer


本教學課程不只專注於Adobe應用程式，也考慮品牌營運的更廣泛生態系統。 為此，在某些課程中，重點是非Adobe應用程式如何與Adobe應用程式整合。 因此，您將深入瞭解以下應用程式如何與Adobe Experience Platform搭配運作：

- Amazon AWS
- Google Cloud Platform
- Microsoft Azure
- Postman
- Snowflake
- ...

## 先決條件

如果您想使用自己的Adobe Experience Cloud執行個體來參加此教學課程，您必須在執行個體中布建下列應用程式，而且必須能夠存取：

- Adobe Firefly [https://firefly.adobe.com/](https://firefly.adobe.com/){target="_blank"}
- Adobe Photoshop
- Adobe Workfront
- Adobe Workfront Fusion [https://fusion.adobe.com/](https://fusion.adobe.com/){target="_blank"}
- Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform){target="_blank"}
- Adobe Experience Platform資料彙集： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/){target="_blank"}
- 存取示範系統： [https://dsn.adobe.com/](https://dsn.adobe.com/){target="_blank"}

## 前期工作

在[這裡](./prework.md){target="_blank"}確認需要安裝在您電腦上的必要應用程式。

## 完成與認證

本教學課程是Adobe認證課程的一部分。 您可以連同本教學課程一起註冊此課程，方法是前往[https://certification.adobe.com](https://certification.adobe.com)。

使用下列教學課程完成的每個模組，都需要提交完成證明，如[此處](./completion.md)所示。

## 內容

若要檢查下列內容的狀態，請移至[狀態頁面](./status.md){target="_blank"}。

### 快速入門

[開始使用](./modules/getting-started/gettingstarted/getting-started.md){target="_blank"}

在此基本單元中，您將設定所有專案，以便存取和使用示範環境。

### 1.工作流程與規劃

### 2.建立與生產

[1.1 Adobe Firefly服務](./modules/creation-production/module1.1/firefly-services.md){target="_blank"}

在此單元中，您將使用Adobe Firefly Services API、Photoshop API和Microsoft Azure儲存服務產生影像並以程式設計方式儲存。

[1.2使用Workfront Fusion自動化創意工作流程](./modules/creation-production/module1.2/automation.md){target="_blank"}

在此基本單元中，您將使用Adobe Workfront Fusion來自動化及調整您的內容建立工作流程。

### 3.資產管理

[1.1 Adobe Experience Manager Cloud Service與Edge Delivery Services](./modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}

在此基本單元中，您將設定Adobe Experience Manager Cloud Service計畫、網站和Assets存放庫。

[1.2使用Adobe Workfront管理工作流程](./modules/asset-mgmt/module2.2/workfront.md){target="_blank"}

在此基本單元中，您將設定並使用Adobe Workfront來管理核准流程，並將使用與Adobe Experience Manager Assets、通用編輯器、Photoshop等整合。

### 4.傳遞與啟用

#### 資料收集

[1.1基礎 — Adobe Experience Platform資料收集與網頁SDK的設定](./modules/delivery-activation/datacollection/dc1.1/data-ingestion-launch-web-sdk.md)

在本基本單元中，您將瞭解Adobe Experience Platform資料收集和新的Web SDK擴充功能。

[1.2 Foundation — 資料擷取](./modules/delivery-activation/datacollection/dc1.2/data-ingestion.md)

在此基本單元中，您會將來自各種來源的資料擷取至Adobe Experience Platform

[1.3同盟對象構成](./modules/delivery-activation/datacollection/dc1.3/fac.md)

在本單元中，您將瞭解如何設定同盟受眾模型，並使用同盟資料產生受眾。

#### Real-Time CDP B2C

[2.1 Foundation — 即時客戶個人檔案](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-1/real-time-customer-profile.md)

在此基本單元中，您將利用UI和API探索Adobe Experience Platform中的即時客戶個人檔案。

[2.2智慧型服務](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-2/intelligent-services.md)

在本單元中，您將瞭解如何設定、設定和使用Adobe Experience Platform Intelligent Services。

[2.3 Real-Time CDP — 建立受眾並採取行動](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/real-time-cdp-build-a-segment-take-action.md)

在本單元中，您將設定對象並將對象啟動至數個目的地，包括Google DV360、Adobe Target和AWS S3。

[2.4 Real-Time CDP： Audience Activation至Microsoft Azure事件中心](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-4/segment-activation-microsoft-azure-eventhub.md)

在此單元中，您將設定Microsoft Azure EventHub目的地為Adobe Experience Platform Real-time CDP的即時目的地。

[2.5 Real-Time CDP連線：事件轉送](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-5/aep-data-collection-ssf.md)

在本單元中，您會將資料伺服器端轉送至數個端點，例如Google Cloud Platform Pub/Sub和AWS Kinesis。

[2.6將Apache Kafka的資料串流至Real-Time CDP](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-6/aep-apache-kafka.md)

在本單元中，您將瞭解如何設定自己的Apache Kafka叢集，並將資料串流至Adobe Experience Platform。

#### Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer：協調流程](./modules/delivery-activation/ajo-b2c/ajob2c-1/journey-orchestration-create-account.md)

在此單元中，您將使用Adobe Journey Optimizer來建置觸發式歷程。

[3.2 Adobe Journey Optimizer：外部資料來源和自訂動作](./modules/delivery-activation/ajo-b2c/ajob2c-2/journey-orchestration-external-weather-api-sms.md)

在此單元中，您將使用Adobe Journey Optimizer來線上及離線監聽客戶行為，並透過各種管道以智慧、情境式及即時方式回應。

[3.3 Adobe Journey Optimizer： Offer Decisioning](./modules/delivery-activation/ajo-b2c/ajob2c-3/offer-decisioning.md)

在此單元中，您將使用Adobe Journey Optimizer來設定個人化優惠和您自己的優惠決定。

[3.4 Adobe Journey Optimizer：事件型歷程](./modules/delivery-activation/ajo-b2c/ajob2c-4/journeyoptimizer.md)

在本單元中，您將瞭解Journey Optimizer的所有須知事項，其可幫助公司為其客戶設計和提供連結、情境式和個人化的體驗。

[3.5 Adobe Journey Optimizer：翻譯服務](./modules/delivery-activation/ajo-b2c/ajob2c-5/ajotranslationsvcs.md)

在本單元中，您將瞭解如何設定並使用Adobe Journey Optimizer中的翻譯服務，將您的訊息當地語系化給您的客戶。

### 5.報表與深入分析

#### Adobe Customer Journey Analytics

[1.1 Customer Journey Analytics：使用Analysis Workspace在Adobe Experience Platform之上建立儀表板](./modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)

在本單元中，您將透過設定包含全頻道資料的儀表板，取得線上到離線深入分析。

[1.2 Customer Journey Analytics：使用BigQuery Source Connector在Adobe Experience Platform中擷取和分析Google Analytics資料](./modules/reporting-insights/cja-b2c/cjab2c-2/customer-journey-analytics-bigquery-gcp.md)

在本單元中，您將設定自己的Google Cloud Platform執行個體、在Google Cloud Platform中載入示範資料，然後使用BigQuery Source Connector將該資料從Google Cloud Platform擷取到Adobe Experience Platform。

#### 資料蒸餾器

[2.1查詢服務](./modules/reporting-insights/datadistiller/dd-1/query-service.md)

在本單元中，您將學習如何使用Adobe Experience Platform查詢服務。

![技術內部人士](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。
