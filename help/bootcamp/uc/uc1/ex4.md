---
title: Bootcamp - Real-time CDP — 建立對象並採取行動 — 將對象傳送到Adobe Target
description: Bootcamp - Real-time CDP — 建立對象並採取行動 — 將對象傳送到Adobe Target
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Audiences, Integrations
exl-id: 6a76c2ab-96b7-4626-a6d3-afd555220b1e
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 1.4採取動作：將對象傳送至Adobe Target

移至[Adobe Experience Platform](https://experience.adobe.com/platform)。 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``Bootcamp``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。

![資料擷取](./images/sb1.png)

## 1.4.1對您的Adobe Target目的地啟用您的對象

Adobe Target可作為Real-Time CDP的目的地。 若要設定您的Adobe Target整合，請前往&#x200B;**目的地**，前往&#x200B;**目錄**。

在&#x200B;**類別**&#x200B;功能表中按一下&#x200B;**Personalization**。 然後您會看到&#x200B;**Adobe Target**&#x200B;目的地卡。 按一下&#x200B;**啟用對象**。

![在](./images/atdest1.png)

選取目的地``Bootcamp Target``並按一下&#x200B;**下一步**。

![在](./images/atdest3.png)

在可用對象清單中，選取您在[1.3中建立的對象。3建立對象](./ex3.md)，其名稱為`yourLastName - Interest in Real-Time CDP`。 然後，按一下&#x200B;**下一步**。

![在](./images/atdest8.png)

在下一頁，按一下&#x200B;**下一步**。

![在](./images/atdest9.png)

按一下&#x200B;**完成**。

![在](./images/atdest10.png)

您的對象現在已對Adobe Target啟用。

![在](./images/atdest11.png)

>[!IMPORTANT]
>
>當您剛剛在Real-Time CDP中建立Adobe Target目的地時，目的地可能需要長達一小時的時間才會上線。 由於後端設定的緣故，此為一次性等待時間。 完成初始1小時的等待時間和後端設定後，傳送至Adobe Target目的地的新增邊緣對象將可即時鎖定目標。

## 1.4.2設定您的Adobe Target表單式活動

現在您的Real-Time CDP對象已設定為傳送至Adobe Target，您可以在Adobe Target中設定體驗鎖定目標活動。 在本練習中，您將設定視覺化體驗撰寫器型活動。

移至[https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/)，前往Adobe Experience Cloud首頁。 按一下&#x200B;**目標**&#x200B;以開啟。

![RTCDP](./images/excl.png)

在&#x200B;**Adobe Target**&#x200B;首頁上，您會看到所有現有的活動。
按一下&#x200B;**+建立活動**&#x200B;以建立新活動。

![RTCDP](./images/exclatov.png)

選取&#x200B;**體驗鎖定目標**。

![RTCDP](./images/exclatcrxt.png)

選取&#x200B;**Visual**&#x200B;並將&#x200B;**活動URL**&#x200B;設定為`https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`，但在您執行此動作之前，請以01到30之間的數字取代XX。

>[!IMPORTANT]
>
>每個啟用參與者都應使用個別網頁，以避免各種Adobe Target體驗發生衝突。 您可以挑選網頁，並前往下列位置尋找URL： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html)。
>
>所有頁面都共用相同的基本URL，並以參與者人數結尾。
>
>例如，參與者1應使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，參與者30應使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`。

選取工作區&#x200B;**AT Bootcamp**。

按一下&#x200B;**下一步**。

![RTCDP](./images/exclatcrxtdtlform.png)

您現在位於視覺化體驗撰寫器中。 網站完全載入可能需要20至30秒。

![RTCDP](./images/atform1.png)

預設對象目前是&#x200B;**所有訪客**。 按一下&#x200B;**所有訪客**&#x200B;旁的&#x200B;**3點**，然後按一下&#x200B;**變更對象**。

![RTCDP](./images/atform3.png)

您現在會看到可用受眾清單，而您先前建立並傳送至Adobe Target的Adobe Experience Platform受眾現在已加入此清單。 選取您先前在Adobe Experience Platform中建立的對象。 按一下&#x200B;**指派對象**。

![RTCDP](./images/exclatvecchaud.png)

您的Adobe Experience Platform對象現在屬於此體驗鎖定目標活動的一部分。

![RTCDP](./images/atform4.png)

您必須先按一下Cookie橫幅上的&#x200B;**全部允許**，才能變更主圖影像。

若要這麼做，請移至&#x200B;**瀏覽**

![RTCDP](./images/cook1.png)

接著，按一下&#x200B;**全部允許**。

![RTCDP](./images/cook2.png)

接著，返回&#x200B;**撰寫**。

![RTCDP](./images/cook3.png)

現在來變更網站首頁的主圖影像。 按一下網站上的預設主圖影像，按一下&#x200B;**取代內容**，然後選取&#x200B;**影像**。

![RTCDP](./images/atform5.png)

搜尋影像檔&#x200B;**rtcdp.png**。 選取該專案，然後按一下[儲存]。**&#x200B;**

![RTCDP](./images/atform6.png)

接著，您就會看到所選對象新影像的新體驗。

![RTCDP](./images/atform7.png)

按一下左上角的活動標題以重新命名。

![RTCDP](./images/exclatvecname.png)

對於名稱，請使用：

- `yourLastName - RTCDP - XT (VEC)`

按一下&#x200B;**下一步**。

![RTCDP](./images/atform8.png)

按一下&#x200B;**下一步**。

![RTCDP](./images/atform8a.png)

在&#x200B;**目標與設定** — 頁面上，移至&#x200B;**目標量度**。

![RTCDP](./images/atform9.png)

將主要目標設為&#x200B;**參與** - **網站逗留時間**。 按一下&#x200B;**儲存並關閉**。

![RTCDP](./images/vec3.png)

您現在位於&#x200B;**活動概覽**&#x200B;頁面。 您仍需要啟用活動。

![RTCDP](./images/atform10.png)

按一下欄位&#x200B;**非使用中**&#x200B;並選取&#x200B;**啟動**。

![RTCDP](./images/atform11.png)

之後，您將會收到視覺化確認，確認您的活動現在處於上線狀態。

![RTCDP](./images/atform12.png)

您的活動現在已上線，並且可以在啟動營網站上進行測試。

如果您現在返回示範網站並造訪&#x200B;**Real-Time CDP**&#x200B;的產品頁面，您將會立即符合您建立的對象資格，且您會看到Adobe Target活動即時顯示在首頁上。

>[!IMPORTANT]
>
>每個啟用參與者都應使用個別網頁，以避免各種Adobe Target體驗發生衝突。 您可以挑選網頁，並前往下列位置尋找URL： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html)。
>
>所有頁面都共用相同的基本URL，並以參與者人數結尾。
>
>例如，參與者1應使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，參與者30應使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`。

![RTCDP](./images/atform12a.png)

下一步： [1.5採取動作：將您的對象傳送到Facebook](./ex5.md)

[返回使用者流程1](./uc1.md)

[返回所有模組](../../overview.md)
