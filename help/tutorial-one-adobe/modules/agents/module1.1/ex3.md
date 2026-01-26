---
title: Adobe Marketing Agent for Microsoft 365 Copilot
description: Microsoft 365 CopilotCopilot適用的Adobe Marketing Agent
kt: 5342
doc-type: tutorial
source-git-commit: 44d0e98ae4c7568411cb0e01ed8eff38b4a34137
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# 1.1.3 Adobe Marketing Agent for Microsoft 365 Copilot

>[!IMPORTANT]
>
>本實驗使用的功能尚未發行。 功能仍在開發中，尚未正式推出。

[!BADGE Beta]

+++Beta詳細資料
藉由將Adobe Marketing Agent與Microsoft 365 Copilot Beta搭配使用，您在此確認Beta係依「現況」提供，並無任何保證。 Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援Beta。 建議您謹慎使用，切勿依賴這類Beta及/或隨附資料的正確運作或效能。 Beta視為Adobe的機密資訊。  任何「意見回饋」(有關Beta的資訊，包括但不限於您在使用Beta時遇到的問題或缺陷、建議、改進和建議)會在此指派給Adobe Adobe，包括所有權利、標題，以及對此等意見回饋的興趣。

+++

## 先決條件

為了遵循本實驗中記錄的步驟，需要以下存取：

- 存取Real-Time CDP、Journey Optimizer和Customer Journey Analytics
- 存取Adobe Experience Cloud中的AI助理
- 存取AEP Agent Orchestrator
- 存取Microsoft 365 Copilot

## 影片

在這段影片中，您將獲得本練習中所有步驟的說明和示範。

