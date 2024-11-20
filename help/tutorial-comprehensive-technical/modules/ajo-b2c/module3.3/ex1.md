---
title: offer decisioning-Offer decisioning101
description: offer decisioning-Offer decisioning101
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
exl-id: 8a627c29-7780-455f-abe1-a69f8fe145ea
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 2%

---

# 3.3.1Offer decisioning101

## 3.3.1.1術語

若要進一步瞭解Offer Decisioning，強烈建議您閱讀[總覽](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en)，瞭解Offer Decisioning應用程式服務如何與Adobe Experience Platform搭配運作。

使用Offer Decisioning時，您需要瞭解以下概念：

| 詞語 | 說明 |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **選件** | 優惠方案是行銷訊息，其中可能包含與其關聯的規則，以指定誰有資格檢視優惠方案。 優惠具有狀態：草稿、已核准或已封存。 |
| **位置** | 位置（或頻道型別）和內容（或內容型別）的組合，優惠會出現在其中以供一般使用者使用。 實際上，這是行動裝置、網路、社交、即時訊息和非數位頻道中的文字、HTML、影像、JSON的組合。 |
| **規則** | 定義並控制一般使用者是否符合優惠方案資格的邏輯。 |
| **個人化優惠** | 根據適用性規則和限制的可自訂行銷訊息。 |
| **遞補優惠** | 當一般使用者不符合使用之集合中任何優惠方案的資格時，所顯示的預設優惠方案。 |
| **上限** | 用於優惠方案定義中，以定義某個優惠方案可總體向特定使用者顯示的次數。 |
| **優先順序** | 從優惠方案結果集決定優先順序排名的層級。 |
| **集合** | 用於從個人化優惠清單中篩選掉優惠方案的子集，以加快offer decisioning流程。 |
| **決定** | 行銷人員希望決策引擎提供適用的最佳優惠方案的一組優惠方案、位置和設定檔組合。 |
| **AEM Assets Essentials** | 適用於在Adobe Experience Cloud解決方案和Adobe Experience Platform間儲存、尋找及選取資產的通用集中式體驗。 |

{style="table-layout:auto"}

## 3.3.1.2Offer decisioning

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。 若要從一個沙箱變更為另一個沙箱，請按一下&#x200B;**PRODUCTION Prod (VA7)**，然後從清單中選取沙箱。 在此範例中，沙箱名為&#x200B;**AEP Enablement FY22**。 然後您就會進入沙箱`--aepSandboxName--`的&#x200B;**首頁**&#x200B;檢視。

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

在左側功能表中，按一下&#x200B;**選件**。 您現在會看到優惠選單，其中包含優惠、集合和決定等專案。

![位置](./images/homedec.png)

按一下&#x200B;**元件**。 您現在會看到「選件」功能表，其中包含「位置」、「標籤」、「規則」和「排名」等專案。

![位置](./images/components.png)

## 3.3.1.3版位

移至&#x200B;**位置**。

![位置](./images/placements.png)

在&#x200B;**版位**&#x200B;索引標籤中，您可以定義優惠方案的版位。 當您定義決定時，版位會定義所產生優惠的出現位置（頻道型別），以及形狀或形式（內容型別）。

如果您在Adobe Experience Platform執行個體中未看到任何版位，請按照底下和熒幕擷取畫面中的指示建立版位。

| 名稱 | 頻道型別 | 內容類型 |
| ---------------------- | ------------ | ------------ |
| **非數位 — 文字** | 非數位 | 文字 |
| **網頁 — JSON** | Web | JSON |
| **網頁 — HTML** | Web | HTML |
| **網頁 — 文字** | Web | 文字 |
| **網頁 — 影像** | Web | 影像 |
| **電子郵件 — JSON** | 電子郵件 | JSON |
| **電子郵件 — HTML** | 電子郵件 | HTML |
| **電子郵件 — 文字** | 電子郵件 | 文字 |
| **電子郵件 — 影像** | 電子郵件 | 影像 |

{style="table-layout:auto"}

**注意**：請勿變更任何已可用的位置。

按一下任何位置以視覺化其設定。

![位置](./images/placement1.png)

您現在會看到位置的所有欄位：

- 位置的&#x200B;**名稱**
- **位置ID**
- 位置的&#x200B;**頻道型別**
- 位置的&#x200B;**內容型別**，可以是&#x200B;**文字**、**HTML**、**影像**&#x200B;或&#x200B;**JSON**
- **說明**&#x200B;欄位，可新增此位置的額外說明

## 3.3.1.4決定規則

規則（也稱為適用性規則）等同於&#x200B;**對象**。 規則實際上是對象本身，唯一差異在於規則可以與選件搭配使用，以在Adobe Experience Platform中為設定檔提供最佳選件。

由於您已知道如何根據先前的啟用模組定義對象，讓我們快速重新造訪細分環境：

移至&#x200B;**規則**。 按一下&#x200B;**+建立規則**。

![決定規則](./images/rules.png)

然後您會看到Adobe Experience Platform的分段環境。

![決定規則](./images/createrule1.png)

您現在可以為即時客戶個人檔案存取所有屬於聯合結構描述的欄位，並且可以建置任何規則。

您也可前往「**對象** > ``--aepTenantId--``」，重複使用已在Adobe Experience Platform中定義的對象，這也是一件有趣的事。

![決定規則](./images/decisionruleaud.png)

然後您會看到以下內容：

![決定規則](./images/decisionruleaud1.png)

您也可設定自己的規則。 在本練習中，您將需要兩個規則：

- 全部 — 男性客戶
- 全部 — 女性客戶

如果這些規則尚未存在，請建立它們。 如果規則已存在，請使用這些規則，且不要建立新規則。

用於建立規則的屬性是&#x200B;**XDM個人設定檔** > **人員** > **性別**。

例如，以下是規則&#x200B;**all - Male Customers**&#x200B;的規則定義：

![決定規則](./images/allmale.png)

例如，以下是規則&#x200B;**all - Female Customers**&#x200B;的規則定義：

![決定規則](./images/allfemale.png)

## 3.3.1.5選件

移至&#x200B;**選件**&#x200B;並選取&#x200B;**選件**。 按一下&#x200B;**+建立選件**。

![決定規則](./images/offers1.png)

然後您會看到此快顯視窗。

![決定規則](./images/offers2.png)

現在不要建立任何選件 — 您會在下一個練習中這樣做。

您現在會看到有兩種優惠方案型別：

- 個人化優惠
- 遞補優惠

個人化優惠是應在特定情況下顯示的特定內容。 個人化優惠是專門建置的，可在符合特定條件時提供個人和情境式體驗。

遞補優惠是一項在不符合個人化優惠條件時顯示的優惠。

## 3.3.1.6決定

決定結合位置、個人化優惠集合和遞補優惠，讓Offer decisioning引擎最終根據每個個人化優惠特性（如優先順序、資格限制和總/使用者上限），為特定設定檔尋找最佳優惠。

若要設定您的&#x200B;**決定**，請按一下&#x200B;**決定**。

![決定規則](./images/activity.png)

在下一個練習中，您將設定自己的優惠和決定。

下一步： [3.3.2設定優惠和決定](./ex2.md)

[返回模組3.3](./offer-decisioning.md)

[返回所有模組](./../../../overview.md)
