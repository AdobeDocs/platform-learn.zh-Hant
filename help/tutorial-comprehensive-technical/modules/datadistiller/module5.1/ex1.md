---
title: 查詢服務 — 快速入門
description: 查詢服務 — 快速入門
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# 5.1.1快速入門

## 5.1.1.1熟悉Adobe Experience Platform UI

移至[Adobe Experience Platform](https://experience.adobe.com/platform)。 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./../../../modules/datacollection/module1.2/images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--module7sandbox--``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。

![資料擷取](./../../../modules/datacollection/module1.2/images/sb1.png)


## 5.1.1.2探索平台上的資料

對於任何品牌而言，從不同管道取得資料都是一項艱鉅的任務。 在此練習中，Citi Signal客戶在其網站、行動應用程式上與Citi Signal互動，購買資料由Citi Signal的銷售點系統收集，他們有CRM和忠誠度資料。 Citi Signal使用Adobe Analytics和Adobe Launch來擷取其網站、行動應用程式以及POS系統的資料，因此這些資料已流入Adobe Experience Platform。 讓我們先來探索Adobe Experience Platform中已存在的Citi Signal所有資料。

在左側功能表中，移至&#x200B;**資料集**。

![emea-website-interaction-dataset.png](./images/emea-website-interaction-dataset.png)

Citi Signal正在將資料串流至Adobe Experience Platform，此資料可在`Demo System - Event Dataset for Website (Global v1.1)`資料集中取得。 搜尋`Demo System - Event Dataset for Website`。

![emea-callcenter-interaction-dataset.png](./images/emea-website-interaction-dataset1.png)

已在`Demo System - Event Dataset for Call Center (Global v1.1)`資料集中擷取Citi Signal的呼叫中心互動資料。 在搜尋方塊中搜尋`Demo System - Event Dataset for Call Center`資料。 按一下資料集的名稱以開啟。

![emea-callcenter-interaction-dataset.png](./images/emea-callcenter-interaction-dataset.png)

按一下資料集後，您將會獲得資料集活動的概覽，例如擷取和失敗的批次。

![preview-interaction-dataset.png](./images/preview-interaction-dataset.png)

按一下&#x200B;**預覽資料集**&#x200B;以檢視`Demo System - Event Dataset for Call Center (Global v1.1)`資料集中儲存的資料範例。 左側面板會顯示此資料集的結構描述。

![explore-interaction-dataset.png](./images/explore-interaction-dataset.png)

按一下「**關閉**」按鈕以關閉「**預覽資料集**」視窗。

## 5.1.1.3查詢服務簡介

按一下左側功能表中的&#x200B;**查詢**，即可存取Adobe Experience Platform查詢服務。

![select-queries.png](./images/select-queries.png)

移至&#x200B;**Log**，您會看到「查詢清單」頁面，此頁面會提供您在此組織中執行的所有查詢清單，最新的查詢會顯示在頂端。

![query-list.png](./images/query-list.png)

按一下清單中的任何SQL查詢，並觀察右側邊欄中提供的詳細資訊。

![click-sql-query.png](./images/click-sql-query.png)

您可以捲動視窗以檢視整個查詢，也可以按一下下面醒目提示的圖示以將整個查詢複製到您的記事本。 您目前不必複製查詢。

![click-copy-query.png](./images/click-copy-query.png)

您不能只看到已執行的查詢，此使用者介面可讓您從查詢建立新的資料集。 這些資料集可以連結到Adobe Experience Platform的即時客戶個人檔案，或用作Adobe Experience Platform資料科學Workspace的輸入。

## 5.1.1.4將PSQL使用者端連線至查詢服務

查詢服務支援具有PostgreSQL驅動程式的使用者端。 在此我們將使用PSQL、命令列介面以及Power BI或Tableau。 讓我們連線到PSQL。

按一下&#x200B;**認證**。

![queries-select-configuration.png](./images/queries-select-configuration.png)

您將會看到下方的畫面。 「組態」畫面會提供伺服器資訊和認證，以驗證「查詢服務」。 目前，我們著重於包含PSQL連線指令的畫面右側。 按一下「複製」按鈕，將命令複製到剪貼簿。

![copy-psql-connection.png](./images/copy-psql-connection.png)

Windows：按下Windows鍵並輸入cmd，然後按一下「命令提示字元」結果以開啟命令列。

![open-command-prompt.png](./images/open-command-prompt.png)

macOS：透過Spotlight搜尋開啟terminal.app：

![open-terminal-osx.png](./images/open-terminal-osx.png)

貼上您從Query Service UI複製的連線命令，然後在命令提示字元視窗中按下Enter：

Windows：

![command-prompt-connected.png](./images/command-prompt-connected.png)

macOS：

![command-prompt-paste-osx.png](./images/command-prompt-paste-osx.png)

您現在已使用PSQL連線至查詢服務。

在接下來的練習中，將會有一些與此視窗的互動。 我們將它稱為您的&#x200B;**PSQL命令列介面**。

現在您已準備好開始提交查詢。

下一步： [5.1.2使用查詢服務](./ex2.md)

[返回模組5.1](./query-service.md)

[返回所有模組](../../../overview.md)
