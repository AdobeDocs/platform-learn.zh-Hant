---
title: 建立區段
seo-title: Build segments | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 建立區段
description: 在本課程中，我們將根據先前課程中擷取的設定檔資料建立一些區段。
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-build-segments.jpg
exl-id: cd05e814-1ea7-48ba-adf6-1a71504c623e
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---

# 建立區段

<!-- 30 min-->
在本課程中，我們將根據先前課程中擷取的設定檔資料建立一些區段。

擁有即時客戶個人檔案後，您就可以建立具有類似特徵且可能對行銷策略有類似回應之個人的區段。 這些區段的組成要素是您先前建立的XDM欄位。

**資料架構師**&#x200B;將需要在本教學課程之外建立區段，並透過此工作支援其同事。

在開始練習之前，請觀看此短片，以進一步瞭解如何建立區段：
>[!VIDEO](https://video.tv.adobe.com/v/27254?learn=on&enablevpops)


## 需要的許可權

在[設定許可權](configure-permissions.md)課程中，您已設定完成本課程所需的所有存取控制，特別是：

* 許可權專案&#x200B;**[!UICONTROL 設定檔管理]** > **[!UICONTROL 管理區段]**、**[!UICONTROL 檢視區段]**&#x200B;以及&#x200B;**[!UICONTROL 匯出對象區段]**
* 許可權專案&#x200B;**[!UICONTROL 設定檔管理]** > **[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 管理設定檔]**
* 許可權專案&#x200B;**[!UICONTROL 沙箱]** > `Luma Tutorial`
* `Luma Tutorial Platform`產品設定檔的使用者角色存取權
* `Luma Tutorial Platform`產品設定檔的開發人員角色存取權（針對API）

## 建立基本區段

讓我們為具有金級或白金級的熟客方案客戶建立一個簡單的區段

1. 在Platform使用者介面中，前往左側導覽中的&#x200B;**[!UICONTROL 區段]**
1. 選取&#x200B;**[!UICONTROL 建立區段]**&#x200B;按鈕
1. 結構描述產生器左側有三個索引標籤，分別代表屬性（記錄資料）、事件（時間序列資料）和對象
1. 選取齒輪圖示，記錄區段產生器預設為僅顯示含有資料的欄位，並允許您變更合併原則
1. 在屬性標籤中，導覽至&#x200B;**XDM個人設定檔>忠誠度**&#x200B;資料夾（您也可以搜尋「忠誠度」）
1. 從屬性欄位功能表拖放`Tier`至區段產生器畫布
1. 選取`Tier` equals `Gold`或`Platinum`
1. 選取&#x200B;**[!UICONTROL 重新整理預估值]**，以檢視有多少設定檔符合您的區段資格
1. 以&#x200B;**[!UICONTROL Name]**&#x200B;的身分，輸入`Luma customers with level Gold or Above`
1. 選取&#x200B;**[!UICONTROL 儲存]**
   ![區段](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## 建立動態區段

在本練習中，我們將為在30天內購買相同產品兩次的客戶建立區段。 動態區段可讓您使用欄位做為變數來擴充分段。

1. 前往左側導覽中的&#x200B;**[!UICONTROL 區段]**
1. 選取&#x200B;**[!UICONTROL 建立區段]**&#x200B;按鈕
1. 選取&#x200B;**[!UICONTROL 事件]**&#x200B;標籤
1. 將清單篩選為`purchases`
1. 將&#x200B;**[!UICONTROL 購買]**&#x200B;事件型別拖曳到畫布&#x200B;_兩次_
1. 選取兩個&#x200B;**[!UICONTROL 購買]**&#x200B;事件之間的時鐘圖示，並選擇[30天內]
1. 確認此時您的區段定義為&#x200B;**「包含至少有1個購買事件的對象，然後在30天內至少有1個購買事件」**
   ![30天內購買兩次](assets/segment-twoPurchases.png)
1. 現在將事件篩選器變更為`sku`
1. 將SKU欄位拖曳至第二個購買事件
   使用SKU在30天內購買![兩次](assets/segment-twoPurchases-addSku.png)
1. 現在清除事件篩選器
1. 您應該會在&#x200B;**[!UICONTROL 瀏覽變數]**&#x200B;區段中看到，有兩個購買事件的資料夾。 按一下以探索&#x200B;**[!UICONTROL 購買1]**\
   ![使用SKU在30天內進行兩次購買，瀏覽第一次購買](assets/segment-twoPurchases-browsePurchaseOne.png)
1. 向下鑽研&#x200B;**[!UICONTROL 產品清單專案]**&#x200B;資料夾，選取&#x200B;**[!UICONTROL SKU]**&#x200B;欄位，並將其拖曳至&#x200B;**[!UICONTROL 等於]**&#x200B;運算元的右側。 當您將滑鼠游標停留在區域上時，請將它拖放到「新增以比較運算元」區段
1. 為您的區段命名`Bought same product within 30 days`
1. 確認您的對象定義為&#x200B;**「包含至少有1個「購買」事件，然後在30天內至少有1個「購買」事件(（SKU等於「購買1 SKU」）)的對象」**
1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;按鈕

   ![在過去30天區段內購買相同的產品](assets/segment-boughtSameProduct.png)

## 建立多實體區段

記得我們在先前的課程中如何建立`Luma Offline Purchase Events Schema`與`Luma Product Catalog Schema`之間的關係嗎？ 我們這麼做是為了可以使用多實體區段在結構描述中利用關係。

透過進階的多實體分段功能，您可以使用多個XDM類別來建立區段以擴充您的結構描述。 因此，區段產生器可存取其他欄位，猶如個人資料存放區的原生欄位

您將套用您在`Luma Product Catalog Schema`與`Luma Offline Purchase Events Schema`之間建立的關聯性，以建立下一個區段。

1. 前往左側導覽中的&#x200B;**[!UICONTROL 區段]**
1. 選取&#x200B;**[!UICONTROL 建立區段]**&#x200B;按鈕
1. 選取&#x200B;**[!UICONTROL 事件]**&#x200B;標籤
1. 將清單篩選為`purchases`
1. 將&#x200B;**[!UICONTROL 購買]**&#x200B;事件型別拖曳到畫布上
1. 選取事件上方的時鐘下拉式清單，並選擇過去30天中的&#x200B;****
1. 篩選&#x200B;**[!UICONTROL 事件]**&#x200B;清單至`category`，然後將&#x200B;**[!UICONTROL 產品類別]**&#x200B;欄位拖曳至&#x200B;**[!UICONTROL 購買]**
1. 將運運算元變更為&#x200B;**[!UICONTROL 開頭為]**，並在文字方塊中輸入`men`
1. 以&#x200B;**[!UICONTROL Name]**&#x200B;的身分，輸入`Purchased a Men's product in the last 30 days`
1. 確認對象定義`(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;按鈕

   ![在過去30天區段內購買相同的產品](assets/segment-purchasedMens.png)

## 批次和串流細分

按一下左側導覽中的&#x200B;**[!UICONTROL 區段]**，讓我們花點時間檢閱我們的三個區段：

* 我們的兩個區段是批次區段，另一個是串流區段。
* Platform會儘可能預設為串流細分，當客戶符合條件時，即讓他們符合區段的資格。 當區段定義太複雜而無法串流時，會自動轉換為批次。 在此情況下，這兩個區段會預設為批次，因為購買事件的回顧期間大於七天。 如需完整且最新的串流限制清單，請參閱[檔案](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html)。
* 批次工作以每日排程執行，該排程可切換。

![在過去30天區段內購買相同的產品](assets/segment-review.png)

## 其他資源

* [Segmentation Service檔案](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=zh-Hant)
* [Segmentation Service API參考](https://www.adobe.io/experience-platform-apis/references/segmentation/)

區段還有更多功能，尤其是啟用區段時。 這些主題將在另一個教學課程中探討。

您已完成所有練習！ 請繼續進行[結論](conclusion.md)。
