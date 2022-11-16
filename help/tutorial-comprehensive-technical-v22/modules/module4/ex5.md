---
title: 查詢服務 — 使用Power BI探索資料集
description: 查詢服務 — 使用Power BI探索資料集
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 0f9e6719-056b-4858-8c86-04b3beaa950e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 4.5查詢服務和Power BI

開啟MicrosoftPower BI案頭。

![start-power-bi.png](./images/start-power-bi.png)

按一下 **取得資料**.

![power-bi-get-data.png](./images/power-bi-get-data.png)

搜尋 **postgres** (1)，選擇 **Postgres** (2)從清單中 **Connect** (3)。

![power-bi-connect-progress.png](./images/power-bi-connect-progress.png)

前往Adobe Experience Platform, **查詢** 和 **憑證**.

![query-service-credentials.png](./images/query-service-credentials.png)

從 **憑證** 頁面，複製 **主機** 並貼入 **伺服器** 欄位，並複製 **資料庫** 並貼入 **資料庫** 欄位，然後按一下「確定」(2)。

>[!IMPORTANT]
>
>請務必包含埠 **:80** 在伺服器值的結尾處，因為查詢服務當前未使用預設的PostgreSQL埠5432。

![power-bi-connect-server.png](./images/power-bi-connect-server.png)

在下一個對話方塊中，使用在 **憑證** 的查詢。

![query-service-credentials.png](./images/query-service-credentials.png)

在「導航器」對話框中，將 **LDAP** 在搜尋欄位(1)中找出CTAS資料集，並勾選每(2)旁的方塊。 然後按一下「載入(3)」。

![power-bi-load-churn-data.png](./images/power-bi-load-churn-data.png)

請確定 **報表** 頁簽(1)。

![power-bi-report-tab.png](./images/power-bi-report-tab.png)

選取地圖(1)，將其新增至報表畫布後，放大地圖(2)。

![power-bi-select-map.png](./images/power-bi-select-map.png)

接下來，我們需要定義測量和維度，您可從 **欄位** 區段至對應的預留位置(位於 **視覺效果**)，如下所示：

![power-bi-drag-lat-lon.png](./images/power-bi-drag-lat-lon.png)

作為衡量指標，我們會使用 **customerId**. 拖曳 **crmid** 欄位 **欄位** 區段 **大小** 佔位符：

![power-bi-drag-crmid.png](./images/power-bi-drag-crmid.png)

最後，做點 **callTopic** 分析，讓我們拖曳 **callTopic** 欄位 **頁面層級篩選器** 預留位置(您可能必須捲動 **視覺效果** 部分);

![power-bi-drag-calltopic.png](./images/power-bi-drag-calltopic.png)

選擇/取消選擇 **callTopics** 要調查：

![power-bi-report-select-calltopic.png](./images/power-bi-report-select-calltopic.png)

你已經完成了這個練習。

下一步： [4.7查詢服務API](./ex7.md)

[返回模組4](./query-service.md)

[返回所有模組](../../overview.md)
