---
title: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
description: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# 4.1Customer Journey Analytics101

## 目標

- 了解CJA應用程式服務
- 了解如何定位CJA
- 了解CJA工作流程：從資料連接到深入分析

## 4.1.1什麼是Customer Journey Analytics?

Customer Journey Analytics(CJA)為商業情報和資料科學團隊提供工具套件，以匯整和分析跨管道資料（線上和離線）。 CJA中的功能可提供內容，並清晰明瞭複雜的多管道客戶歷程。 提供的內容可提供可操作的深入分析，讓您從客戶轉換程式中去除棘手問題，並針對最重要的時刻設計和提供優越體驗。

CJA將Analysis Workspace帶上Adobe Experience Platform。 Adobe Experience Platform是溝通與協調的大腦，有了CJA，品牌現在可以將所有資料進行情境化和視覺化，讓業務和分析團隊能夠透過分析完整的線上至離線客戶歷程從中學習。

透過Analysis Workspace的拖放、點按和方便使用的UI，業務和Insight團隊可以與CJA對話、提出問題並即時取得解答。

![示範](./images/cja-adv-analysis1.png)

## 4.1.2主要優點

客戶的三大優點：

- 讓每個人都能查看深入分析的能力（例如讓資料存取大眾化）
- 可在內容歷程中查看客戶（亦即資料可依序視覺化，橫跨線上和離線多個管道）
- 不需要就能駕馭資料的力量（亦即，它可讓一般人使用資料來發掘深入見解及分析，以利行銷活動）

## 4.1.3為什麼選擇Customer Journey Analytics?

CJA不是要取代目前的BI應用程式，例如Power BI、Microstrategy、Locker或Tableau。 這些BI應用程式的用意是視覺化資料，以建立公司控制面板，讓組織中的每個人都能快速查看重要量度。\
CJA的目標是為行銷和業務團隊帶來分析功能，使其成為這些角色的「必備」分析工具。

傳統上，BI應用程式無法實現真正的客戶智慧：

- 他們無法進行歸因，也無法進行客戶歷程分析。
- BI應用程式需要提前了解問題
- 互動式查詢受資料庫結構的限制
- 需要SQL技能。
- BI應用程式無法讓您詢問為何發生某些情況。
- BI應用程式與客戶接觸點沒有直接連線。

由於上述原因，業務用戶和分析師幾乎立即陷入死衚衕，導致分析成本昂貴、速度慢、不靈活，而且與行動系統脫節。

透過CJA，您可以使用離線和線上資料，以360度檢視客戶歷程，並擁有適當的工具來縮短深入分析的時間，讓商務使用者在了解某件事發生的原因及如何回應時不受影響。

![示範](./images/cja-use-case.png)

## 4.1.4了解Customer Journey Analytics工作流程

在開始下一個練習之前，請務必了解將資料從Adobe Experience Platform匯入CJA所需的步驟，以便加以視覺化並獲得深入見解。 這就是我們所謂的CJA Workflow。 讓我們看一下：

![示範](./images/cja-work-flow.jpg)

開始上述步驟之前，請別忘記步驟0，這是為了了解Adobe Experience Platform中可用的資料。

**垃圾進去，垃圾出去。** 記得嗎？ 您必須清楚了解哪些資料可供使用，以及Adobe Experience Platform中的結構設定方式。 了解Adobe Experience Platform中的資料不僅可讓資料連線部分更輕鬆，在建立視覺效果和進行分析時也能更輕鬆。

## 4.1.5步驟0:了解Adobe Experience Platform結構和資料集

前往此URL登入Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

登入後，您會登陸Adobe Experience Platform首頁。

![資料擷取](../uc1/images/home.png)

繼續之前，您需要選取 **沙箱**. 要選取的沙箱已命名 ``Bootcamp``. 您可以按一下文字 **[!UICONTROL 生產]** 在螢幕的右上角。 選取適當的沙箱後，畫面會變更，現在您就位於專用的沙箱中。

![資料擷取](../uc1/images/sb1.png)

請參閱Adobe Experience Platform中的這些結構和資料集。

| 資料集 | 方案 |
| ----------------- |-------------| 
| 示範系統 — 網站事件資料集（全域v1.1） | 示範系統 — 網站事件結構（全域v1.1） |
| 示範系統 — 客服中心（全域v1.1）的事件資料集 | 示範系統 — 客服中心（全域v1.1）的事件結構 |
| 示範系統 — 語音助理事件資料集（全域v1.1） | 示範系統 — 語音助理的事件結構（全域v1.1） |

請務必至少檢查下列項目：

- 身分：CRMID, phoneNumber, ECID，電子郵件。 哪些身分是主要識別碼，哪些是次要識別碼？
您可以開啟結構並查看物件，以尋找識別碼 `_experienceplatform.identification.core`. 查看結構 [示範系統 — 網站事件結構（全域v1.1）](https://experience.adobe.com/platform/schema).

![示範](./images/identity.png)

- 探索架構內的商務物件 [示範系統 — 網站事件結構（全域v1.1）](https://experience.adobe.com/platform/schema).

![示範](./images/commerce.png)

- 預覽所有 [資料集](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) 並查看資料

您現在已可以開始使用Customer Journey AnalyticsUI。

下一步： [4.2連線Adobe Experience Platform資料集(Customer Journey Analytics)](./ex2.md)

[返回用戶流4](./uc4.md)

[返回所有模組](../../overview.md)
