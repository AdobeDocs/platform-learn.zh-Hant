---
title: 透過同盟對象構成解鎖跨管道見解
description: 同盟受眾構成是一項強大的功能，可讓資料架構師和資料工程師直接從第三方資料倉儲建立受眾，並擴充受眾。
breadcrumb-title: 概觀
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: 15619a8419f608da6a77745fabf72c356a2ac4b4
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 概觀

同盟對象構成是一項功能強大的功能，可供Adobe Real-Time Customer Data Platform (Real-Time CDP)和Adobe Journey Optimizer環境使用。 它可讓資料架構師和資料工程師直接從[支援的協力廠商資料倉儲](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}建立及擴充對象，而不需將資料複製到Adobe Experience Platform。 本教學課程為技術使用者提供實作指引，協助他們連線企業資料倉儲、建立和豐富受眾，以及針對個人化行銷體驗啟用受眾。

## 視覺化指南

本視覺化指南會針對支援業務案例各個層面而採取的所有活動，向您展示相關步驟。 目標是要提供您可在環境中運用的活動，包括：

- 將Adobe Experience Platform連線至企業資料倉儲。
- 使用同盟對象構成建立和管理對象。
- 將同盟對象對應至外部目的地，例如Amazon S3。
- 透過同盟資料豐富現有對象。
- 建立受眾以推動「即時」個人化。
- 使用同盟受眾資料建置客戶歷程。

本指南專為使用Real-Time CDP或Journey Optimizer的資料架構師和資料工程師所設計。 此教學課程假設您已熟悉Adobe Experience Platform和基本的Data Warehouse概念。

## 業務內容

SecurFinancial是一家領先的金融服務公司。 它會跨不同的來源運用其豐富的客戶資料，為許多區段提供個人化的優惠方案和行銷活動。 他們計畫使用Adobe的Real-Time CDP同盟對象構成功能，此功能可讓企業使用其現有的資料倉儲，同時使用Adobe Experience Platform的應用程式來提供個人化的客戶體驗。 主要優點包括：

- **存取倉儲資料**：從支援的資料倉儲中的資料集建立高價值受眾，而不需要資料復寫。
- **將資料移動最小化**：直接在倉儲中查詢資料，減少重複並維護資料控管。
- **整合式體驗工作流程**：針對跨管道使用案例，在Adobe Experience Platform中組織和啟用對象。
- **增強的個人化**：使用倉儲屬性豐富設定檔和對象，以支援即時、觸發的體驗。

## 業務案例

SecurFinancial想要啟動電子郵件行銷活動，重新鎖定根據信用狀況良好而具備貸款預先資格且其SecurFinancial投資組合中沒有有效貸款的客戶。 雖然他們會即時擷取線上行為資料，但由於無法將信用資訊擷取至AEP，因此在識別客戶預先資格時面臨挑戰。 為了在不移動受限制資料的情況下符合預先資格的客戶的資格，他們將使用同盟對象構成來豐富其AEP行為對象。

## 先決條件

若要在環境中執行類似活動，請確定您具有：

- 存取已透過Real-Time CDP或Journey Optimizer布建的Adobe Experience Platform帳戶。
- 系統管理員許可權或設定許可權的功能。
- 熟悉Adobe Experience Platform概念，例如結構描述、資料集和對象(建議：完成Experience League上的[Adobe Experience Platform播放清單簡介](https://experienceleague.adobe.com/zh-hant/playlists/experience-platform-introduction?lang=en){target="_blank"})。
- 存取支援的企業資料倉儲(例如Amazon Redshift、Azure Synapse Analytics、Snowflake或Google BigQuery)。
- 用於查詢資料倉儲的SQL基本知識。
- **沙箱環境**：在您組織的Real-Time CDP執行個體中建立沙箱，以安全地實驗而不會影響生產資料。
- **Data Warehouse連線**：此教學課程使用Snowflake連線，但您可以使用任何[支援的雲端倉儲](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/start/access-prerequisites)。

讓我們從[Data Warehouse連線](data-warehouse-connection.md)開始。
