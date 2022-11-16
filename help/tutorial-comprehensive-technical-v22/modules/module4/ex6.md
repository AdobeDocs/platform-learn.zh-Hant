---
title: 查詢服務 — 使用Tableau探索資料集
description: 查詢服務 — 使用Tableau探索資料集
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 04209eb4-b054-4a2e-885e-61f601c3fc2c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 4.6查詢服務和Tableau

開啟Tableau。

![start-tableau.png](./images/start-tableau.png)

在 **連接到伺服器** 選取 **PostgreSQL**:

![tableau-connect-postogress.png](./images/tableau-connect-postgress.png)

前往Adobe Experience Platform, **查詢** 和 **憑證**.

![query-service-credentials.png](./images/query-service-credentials.png)

從 **憑證** 頁面，複製 **主機** 並貼入 **伺服器** 欄位，複製 **資料庫** 並貼入 **資料庫** 欄位，複製 **埠** 並貼到欄位中 **埠**&#x200B;在Tableau中，對 **使用者名稱** 和 **密碼**. 下一步，按一下 **登入**.

登入：

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

按一下搜尋(1)，然後輸入 **ldap** 在搜尋欄位中，從結果集中識別您的表格，並將其拖曳(3)至名為的位置 **拖曳表格至此**. 完成後，按一下 **表1** (3)。

![tableau-drag-table.png](./images/tableau-drag-table.png)

若要將地圖上的資料視覺化，我們需要將經度和緯度轉換為維度。 在 **措施** 選取 **緯度** (1)並開啟欄位的下拉式清單，然後選取 **轉換為Dimension** (2)。 對 **經度** 測量。

![tableau-convert-dimension.png](./images/tableau-convert-dimension.png)

拖曳 **經度** 測量 **欄** 和 **緯度** 測量 **列**. 自動 **比利時** 會以小點顯示，代表外部資料集中的城市。

![tableau-drag-lon-lat.png](./images/tableau-drag-lon-lat.png)

選擇 **度量名稱** (1)，開啟下拉式清單並選取 **添加到工作表** (2):

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

您現在會有一張地圖，其中各種大小的點。 大小表示該特定城市的客服中心互動次數。 若要變更點的大小，請導覽至右側面板並開啟 **度量值** （使用下拉式圖示）。 從下拉式清單中選取 **編輯大小**. 用不同大小玩。

![tableau-vary-size-dots.png](./images/tableau-vary-size-dots.png)

若要進一步顯示 **呼叫主題**，拖曳(1) **呼叫主題** 維度 **頁面**. 導覽不同的 **呼叫主題** 使用 **呼叫主題** (2)螢幕右側：

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

你已經完成了這個練習。

下一步： [4.7查詢服務API](./ex7.md)

[返回模組4](./query-service.md)

[返回所有模組](../../overview.md)
