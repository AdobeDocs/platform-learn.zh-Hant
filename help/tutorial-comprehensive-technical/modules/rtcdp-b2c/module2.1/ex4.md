---
title: Foundation — 即時客戶設定檔 — 建立區段 — UI
description: Foundation — 即時客戶設定檔 — 建立區段 — UI
kt: 5342
doc-type: tutorial
source-git-commit: c6ba1f751f18afe39fb6b746a62bc848fa8ec9bf
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 3%

---

# 2.1.4建立區段 — UI

在本練習中，您將使用Adobe Experience Platform的區段產生器來建立區段。

## Story

移至[Adobe Experience Platform](https://experience.adobe.com/platform)。 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./../../../modules/datacollection/module1.2/images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--aepSandboxId--``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。

![資料擷取](./../../../modules/datacollection/module1.2/images/sb1.png)

在左側的功能表中，移至&#x200B;**區段**。 您可以在此頁面上檢視所有現有區段的概觀。 按一下「**+建立區段**」按鈕以開始建立新區段。

![區段](./images/menuseg.png)

進入新的區段產生器後，您會立即注意到&#x200B;**屬性**&#x200B;功能表選項和&#x200B;**XDM個人設定檔**&#x200B;參考。

![區段](./images/segmentationui.png)

由於XDM是支援體驗業務的語言，因此XDM也是區段產生器的基礎。 Platform擷取的所有資料都應對應至XDM，因此無論資料來自何處，所有資料都會成為相同資料模型的一部分。 這為您在建立區段時提供了一項絕佳優勢，因為從這個區段產生器UI，您可以在相同工作流程中合併來自任何來源的資料。 在Segment Builder中建立的區段可傳送至Adobe Target、Adobe Campaign和Adobe Audience Manager等解決方案以進行啟用。

讓我們建立包含所有&#x200B;**男性**&#x200B;客戶的區段。

若要取得性別屬性，您需要瞭解並瞭解XDM。

性別是「人員」的屬性，可在「屬性」下找到。 若要開始進行，請先按一下&#x200B;**XDM個人設定檔**。 您將會看到此訊息。 從&#x200B;**XDM Individual Profile**&#x200B;視窗中，選取&#x200B;**人員**。

![區段](./images/person.png)

您將會看到此訊息。 在&#x200B;**人員**&#x200B;中，您可以找到&#x200B;**性別**&#x200B;屬性。 將「性別」屬性拖曳至區段產生器。

![區段](./images/gender.png)

現在您可以從預先填入的選項中選擇特定的性別。 在這種情況下，讓我們選擇&#x200B;**男性**。

![區段](./images/genderselection.png)

選取&#x200B;**男性**&#x200B;後，您可以按下&#x200B;**重新整理預估值**&#x200B;按鈕，以取得區段母體的預估值。 這對於業務使用者非常有用，因此他們可以檢視特定屬性對結果區段大小的影響。

![區段](./images/segmentpreview.png)

然後您會看到如下所示的估計：

![區段](./images/segmentpreviewest.png)

接下來，您應該稍微調整區段。 您必須針對檢視過產品&#x200B;**Proteus Fitness Jackshirt （橙色）**&#x200B;的所有男性客戶建立區段。

若要建置此區段，您必須新增體驗事件。 按一下&#x200B;**欄位**&#x200B;功能表列中的&#x200B;**事件**&#x200B;圖示，即可找到所有體驗事件。

![區段](./images/findee.png)

接下來，您將會看到最上層&#x200B;**XDM ExperienceEvents**&#x200B;節點。 按一下&#x200B;**XDM ExperienceEvent**。

![區段](./images/see.png)

移至&#x200B;**產品清單專案**。

![區段](./images/plitems.png)

選取「**名稱**」，然後從左側功能表將「**名稱**」物件拖放至區段產生器畫布中的「**事件**」區段。

![區段](./images/eeweb.png)

然後您會看到以下內容：

![區段](./images/eewebpdtlname.png)

比較引數應為&#x200B;**等於**，並在輸入欄位中輸入&#x200B;**MONTANA WIND JACKET**。

![區段](./images/pv.png)

每次將元素新增至區段產生器時，都可以按一下&#x200B;**重新整理預估值**&#x200B;按鈕，以取得區段中母體的新預估值。

到目前為止，您僅使用UI建立區段，但也有程式碼選項可建立區段。

建立區段時，您實際上是構成Profile Query Language (PQL)查詢。 若要以視覺效果呈現PQL程式碼，您可以按一下區段產生器右上角的&#x200B;**程式碼檢視**&#x200B;切換器。

![區段](./images/codeview.png)

現在您可以檢視完整的PQL陳述式：

```sql
person.gender in ["male"] and CHAIN(xEvent, timestamp, [C0: WHAT(productListItems.exists(name.equals("MONTANA WIND JACKET", false)))])
```

您也可以按一下&#x200B;**檢視設定檔**，以預覽屬於此區段之客戶設定檔的範例。

![區段](./images/previewprofiles.png)

![區段](./images/previewprofilesdtl.png)

最後，為區段命名並儲存。

作為命名慣例，請使用：

- `--demoProfileLdap-- - Male customers with interest in Montana Wind Jacket`

![區段](./images/segmentname.png)

然後，按一下&#x200B;**儲存並關閉**&#x200B;按鈕以儲存您的區段，之後您將返回「區段概述」頁面。

![區段](./images/savedsegment.png)

您現在可以繼續下一個練習，並透過API建立區段。

下一步： [2.1.5建立區段 — API](./ex5.md)

[返回模組2.1](./real-time-customer-profile.md)

[返回所有模組](../../../overview.md)
