---
title: Experience Decisioning - Experience Decisioning 101
description: Experience Decisioning - Experience Decisioning 101
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# 3.7.1 Experience Decisioning 101

## 3.7.1.1術語

若要進一步瞭解Experience Decisioning，強烈建議您閱讀[概述](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=zh-Hant)，瞭解Offer Decisioning應用程式服務如何與Adobe Experience Platform搭配運作。

使用Offer Decisioning時，您需要瞭解下列概念：

| 詞語 | 說明 |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **選件** | 優惠方案是行銷訊息，其中可能包含與其關聯的規則，以指定誰有資格檢視優惠方案。 優惠具有狀態：草稿、已核准或已封存。 |
| **位置** | 位置（或頻道型別）和內容（或內容型別）的組合，優惠會出現在其中以供一般使用者使用。 實際上，這是行動裝置、網路、社交、即時訊息和非數位頻道中的文字、HTML、影像、JSON的組合。 |
| **規則** | 定義並控制一般使用者是否符合優惠方案資格的邏輯。 |
| **個人化優惠** | 根據適用性規則和限制的可自訂行銷訊息。 |
| **遞補優惠** | 當一般使用者不符合使用之集合中任何優惠方案的資格時，所顯示的預設優惠方案。 |
| **上限** | 用於優惠方案定義中，以定義某個優惠方案可總體向特定使用者顯示的次數。 |
| **優先順序** | 從優惠方案結果集決定優先順序排名的層級。 |
| **集合** | 用於從個人化優惠清單中篩選掉優惠方案的子集，以加快優惠方案決策流程。 |
| **決定** | 行銷人員希望決策引擎提供適用的最佳優惠方案的一組優惠方案、位置和設定檔組合。 |
| **AEM Assets Essentials** | 適用於在Adobe Experience Cloud解決方案和Adobe Experience Platform間儲存、尋找及選取資產的通用集中式體驗。 |

{style="table-layout:auto"}

## 3.7.1.2體驗決策

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。 然後您就會進入沙箱&#x200B;**的**&#x200B;首頁`--aepSandboxName--`檢視。

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

在下一個練習中，您將設定自己的優惠和決定。

## 後續步驟

移至[3.7.2設定優惠與決定](./ex2.md){target="_blank"}

返回[體驗決策](ajo-decisioning.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