>[!VIDEO](https://video.tv.adobe.com/v/3479158?quality=12&learn=on)

## 1.1.3.1將Adobe Marketing Agent新增至Microsoft 365 Teams &amp; Copilot

開啟Microsoft Teams並使用您的帳戶詳細資料登入。 登入後，您應該會看到此訊息。

按一下&#x200B;**應用程式**。

![ChatGPT](./images/copilot1.png)

選取&#x200B;**管理您的應用程式**。

![ChatGPT](./images/copilot2.png)

選取&#x200B;**上傳應用程式**。

![ChatGPT](./images/copilot3.png)

選取&#x200B;**上傳自訂應用程式**。

![ChatGPT](./images/copilot4.png)

選取講師提供給您的資訊清單檔案，然後按一下[開啟]。**&#x200B;**

![ChatGPT](./images/copilot5.png)

按一下&#x200B;**新增**。

![ChatGPT](./images/copilot6.png)

按一下&#x200B;**使用Copilot**&#x200B;開啟。

![ChatGPT](./images/copilot7.png)

Adobe Marketing Agent現在已成功載入。

![ChatGPT](./images/copilot8.png)

輸入提示`login`並按一下&#x200B;**傳送**&#x200B;按鈕。

![ChatGPT](./images/copilotlogin1.png)

按一下&#x200B;**登入Adobe Marketing Agent**。

![ChatGPT](./images/copilotlogin2.png)

系統隨即開啟新視窗，要求您使用Adobe帳戶憑證登入。

![ChatGPT](./images/copilotlogin3.png)

成功驗證後，您可能需要選取要使用的特定執行個體。 如果您看到此畫面，請選取執行個體 — aepImsOrgName—。

![ChatGPT](./images/copilotlogin4.png)

然後您會看到產生類似的程式碼。 按一下&#x200B;**複製**&#x200B;以複製代碼。

![ChatGPT](./images/copilotlogin5.png)

在Copilot的Adobe Marketing Agent視窗中貼上程式碼，然後按一下&#x200B;**傳送**&#x200B;按鈕。

![ChatGPT](./images/copilotlogin6.png)

之後，您應該會看到類似以下內容。 您現在已成功登入Microsoft 365 Copilot的Adobe Marketing Agent。

![ChatGPT](./images/copilotlogin7.png)

## 1.1.3.2在Adobe Marketing Agent中設定內容

在透過Copilot進一步與Adobe Marketing Agent互動之前，需要設定上下文。

在本練習中，需要將內容設定為使用：

- **沙箱**： **Prod — 加速(VA7)**

  沙箱設定可協助識別在詢問問題時哪個沙箱AI Assistant應該檢視。

- **資料檢視**： **加速2026 B2C**

  資料檢視設定可協助識別詢問問題時資料檢視AI助理應該檢視哪個資料檢視。

![Agent Orchestrator](./images/copilotlogin7.png)

若要變更沙箱，請輸入以下命令並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
change sandbox
```

![Agent Orchestrator](./images/copilot9.png)

之後，您應該會看到類似以下內容。 選取您需要使用的沙箱，然後按一下&#x200B;**選取**。

![Agent Orchestrator](./images/copilot10.png)

您應該會看到此訊息。 若要變更資料檢視，請輸入以下命令並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
change dataview
```

![Agent Orchestrator](./images/copilot11.png)

之後，您應該會看到類似以下內容。 選取您需要使用的資料檢視，然後按一下&#x200B;**選取**。

![Agent Orchestrator](./images/copilot12.png)

您應該會看到此訊息。 內容現在已正確設定，以便您接下來可以開始傳送特定提示。

![Agent Orchestrator](./images/copilot13.png)

## 1.1.3.3從整體購買趨勢開始，錨定內容並放大光纖

**意圖**

獲得全方位的類別需求脈衝：行動、有線電話、網際網路、電視、光纖，特別是最近60天的應用。 這會設定紐約推出後的季節性、促銷效果及區域差異的基線。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Show me purchases by mainCategory over the last 4 months.
```

![Agent Orchestrator](./images/copilot18.png)

您應該會看到以下內容：

![Agent Orchestrator](./images/copilot19.png)

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Show me purchases by mainCategory = Fiber over the last 4 months broken down by week
```

![Agent Orchestrator](./images/copilot20.png)

您應該會看到此資訊，深入瞭解光纖特有的趨勢。

![Agent Orchestrator](./images/copilot21.png)

## 1.1.3.4將訂單與內容偏好設定建立關聯

**意圖**

測試特定型別（例如SciFi、Sports、Drama）的偏好預測寬頻升級行為的假設 — 尤其是針對高頻寬需求。

首先，您需要找出哪個欄位用於儲存型別偏好設定。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Which field is used to store the preferred genre
```

![Agent Orchestrator](./images/copilot22.png)

您應該會看到此訊息，其中顯示用於型別的欄位是&#x200B;**_experienceplatform.individualCharacteristics.preferences.preferredGenre**。

![Agent Orchestrator](./images/copilot23.png)

有了這些資訊，您就可以開始向下鑽研購買資料。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Show me ordersYTD by preferredGenre for the last 4 months
```

![Agent Orchestrator](./images/copilot24.png)

您應該會看到此訊息。 按一下&#x200B;**檢視資料**。

![Agent Orchestrator](./images/copilot25.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/copilot26.png)

## 1.1.3.5識別現有的Fiber歷程

**意圖**

探索標題中包含「Fiber」的活動或最近結束的歷程，例如「Fiber Upgrade NYC - September」、「Fiber Trial - Streaming Bundle」。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/copilot28.png)

之後，您應該會看到歷程清單。

![Agent Orchestrator](./images/copilot29.png)

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/copilot31.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/copilot33.png)

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/copilot35.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/copilot36.png)

## 1.1.3.6透過流失分析驗證歷程績效

**意圖**

您想要瞭解歷程效能流失，以瞭解歷程中是否有任何節點或條件發生大量設定檔被捨棄的情況。 這有助於瞭解歷程中是否需要其他調整。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/copilot37.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/copilot38.png)

再向下捲動一點以檢視觀察結果和建議。 按一下3個點&#x200B;**...**，然後選取&#x200B;**歷程詳細資料**&#x200B;以開啟Adobe Journey Optimizer中的特定歷程。

![Agent Orchestrator](./images/copilot40.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/copilot41.png)

您現在已經完成了這個實驗。

返回[Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}