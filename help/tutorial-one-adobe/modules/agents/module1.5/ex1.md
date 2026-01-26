---
title: CJA與ChatGPT搭配MCP伺服器
description: CJA與ChatGPT搭配MCP伺服器
kt: 5342
doc-type: tutorial
source-git-commit: ca2812e14a22b80b7f00066f9cc482e708b4ac6a
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# 1.5.1 CJA與ChatGPT搭配MCP伺服器

>[!IMPORTANT]
>
>本實驗使用的功能尚未發行。 功能仍在開發中，尚未正式推出。


>[!NOTE]
>
>此關於設定及使用具有ChatGPT的MCP伺服器連線至CJA的練習與此練習[1.1 Customer Journey Analytics：在Adobe Experience Platform之上使用Analysis Workspace建置儀表板](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)相關。 以下練習中使用的CJA資料檢視和連線是在該練習中設定的資料檢視和連線。 如果要複製以下結果，您應該先按照這些指示操作。

## 影片

在這段影片中，您將獲得本練習中所有步驟的說明和示範。

>[!VIDEO](https://video.tv.adobe.com/v/3479159?quality=12&learn=on)

## 1.5.1.1在ChatGPT中為CJA建立自訂應用程式

>[!NOTE]
>
>在ChatGPT中使用CJA需要下列專案：
>- OpenAI的ChatGPT付費版本
>- 使用ChatGPT網頁使用者端

移至[https://chatgpt.com/](https://chatgpt.com/){target="_blank"}並使用您的帳戶詳細資料登入。 登入後，您應該會看到此訊息。 按一下您的使用者名稱。

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

- **名稱**： `CJA`
- **MCP伺服器URL**：請洽詢您的Adobe代表
- **驗證**： `OAuth`

勾選&#x200B;**我瞭解並想要繼續**&#x200B;的核取方塊。

按一下&#x200B;**建立**。

![ChatGPT](./images/chatgpt6.png)

成功登入後，您應該會看到CJA應用程式現在已成功連線。

![ChatGPT](./images/chatgpt8.png)

## 1.5.1.2在CJA中設定內容

關閉此視窗。

![ChatGPT與CJA](./images/chatgpt9.png)

您應該會看到此訊息。 按一下&#x200B;**+**&#x200B;圖示，移至&#x200B;**更多**，然後選取&#x200B;**CJA**。

![ChatGPT與CJA](./images/chatgpt10.png)

在透過ChatGPT進一步與CJA互動之前，需要設定內容。

在本練習中，需要將內容設定為使用：

- **資料檢視**： **—aepUserLdap— 全通路資料檢視**

資料檢視設定可協助識別ChatGPT在詢問問題時應檢視的資料檢視。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
list dataviews
```

![ChatGPT與CJA](./images/chatgpt11.png)

之後，您應該會看到類似的可用資料檢視清單。

![ChatGPT與CJA](./images/chatgpt11a.png)

若要將其變更為需要使用的資料檢視，請輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![ChatGPT與CJA](./images/chatgpt12.png)

您應該會看到此訊息。

![ChatGPT與CJA](./images/chatgpt16.png)

您的內容現在已正確設定，以便您接下來可以開始傳送特定提示。

## 1.5.1.3探索資料檢視

>[!NOTE]
>
>此處使用的資料檢視已設定為練習[建立資料檢視](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md)的一部分。

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕，以探索哪些量度和維度可供您使用。

```javascript
list the available metrics and dimensions
```

![ChatGPT與CJA](./images/chatgpt101.png)

您應該會看到此回應，其中包含練習[建立資料檢視](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md)中設定的量度和維度。

![ChatGPT與CJA](./images/chatgpt102.png)

## 1.5.1.4自由格式表格 — 產品檢視

您現在可以開始探索資料。 首先輸入以下提示，然後按一下&#x200B;**傳送**&#x200B;以提交您的報表請求。

```javascript
how many product views happened on January 21?
```

![ChatGPT與CJA](./images/chatgpt103.png)

選取&#x200B;**執行報告**。

![ChatGPT與CJA](./images/chatgpt104.png)

之後，您應該會看到如下的回應。

![ChatGPT與CJA](./images/chatgpt105.png)

您現在可以新增維度來劃分回應。 輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
break down product views by product name
```

![ChatGPT與CJA](./images/chatgpt106.png)

之後，您應該會看到如下的回應。

![ChatGPT與CJA](./images/chatgpt107.png)

您現在也可以建立視覺效果。 輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
create a line visualization by hour for product views on January 21
```

![ChatGPT與CJA](./images/chatgpt108.png)

選取&#x200B;**更新插入專案**。

![ChatGPT與CJA](./images/chatgpt109.png)

選取&#x200B;**執行報告**。

![ChatGPT與CJA](./images/chatgpt110.png)

您應該會看到此訊息。

![ChatGPT與CJA](./images/chatgpt111.png)

向下捲動。

![ChatGPT與CJA](./images/chatgpt112.png)

您現在也可以下載此折線圖。 輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
export this chart to PNG
```

![ChatGPT與CJA](./images/chatgpt113.png)

您應該會看到此訊息。 按一下&#x200B;**下載PNG**。

![ChatGPT與CJA](./images/chatgpt114.png)

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
can you breakdown product views by user agent?
```

![ChatGPT與CJA](./images/chatgpt115.png)

選取&#x200B;**執行報告**。

![ChatGPT與CJA](./images/chatgpt116.png)

您應該會看到此訊息。

![ChatGPT與CJA](./images/chatgpt117.png)

## 1.5.1.5流失視覺效果

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![ChatGPT與CJA](./images/chatgpt118.png)

選取&#x200B;**更新插入專案**。

![ChatGPT與CJA](./images/chatgpt119.png)

選取&#x200B;**執行報告**。

![ChatGPT與CJA](./images/chatgpt120.png)

您應該會看到類似這樣的內容。 輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
can you show me a visualization of the above fallout analysis?
```

![ChatGPT與CJA](./images/chatgpt120a.png)

按一下&#x200B;**下載PNG**。

![ChatGPT與CJA](./images/chatgpt121.png)

您現在可以看到流失分析的視覺效果。

![ChatGPT與CJA](./images/chatgpt122.png)

輸入下列&#x200B;**提示**&#x200B;並按一下&#x200B;**傳送**&#x200B;按鈕。

```javascript
break down the fallout analysis at the touchpoint of the add to carts
```

![ChatGPT與CJA](./images/chatgpt123.png)

選取&#x200B;**執行報告**。

![ChatGPT與CJA](./images/chatgpt124.png)

返回[Analytics與代理程式](./analyticsagents.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}