---
title: Bootcamp — 客服中心中的個人化
description: Bootcamp — 客服中心中的個人化
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: f7697673-38f9-41f6-ac4d-2561db2ece67
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 2.6客服中心中的個人化

如同在訓練營中多次討論的那樣，個人化客戶體驗應以全通路的方式進行。 客服中心通常與客戶歷程的其餘部分非常脫節，這通常會導致令人沮喪的客戶體驗，但並不需要如此。 讓我們來示範呼叫中心如何輕鬆即時連線至Adobe Experience Platform。

## 客戶歷程流程

在上一個練習中，您透過行動應用程式按一下 **購買** 按鈕。

![DSN](./images/app20.png)

假設您對訂單的狀態有疑問，您會怎麼做？ 通常您可以致電客服中心。

呼叫客服中心前，您必須先瞭解您的 **熟客ID**. 您可以在網站的設定檔檢視器上找到您的忠誠度ID。

![DSN](./images/cc1.png)

在此案例中， **熟客ID** 是 **5863105**. 在示範環境中，呼叫中心功能的自訂實作需要新增前置詞至 **熟客ID**. 前置詞為 **11373**，因此在此範例中使用的忠誠度ID為 **11373 5863105**.

現在開始吧。 使用您的電話並撥打電話號碼 **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

系統會要求您輸入忠誠度ID，接著 **#**. 輸入您的熟客ID。

![DSN](./images/cc3.png)

然後您會聽到 **您好，名字**. 名字取自Adobe Experience Platform中的即時客戶個人檔案。 您有3個選項。 按住號碼 **1**， **訂單狀態**.

![DSN](./images/cc4.png)

聽完您的訂單狀態後，您可以選擇按下 **1** 返回主功能表，或按2。 按下 **2**.

![DSN](./images/cc5.png)

接著，系統會要求您選取介於1到5之間的數字（1表示低，5表示高），給您的客服中心體驗評分。 做出您的選擇。

![DSN](./images/cc6.png)

您致電客服中心的電話現在將結束。

前往 [Adobe Experience Platform](https://experience.adobe.com/platform). 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./images/home.png)

在繼續之前，您需要選取 **沙箱**. 要選取的沙箱已命名 ``Bootcamp``. 您可以按一下文字來執行此操作 **[!UICONTROL 生產產品]** 在熒幕上方的藍線中。 選取適當的 [!UICONTROL 沙箱]，您會看到畫面變更，現在您已進入專屬團隊 [!UICONTROL 沙箱].

![資料擷取](./images/sb1.png)

在左側功能表中，前往 **設定檔** 和 **瀏覽**.

![客戶設定檔](./images/homemenu.png)

選取 **身分名稱空間** **電子郵件** 並輸入客戶設定檔的電子郵件地址。 按一下 **檢視**. 按一下以開啟您的設定檔。

![DSN](./images/cc7.png)

您會再次看到客戶設定檔。 前往 **事件**.

![DSN](./images/cc8.png)

在「事件」底下，您會看到2個事件的eventType為 **呼叫中心**. 第一個事件是您回答問題後的結果 **評價您的通話滿意度**.

![DSN](./images/cc9.png)

向下捲動一點，您就會看到在您選取核取選項時所記錄的事件。 **訂單狀態**.

![DSN](./images/cc10.png)

前往 **區段會籍**. 您現在會看到，根據您透過客服中心的互動，2個區段即時符合您的個人資料資格。 這些區段會籍可以且應該用於影響任何其他頻道中進行的溝通和個人化。

![DSN](./images/cc11.png)

您現在已經完成此練習。

[返回使用者流程2](./uc2.md)

[返回所有模組](../../overview.md)
