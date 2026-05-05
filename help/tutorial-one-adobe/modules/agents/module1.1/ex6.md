---
title: AI配線
description: AI配線
kt: 5342
doc-type: tutorial
exl-id: ce845231-17d1-40ab-96f7-bd386753e625
source-git-commit: 11ce179c0a94113dba391790ee6a86d70a7e9241
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 0%

---

# 1.1.6 AI環境

## 先決條件

為了遵循本實驗中記錄的步驟，需要以下存取：

- 存取Real-Time CDP、Journey Optimizer和Customer Journey Analytics
- 存取Adobe Experience Cloud中的AI助理
- 存取AEP Agent Orchestrator
- 您的系統上必須安裝Node.js 18+

## 1.1.6.1存取Agent Orchestrator

移至[https://ao.adobe.io/](https://ao.adobe.io/)。 使用您的Adobe帳戶登入。 登入後，請依下方指示變更選取執行個體和沙箱，以確定已選取正確的執行個體和沙箱。

![AO](./images/aov2lab1.png)

## 1.1.6.2設定您的內容

輸入下列命令，然後按一下&#x200B;**傳送**。

```
list dataviews
```

![AO](./images/aov2lab18.png)

您可能會收到此請求。 提供必要許可權。

![AO](./images/aov2lab19.png)

您可能會收到此請求。 提供必要許可權。

![AO](./images/aov2lab19a.png)

您應該會看到此訊息。 輸入下列命令，然後按一下&#x200B;**傳送**。

```
switch to dataview AdobeOne - Unified Customer Data View
```

![AO](./images/aov2lab20.png)

您應該會看到此訊息。

![AO](./images/aov2lab21.png)

## 1.1.6.3從整體購買趨勢開始，錨定內容並放大光纖

**意圖**

獲得全方位的類別需求脈衝：行動、有線電話、網際網路、電視、光纖，特別是最近60天的應用。 這會設定紐約推出後的季節性、促銷效果及區域差異的基線。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/aotechlab4.png)

您應該會看到以下內容：

![Agent Orchestrator](./images/aotechlab5.png)

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/aotechlab6.png)

您應該會看到此資訊，深入瞭解光纖特有的趨勢。

![Agent Orchestrator](./images/aotechlab7.png)

## 1.1.6.4將訂單與內容偏好設定建立關聯

**意圖**

測試特定型別（例如SciFi、Sports、Drama）的偏好預測寬頻升級行為的假設 — 尤其是針對高頻寬需求。

首先，您需要找出哪個欄位用於儲存型別偏好設定。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Which field is used to store the favourite genre?
```

![Agent Orchestrator](./images/aotechlab7a.png)

您應該會看到此訊息，其中顯示用於型別的欄位為&#x200B;**`--aepTenantId--.individualCharacteristics.telco.mediaPreferences.favouriteGenre`**。

![Agent Orchestrator](./images/aotechlab7b.png)

有了這些資訊，您就可以開始向下鑽研購買資料。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Show me purchases by favourite genre for the last 2 months
```

![Agent Orchestrator](./images/aotechlab8.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/aotechlab9.png)

## 1.1.6.5識別現有的Fiber歷程

**意圖**

探索標題中包含「Fiber」的活動或最近結束的歷程，例如「Fiber Upgrade NYC - September」、「Fiber Trial - Streaming Bundle」。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/aotechlab12.png)

您應該會看到類似這樣的內容。

![Agent Orchestrator](./images/aotechlab13.png)

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/aotechlab14.png)

您應該會看到此訊息。 按一下其中一個歷程上的連結。

![Agent Orchestrator](./images/aotechlab15.png)

將會開啟新視窗，並立即帶您前往歷程詳細資料概觀。

![Agent Orchestrator](./images/aotechlab15a.png)

## 1.1.6.6檢查使用的對象

**意圖**：

