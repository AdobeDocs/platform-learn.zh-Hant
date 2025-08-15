---
title: 使用同盟對象構成概觀，直接從您的資料倉儲吸引對象
description: 同盟受眾構成是一項強大的功能，可讓資料架構師和資料工程師直接從支援的資料倉儲中組織和啟用高價值受眾。
breadcrumb-title: 概觀
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: 93b787112134919444150974c7149dc10c2d0ca6
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# 使用同盟對象構成概觀，直接從您的資料倉儲吸引對象

同盟對象構成(FAC)是適用於Adobe Real-Time Customer Data Platform (Real-Time CDP)和Adobe Journey Optimizer的模組。 它也可以透過Adobe Real-Time CDP Composable Audiences使用（為客戶提供量身打造的解決方案，作為可組合CDP）。 它可讓資料架構師和資料工程師直接從[支援的企業資料倉儲](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}中組織和啟用高價值對象，而不需將客戶資料複製或移至Adobe Experience Platform (AEP)。 這種可組合的CDP方法（一種為客戶量身打造的解決方案）符合業界趨勢，讓企業能夠運用資料基礎架構打造個人化數位體驗，同時維持資料控管。

## 業務內容

SecurFinancial是一家領先的金融服務公司。 它會跨不同的來源運用其豐富的客戶資料，為許多區段提供個人化的優惠方案和行銷活動。 他們計畫使用Adobe Real-Time CDP同盟對象構成模組，讓企業能夠使用其資料倉儲進行資料管理，同時使用Adobe Experience Platform提供個人化的客戶體驗。 主要優點包括：

- **存取倉儲資料**：從支援的資料倉儲中的資料集建立高價值受眾，而不需要資料復寫。
- **將資料移動最小化**：直接在倉儲中查詢資料，不需要重複和維護資料控管。
- **整合式體驗工作流程**：針對跨管道使用案例，在Adobe Experience Platform中組織和啟用對象。
- **增強的個人化**：使用倉儲屬性豐富設定檔和對象，以支援即時、觸發的體驗。

## 業務案例

SecurFinancial想要啟動電子郵件行銷活動，重新鎖定根據信用狀況良好而具備貸款預先資格且其SecurFinancial投資組合中沒有有效貸款的客戶。 雖然他們會即時擷取線上行為資料，但由於無法將信用資訊擷取至AEP，因此在識別客戶預先資格時面臨挑戰。 為了在不移動受限制資料的情況下符合預先合格客戶的資格，他們將使用同盟對象構成來豐富其AEP行為受眾。

## 指南

本指南說明我們如何支援SecureFinancial商務模式。 具體來說，它涵蓋我們如何讓受眾接觸到需要這些受眾的系統，包括S3儲存帳戶、在Journey Optimizer中推動電子郵件行銷活動的歷程，以及針對已預先核准貸款的客戶進行現場重新目標定位。

這些步驟包括：

1. 將Adobe Experience Platform連線至企業資料倉儲。
2. 使用同盟對象構成建立對象。
3. 將同盟對象對應至外部Amazon S3目的地。
4. 使用同盟受眾資料建立客戶歷程。
5. 使用同盟資料豐富受眾。
6. 推動Edge上的「即時」個人化。

## 先決條件

若要在環境中執行類似活動，請確定您具有：

- 存取已透過Real-Time CDP或Journey Optimizer布建的Adobe Experience Platform帳戶。
- 系統管理員許可權或設定許可權的功能。
- 熟悉Adobe Experience Platform概念，例如結構描述、資料集和對象(建議：完成Experience League上的[Adobe Experience Platform播放清單簡介](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction?lang=en){target="_blank"})。
- 存取支援的[企業資料倉儲](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}。
- 用於查詢資料倉儲的SQL基本知識。
- **沙箱環境**：在您組織的執行個體中建立沙箱，以安全地實驗而不會影響生產資料。
- **Data Warehouse連線**：此教學課程使用Snowflake連線，但您可以使用任何[支援的資料倉儲](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites)。

首先，讓我們檢閱同盟對象構成的[高階架構和流程](fac-architecture-and-flow.md)。
