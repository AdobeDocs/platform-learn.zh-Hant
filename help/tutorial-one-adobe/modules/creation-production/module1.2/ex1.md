---
title: Workfront Fusion 快速入門
description: 瞭解如何使用Workfront Fusion和Adobe I/O來查詢Adobe Firefly Services API
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: 603e48e0453911177823fe7ceb340f8ca801c5e1
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---

# 1.2.1 Workfront Fusion快速入門

瞭解如何使用 Workfront Fusion 和 Adobe Systems I/O 來查詢 Adobe Systems Firefly Services API。

## 1.2.1.1 建立新藍本

轉到 [https://experience.adobe.com/](https://experience.adobe.com/)。 開啟 **Workfront Fusion**。

![WF 融合](./images/wffusion1.png)

轉到 **“方案**”。

![WF Fusion](./images/wffusion2.png)

按一下&#x200B;**+圖示**，為您的工作建立新資料夾。

![WF Fusion](./images/wffusion2a.png)

為資料夾命名`--aepUserLdap--`並選取&#x200B;**儲存**。

![WF Fusion](./images/wffusion2b.png)

選取您的資料夾，然後選取&#x200B;**建立新情境**。

![WF Fusion](./images/wffusion3.png)

出現空白情境，請選取&#x200B;**工具**&#x200B;並選取&#x200B;**設定多個變數**。

![WF Fusion](./images/wffusion4.png)

將&#x200B;**時鐘**&#x200B;圖示移至新新增的&#x200B;**設定多個變數**。

![WF Fusion](./images/wffusion5.png)

您的屏幕應該看起來按讚這樣。

![WF 融合](./images/wffusion6.png)

右鍵按下問號並選擇 **刪除模組**。

![WF Fusion](./images/wffusion7.png)

接著，用滑鼠右鍵按一下&#x200B;**設定多個變數**&#x200B;並選取&#x200B;**設定**。

![WF 融合](./images/wffusion8.png)

## 1.2.1.2 配置Adobe Systems I/O 身份驗證

現在，您需要配置針對Adobe Systems I/O 進行身份驗證所需的變數。在上一練習中，您創建了一個 Adobe Systems I/O 專案。 現在需要在 Workfront Fusion 中定義該 Adobe Systems I/O 專案的變數。

您必須定義下列變數：

| 索引鍵 | 值 |
|:-------------:| :---------------:| 
| `CONST_client_id` | 您的Adobe I/O專案使用者端ID |
| `CONST_client_secret` | 您的Adobe I/O專案使用者端密碼 |
| `CONST_scope` | 您的Adobe I/O專案範圍 |

前往[https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)並開啟名為`--aepUserLdap-- One Adobe tutorial`的Adobe I/O專案，以尋找這些變數。

![WF Fusion](./images/wffusion9.png)

在您的專案中，選取&#x200B;**OAuth Serverto-Server**&#x200B;以檢視上述金鑰的值。

![WF Fusion](./images/wffusion10.png)

使用上述索引鍵和值，您可以設定&#x200B;**設定多個變數**&#x200B;物件。 選取&#x200B;**新增專案**。

![WF Fusion](./images/wffusion11.png)

輸入&#x200B;**變數名稱**： **CONST_client_id**&#x200B;及其&#x200B;**變數值**，請選取&#x200B;**新增**。

![WF 融合](./images/wffusion12.png)

選取&#x200B;**新增專案**。

![WF Fusion](./images/wffusion13.png)

輸入&#x200B;**變數名稱**： **CONST_client_secret**&#x200B;及其&#x200B;**變數值**，請選取&#x200B;**新增**。

![WF Fusion](./images/wffusion14.png)

選擇添加 **項**。

![WF Fusion](./images/wffusion15.png)

輸入&#x200B;**變數名稱**： **CONST_scope**&#x200B;及其&#x200B;**變數值**，請選取&#x200B;**新增**。

![WF Fusion](./images/wffusion16.png)

選取&#x200B;**確定**。

![WF Fusion](./images/wffusion17.png)

將游標暫留在&#x200B;**設定多個變數**&#x200B;上，並選取大&#x200B;**+**&#x200B;圖示以新增另一個模組。

![WF Fusion](./images/wffusion18.png)

您的熒幕應如下所示。

![WF Fusion](./images/wffusion19.png)

在搜尋列中輸入&#x200B;**http**。 選取&#x200B;**HTTP**&#x200B;以開啟。

![WF 融合](./images/wffusion21.png)

選擇「 **製作請求**」。

![WF 融合](./images/wffusion20.png)

| 索引鍵 | 值 |
|:-------------:| :---------------:| 
| `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
| `Method` | `POST` |
| `Body Type` | `x-www-form-urlencoded` |

選擇添加 **項**。

![WF 融合](./images/wffusion22.png)

為以下每個值新增專案：

| 索引鍵 | 值 |
|:-------------:| :---------------:| 
| `client_id` | 您預先定義的 變數 `CONST_client_id` |
| `client_secret` | 您預先定義的`CONST_client_secret`變數 |
| `scope` | 您預先定義的`CONST_scope`變數 |
| `grant_type` | `client_credentials` |

`client_id`的設定：

![WF Fusion](./images/wffusion23.png)

`client_secret`的設定。

![WF Fusion](./images/wffusion25.png)

`scope`的設定。

![WF Fusion](./images/wffusion26.png)

`grant_type`的設定。

![WF Fusion](./images/wffusion28.png)

向下捲動並勾選&#x200B;**剖析回應**&#x200B;的方塊。 選擇確定&#x200B;****。

![WF 融合](./images/wffusion27.png)

您的屏幕應該看起來按讚這樣。 選取&#x200B;**執行一次**。

![WF Fusion](./images/wffusion29.png)

案例執行後，您的畫面應如下所示：

![WF 融合](./images/wffusion30.png)

**選擇「設置多個變數**」**物件上的問號**&#x200B;圖示，查看該物件運行時發生的情況。

![WF 融合](./images/wffusion31.png)

**選擇 HTTP**- 建立請求&#x200B;**物件上的問號**&#x200B;圖示以查看該物件運行時發生的情況。在 **輸出**&#x200B;中，查看 **I/O 返回Adobe Systems access_token** 。

![WF 融合](./images/wffusion32.png)

將游標暫留在&#x200B;**HTTP上 — 提出要求**&#x200B;並選取&#x200B;**+**&#x200B;圖示以新增另一個模組。

![WF Fusion](./images/wffusion33.png)

在搜尋列中搜尋`tools`。 選取&#x200B;**工具**。

![WF Fusion](./images/wffusion34.png)

選擇設置 **多個變數**。

![WF Fusion](./images/wffusion35.png)

選擇添加 **項**。

![WF 融合](./images/wffusion36.png)

將&#x200B;**變數名稱**&#x200B;設為`bearer_token`。 選取`access_token`作為動態&#x200B;**變數值**。 選取&#x200B;**新增**。

![WF Fusion](./images/wffusion37.png)

您的屏幕應該看起來按讚這樣。 選擇確定&#x200B;****。

![WF 融合](./images/wffusion38.png)

再次選擇「 **運行** 」。

![WF 融合](./images/wffusion39.png)

方案運行后，選擇&#x200B;**最後一個**「設置多個變數&#x200B;**」物件上的問號**&#x200B;圖示。您應該會看到access_token儲存在變數`bearer_token`中。

![WF Fusion](./images/wffusion40.png)

接著，用滑鼠右鍵按一下第一個物件&#x200B;**設定多個值**&#x200B;並選取&#x200B;**重新命名**。

![WF Fusion](./images/wffusion41.png)

將名稱設定為&#x200B;**初始化常數**。 選取&#x200B;**確定**。

![WF Fusion](./images/wffusion42.png)

將第二個物件重新命名為&#x200B;**驗證Adobe I/O**。 選取&#x200B;**確定**。

![WF Fusion](./images/wffusion43.png)

將第三個物件重新命名為&#x200B;**設定持有人權杖**。 選取&#x200B;**確定**。

![WF Fusion](./images/wffusion44.png)

您的螢幕應按讚如下所示：

![WF 融合](./images/wffusion45.png)

下一個，將方案 `--aepUSerLdap-- - Adobe I/O Authentication`的名稱更改為 。

![WF 融合](./images/wffusion46.png)

選取「**儲存**」。

![WF 融合](./images/wffusion47.png)

## 後續步驟

前往在 [Workfront Fusion 中使用 Adobe Systems API](./ex2.md){target="_blank"}

[返回 Creative 工作流程自動化與 Workfront 融合](./automation.md){target="_blank"}

返回 [「所有模組」](./../../../overview.md){target="_blank"}
