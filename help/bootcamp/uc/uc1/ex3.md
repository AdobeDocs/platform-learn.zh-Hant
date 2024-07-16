---
title: Bootcamp — 即時客戶設定檔 — 建立對象 — UI
description: Bootcamp — 即時客戶設定檔 — 建立對象 — UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Audiences
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# 1.3建立對象 — UI

在本練習中，您將使用Adobe Experience Platform的Audience Builder來建立對象。

## Story

移至[Adobe Experience Platform](https://experience.adobe.com/platform)。 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``Bootcamp``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。

![資料擷取](./images/sb1.png)

在左側的功能表中，移至&#x200B;**對象**。 在此頁面中，您會看到提供有關&#x200B;**對象**&#x200B;效能之基本資訊的儀表板。

![區段](./images/menuseg.png)

按一下&#x200B;**瀏覽**，檢視所有現有對象的概觀。 按一下&#x200B;**+建立對象**&#x200B;按鈕以開始建立新對象。


![區段](./images/segmentationui.png)

將會出現一個Pop-IP，詢問您是要&#x200B;**&#39;撰寫對象&#39;**&#x200B;還是&#x200B;**&#39;建置規則&#39;**。 選擇&#x200B;**&#39;建置規則&#39;**&#x200B;以繼續，然後按一下&#x200B;**建立**。

![區段][def]

進入對象產生器後，您會立即注意到&#x200B;**屬性**&#x200B;功能表選項和&#x200B;**XDM個人設定檔**&#x200B;參考。


由於XDM是支援體驗業務的語言，因此XDM也是對象產生器的基礎。 Platform擷取的所有資料都應對應至XDM，因此無論資料來自何處，所有資料都會成為相同資料模型的一部分。 這可讓您在建立受眾時享有絕佳優勢，因為從這個受眾產生器UI，您可以在相同工作流程中合併來自任何來源的資料。 在Audience Builder中建立的對象可傳送至Adobe Target、Adobe Campaign或任何其他啟用管道等解決方案。

您現在需要建立已檢視產品&#x200B;**Real-Time CDP**&#x200B;之所有客戶的對象。

若要建立此對象，您必須新增體驗事件。 按一下&#x200B;**欄位**&#x200B;功能表列中的&#x200B;**事件**&#x200B;圖示，即可找到所有體驗事件。

![區段](./images/findee.png)

接下來，您將會看到最上層&#x200B;**XDM ExperienceEvents**&#x200B;節點。 按一下&#x200B;**XDM ExperienceEvent**。

![區段](./images/see.png)

移至&#x200B;**產品清單專案**。

![區段](./images/plitems.png)

選取「**名稱**」，然後從左側功能表將「**名稱**」物件拖放至對象產生器畫布的「**事件**」區段。 然後您會看到以下內容：

![區段](./images/eewebpdtlname.png)

比較引數應為&#x200B;**等於**，並在輸入欄位中輸入&#x200B;**即時CDP**。

![區段](./images/pv.png)

每次將元素新增至對象產生器時，您都可以按一下&#x200B;**重新整理預估值**&#x200B;按鈕，以取得對象中母體的新預估值。

![區段](./images/refreshest.png)

以&#x200B;**評估方法**&#x200B;的形式，選取&#x200B;**Edge**。

![區段](./images/evedge.png)

最後，讓我們為您的對象命名並儲存。

作為命名慣例，請使用：

- `yourLastName - Interest in Real-Time CDP`

然後，按一下&#x200B;**儲存並關閉**&#x200B;按鈕以儲存您的對象。

![區段](./images/segmentname.png)

您現在將返回對象概觀頁面，在那裡您將看到符合對象資格的客戶設定檔範例預覽。

![區段](./images/savedsegment.png)

您現在可以繼續進行下一個練習，並將您的對象用於Adobe Target。

下一步： [1.4採取動作：將您的對象傳送到Adobe Target](./ex4.md)

[返回使用者流程1](./uc1.md)

[返回所有模組](../../overview.md)


[def]: ./images/segmentationpopup.png
