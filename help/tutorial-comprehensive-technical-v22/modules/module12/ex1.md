---
title: 使用BigQuery Source Connector擷取和分析Adobe Experience Platform中的Google Analytics資料 — 建立您的Google雲端平台帳戶
description: 使用BigQuery Source Connector擷取和分析Adobe Experience Platform中的Google Analytics資料 — 建立您的Google雲端平台帳戶
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 632ff2fe-ae56-4481-b281-c11224b18639
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# 12.1建立您的Google雲端平台帳戶

## 目標

- 建立您的Google Cloud Platform帳戶
- 熟悉Google Cloud Platform Console
- 建立並準備您的BigQuery專案

## 12.1.1為何將Google BigQuery連線至Adobe Experience Platform以取得Google Analytics資料

Google雲端平台(GCP)是Google提供的一套公用雲端運算服務。 Google雲端平台包含多種托管服務，可在Google硬體上執行，用於計算、儲存和應用程式開發。

BigQuery是這些服務之一，一律包含在Google Analytics360中。 當我們嘗試直接從資料中取得資料時，Google Analytics資料會經常取樣（例如API）。 這就是為什麼Google包含BigQuery來取得未取樣的資料，讓品牌能使用SQL進行進階分析，並受益於GCP的強大功能。

Google Analytics資料會使用批次機制每天載入到BigQuery中。 因此，將此GCP/BigQuery整合用於即時個人化和啟動使用案例沒有任何意義。

如果品牌想要根據Google Analytics資料提供即時個人化使用案例，可以使用Google Tag Manager在網站上收集該資料，然後即時串流至Adobe Experience Platform。

GCP/BigQuery Source Connector應用於……

- 追蹤網站上的所有客戶行為，並在Adobe Experience Platform中載入該資料以進行分析、資料科學和個人化使用案例，不需要即時啟動。
- 將Google Analytics歷史資料重新載入Adobe Experience Platform，以利分析和資料科學使用案例

## 12.1.2建立您的Google帳戶

若要取得Google Cloud Platform帳戶，您需要Google帳戶。

## 12.1.3啟用您的Google雲端平台帳戶

現在您擁有Google帳戶，即可建立Google雲端平台環境。 若要這麼做，請前往 [https://console.cloud.google.com/](https://console.cloud.google.com/).

在下一頁，接受條款與條件。

![示範](./images/ex1/1.png)

下一步，按一下 **選取專案**.

![示範](./images/ex1/2.png)

按一下 **新增專案**.

![示範](./images/ex1/createproject.png)

依照此命名慣例為專案命名：

| 《公約》 | 範例 |
| ----------------- |-------------| 
| `--demoProfileLdap---googlecloud` | delaigle-goglecloud |

![示範](./images/ex1/3.png)

按一下&#x200B;**建立**。

![示範](./images/ex1/3-1.png)

等到畫面右上方的通知指出建立已完成。 然後，按一下 **檢視專案**.

![示範](./images/ex1/4.png)

接下來，前往畫面上方的搜尋列並輸入 **BigQuery**. 選取第一個結果。

![示範](./images/ex1/7.png)

接著，系統會將您重新導向至BigQuery主控台，您會看到快顯訊息。

**按一下「完成」**。

![示範](./images/ex1/5.png)

此模組的目標是將Google Analytics資料匯入Adobe Experience Platform。 為此，我們需要Google Analytics資料集中的虛擬資料才能開始。

按一下 **新增資料** ，然後按一下 **探索公開資料集**.

![示範](./images/ex1/18.png)

然後您會看到此視窗：

![示範](./images/ex1/19.png)

輸入搜索詞 **Google Analytics範例** 在搜尋列中選取第一個結果。

![示範](./images/ex1/20.png)

您會看到下列畫面，其中包含資料集的說明。 按一下 **檢視資料集**.

![示範](./images/ex1/21.png)

接著，系統會將您重新導向至BigQuery，您會在其中看到此內容 **bigquery-public-data** 資料集 **瀏覽器**.

![示範](./images/ex1/22a.png)

在 **瀏覽器**，您現在應該會看到許多表格。 歡迎探索。 前往 `google_analytics_sample`.

![示範](./images/ex1/22.png)

按一下以開啟表格 `ga_sessions`.

![示範](./images/ex1/23.png)

在繼續下一個練習之前，請在電腦上的單獨文本檔案中記下以下內容：

| 憑據 | 命名 | 範例 |
| ----------------- |-------------| -------------|
| 專案名稱 | `--demoProfileLdap---googlecloud` | 萬熱盧 |
| 專案 ID | random | comperted-task-306413 |

按一下 **專案名稱** 在頂端功能表列中：

![示範](./images/ex1/projectMenu.png)

接著，您會在右側看到您的專案ID:

![示範](./images/ex1/projetcselection.png)

您現在可以改用練習12.2，在練習中，您會查詢Google Analytics資料，弄臟手。

下一步： [12.2在BigQuery中建立第一個查詢](./ex2.md)

[返回模組12](./customer-journey-analytics-bigquery-gcp.md)

[返回所有模組](./../../overview.md)