瞭解「CitiSignal - Fiber Max啟動促銷活動」歷程的種子定義 — 哪些特徵會推動目標定位（例如「SciFi型別偏好」、「4+裝置」、「串流≥300GB/月」）。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
What was the initial audience in the journey named CitiSignal - Fiber Max Launch Promotion?
```

![Agent Orchestrator](./images/aotechlab16.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/aotechlab18.png)

## 1.1.6.7透過流失分析驗證歷程績效

**意圖**

您想要瞭解歷程效能流失，以瞭解歷程中是否有任何節點或條件發生大量設定檔被捨棄的情況。 這有助於瞭解歷程中是否需要其他調整。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/aotechlab19.png)

您應該會看到此訊息。

![Agent Orchestrator](./images/aotechlab20.png)

## 1.1.6.8建立新對象

**意圖**

根據上述發現與研究，消費大量資料且偏好科幻或幻想型別的客戶之間存在相關性。 您現在可以在對象中組合這些屬性。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Create an audience that combines people with an average download usage per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/aotechlab32.png)

如果類似，已有對象可用，您應會看到類似訊息。

![Agent Orchestrator](./images/aotechlab32a.png)

檢閱計畫。 按一下&#x200B;**核准計畫**。

![Agent Orchestrator](./images/aotechlab33.png)

您的對象現已建立。

![Agent Orchestrator](./images/aotechlab38.png)

>[!NOTE]
>
>建立新受眾時，需要24小時的時間，AI Assistant才能使用受眾以供進一步使用。

## 1.1.6.9尋找符合高使用率的現有對象，並檢查它們是否在使用中

**意圖**：

找出任何具有「大量下載者」（依每月資料使用量臨界值定義）的受眾。

>[!NOTE]
>
>在上一步中，您建立了新對象，請記住，對象需要24小時才能供AI助理進一步使用。 您現在應該改用其他已存在的對象。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

您應該會看到此訊息。 您現在想要檢視您的所有對象，以及這些對象在過去幾天內的變更程度。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
List how much these audiences changed over the last few days.
```

![Agent Orchestrator](./images/ao31.png)

您應該會看到此訊息。 按一下&#x200B;**顯示更多**。

![Agent Orchestrator](./images/ao31a.png)

您應該會看到此訊息。 按一下以關閉右窗格。

![Agent Orchestrator](./images/ao31b.png)

向下捲動一點以檢閱AI Assistant採取的步驟。

![Agent Orchestrator](./images/ao31c.png)

已經有一些針對「大量下載者」的現有受眾。 讓我們看看它們是否已在使用中。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao50.png)

之後，您應該會看到類似以下內容。

![Agent Orchestrator](./images/ao51.png)

您現在應該確認該歷程是否有效。 輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Are these journeys active? 
```

![Agent Orchestrator](./images/ao52.png)

之後，您應該會看到類似以下內容。 這些歷程目前都沒有執行。

![Agent Orchestrator](./images/ao53.png)

對於即將推出的Fiber Max，您現在應該建立新的歷程。

## 1.1.6.10建立Fiber Max啟動的新歷程

**意圖**：

建立以複合對象為目標的新歷程：

大量下載者∩SciFi偏好設定。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

您應該會看到此訊息。 輸入`yes`並按一下[產生]。

![Agent Orchestrator](./images/aocj2.png)

您應該會看到此訊息。 輸入`yes`並按一下[產生]。

![Agent Orchestrator](./images/aocj3.png)

您應該會看到此訊息。 輸入`The first one`並按一下[傳送]。

![Agent Orchestrator](./images/aocj4.png)

您應該會看到此訊息。 輸入`yes`並按一下[傳送]。

![Agent Orchestrator](./images/aocj5.png)

檢閱回應。 輸入`yes`並按一下[傳送]。

![Agent Orchestrator](./images/aocj6.png)

按一下&#x200B;**檢閱**。

![Agent Orchestrator](./images/aocj7.png)

使用您的LDAP更新歷程名稱，使其成為唯一名稱。 按一下&#x200B;**儲存**。

![Agent Orchestrator](./images/aocj8.png)

您的歷程現在已建立為草稿模式。

![Agent Orchestrator](./images/aocj9.png)

## 1.1.6.11歷程衝突管理

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
How can I manage journey conflicts?
```

![Agent Orchestrator](./images/aocj80.png)

檢閱資訊。

![Agent Orchestrator](./images/aocj81.png)

向下捲動並選取&#x200B;**來源**，以找出資訊來源於Experience League。

![Agent Orchestrator](./images/aocj82.png)

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
List any conflicts for the journey +CitiSignal Fiber Max
```

然後從清單中手動選取歷程&#x200B;**CitiSignal - Fiber Max啟動促銷活動**。

![Agent Orchestrator](./images/aocj70.png)

您應該會看到此訊息。 按一下&#x200B;**傳送**。

![Agent Orchestrator](./images/aocj70a.png)

檢閱歷程衝突資訊。

![Agent Orchestrator](./images/aocj71.png)

向下捲動以尋找更多歷程衝突詳細資料。

![Agent Orchestrator](./images/aocj72.png)

## 1.1.6.12個實驗

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

您應該會看到以下內容：

![Agent Orchestrator](./images/aoea1.png)

向下捲動，然後按一下其中一個建議。 按一下&#x200B;**傳送**。

>[!NOTE]
>
>建議是動態的，因此在每次產生回應時，您應該會看到不同的建議。 您的建議可能會與此熒幕擷圖中所顯示的建議不同。

![Agent Orchestrator](./images/aoea2.png)

之後，您應該會看到與所選建議相關的詳細答案。

![Agent Orchestrator](./images/aoea4.png)

您現在已經完成了這個實驗。

## 後續步驟

返回[Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}

