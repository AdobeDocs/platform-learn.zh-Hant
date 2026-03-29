---
title: 克勞德的Adobe Marketing Agent
description: 克勞德的Adobe Marketing Agent
kt: 5342
doc-type: tutorial
source-git-commit: e476d5b516dcbe0f094eb2dfc38f4985798ecc3b
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 1%

---

# 1.1.5克勞德的Adobe Marketing Agent

[!BADGE Beta]

+++Beta詳細資料
藉由將Adobe Marketing Agent與Claude Beta搭配使用，您在此確認Beta係依「現況」提供，並無任何保證。 Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援Beta。 建議您謹慎使用，切勿依賴這類Beta及/或隨附資料的正確運作或效能。 Beta視為Adobe的機密資訊。  任何「意見回饋」（有關Beta的資訊，包括但不限於您在使用Beta時遇到的問題或缺陷、建議、改進和建議）會在此指派給Adobe，包括所有權利、標題，以及對此等意見回饋的興趣。

+++

## 先決條件

為了遵循本實驗中記錄的步驟，需要以下存取：

- 存取Real-Time CDP、Journey Optimizer和Customer Journey Analytics
- 存取Adobe Experience Cloud中的AI助理
- 存取AEP Agent Orchestrator
- 存取Claude

## 影片

在這段影片中，您將獲得本練習中所有步驟的說明和示範。

>[!VIDEO](https://video.tv.adobe.com/v/3482212?quality=12&learn=on)

本實驗室正在開發中。

## 1.1.5.1在Claude.ai中為CJA建立自訂應用程式

>[!NOTE]
>
>在Claude.ai中使用Adobe Marketing Agent需要下列專案：
>- 付費版本的Claude.ai

移至[https://claude.ai/](https://claude.ai/){target="_blank"}並使用您的帳戶詳細資料登入。 登入後，您應該會看到此訊息。

![Claude.ai](./images/claude1.png)

按一下以開啟您的帳戶，然後選取&#x200B;**設定**。

![Claude.ai](./images/claude2.png)

移至&#x200B;**聯結器**，然後按一下&#x200B;**移至[自訂]**。

![Claude.ai](./images/claude2a.png)

按一下&#x200B;**+**，然後選取&#x200B;**新增自訂聯結器**。

![Claude.ai](./images/claude3.png)

填寫欄位，如下所示：

- **名稱**： `Adobe Marketing Agent`
- **MCP伺服器URL**：請洽詢您的Adobe代表

按一下&#x200B;**新增**。

![Claude.ai](./images/claude4.png)

您應該會看到此訊息。 按一下&#x200B;**+**&#x200B;開始新的聊天。

![Claude.ai](./images/claude5.png)

按一下&#x200B;**+**&#x200B;圖示，前往&#x200B;**聯結器**，並確認已啟用&#x200B;**Adobe Marketing Agent****。

![Claude.ai](./images/claude6.png)

## 1.1.5.2驗證及設定內容

在透過Claude.ai進一步與Adobe Marketing Agent互動之前，您需要登入並設定上下文。

輸入以下提示並按一下&#x200B;**傳送**。

```
login to Adobe Marketing Agent
```

![Claude.ai](./images/claude7.png)

選取&#x200B;**永遠允許**。

![Claude.ai](./images/claude8.png)

按一下連結，登入Adobe Marketing Agent**。

![Claude.ai](./images/claude8a.png)

按一下&#x200B;**開啟連結**。

![Claude.ai](./images/claude8b.png)

按一下&#x200B;**允許存取**。

![Claude.ai](./images/claude8c.png)

在成功驗證後，您應該會看到這個訊息。 回到克勞德。

![Claude.ai](./images/claude8d.png)

輸入下列命令，然後按一下&#x200B;**傳送**。

```javascript
logged in
```

![Claude.ai](./images/claude8e.png)

您現在已成功登入。 下一步是設定內容。 輸入以下提示並按一下&#x200B;**傳送**。


```javascript
change context
```

![Claude.ai與CJA](./images/claude9.png)

選取&#x200B;**組織**。 您也可以稍後重複此命令，以變更沙箱和資料檢視。

![Claude.ai與CJA](./images/claude10.png)

輸入執行個體的名稱，然後按一下&#x200B;**傳送**。

![Claude.ai與CJA](./images/claude11.png)

選取&#x200B;**永遠允許**。

![Claude.ai與CJA](./images/claude12.png)

您應該會看到類似這樣的內容。

![Claude.ai與CJA](./images/claude13.png)

如果沙箱尚未正確設定，您可以使用以下命令來變更為您需要使用的沙箱。 按一下&#x200B;**傳送**。 或者，您可以使用上述命令`change context`，然後選取&#x200B;**沙箱**

```javascript
change sandbox to --aepSandboxName--
```

![Claude.ai與CJA](./images/claude14.png)

如果資料檢視尚未正確設定，您可以使用以下命令來變更為您需要使用的沙箱（以下命令中的XXX以資料檢視的名稱取代）。 按一下&#x200B;**傳送**。 或者，您可以使用上述命令`change context`，然後選取&#x200B;**資料檢視**

```javascript
change dataview to XXX
```

![Claude.ai與CJA](./images/claude15.png)

當&#x200B;**組織**、**沙箱**&#x200B;和&#x200B;**資料檢視**&#x200B;設定正確後，您就可以開始向Adobe Marketing Agent提出問題了。

## 後續步驟

返回[Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}
