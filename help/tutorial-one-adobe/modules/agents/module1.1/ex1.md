---
title: Agent Orchestrator快速入門
description: Agent Orchestrator快速入門
kt: 5342
doc-type: tutorial
source-git-commit: e90dee164dfe098c9fc56a04c481a733c0843858
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# 1.1.1 Agent Orchestrator快速入門

## 1.1.1在Agent Orchestrator中設定內容

導覽至AI助理並開啟大型檢視。

確認您是在CJA內容中執行分析任務。

>[!NOTE]
>
>在分析之間移動(CJA)和協調流程(JO)時，請使用內容切換。

## 1.1.2從整體購買趨勢開始，錨定內容並放大光纖

**提示**：

```javascript
Show me purchases by mainCategory over the last 2 month
```

**意圖**：取得最新的60天內toplevel pulse on category demand — 行動、有線電話、網際網路、電視、光纖。 這會設定NY轉出後的季節性、促銷效果以及區域差異的基線。

思考：

「Fiber是否能在紐約獲得市場份額？ 我們是否看到銅線/DSL網際網路的自我吞噬效應？ 與電視套裝相比，這種轉換又是什麼呢？」

「這有助於我評估維也納的可定址對象規模，並設定現實的目標。」

行銷人員期望的可操作性閱讀：

依mainCategory區分的棧疊購買長條圖/折線圖（每日/每週粒度）。

依類別與先前時段區分的購買百分比份額。

與促銷日期相關的明顯尖峰。

>[!NOTE]
>
>留意延遲歸因 — 在一些舊式結構描述中，光纖訂單可能會記錄在「網際網路」下。 若是如此，請在決定之前協調分類。

 

**提示**：

```javascript
Show me purchases by mainCategory over the last 2 monthzoom into fiber performance
```

**下一個提示**

`Show me purchases by mainCategory = Fiber over the last 2 months`

深入探討Fiber特定趨勢。

**動作**&#x200B;記事成長曲線和區域尖峰。

## 1.1.3將訂單與內容偏好設定建立關聯

**提示**：

```javascript
Show me ordersYTD by preferred genre for the last 2 months
```

**意圖**&#x200B;測試內容喜好設定（例如SciFi、Sports、Drama）預測寬頻升級行為的假設，尤其是針對高頻寬需求。

**正在思考**

「SciFi愛好者經常觀看4K節目並從多部裝置進行串流，因此可能重視低延遲性。」

「讓我們量化SciFi （或許還有Sports）是否與近期訂單相關。」

**預期輸出**

依偏好型別劃分的訂單樞紐（套用YTD篩選器），限制在過去2個月。

依訂單轉換率和AOV （平均訂單值）來排名型別。

決定：如果SciFi顯示強烈訊號，這會成為維也納Fiber Max發佈的主要創意支柱（例如「永不緩衝」訊息、優質套裝）。

**提示**

`Show me ordersYTD by preferred genre for the last 2 months`

**意圖**

依型別（例如科幻片、運動）分析轉換。

**目標**&#x200B;驗證Sci-Fi風扇是否過度索引以進行Fiber升級。

## 1.1.4識別現有的光纖歷程

**提示**：

```javascript
What journey was running and had Fiber in the name
```

**意圖**&#x200B;探索哪些作用中或最近結束的歷程包含「Fiber」標題，例如「Fiber Upgrade NYC - September」、「Fiber Trial - Streaming Bundle」。

**正在思考**

「這些歷程中，哪些執行良好，其觸發因素為何？」

「我可以在維也納重複使用成功協調邏輯嗎？」

**預期輸出**

具有狀態（作用中、已暫停、已結束）、日期範圍、目標區段、KPI （開放率、CTR、轉換）的歷程清單。

下一步：將一或兩個成功的光纖歷程加入候選清單，以便複製/改寫。

**提示**

`What journey was running and had Fiber in the name?`

使用Fiber訊息列出作用中或過去的歷程。

動作：將復製作業的高成效歷程加入短清單。

## 1.1.5檢查種子對象，瞭解相關的歷史促銷活動

**提示**：

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey
```

**意圖**&#x200B;瞭解「SciFi Promo 2024 - jl」歷程的種子定義 — 哪些特徵會驅動鎖定目標(例如「SciFi型別偏好」、「4+裝置」、「串流≥ 300GB/月」)。

**正在思考**

「我想結合備受肯定的科幻創意，以及Fiber Max的效能傳訊。」

「如果對象與大量下載者重疊，我們可以棧疊傾向。」

**預期輸出**

對象條件（包含/排除）、對象人數、區域篩選器、造訪間隔、頻率臨界值。

>[!NOTE]
>
>變更內容至CJA

從這時起，行銷人員會切換為分析模式，以確保正確的報告。

**提示**：

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey?
```

檢閱對象條件（串流習慣、裝置計數）。

目標：瞭解高頻寬需求的特性。

