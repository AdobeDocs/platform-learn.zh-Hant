---
title: 同盟對象構成高階架構和流程
seo-title: Federated Audience Composition high-level architecture & flow | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: 同盟對象構成高階架構和流程
description: 同盟對象構成的高階架構和流程概觀。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-high-level-architecture.jpg
exl-id: 4cb0b730-4206-476b-93d9-776dfbd464ff
source-git-commit: 0564f516cfba7ea09ac9da19d94f46d984e9e00a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# 同盟對象構成高階架構和流程

在深入探討支援SecurFinancial業務案例的步驟之前，我們將檢閱此可組合CDP方法的高階架構和流程。

Adobe Experience Platform中的同盟對象構成模組無需複製基礎資料即可擴充資料倉儲資料集的存取權，進而將資料移動和重複降至最低。

這也為組織提供必要的可撰寫架構，這些組織已完成倉儲所需的資料管理工作，且想要使用零複製模式，讓Adobe Experience Platform成為參與引擎。

它可讓企業快速處理儲存在一或多個資料倉儲中的資訊。 它免除了將資料內嵌至Adobe Experience的需求。 此外，它還能讓您存取企業資料倉儲中的新資料集，不過到目前為止，客戶體驗工作流程仍無法存取這些資料集。 例如，歷史交易或個人資料對於客戶參與彙總的對象層級很有用。

![fac-architecture](assets/fac-architecture.png)

現在我們繼續建立[Data Warehouse連線](data-warehouse-connection.md)。
