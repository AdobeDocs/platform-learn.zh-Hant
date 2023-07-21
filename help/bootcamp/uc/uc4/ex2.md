---
title: Bootcamp -Customer Journey Analytics — 連線Customer Journey Analytics中的Adobe Experience Platform資料集
description: Bootcamp -Customer Journey Analytics — 連線Customer Journey Analytics中的Adobe Experience Platform資料集
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 47e02021-019c-4ea4-a7a8-003deef7c9e5
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 3%

---

# 4.2Customer Journey Analytics中的連線Adobe Experience Platform資料集

## 目標

- 瞭解Data Connection UI
- 將Adobe Experience Platform資料帶入CJA
- 瞭解人員ID和資料彙整
- 瞭解Customer Journey Analytics資料串流的概念

## 4.2.1連線

前往 [analytics.adobe.com](https://analytics.adobe.com) 以存取Customer Journey Analytics。

在Customer Journey Analytics首頁上，前往 **連線**.

![示範](./images/cja2.png)

在這裡，您可以看到CJA和平台之間建立的所有不同連線。 這些連線與Adobe Analytics中的報表套裝有相同的目標。 不過，資料的收集是完全不同的。 所有資料都來自Adobe Experience Platform資料集。

讓我們建立您的第一個連線。 按一下&#x200B;**建立新連線**。

![示範](./images/cja4.png)

然後您會看到 **建立連線** UI。

![示範](./images/cja5.png)

您現在可以為連線命名。

請使用此命名慣例： `yourLastName – Omnichannel Data Connection`.

範例：`vangeluw - Omnichannel Data Connection`

您也需要選取要使用的正確沙箱。 在沙箱功能表中，選取您的沙箱，應為 `Bootcamp`. 在此範例中，要使用的沙箱是 **Bootcamp**. 此外，您也需將 **平均每日事件數** 至 **少於100萬**.

![示範](./images/cjasb.png)

選取您的沙箱後，您可以開始將資料集新增至此連線。 按一下 **新增資料集**.

![示範](./images/cjasb1.png)

## 4.2.2選取Adobe Experience Platform資料集

搜尋資料集 `Demo System - Event Dataset for Website (Global v1.1)`. 按一下 **+** 以將資料集新增至此連線。

![示範](./images/cja7.png)

現在搜尋並核取核取方塊 `Demo System - Profile Dataset for Loyalty (Global v1.1)` 和 `Demo System - Event Dataset for Call Center (Global v1.1)`.

然後您就會擁有此專案。 按&#x200B;**「下一步」**。

![示範](./images/cja9.png)

## 4.2.3人員ID與資料彙整

### 人員 ID

目標現在是要加入這些資料集。 對於您選取的每個資料集，都會看到一個欄位，稱為 **個人ID**. 每個資料集都有專屬的人員ID欄位。

![示範](./images/cja11.png)

如您所見，其中大多數會自動選取人員ID。 這是因為在Adobe Experience Platform的每個結構描述中都會選取主要識別碼。 例如，以下是的結構描述 `Demo System - Event Schema for Call Center (Global v1.1)`，您可以看到主要識別碼已設為 `phoneNumber`.

![示範](./images/cja13.png)

不過，您仍然可以影響將使用哪個識別碼將連線的資料集拼接在一起。 您可以使用連結至資料集的結構描述中設定的任何識別碼。 按一下下拉式清單，探索每個資料集上可用的ID。

![示範](./images/cja14.png)

如前所述，您可以為每個資料集設定不同的人員ID。 這可讓您在CJA中將來自多個來源的不同資料集集合在一起。 想像一下，引入NPS或調查資料會非常有趣，並且有助於瞭解背景以及某些事情發生的原因。

人員ID欄位的名稱並不重要，只要人員ID欄位中的值相符。 例如，如果人員ID為 `email` 在一個資料集中和 `emailAddress` 在另一個，和 `dnb-bootcamp@adobe.com` 人員ID — 欄位在兩個資料集中的值相同，CJA將能夠拼接資料。

目前，還有其他限制，例如將匿名行為拼接到已知。 請在這裡檢閱常見問答： [常見問題集](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=zh-Hant).

### 使用人員ID彙整資料

現在您已瞭解使用人員ID彙整資料集的概念，接下來讓我們選擇 `email` 作為每個資料集的人員ID。

![示範](./images/cja15.png)

前往每個資料集以更新人員ID。

![示範](./images/cja12a.png)

現在填寫欄位「人員ID」，選擇 `email` 在下拉式清單中。

![示範](./images/cja17.png)

在您彙整三個資料集後，我們就可以繼續了。

| 資料集 | 人員 ID |
| ----------------- |-------------| 
| 示範系統 — 網站的事件資料集（全域v1.1） | 電子郵件 |
| 示範系統 — 忠誠度的設定檔資料集（全域v1.1） | 電子郵件 |
| 示範系統 — 客服中心的事件資料集（全域v1.1） | 電子郵件 |

您也需要確保對每個資料集都啟用以下選項：

- 匯入所有新資料
- 回填所有現有資料

按一下 **新增資料集**.

![示範](./images/cja16.png)

按一下 **儲存** 並繼續進行下一個練習。
建立您的 **連線** 您的資料可能需要幾個小時才能在CJA中使用。

![示範](./images/cja20.png)

下一步： [4.3建立資料檢視](./ex3.md)

[返回使用者流程4](./uc4.md)

[返回所有模組](./../../overview.md)
