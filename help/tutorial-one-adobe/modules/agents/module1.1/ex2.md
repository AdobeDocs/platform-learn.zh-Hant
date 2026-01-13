---
title: Adobe Marketing Agent與ChatGPT
description: Adobe Marketing Agent與ChatGPT
kt: 5342
doc-type: tutorial
source-git-commit: 9663ef2838024e293acc72c203b1e3578911d57f
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# 1.1.2含ChatGPT的Adobe Marketing Agent

>[!IMPORTANT]
>
>本實驗使用的功能尚未發行。 功能仍在開發中，尚未正式推出。

## 影片

在這段影片中，您將獲得本練習中所有步驟的說明和示範。

>[!VIDEO](https://video.tv.adobe.com/v/3478410?quality=12&learn=on)

## 1.1.2.1在ChatGPT中為Adobe Marketing Agent建立自訂應用程式

>[!NOTE]
>
>在ChatGPT中使用Adobe Marketing Agent需要下列專案：
>- OpenAI的ChatGPT付費版本
>- 使用ChatGPT網頁使用者端

前往https://chatgpt.com/並使用您的帳戶詳細資料登入。 登入後，您應該會看到此訊息。 按一下您的使用者名稱。

![ChatGPT](./images/chatgpt1.png)

選取&#x200B;**設定**。

![ChatGPT](./images/chatgpt2.png)

移至&#x200B;**應用程式**，然後選取&#x200B;**進階設定**。

![ChatGPT](./images/chatgpt3.png)

開啟&#x200B;**開發人員模式**，然後按一下&#x200B;**上一步**。

![ChatGPT](./images/chatgpt4.png)

按一下&#x200B;**建立應用程式**。

![ChatGPT](./images/chatgpt5.png)

填寫欄位，如下所示：

- **名稱**： `Adobe Marketing Agent`
- **MCP伺服器URL**：請洽詢您的Adobe代表
- **驗證**： `OAuth`

勾選&#x200B;**我瞭解並想要繼續**&#x200B;的核取方塊。

按一下&#x200B;**建立**。

![ChatGPT](./images/chatgpt6.png)

ChatGPT現在將嘗試連線至您的Adobe帳戶。 選取&#x200B;**允許存取**，然後您必須使用您的Adobe帳戶登入。

![ChatGPT](./images/chatgpt7.png)

成功登入後，您應該會看到Adobe Marketing Agent現在已成功連線。

![ChatGPT](./images/chatgpt8.png)

## 1.1.2.2在Adobe Marketing Agent中設定內容

關閉此視窗。

![Agent Orchestrator](./images/chatgpt9.png)

您應該會看到此訊息。 按一下&#x200B;**+**&#x200B;圖示，移至&#x200B;**更多**，然後選取&#x200B;**Adobe Marketing Agent**。

![Agent Orchestrator](./images/chatgpt10.png)

在透過ChatGPT進一步與Adobe Marketing Agent互動之前，需要設定內容。

在本練習中，需要將內容設定為使用：

- **沙箱**： **Prod — 加速(VA7)**

沙箱設定可協助識別在詢問問題時哪個沙箱AI小幫手應該檢視。

- **資料檢視**： **加速2026 B2C**

資料檢視設定可協助識別詢問問題時資料檢視AI助理應該檢視哪個資料檢視。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
list sandboxes
```

![Agent Orchestrator](./images/chatgpt11.png)

之後，您應該會看到類似的可用沙箱清單。 此範例中的目前沙箱設定為&#x200B;**prod**。

若要將其變更為需要使用的沙箱，請輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
switch to sandbox accelerate
```

![Agent Orchestrator](./images/chatgpt12.png)

您應該會看到此訊息。 按一下&#x200B;**設定內容**。

![Agent Orchestrator](./images/chatgpt13.png)

您應該會看到此訊息。 輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕，設定要使用的資料檢視。

```javascript
list dataviews
```

![Agent Orchestrator](./images/chatgpt14.png)

之後，您應該會看到類似的可用沙箱清單。 此範例中的目前沙箱設定為&#x200B;**prod**。

若要將其變更為需要使用的沙箱，請輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
switch to Accelerate 2026 B2C
```

![Agent Orchestrator](./images/chatgpt15.png)

您應該會看到此訊息。 按一下&#x200B;**設定內容**。

![Agent Orchestrator](./images/chatgpt16.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/chatgpt17.png)

您的內容現在已正確設定，因此您之後可以開始傳送特定提示。

## 1.1.2.3從整體購買趨勢開始，錨定內容並放大光纖

**意圖**

獲得全方位的類別需求脈衝：行動、有線電話、網際網路、電視、光纖，特別是最近60天的應用。 這會設定紐約推出後的季節性、促銷效果及區域差異的基線。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/chatgpt18.png)

您應該會看到以下內容：

![Agent Orchestrator](./images/chatgpt19.png)

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/chatgpt20.png)

您應該會看到此資訊，深入瞭解光纖特有的趨勢。

![Agent Orchestrator](./images/chatgpt21.png)

## 1.1.2.4將訂單與內容偏好設定建立關聯

**意圖**

測試特定型別（例如SciFi、Sports、Drama）的偏好預測寬頻升級行為的假設 — 尤其是針對高頻寬需求。

首先，您需要找出哪個欄位用於儲存型別偏好設定。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Which field is used to store the preferred genre in the sandbox accelerate?
```

![Agent Orchestrator](./images/chatgpt22.png)

您應該會看到此訊息，其中顯示用於型別的欄位是&#x200B;**_experienceplatform.individualCharacteristics.preferences.preferredGenre**。

![Agent Orchestrator](./images/chatgpt23.png)

有了這些資訊，您就可以開始向下鑽研購買資料。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/chatgpt24.png)

您應該會看到此訊息。 按一下&#x200B;**研究**。

![Agent Orchestrator](./images/chatgpt25.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/chatgpt26.png)

向下捲動以檢視詳細資訊。

![Agent Orchestrator](./images/chatgpt27.png)

## 1.1.2.5識別現有的Fiber歷程

**意圖**

探索標題中包含「Fiber」的活動或最近結束的歷程，例如「Fiber Upgrade NYC - September」、「Fiber Trial - Streaming Bundle」。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/chatgpt28.png)

您應該會看到此訊息。 按一下&#x200B;**研究**。

![Agent Orchestrator](./images/chatgpt29.png)

之後，您應該會看到歷程清單。

![Agent Orchestrator](./images/chatgpt30.png)

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/chatgpt31.png)

您應該會看到此訊息。 按一下&#x200B;**研究**。

![Agent Orchestrator](./images/chatgpt32.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/chatgpt33.png)

向下捲動以檢視更多詳細資料。

![Agent Orchestrator](./images/chatgpt34.png)

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/chatgpt35.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/chatgpt36.png)

## 1.1.2.6透過流失分析驗證歷程績效

**意圖**

您想要瞭解歷程效能流失，以瞭解歷程中是否有任何節點或條件發生大量設定檔被捨棄的情況。 這有助於瞭解歷程中是否需要其他調整。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/chatgpt37.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/chatgpt38.png)

向下捲動一點。 您現在可以透過檢查每個節點及其各自的輸入編號、流失編號和流失率來檢閱表格。

![Agent Orchestrator](./images/chatgpt39.png)

再向下捲動一點以檢視觀察結果和建議。

![Agent Orchestrator](./images/chatgpt40.png)

您現在已經完成了這個實驗。

返回[Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}