---
title: Bootcamp — 即時CDP — 建立區段並採取行動 — 將區段傳送至Adobe Target — 巴西
description: Bootcamp — 即時CDP — 建立區段並採取行動 — 將區段傳送至Adobe Target — 巴西
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 1%

---

# 1.4採取行動：將區段傳送至Adobe Target

前往 [Adobe Experience Platform](https://experience.adobe.com/platform). 登入後，您會登陸Adobe Experience Platform首頁。

![資料擷取](./images/home.png)

繼續之前，您需要選取 **沙箱**. 要選取的沙箱已命名 ``Bootcamp``. 您可以按一下文字 **[!UICONTROL 生產產品]** 在螢幕上方的藍線。 選取適當的 [!UICONTROL 沙箱]，您會看到畫面變更，現在您已進入專屬 [!UICONTROL 沙箱].

![資料擷取](./images/sb1.png)

## 1.4.1啟用區段至Adobe Target目的地

Adobe Target是Real-Time CDP的目的地。 若要設定Adobe Target整合，請前往 **目的地**，到 **目錄**.

按一下 **個人化** 在 **類別** 功能表。 然後您會看到 **Adobe Target** 目的地卡。 按一下 **啟用區段**.

![AT](./images/atdest1.png)

選取目的地 ``Bootcamp Target`` 按一下 **下一個**.

![AT](./images/atdest3.png)

在可用區段清單中，選取您在中建立的區段 [1.3建立區段](./ex3.md)，此名稱為 `yourLastName - Interest in Real-Time CDP`. 然後，按一下 **下一個**.

![AT](./images/atdest8.png)

在下一頁，按一下 **下一個**.

![AT](./images/atdest9.png)

按一下&#x200B;**完成**。

![AT](./images/atdest10.png)

您的區段現在已啟動至Adobe Target。

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>當您剛在Real-Time CDP中建立Adobe Target目的地時，該目的地可能需要一小時的時間才能上線。 由於後端設定的設定，這是一次性的等候時間。 完成初始1小時等候時間和後端設定後，傳送至Adobe Target目的地的新新增邊緣區段便可即時用於鎖定目標。

## 1.4.2設定Adobe Target表單式活動

現在您的Real-Time CDP區段已設定為傳送至Adobe Target，您可以在Adobe Target中設定您的體驗鎖定目標活動。 在本練習中，您將設定可視化體驗撰寫器型活動。

前往Adobe Experience Cloud首頁， [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). 按一下 **目標** 來開啟它。

![RTCDP](./images/excl.png)

在 **Adobe Target** 首頁，您會看到所有現有活動。
按一下 **+建立活動** 來建立新活動。

![RTCDP](./images/exclatov.png)

選擇 **體驗鎖定**.

![RTCDP](./images/exclatcrxt.png)

選擇 **視覺** 並設定 **活動URL** to `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`，但在執行此操作之前，請以01到30之間的數字取代XX。

>[!IMPORTANT]
>
>啟用的每位參與者都應使用個別的網頁，以避免各種Adobe Target體驗發生衝突。 您可以前往下列位置，選擇網頁並尋找URL: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>頁面都共用相同的基本URL，結尾為參與者的編號。
>
>例如，參與者1應使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，參與者30應使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

選取工作區 **AT Bootcamp**.

按&#x200B;**「下一步」**。

![RTCDP](./images/exclatcrxtdtlform.png)

您現在是可視化體驗撰寫器。 網站完全載入前，可能需要20-30秒。

![RTCDP](./images/atform1.png)

預設對象目前為 **所有訪客**. 按一下 **3點** 下一頁 **所有訪客** 按一下 **變更對象**.

![RTCDP](./images/atform3.png)

您現在會看到可用對象的清單，而您先前建立並傳送至Adobe Target的Adobe Experience Platform區段現已成為此清單的一部分。 選取您先前在Adobe Experience Platform中建立的區段。 按一下 **指派對象**.

![RTCDP](./images/exclatvecchaud.png)

您的Adobe Experience Platform區段現在是此體驗鎖定目標活動的一部分。

![RTCDP](./images/atform4.png)

在可以更改主圖影像之前，您需要按一下 **允許全部** 上。

若要這麼做，請前往 **瀏覽**

![RTCDP](./images/cook1.png)

下一步，按一下 **允許全部**.

![RTCDP](./images/cook2.png)

接下來，返回 **撰寫**.

![RTCDP](./images/cook3.png)

現在來變更網站首頁上的主圖影像。 按一下網站上的預設主圖影像，按一下 **取代內容** 然後選取 **影像**.

![RTCDP](./images/atform5.png)

搜尋影像檔案 **rtcdp.png**. 選取它，然後按一下 **儲存**.

![RTCDP](./images/atform6.png)

然後，您就會看到您所選對象的新影像體驗。

![RTCDP](./images/atform7.png)

按一下左上角的活動標題，將其重新命名。

![RTCDP](./images/exclatvecname.png)

名稱請使用：

- `yourLastName - RTCDP - XT (VEC)`

按&#x200B;**「下一步」**。

![RTCDP](./images/atform8.png)

按&#x200B;**「下一步」**。

![RTCDP](./images/atform8a.png)

在 **目標與設定**  — 頁，轉到 **目標量度**.

![RTCDP](./images/atform9.png)

將主要目標設為 **參與** - **網站逗留時間**. 按一下&#x200B;**「儲存並關閉」**。

![RTCDP](./images/vec3.png)

你現在在 **活動概覽** 頁面。 您仍需要啟用活動。

![RTCDP](./images/atform10.png)

按一下欄位 **非作用中** 選取 **啟動**.

![RTCDP](./images/atform11.png)

之後，您會獲得活動現已上線的視覺確認。

![RTCDP](./images/atform12.png)

您的活動現在已上線，可在bootcamp網站上測試。

如果您現在回到示範網站，並造訪的產品頁面 **Real-Time CDP**，您就會立即符合所建立區段的資格，且您會看到Adobe Target活動即時顯示在首頁上。

>[!IMPORTANT]
>
>啟用的每位參與者都應使用個別的網頁，以避免各種Adobe Target體驗發生衝突。 您可以前往下列位置，選擇網頁並尋找URL: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>頁面都共用相同的基本URL，結尾為參與者的編號。
>
>例如，參與者1應使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，參與者30應使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

下一步： [1.5採取行動：將區段傳送至Facebook](./ex5.md)

[返回用戶流1](./uc1.md)

[返回所有模組](../../overview.md)
