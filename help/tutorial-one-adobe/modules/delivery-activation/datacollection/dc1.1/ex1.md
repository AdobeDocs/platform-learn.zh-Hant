---
title: 基礎 — Adobe Experience Platform資料收集和Web SDK擴充功能的設定 — 說明Adobe Experience Platform資料收集
description: 基礎 — Adobe Experience Platform資料收集和Web SDK擴充功能的設定 — 說明Adobe Experience Platform資料收集
kt: 5342
doc-type: tutorial
exl-id: 1f5dd730-d84a-4d3a-b5ef-2be3e089c7fd
source-git-commit: 9c4d585d99920f0cdfd9de083c3f020f0d8171ab
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---

# 1.1.1瞭解Adobe Experience Platform資料收集

## 內容

品牌會將Adobe Experience Platform資料收集用於許多使用案例。 這是新一代的Tag Management系統(TMS)，可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告解決方案功能，以便支援相關客戶體驗。 Adobe Experience Platform資料收集無需額外付費，所有Adobe Experience Cloud客戶均可使用此功能。 品牌可使用Adobe Experience Platform Data Collection來：

- 實作Adobe Experience Cloud應用程式以及Adobe Experience Platform。
- 為組織內不同部門提供各自要管理的&#x200B;**屬性**，以管理這些部門的不同需求。
- 可進行測試和生命週期管理。
- 插入自訂JavaScript和第三方標籤，並集中管理。

## 探索UI

移至[Adobe Experience Platform資料彙集](https://experience.adobe.com/#/data-collection/)。 確定您使用正確的環境，應該是`--aepImsOrgName--`。

>[!NOTE]
>
>本教學課程是使用環境&#x200B;**Experience Platform International**&#x200B;記錄的。 您的環境名稱可能不同，因此每當您在熒幕擷取畫面中看到&#x200B;**Experience Platform International**&#x200B;名稱時，應該將該名稱取代為您自己的環境名稱，即`--aepImsOrgName--`。

![啟動項屬性檢視](./images/launch0.png)

移至&#x200B;**標籤**。 您現在看到&#x200B;**[!UICONTROL 屬性]**&#x200B;檢視。 此處列出的屬性用於教學課程管理。 這些屬性代表：

- 應用程式和Web屬性
- 不同的網站以不同的方式為客戶提供服務。 例如，Luma Retail會有一個屬性，Luma Travel則會有另一個屬性。
- 舊版以及目前的網站
- 適用於多個不同網站的特定Adobe Analytics設計
- 內部內部網路頁面與外部網站並存

![啟動項屬性檢視](./images/launch1.png)

現在，請檢視左側邊欄。

![啟動左側邊欄](./images/launch2.png)

- **[!UICONTROL 標籤]**&#x200B;提供所有使用者端屬性的概觀
- **[!UICONTROL 應用程式介面]**&#x200B;提供啟用推播通知（與Sierra專案搭配使用/啟用）的所有應用程式設定的概觀
- **[!UICONTROL 資料串流]**&#x200B;已在[下一個練習](./ex2.md)中探索
- **[!UICONTROL 事件轉送]**&#x200B;提供在[模組2.5 - Real-Time CDP連線：事件轉送](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-5/aep-data-collection-ssf.md)中探索的所有伺服器端屬性的概觀
- **[!UICONTROL 監視]**&#x200B;提供透過事件轉送的傳入和傳出事件流量概觀
- **[!UICONTROL Assurance]**&#x200B;提供使用Adobe Debugger偵錯實作的存取權
- **[!UICONTROL 地點]**&#x200B;提供管理POI的存取權，在行動應用程式中以地點為基礎的個人化可存取這些地點
- **[!UICONTROL 結構描述]**&#x200B;提供對Adobe Experience Platform結構描述編輯器的存取權
- **[!UICONTROL 身分]**&#x200B;提供存取Adobe Experience Platform身分圖表設定的許可權

## 進一步資訊

Adobe Experience Platform資料彙集是一項非常進階的工具，其範圍超出Adobe Experience Platform教學課程。 組織可能無法使用Adobe Experience Platform資料收集來獲取其標籤管理功能，而是使用非Adobe標籤管理解決方案來插入程式碼和管理標籤。 Adobe和Adobe Professional Services支援使用非Adobe標籤管理解決方案。
有興趣進一步瞭解Adobe Experience Platform資料彙集的讀者可參閱以下內容。

- [Adobe Experience Platform資料彙集使用手冊](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hant)
- [「使用 Web SDK 實施 Adobe Experience Cloud」教學課程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hant)
- [設定使用者許可權](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=zh-Hant)
- [API檔案](https://developer.adobelaunch.com/api/)

## 後續步驟

移至[1.1.2 Edge Network、資料串流和伺服器端資料收集](./ex2.md){target="_blank"}

返回[設定Adobe Experience Platform Data Collection和Web SDK標籤擴充功能](./data-ingestion-launch-web-sdk.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