## 1.1.6透過流失分析驗證歷程績效

**提示**：

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey
```

>[!NOTE]
>
>變更內容至CJA)

**意圖**&#x200B;在Customer Journey Analytics中建置逐步式funnel

已傳遞→開啟→按一下→抵達→產品檢視→新增到購物車→結帳→完成訂單

包括光纖相關的SKU檢視作為分支。

思考：

「哪裡有人員流失 — 電子郵件開啟、登陸頁面載入、PDP、結帳摩擦？」

「SciFi使用者跳出率是否高於或低於Fiber PDP的平均值？」

預期輸出：

每個步驟都有流失率的流失視覺效果。

區段覆蓋（SciFi與運動相較於其他）。

技術摩擦導致裝置/瀏覽器故障。

決定：

如果結帳流失率很高，請與product/UX協調以修正付款流程。

如果PDP退出次數很高，則重工要求清晰度（速度、安裝時間、套件價值）。

>[!NOTE]
>
>將內容變更為JO

現在，行銷人員進入Adobe Journey Optimizer進行協調和受眾操作。

**提示**：

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey 
```

建立funnel視覺效果：傳遞→開啟→按→下→次結帳。

動作：識別流失點並最佳化傳訊或UX。


## 1.1.7尋找符合高使用率的現有對象

**提示**：

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

>[!NOTE]
>
>變更內容至Adobe Journey Optimizer

目的：找出任何具有「大量下載者」名稱的JO對象 — 可能由每月資料使用閾值、串流時數或裝置並行定義。

思考：

「如果存在像大量下載者的受眾，就非常適合使用光纖最大功能：速度、可靠性、無限層級。」

預期輸出：

對象中繼資料：定義條件、大小、上次重新整理、治理標籤、區域可用性。

**提示**：

```javascript
Is there an audience that has " heavy downloaders" in the title 
```

找出資料使用量高的對象。

目標：結合Fiber Max定位的科幻偏好設定。

## 1.1.8判斷這些對象是否已在使用中

**提示**：

```javascript
Which of the above are used in a journey? 
```

目的：檢查對象與歷程連結，確保我們不會對目前的程式重複訊息或發生衝突。

思考：

「如果大量下載者已處於保留歷程，我們需要隱藏邏輯或頻率上限以避免疲勞。」

預期輸出：

對應：對象→歷程名稱、狀態、聯絡人原則、上次傳送、績效。

決定：

如果正在使用中，請為Vienna啟動建立排除專案或共用隱藏專案。

如果未使用，則加入新歷程的綠光。

提示：

歷程中使用了上述哪一項？

確保與作用中的行銷活動沒有重疊。

動作：視需要套用隱藏。

## 1.1.9建立Fiber Max啟動的新歷程

**提示**：

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

目的：建置以複合對象為目標的新JO歷程：

大量下載者∩SciFi偏好設定（kbaa_5207bf對象金鑰）。

思考：

「這是Fiber Max的最佳選擇：高傾向性+創意關聯性。」

「我們將打造與維也納可用性相連結的多點觸控體驗。」

歷程設計(JO)：

進入條件：

對象：大量下載者 — 科幻偏好設定_kbaa_5207bf

Geography： Vienna metro （郵遞區號清單或地理多邊形）

資格：不在使用中的「Fiber Upgrade NYC - Sept」行銷活動中；不是目前的Fiber訂閱者。

觸發器和時機：

T14天後（2026年1月）：預覽電子郵件 — 「Fiber Max即將推出」。

啟動周：主要電子郵件+應用程式內橫幅+付費媒體同步（透過CDP目的地）。

T+3天：行為分割 — 如果沒有按一下，SMS會輕推；如果按一下但未訂購，則會使用安裝程式可用性CTA重新進行目標定位。

T+10天：優惠測試 — 免費安裝與第1個月折扣(A/B)。

Personalization：

SciFi愛好者的動態複製（延遲/4K串流勾點）。

針對裝置組合（遊戲主機、串流盒）量身打造的速度/延遲宣告。

套件推薦：Fiber Max +優質電視節目內容套件。

治理：

頻率上限：每10天最多3次接觸。

如果目前的Fiber訂閱者或存在安裝票證，則隱藏。

遵守選擇退出偏好設定。

測量計畫(CJA)：

追蹤：傳送、開啟、按一下、PDP檢視、結帳開始、訂單完成。

KPI：Fiber Max的轉換率、提升與控制、安裝時間。

診斷：依裝置/型別區段的流失報表。

形狀

這一切如何結合（行銷人員的思維模式）

診斷需求(特別是Fiber→整體類別)。

證明內容至轉換訊號（依型別的訂單）。

我的成功歷程（尋找纖維名稱歷程和SciFi促銷對象）。

驗證摩擦點(SciFi歷程中的CJA流失)。

針對高傾向區段(大量下載者∩SciFi)啟用。


返回[Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}