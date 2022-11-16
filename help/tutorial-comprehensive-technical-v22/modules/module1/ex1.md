---
title: Foundation — 設定Adobe Experience Platform資料收集與Web SDK擴充功能 — 說明Adobe Experience Platform資料收集
description: Foundation — 設定Adobe Experience Platform資料收集與Web SDK擴充功能 — 說明Adobe Experience Platform資料收集
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: f498bb8c-659c-44b4-bb2e-36ea14640773
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 5%

---

# 1.1了解Adobe Experience Platform資料收集

## 內容

Adobe Experience Platform資料收集供品牌用於多種使用案例。 這是新一代Tag Management系統(TMS)，可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告解決方案，以便支援相關客戶體驗。 Adobe Experience Platform資料收集不需額外付費，且可供任何Adobe Experience Cloud客戶使用。 品牌可使用Adobe Experience Platform資料收集來：

- 實作Adobe Experience Cloud應用程式和Adobe Experience Platform。
- 通過為組織的不同部門提供各自的需求，來管理組織的不同部門 **屬性** 來管理。
- 允許測試和生命週期管理。
- 插入自訂javascript和第三方標籤，所有標籤都在一個位置管理。

## 探索UI

前往 [Adobe Experience Platform資料收集](https://experience.adobe.com/#/data-collection/).

前往 **標籤**. 您現在看到 **[!UICONTROL 屬性]** 檢視。 此處列出的屬性用於教學課程管理。 這些屬性表示……

- 應用程式和Web屬性
- 以不同方式為客戶提供服務的不同網站。 例如，Luma Retail會有一個屬性，Luma Travel則會有另一個屬性
- 舊版和最新網站
- 多個不同網站通用的特定Adobe Analytics設計
- 與外部站點一起的內部網頁

![啟動屬性檢視](./images/launch1.png)

現在，看看左邊的邊欄。

![啟動左側欄](./images/launch2.png)

- **[!UICONTROL 標籤]** 提供所有用戶端屬性的概觀
- **[!UICONTROL 應用程式曲面]** 提供所有應用程式設定的概觀，以啟用推播通知（會與Project Sierra搭配使用/啟用）
- **[!UICONTROL 資料流]** 在 [下次練習](./ex2.md)
- **[!UICONTROL 事件轉送]** 提供所有伺服器端屬性的概觀，如 [模組14 - Real-Time CDP連線：事件轉送](../module14/aep-data-collection-ssf.md)

## 更多資訊

Adobe Experience Platform資料收集是非常進階的工具，其範圍超過Adobe Experience Platform教學課程。 組織可能不會針對其標籤管理功能使用Adobe Experience Platform資料收集，而是會改為使用非Adobe標籤管理解決方案來插入程式碼及管理標籤。 Adobe和Adobe Professional Services支援使用非Adobe標籤管理解決方案。
以下為有興趣進一步了解Adobe Experience Platform資料收集的人士提供的進一步閱讀資料。

- [Adobe Experience Platform資料收集使用手冊](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
- [使用 Web SDK 教學課程實作 Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hant)
- [設定使用者權限](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html)
- [API檔案](https://developer.adobelaunch.com/api/)

下一步： [1.2邊緣網路、資料流和伺服器端資料收集](./ex2.md)

[返回模組1](./data-ingestion-launch-web-sdk.md)

[返回所有模組](./../../overview.md)
