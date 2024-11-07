---
title: Foundation — 資料擷取 — 設定資料集
description: Foundation — 資料擷取 — 設定資料集
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 7%

---

# 1.2.3設定資料集

在本練習中，您將設定擷取和儲存設定檔資訊及客戶行為所需的資料集。 您在此建立的每個資料集都會使用您在上一步中建立的其中一個結構描述。

## Story

定義問題的答案後，**此客戶是誰？**&#x200B;和&#x200B;**此客戶做什麼？**&#x200B;看起來應該類似，您現在需要建立使用該資訊的貯體，以接收及驗證傳送至Adobe Experience Platform的資料。

## 1.2.3.1 — 建立資料集

您現在需要建立2個資料集：

- 1個資料集以擷取回答&#x200B;**此客戶是誰？** — 問題。
- 1個資料集以擷取回答&#x200B;**此客戶做什麼的資訊？** — 問題。

前往此URL登入Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./images/home.png)

繼續之前，您必須選取&#x200B;**[!UICONTROL 沙箱]**。 要選取的沙箱名為``--module2sandbox--``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。

![資料擷取](./images/sb1.png)

在Adobe Experience Platform中，按一下畫面左側功能表中的&#x200B;**[!UICONTROL 資料集]**。  然後您會看到以下內容：

![資料擷取](./images/menudatasets.png)

讓我們從建立資料集以擷取網站註冊資訊開始。

您應該建立新的資料集。 若要建立新資料集，請按一下[建立資料集]按鈕&#x200B;**[!UICONTROL +。]**

![資料擷取](./images/createdataset.png)

按一下「**[!UICONTROL +建立資料集]**」按鈕後，您會看到下列畫面。

![資料擷取](./images/datasetsetup.png)

您必須使用上一步中定義的結構描述來定義資料集。 按一下&#x200B;**[!UICONTROL 從結構描述建立資料集]** — 選項。

![資料擷取](./images/datasetfromschema.png)

在下一個畫面中，您必須選取您在1， `--demoProfileLdap-- - Demo System - Profile Schema for Website`中建立的結構描述。

![資料擷取](./images/schemaselection.png)

選取結構描述後，按一下[下一步] ****&#x200B;繼續。

![資料擷取](./images/next.png)

為資料集命名。

將當作資料集的名稱，請使用以下專案：

`--demoProfileLdap-- - Demo System - Profile Dataset for Website`

例如，對於ldap **[!UICONTROL vangeluw]**，這應該是結構描述的名稱：

**[!UICONTROL vangeluw — 示範系統 — 網站的設定檔資料集]**

這應該會提供如下的內容：

![資料擷取](./images/datasetname.png)

按一下&#x200B;**[!UICONTROL 完成]**&#x200B;以完成您的資料集組態。

![資料擷取](./images/finish.png)

您現在會看到以下內容：

![資料擷取](./images/dsoverview1.png)

返回[!UICONTROL 資料集]總覽。 您現在會在概觀中看到您所建立的資料集快顯視窗。

![資料擷取](./images/dsoverview2.png)

接下來，您將設定第二個資料集以擷取網站互動。

您應該建立新的資料集。 若要建立新資料集，請按一下[建立資料集]按鈕&#x200B;**[!UICONTROL +。]**

![資料擷取](./images/createdataset.png)

按一下「**[!UICONTROL +建立資料集]**」按鈕後，您會看到下列畫面。

![資料擷取](./images/datasetsetup.png)

您必須使用上一步中定義的結構描述來定義資料集。 按一下&#x200B;**[!UICONTROL 從結構描述建立資料集]** — 選項。

![資料擷取](./images/datasetfromschema.png)

在下一個畫面中，您必須選取您在2.2 `--demoProfileLdap-- - Demo System - Event Schema for Website`中建立的結構描述。

![資料擷取](./images/schemaselectionee.png)

選取結構描述後，按一下[下一步] ****&#x200B;繼續。

![資料擷取](./images/next.png)

為資料集命名。

將資料集命名時，我們會使用這個名稱：

`--demoProfileLdap-- - Demo System - Event Dataset for Website`

例如，對於ldap **[!UICONTROL vangeluw]**，這應該是結構描述的名稱：

**[!UICONTROL vangeluw — 示範系統 — 網站的事件資料集]**

這應該會提供如下的內容：

![資料擷取](./images/datasetnameee.png)

按一下&#x200B;**[!UICONTROL 完成]**&#x200B;以完成您的資料集組態。

![資料擷取](./images/finish.png)

然後您會看到以下內容：

![資料擷取](./images/finish1.png)

返回[!UICONTROL 資料集]總覽畫面。

![資料擷取](./images/datasetsoverview.png)

您現在必須啟用資料集，使其成為Adobe Experience Platform即時客戶個人檔案的一部分。

按一下您的資料集`--demoProfileLdap--` — 示範系統 — 網站的設定檔資料集，以將其開啟。

在畫面右側找到[!UICONTROL 設定檔]切換圖示。

![資料擷取](./images/ds1.png)

按一下[!UICONTROL 設定檔]切換即可為[!UICONTROL 設定檔]啟用此資料集。

![資料擷取](./images/ds2.png)

按一下&#x200B;**[!UICONTROL 啟用]**。

![資料擷取](./images/ds3.png)

您的資料集現在已啟用[!UICONTROL 設定檔]。

返回資料集總覽，然後按一下以開啟您網站的資料集`--demoProfileLdap-- - Demo System - Event Dataset`。

在畫面右側找到[!UICONTROL 設定檔]切換圖示。

![資料擷取](./images/ds4.png)

按一下[!UICONTROL 設定檔]切換以啟用[!UICONTROL 設定檔]。

![資料擷取](./images/ds2.png)

按一下&#x200B;**[!UICONTROL 啟用]**。

![資料擷取](./images/ds5.png)

您的資料集現在已啟用[!UICONTROL 設定檔]。

下一步： [1.2.4從離線來源擷取的資料](./ex4.md)

[返回模組1.2](./data-ingestion.md)

[返回所有模組](../../../overview.md)
