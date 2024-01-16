---
title: 建立標籤規則
description: 瞭解如何使用標籤規則，透過XDM物件將事件傳送至Platform Edge Network。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 1%

---

# 建立標籤規則

瞭解如何使用標籤規則，透過XDM物件將事件傳送至Platform Edge Network。 標籤規則是事件、條件和動作的組合，可告知標籤屬性執行動作。

>[!NOTE]
>
> 為了示範，本課程中的練習會以期間使用的範例為基礎進行 [建立身分](create-identities.md) 步驟；傳送XDM事件動作以從上的使用者擷取內容和身分 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html).


## 學習目標

在本課程結束時，您能夠：

* 使用命名慣例來管理標籤內的規則
* 在標籤規則中使用更新變數和傳送事件動作型別來傳送XDM事件
* 將標籤規則發佈至開發程式庫


## 先決條件

您熟悉資料收集標籤和 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html)，而且您必須先完成本教學課程中的下列課程：

* [設定XDM結構描述](configure-schemas.md)
* [設定身分名稱空間](configure-identities.md)
* [設定資料流](configure-datastream.md)
* [安裝在標籤屬性中的Web SDK擴充功能](install-web-sdk.md)
* [建立資料元素](create-data-elements.md)
* [建立身分](create-identities.md)

## 命名慣例

若要更妥善地管理標籤中的規則，建議遵循標準命名慣例。 本教學課程使用三部分命名慣例：

* [**位置**] - [**事件**] - [**工具**] (**序列**)

其中；

1. **位置** 是規則觸發所在網站的一或多個頁面
1. **事件** 是規則的觸發器
1. **工具** 是該規則之動作步驟中使用的特定應用程式
1. **序列** 是規則相對於其他規則所應引發的順序
<!-- minor update -->

## 建立標籤規則

在標籤中，規則是用來在不同的條件下執行動作（引發呼叫）。 Platform Web SDK標籤擴充功能包含本課程將使用的兩個動作：

* **[!UICONTROL 更新變數]** 將資料元素對應至XDM欄位
* **[!UICONTROL 傳送事件]** 傳送XDM物件至Experience Platform Edge Network

### 更新變數

將第一個規則建立為「全域設定」，以使用Platform Web SDK的 **[!UICONTROL 更新變數]** 動作。 接著建立第二個規則，並依序列排列，以在第一個規則之後觸發，以使用將XDM物件傳送至Platform Edge Network **[!UICONTROL 傳送事件]** 動作。 在本教學課程的稍後部分，您將根據訪客所在的頁面型別（例如產品頁面上的產品SKU）傳送不同的XDM欄位。 您可以排序包含的規則來完成此作業 **[!UICONTROL 更新變數]** 使用「 」的規則之前的動作 **[!UICONTROL 傳送事件]** 動作。

若要建立標籤規則：

1. 開啟您在本教學課程中使用的標籤屬性

1. 前往 **[!UICONTROL 規則]** 在左側導覽列中

1. 選取 **[!UICONTROL 建立新規則]** 按鈕

   ![建立規則](assets/rules-create.png)

1. 將規則命名為 `all pages global content variables - page bottom - AA (order 1)`

1. 在 **[!UICONTROL 活動]** 區段，選取 **[!UICONTROL 新增]**

   ![為規則命名並新增事件](assets/rule-name-new.png)

1. 使用 **[!UICONTROL 核心擴充功能]** 並選取 `Page Bottom` 作為 **[!UICONTROL 事件型別]**

1. 在 **[!UICONTROL 名稱]** 欄位，將其命名 `Core - Page Bottom - order 1`. 這可協助您以有意義的名稱說明觸發器。

1. 選取 **[!UICONTROL 進階]** 下拉式清單並輸入 `1` 在 **[!UICONTROL 訂購]**

   >[!NOTE]
   >
   > 您輸入的數字越高，其觸發的整體作業順序越靠後。

1. 選取 **[!UICONTROL 保留變更]** 以返回主規則畫面
   ![選取頁面底部觸發器](assets/create-tag-rule-trigger-bottom.png)

1. 在 **[!UICONTROL 動作]** 區段，選取 **[!UICONTROL 新增]**

1. 作為 **[!UICONTROL 副檔名]**，選取 **[!UICONTROL Adobe Experience Platform Web SDK]**

1. 作為 **[!UICONTROL 動作型別]**，選取 **[!UICONTROL 更新變數]**

1. 作為 **[!UICONTROL 資料元素]**，選取 `xdm.variable.content` 您已在以下位置建立： [建立資料元素](create-data-elements.md) 課程

   ![更新變數結構](assets/create-rule-update-variable.png)

現在對應您的 [!UICONTROL 資料元素] 至 [!UICONTROL 綱要] 由您的XDM物件使用。

>[!NOTE]
> 
> 您可以對應至個別屬性或整個物件。 在此範例中，您會對應至個別屬性。


