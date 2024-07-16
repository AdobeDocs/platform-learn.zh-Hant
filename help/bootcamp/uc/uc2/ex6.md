---
title: Bootcamp — 呼叫中心的Personalization
description: Bootcamp — 呼叫中心的Personalization
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: f7697673-38f9-41f6-ac4d-2561db2ece67
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 2.6呼叫中心的Personalization

正如在啟動訓練營中曾多次討論的，個人化客戶體驗應該是全通路的事情。 客服中心通常與客戶歷程的其餘部分相當脫節，這通常會導致令人沮喪的客戶體驗，但並非必須如此。 以下提供呼叫中心如何輕鬆即時連線至Adobe Experience Platform的範例。

## 客戶歷程流程

在上一個練習中，您使用行動應用程式，按一下&#x200B;**購買**&#x200B;按鈕購買產品。

![DSN](./images/app20.png)

假設您對訂單的狀態有疑問，您會怎麼做？ 通常您可以致電客服中心。

呼叫呼叫中心之前，您必須知道您的&#x200B;**忠誠度識別碼**。 您可以在網站的設定檔檢視器上找到您的熟客方案ID。

![DSN](./images/cc1.png)

在此案例中，**忠誠度識別碼**&#x200B;為&#x200B;**5863105**。 在示範環境中，客服中心功能的自訂實作中，您必須為&#x200B;**忠誠度識別碼**&#x200B;新增前置詞。 前置詞是&#x200B;**11373**，所以在此範例中使用的熟客識別碼是&#x200B;**11373 5863105**。

現在開始吧。 使用您的電話並撥打&#x200B;**+1 (323) 745-1670**。

![DSN](./images/cc2.png)

系統會要求您輸入忠誠度識別碼，接著輸入&#x200B;**#**。 輸入您的熟客方案ID。

![DSN](./images/cc3.png)

您將會聽到&#x200B;**名字**&#x200B;您好。 該名字取自Adobe Experience Platform中的即時客戶個人檔案。 您有3種選擇。 按號碼&#x200B;**1**，**訂單狀態**。

![DSN](./images/cc4.png)

聽完您的訂單狀態後，您可以選擇按&#x200B;**1**&#x200B;返回主功能表，或按2。 按&#x200B;**2**。

![DSN](./images/cc5.png)

接著，系統會要求您選取介於1到5之間、1代表低而5代表高的數字，給您的客服中心體驗評分。 做出您的選擇。

![DSN](./images/cc6.png)

您致電客服中心的工作將結束。

移至[Adobe Experience Platform](https://experience.adobe.com/platform)。 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``Bootcamp``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。

![資料擷取](./images/sb1.png)

在左側功能表中，移至&#x200B;**設定檔**&#x200B;和&#x200B;**瀏覽**。

![客戶設定檔](./images/homemenu.png)

選取&#x200B;**身分名稱空間** **電子郵件**，然後輸入客戶設定檔的電子郵件地址。 按一下&#x200B;**檢視**。 按一下以開啟您的設定檔。

![DSN](./images/cc7.png)

您會再次看到客戶設定檔。 移至&#x200B;**活動**。

![DSN](./images/cc8.png)

在「事件」底下，您會看到2個事件的eventType為&#x200B;**呼叫中心**。 第一個活動是您回答問題&#x200B;**評定您的通話滿意度**&#x200B;的結果。

![DSN](./images/cc9.png)

向下捲動一點，您會看到選取檢查&#x200B;**訂單狀態**&#x200B;選項時所記錄的事件。

![DSN](./images/cc10.png)

移至&#x200B;**區段會籍**。 您現在會看到，根據您透過客服中心的互動，2個區段即時符合您的個人檔案資格。 這些區段會籍可以（且應該）用於影響任何其他頻道中進行的通訊和個人化。

![DSN](./images/cc11.png)

您現在已經完成此練習。

[返回使用者流程2](./uc2.md)

[返回所有模組](../../overview.md)
