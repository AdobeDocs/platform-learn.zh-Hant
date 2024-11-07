---
title: 查詢服務 — 使用Tableau探索資料集
description: 查詢服務 — 使用Tableau探索資料集
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 5.1.6 Query Service和Tableau

開啟Tableau

![start-tableau.png](./images/start-tableau.png)

在&#x200B;**連線至伺服器**&#x200B;中，選取&#x200B;**PostgreSQL**：

![tableau-connect-postgress.png](./images/tableau-connect-postgress.png)

移至Adobe Experience Platform、移至&#x200B;**查詢**&#x200B;和&#x200B;**認證**。

![query-service-credentials.png](./images/query-service-credentials.png)

從Adobe Experience Platform的&#x200B;**認證**&#x200B;頁面，複製&#x200B;**主機**&#x200B;並將其貼到&#x200B;**伺服器**&#x200B;欄位中，複製&#x200B;**資料庫**&#x200B;並將其貼到Tableau的&#x200B;**資料庫**&#x200B;欄位中，複製&#x200B;**連線埠**&#x200B;並將其貼到Tableau的&#x200B;**連線埠**&#x200B;欄位中，對&#x200B;**使用者名稱**&#x200B;和&#x200B;**密碼**&#x200B;執行相同的操作。 接著，按一下&#x200B;**登入**。

登入：

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

按一下搜尋(1)，並在搜尋欄位中輸入您的&#x200B;**ldap**，從結果集識別您的資料表，然後將其拖曳至名為&#x200B;**將資料表拖曳到這裡**&#x200B;的位置。 完成後，按一下&#x200B;**工作表1** (3)。

![tableau-drag-table.png](./images/tableau-drag-table.png)

若要在地圖上視覺化我們的資料，必須將經度和緯度轉換為維度。 在&#x200B;**測量**&#x200B;中選取&#x200B;**緯度** (1)，並開啟欄位的下拉式清單，然後選取&#x200B;**轉換成Dimension** (2)。 對&#x200B;**經度**&#x200B;量值執行相同操作。

![tableau-convert-dimension.png](./images/tableau-convert-dimension.png)

將&#x200B;**Longitude**&#x200B;量值拖曳至&#x200B;**欄**，並將&#x200B;**緯度**&#x200B;量值拖曳至&#x200B;**列**。 **Belgium**&#x200B;的地圖會自動出現，並以小點表示out資料集中的城市。

![tableau-drag-lon-lat.png](./images/tableau-drag-lon-lat.png)

選取&#x200B;**量值名稱** (1)，開啟下拉式清單並選取&#x200B;**新增至工作表** (2)：

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

您現在會有一張地圖，內含各種大小的點。 大小代表該特定城市的客服中心互動次數。 若要改變點的大小，請導覽至右側面板，然後開啟&#x200B;**量值** （使用下拉式圖示）。 從下拉式清單中選取&#x200B;**編輯大小**。 玩不同大小的遊戲。

![tableau-vary-size-dots.png](./images/tableau-vary-size-dots.png)

若要進一步顯示每個&#x200B;**呼叫主題**&#x200B;的資料，請將(1) **呼叫主題**&#x200B;維度拖曳至&#x200B;**頁面**。 使用畫面右側的&#x200B;**通話主題** (2)，瀏覽不同的&#x200B;**通話主題**：

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

您現在已經完成此練習。

下一步： [5.1.7查詢服務API](./ex7.md)

[返回模組5.1](./query-service.md)

[返回所有模組](../../../overview.md)