1. 向下捲動，直到達到 **`web`** 物件

1. 選取以開啟

1. 將下列資料元素對應至對應的 `web` XDM變數

   * **`web.webPageDetials.name`** 至 `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** 至 `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** 至 `%page.pageInfo.hierarchie1%`

   ![更新變數內容](assets/create-rule-xdm-variable-content.png)

1. 接下來，尋找 `identityMap` 物件並選取它

1. 將對應至 `identityMap.loginID` 資料元素

   ![更新變數身分對應](assets/create-rule-variable-identityMap.png)

1. 接著，尋找eventType欄位並加以選取

1. 輸入值 `web.webpagedetails.pageViews`

   >[!WARNING]
   >
   > 此下拉式清單會填入 **`xdm.eventType`** 變數中識別資料中心。 雖然您也可以在此欄位中輸入任意格式的標籤，強烈建議您這麼做 **不要** 因為它對Platform有不利的影響。

   >[!TIP]
   >
   > 若要瞭解要填入 `eventType` 欄位，您必須移至「綱要」頁面並選取 `eventType` 欄位以檢視右側邊欄上的建議值。

   ![更新變數身分對應](assets/create-tag-rule-eventType.png)


1. 選取 **[!UICONTROL 保留變更]** 然後 **[!UICONTROL 儲存]** 下一個畫面中要完成規則建立的規則

### 傳送事件

現在您已設定變數，您可以建立第二個規則，使用將XDM物件傳送至Platform Edge Network **[!UICONTROL 傳送事件]** 動作型別。

1. 在右側，選取 **[!UICONTROL 新增規則]** 以建立其他規則

1. 將規則命名為 `all pages send event - page bottom - AA (order 50)`

1. 在 **[!UICONTROL 活動]** 區段，選取 **[!UICONTROL 新增]**

1. 使用 **[!UICONTROL 核心擴充功能]** 並選取 `Page Bottom` 作為 **[!UICONTROL 事件型別]**

1. 在 **[!UICONTROL 名稱]** 欄位，將其命名 `Core - Page Bottom - order 50`. 這可協助您以有意義的名稱說明觸發器。

1. 選取 **[!UICONTROL 進階]** 下拉式清單並輸入 `50` 在 **[!UICONTROL 訂購]**. 這將確保第二個規則會在您設定為觸發的第一個規則之後觸發 `1`.

1. 選取 **[!UICONTROL 保留變更]** 以返回主規則畫面
   ![選取頁面底部觸發器](assets/create-tag-rule-trigger-bottom-send.png)

1. 在 **[!UICONTROL 動作]** 區段，選取 **[!UICONTROL 新增]**

1. 作為 **[!UICONTROL 副檔名]**，選取  **[!UICONTROL Adobe Experience Platform Web SDK]**

1. 作為  **[!UICONTROL 動作型別]**，選取  **[!UICONTROL 傳送事件]**

1. 作為 **[!UICONTROL XDM]**，選取 `xdm.variable.content` 在上一課程中建立的資料元素

1. 選取 **[!UICONTROL 保留變更]** 以返回主規則畫面

   ![新增「傳送事件」動作](assets/create-rule-send-event-action.png)
1. 選取 **[!UICONTROL 儲存]** 儲存規則的方式

   ![儲存規則](assets/create-rule-save-rule.png)

## 在程式庫中發佈規則

接下來，將規則發佈至您的開發環境，以便您可以驗證其是否有效。

若要建立程式庫：

1. 前往 **[!UICONTROL 發佈流程]** 在左側導覽列中

1. 選取 **[!UICONTROL 新增程式庫]**

   ![選取新增程式庫](assets/rule-publish-library.png)
1. 對於 **[!UICONTROL 名稱]**，輸入 `Luma Web SDK Tutorial`
1. 對於 **[!UICONTROL 環境]**，選取 `Development`
1. 選取  **[!UICONTROL 新增所有變更的資源]**

   >[!NOTE]
   >
   >    除了Adobe Experience Platform Web SDK擴充功能和 `all pages global content variables - page bottom - AA (order 50)` 規則中，您會看見前述課程中建立的標籤元件。 核心擴充功能包含所有Web標籤屬性所需的基本JavaScript。

1. 選取 **[!UICONTROL 儲存並為開發環境建置]**

   ![建立及建置程式庫](assets/create-tag-rule-library-changes.png)

程式庫可能需要幾分鐘的時間才能建置，建置完成後，程式庫名稱左側會顯示一個綠色點：

![建置完成](assets/create-rule-development-success.png)

如您所見 [!UICONTROL 發佈流程] 畫面中，發佈程式還有許多不在本教學課程的討論範圍內。 本教學課程僅在您的開發環境中使用單一程式庫。

現在您已準備好使用Adobe Experience Platform Debugger驗證請求中的資料。

[下一個 ](validate-with-debugger.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
