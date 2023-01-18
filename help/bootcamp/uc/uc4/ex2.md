---
title: Bootcamp -Customer Journey Analytics — 連接Adobe Experience Platform資料集，Customer Journey Analytics
description: Bootcamp -Customer Journey Analytics — 連接Adobe Experience Platform資料集，Customer Journey Analytics
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 47e02021-019c-4ea4-a7a8-003deef7c9e5
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# 4.2連線Adobe Experience Platform資料集(Customer Journey Analytics)

## 目標

- 了解Data Connection UI
- 將Adobe Experience Platform資料帶入CJA
- 了解人員ID和資料匯整
- 了解Customer Journey Analytics中的資料串流概念

## 4.2.1連接

前往 [analytics.adobe.com](https://analytics.adobe.com) 來存取Customer Journey Analytics。

在Customer Journey Analytics首頁上，前往 **連線**.

![示範](./images/cja2.png)

您可以在這裡看到CJA和Platform之間所有不同的連線。 這些連線的目標與Adobe Analytics中的報表套裝相同。 然而，資料的收集卻完全不同。 所有資料都來自Adobe Experience Platform資料集。

讓我們建立您的第一個連線。 按一下&#x200B;**建立新連線**。

![示範](./images/cja4.png)

然後您會看到 **建立連線** UI。

![示範](./images/cja5.png)

您現在可以為連線命名。

請使用此命名慣例： `yourLastName – Omnichannel Data Connection`.

範例：`vangeluw - Omnichannel Data Connection`

您也需要選取要使用的正確沙箱。 在沙箱功能表中，選取您的沙箱，沙箱應為 `Bootcamp`. 在此範例中，要使用的沙箱為 **布坎普**. 您也需要設定 **每日事件平均數** to **不到100萬**.

![示範](./images/cjasb.png)

選取沙箱後，您就可以開始新增資料集至此連線。 按一下 **新增資料集**.

![示範](./images/cjasb1.png)

## 4.2.2選取Adobe Experience Platform資料集

搜尋資料集 `Demo System - Event Dataset for Website (Global v1.1)`. 按一下 **+** 將資料集新增至此連線。

![示範](./images/cja7.png)

現在，搜索並檢查 `Demo System - Event Dataset for Voice Assistants (Global v1.1)` 和 `Demo System - Event Dataset for Call Center (Global v1.1)`.

那你就拿這個。 按&#x200B;**「下一步」**。

![示範](./images/cja9.png)

## 4.2.3人員ID和資料匯整

### 人員 ID

現在的目標是加入這些資料集。 對於您選取的每個資料集，您會看到名為的欄位 **人員ID**. 每個資料集都有其專屬的「人員ID」欄位。

![示範](./images/cja11.png)

如您所見，其中大多數會自動選取人員ID。 這是因為在Adobe Experience Platform的每個架構中都選取了主要識別碼。 例如，以下是 `Demo System - Event Schema for Call Center (Global v1.1)`，您可以在其中看到主要識別碼已設為 `phoneNumber`.

![示範](./images/cja13.png)

不過，您仍可能影響使用哪個識別碼來拼接連線的資料集。 您可以使用連結至資料集之結構中所設定的任何識別碼。 按一下下拉式清單，探索每個資料集上可用的ID。

![示範](./images/cja14.png)

如上所述，您可以為每個資料集設定不同的人員ID。 這可讓您在CJA中將多個原始資料集的不同資料集一起顯示。 想像一下，引入NPS或調查資料，這些資料將非常有趣，有助於理解背景以及為什麼發生了某些事情。

只要人員ID欄位中的值對應，人員ID欄位的名稱就不重要。 假設我們 `email` 在一個資料集和 `emailAddress` 在另一個定義為「人員ID」的資料集中。 若 `delaigle@adobe.com` 是兩個資料集上「人員ID」欄位的相同值，CJA將能拼接資料。

目前還有其他一些限制，例如，將匿名行為連結至已知。 請在此查看常見問題集： [常見問題集](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html).

### 使用人員ID匯整資料

現在您已了解使用人員ID連結資料集的概念，接下來再選擇 `email` 做為每個資料集的人員ID。

![示範](./images/cja15.png)

前往每個資料集以更新人員ID。

![示範](./images/cja12a.png)

現在填入「人員ID」欄位，選擇 `email` 的下拉式清單中。

![示範](./images/cja17.png)

在您匯整三個資料集後，即可繼續。

| 資料集 | 人員 ID |
| ----------------- |-------------| 
| 示範系統 — 網站事件資料集（全域v1.1） | 電子郵件 |
| 示範系統 — 語音助理事件資料集（全域v1.1） | 電子郵件 |
| 示範系統 — 客服中心（全域v1.1）的事件資料集 | 電子郵件 |

您也必須確定已針對每個資料集啟用下列選項：

- 匯入所有新資料
- 回填所有現有資料

按一下 **新增資料集**.

![示範](./images/cja16.png)

按一下 **儲存** 然後去下一個練習。
建立 **連線** CJA可能需要數小時才能提供資料。

![示範](./images/cja20.png)

下一步： [4.3建立資料檢視](./ex3.md)

[返回用戶流4](./uc4.md)

[返回所有模組](./../../overview.md)
