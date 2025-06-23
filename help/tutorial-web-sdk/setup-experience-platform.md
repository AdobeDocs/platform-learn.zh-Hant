---
title: 透過Platform Web SDK將資料串流至Adobe Experience Platform
description: 瞭解如何使用網頁SDK將網頁資料串流至Adobe Experience Platform。 本課程是「使用 Web SDK 實施 Adob​​e Experience Cloud」教學課程的一部分。
jira: KT-15407
exl-id: 4d749ffa-e1c0-4498-9b12-12949807b369
source-git-commit: 7c302bf9503e7a95162ab83af59d466bb4ff1f7e
workflow-type: tm+mt
source-wordcount: '2307'
ht-degree: 4%

---

# 使用網頁SDK將資料串流至Experience Platform

了解如何使用 Platform Web SDK 將 Web 資料串流傳輸至 Adob&#x200B;&#x200B;e Experience Platform。

Experience Platform是所有新Experience Cloud應用程式(例如Adobe Real-Time Customer Data Platform、Adobe Customer Journey Analytics和Adobe Journey Optimizer)的骨幹。 這些應用程式的設計是要使用Platform Web SDK作為其最佳的Web資料收集方法。

![網頁SDK和Adobe Experience Platform圖表](assets/dc-websdk-aep.png)

Experience Platform會使用您先前建立的相同XDM結構描述，從Luma網站擷取事件資料。 當該資料傳送到Platform Edge Network時，資料流設定可以將其轉送到Experience Platform。

## 學習目標

在本課程結束時，您將能夠：

* 在Adobe Experience Platform中建立資料集
* 設定資料流以將網頁SDK資料傳送至Adobe Experience Platform
* 為即時客戶個人檔案啟用串流網頁資料
* 驗證資料已著陸Platform資料集和即時客戶設定檔中
* 將忠誠度計畫資料範例擷取至Platform
* 建立簡單的平台對象

## 先決條件

若要完成本課程，您必須先：

* 擁有Adobe Experience Platform應用程式的存取權，例如Real-Time Customer Data Platform、Journey Optimizer或Customer Journey Analytics
* 完成本教學課程之初始設定和標籤設定區段中先前的課程。

>[!NOTE]
>
>如果您沒有任何Platform應用程式，您可以略過本課程或一起閱讀。

## 建立資料集

所有成功內嵌至Adobe Experience Platform的資料都會以資料集的形式保留在資料湖中。 [資料集](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/catalog/datasets/overview)是資料集合的儲存和管理結構，通常是包含結構描述（欄）和欄位（列）的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。

讓我們為您的Luma Web事件資料設定資料集：


1. 移至[Experience Platform](https://experience.adobe.com/platform/)或[Journey Optimizer](https://experience.adobe.com/journey-optimizer/)介面
1. 確認您是在本教學課程使用的開發沙箱中
1. 從左側導覽開啟&#x200B;**[!UICONTROL 資料管理>資料集]**
1. 選取&#x200B;**[!UICONTROL 建立資料集]**

   ![建立結構描述](assets/experience-platform-create-dataset.png)

1. 選取&#x200B;**[!UICONTROL 從結構描述建立資料集]**&#x200B;選項

   ![從結構描述建立資料集](assets/experience-platform-create-dataset-schema.png)

1. 選取在[先前的課程](configure-schemas.md)中建立的`Luma Web Event Data`結構描述，然後選取&#x200B;**[!UICONTROL 下一步]**

   ![資料集，選取結構描述](assets/experience-platform-create-dataset-schema-selection.png)

1. 為資料集提供&#x200B;**[!UICONTROL 名稱]**&#x200B;和選用的&#x200B;**[!UICONTROL 描述]**。 此練習請使用`Luma Web Event Data`，然後選取&#x200B;**[!UICONTROL 完成]**

   ![資料集名稱](assets/experience-platform-create-dataset-schema-name.png)

資料集現在已設定為開始從Platform Web SDK實作收集資料。

## 設定資料串流

現在您可以設定您的[!UICONTROL 資料串流]，將資料傳送至[!UICONTROL Adobe Experience Platform]。 資料串流是標籤屬性、Platform Edge Network和Experience Platform資料集之間的連結。

1. 開啟[資料彙集](https://experience.adobe.com/#/data-collection){target="blank"}介面
1. 從左側導覽中選取&#x200B;**[!UICONTROL 資料串流]**
1. 開啟您在[設定資料流](configure-datastream.md)課程`Luma Web SDK`中建立的資料流

   ![選取Luma Web SDK資料流](assets/datastream-luma-web-sdk-development.png)

1. 選取&#x200B;**[!UICONTROL 新增服務]**
   ![新增服務至資料流](assets/experience-platform-addService.png)
1. 選取&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;做為&#x200B;**[!UICONTROL 服務]**
1. 選取`Luma Web Event Data`做為&#x200B;**[!UICONTROL 事件資料集]**

1. 選取「**[!UICONTROL 儲存]**」。

   ![資料流設定](assets/experience-platform-datastream-config.png)

當您在對應至標籤屬性的[Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html)上產生流量時，資料會填入Experience Platform中的資料集！

## 驗證資料集

此步驟對於確保資料已抵達資料集至關重要。 驗證傳送至資料集的資料有兩個方面。

* 使用[!UICONTROL Experience Platform Debugger]進行驗證
* 使用[!UICONTROL 預覽資料集]進行驗證
* 使用[!UICONTROL 查詢服務]進行驗證

### Experience Platform Debugger

這些步驟與您在[偵錯工具課程](validate-with-debugger.md)中所執行的步驟大致相同。 不過，由於資料只有在資料流中啟用後才會傳送至Platform，因此您必須產生更多範例資料：

1. 開啟[Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html)並選取[!UICONTROL Experience Platform Debugger]擴充功能圖示

1. 設定偵錯工具將標籤屬性對應至&#x200B;*您的*&#x200B;開發環境，如[使用偵錯工具驗證](validate-with-debugger.md)課程中所述

   ![Debugger 中顯示的 Launch 開發環境](assets/experience-platform-debugger-dev.png)

1. 使用 `test@test.com`/`test` 認證登入 Luma 網站

1. 返回 [Luma 首頁](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 在Debugger顯示的Platform Web SDK網路信標中，選取「事件」列以在快顯視窗中展開詳細資訊

   Debugger中的![Web SDK](assets/experience-platform-debugger-dev-eventType.png)

1. 在快顯視窗中搜尋「identityMap」。 您應該會在這裡看到lumaCrmId包含authenticatedState、id和primary的三個索引鍵
   Debugger中的![Web SDK](assets/experience-platform-debugger-dev-idMap.png)

現在，資料應填入`Luma Web Event Data`資料集，並準備好「預覽資料集」驗證。

### 預覽資料集

若要確認資料已著陸Platform的資料湖，快速選項是使用&#x200B;**[!UICONTROL 預覽資料集]**&#x200B;功能。 網頁SDK資料會微批次處理至資料湖，並定期在平台介面中重新整理。 您可能需要10到15分鐘的時間才能看到您產生的資料。

1. 在[Experience Platform](https://experience.adobe.com/platform/)介面中，選取左側導覽中的&#x200B;**[!UICONTROL 資料管理>資料集]**&#x200B;以開啟&#x200B;**[!UICONTROL 資料集]**&#x200B;儀表板。

   控制面板會列出貴組織的所有可用資料集。 系統會顯示每個列出資料集的詳細資訊，包括其名稱、資料集所遵守的結構描述，以及最新擷取執行的狀態。

1. 選取您的`Luma Web Event Data`資料集以開啟其&#x200B;**[!UICONTROL 資料集活動]**&#x200B;畫面。

   ![資料集Luma Web事件](assets/experience-platform-dataset-validation-lumaSDK.png)

   活動畫麵包含以視覺效果呈現訊息使用率的圖表，以及成功和失敗批次的清單。

1. 從&#x200B;**[!UICONTROL 資料集活動]**&#x200B;畫面中，選取靠近熒幕右上角的&#x200B;**[!UICONTROL 預覽資料集]**，以預覽最多100列的資料。 如果資料集空白，則會停用預覽連結。

   ![資料集預覽](assets/experience-platform-dataset-preview.png)

   在預覽視窗中，資料集的結構描述階層檢視會顯示在右側。

   ![資料集預覽1](assets/experience-platform-dataset-preview-1.png)


### 查詢資料

1. 在[Experience Platform](https://experience.adobe.com/platform/)介面中，選取左側導覽中的&#x200B;**[!UICONTROL 資料管理>查詢]**&#x200B;以開啟&#x200B;**[!UICONTROL 查詢]**&#x200B;畫面。
1. 選取&#x200B;**[!UICONTROL 建立查詢]**
1. 首先，執行查詢以檢視資料湖中表格的所有名稱。 在查詢編輯器中輸入`SHOW TABLES`，然後按一下播放圖示以執行查詢。
1. 在結果中，請注意資料表的名稱類似於`luma_web_event_data`的情況
1. 現在，使用參考您表格的簡單查詢來查詢表格（請注意，查詢預設將限製為100個結果）： `SELECT * FROM "luma_web_event_data"`
1. 過了一會兒，您應該會看到網頁資料的範例記錄。

>[!ERROR]
>
>如果您收到「未布建表格」錯誤，請仔細檢查表格的名稱。 也可能是微批次資料尚未抵達資料湖。 10-15分鐘後再試一次。

>[!INFO]
>
>  如需Adobe Experience Platform查詢服務的詳細資訊，請參閱Platform教學課程一節中的[探索資料](https://experienceleague.adobe.com/zh-hant/docs/platform-learn/tutorials/queries/explore-data)。


## 為即時客戶個人檔案啟用資料集和結構描述

對於Real-Time Customer Data Platform和Journey Optimizer的客戶，下一步是啟用即時客戶個人檔案的資料集和結構描述。 從Web SDK串流的資料會是流入Platform的眾多資料來源之一，而您想要將您的Web資料與其他資料來源結合，以建置360度客戶設定檔。 若要深入瞭解即時客戶個人檔案，請觀看此短片：

>[!VIDEO](https://video.tv.adobe.com/v/27251?learn=on&captions=eng)

>[!CAUTION]
>
>使用您自己的網站和資料時，建議在啟用資料以用於即時客戶個人檔案之前，先對資料進行更強大的驗證。


**若要啟用資料集：**

1. 開啟您建立的資料集，`Luma Web Event Data`

1. 選取&#x200B;**[!UICONTROL 設定檔切換]**&#x200B;以開啟

   ![設定檔切換](assets/setup-experience-platform-profile.png)

1. 確認您要&#x200B;**[!UICONTROL 啟用]**&#x200B;資料集

   ![設定檔啟用切換](assets/setup-experience-platform-profile-enable.png)

**若要啟用結構描述：**

1. 開啟您建立的結構描述，`Luma Web Event Data`

1. 選取&#x200B;**[!UICONTROL 設定檔切換]**&#x200B;以開啟

   ![設定檔切換](assets/setup-experience-platform-profile-schema.png)

1. 選取&#x200B;**[!UICONTROL 此結構描述的資料將在identityMap欄位中包含主要身分。]**

   >[!IMPORTANT]
   >
   >    傳送到Real-Time Customer Profile的每個記錄都需要主要身分。 一般而言，身分欄位會在結構描述中加上標籤。 但是，使用身分對應時，結構描述中不會顯示身分欄位。 此對話方塊是確認您心中有一個主要身分，且您會在傳送資料時，在身分對應中指定該身分。 如您所知，Web SDK會使用身分對應，以Experience Cloud ID (ECID)作為預設主要身分，並以已驗證的ID作為主要身分（若可用）。


1. 選取&#x200B;**[!UICONTROL 啟用]**

   ![設定檔啟用切換](assets/setup-experience-platform-profile-schema-enable.png)

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存更新的結構描述

現在結構描述也針對設定檔啟用。

>[!IMPORTANT]
>
>    為設定檔啟用結構描述後，如果不重設或刪除整個沙箱，就無法停用或刪除它。 此外，此時之後無法從結構描述中移除欄位。
>
>   
> 使用您自己的資料時，我們建議您依照下列順序操作：
> 
> * 首先，將一些資料內嵌到資料集中。
> * 解決資料擷取程式期間發生的任何問題（例如資料驗證或對應問題）。
> * 為設定檔啟用資料集和結構描述
> * 視需要重新內嵌資料


### 驗證設定檔

您可以在Platform介面(或Journey Optimizer介面)中查詢客戶設定檔，確認資料已著陸Real-Time Customer Profile。 顧名思義，設定檔會即時填入，因此不會像資料集中的驗證資料一樣延遲。

首先，您必須產生更多範例資料。 重複本課程中先前步驟以在Luma網站對應至您的標籤屬性時登入。 檢查Platform Web SDK要求，以確定其會傳送包含`lumaCRMId`的資料。

1. 在[Experience Platform](https://experience.adobe.com/platform/)介面中，選取左側導覽中的&#x200B;**[!UICONTROL 客戶]** > **[!UICONTROL 設定檔]**

1. 作為&#x200B;**[!UICONTROL 身分識別名稱空間]**&#x200B;使用`lumaCRMId`
1. 複製並貼上您在Experience Platform Debugger中檢查之呼叫中傳遞的`lumaCRMId`值，此案例中為`b642b4217b34b1e8d3bd915fc65c4452`。

   ![輪廓](assets/experience-platform-validate-dataset-profile.png)

1. 如果`lumaCRMId`的設定檔中有有效值，則主控台中會填入設定檔ID：

   ![輪廓](assets/experience-platform-validate-dataset-profile-set.png)

1. 若要檢視每個ID的完整&#x200B;**[!UICONTROL 客戶設定檔]**，請在主視窗中選取&#x200B;**[!UICONTROL 設定檔識別碼]**。

   >[!NOTE]
   >
   >請注意，您可以選取「設定檔ID」的超連結，或者如果您選取該列，則會開啟右邊的功能表，您可以在其中選取「設定檔ID」超連結
   > ![客戶設定檔](assets/experience-platform-select-profileId.png)

   在這裡，您可以看到連結至`lumaCRMId`的所有身分識別，例如`ECID`。

   ![客戶設定檔](assets/experience-platform-validate-dataset-custProfile.png)

您現在已啟用Experience Platform (和Real-Time CDP適用的Platform Web SDK！ 以及Journey Optimizer！ 和Customer Journey Analytics！)。

## 建立Edge評估的對象

建議使用Real-Time Customer Data Platform和Journey Optimizer的客戶完成此練習。

將Web SDK資料擷取至Adobe Experience Platform時，其他您已擷取至Platform的資料來源可豐富該資料。 例如，當使用者登入Luma網站時，身分圖表會在Experience Platform中建構，而所有其他已啟用設定檔的資料集可能會連結在一起，以建置即時客戶設定檔。 為了實際操作，您將會在Adobe Experience Platform中快速建立另一個資料集，其中包含一些忠誠度資料範例，好讓您可以搭配Real-Time Customer Data Platform和Journey Optimizer使用即時客戶設定檔。 然後，您將根據此資料建置對象。

### 建立忠誠度方案並擷取範例資料

由於您已完成類似的練習，因此會提供簡短的指示。

建立熟客方案：

1. 建立新結構描述
1. 選擇&#x200B;**[!UICONTROL 個別設定檔]**&#x200B;做為[!UICONTROL 基底類別]
1. 命名結構描述`Luma Loyalty Schema`
1. 新增[!UICONTROL 熟客方案詳細資料]欄位群組
1. 新增[!UICONTROL 人口統計詳細資料]欄位群組
1. 選取`Person ID`欄位，並使用`Luma CRM Id` [!UICONTROL 身分名稱空間]將其標示為[!UICONTROL 身分]和[!UICONTROL 主要身分]。
1. 為[!UICONTROL 設定檔]啟用結構描述。 如果您找不到設定檔切換，請嘗試按一下左上方的結構描述名稱。
1. 儲存結構描述

   ![熟客方案](assets/web-channel-loyalty-schema.png)

若要建立資料集並擷取範例資料：

1. 從`Luma Loyalty Schema`建立新的資料集
1. 為資料集命名`Luma Loyalty Dataset`
1. 為[!UICONTROL 設定檔]啟用資料集
1. 下載範例檔案[luma-loyalty-forWeb.json](assets/luma-loyalty-forWeb.json)
1. 將檔案拖放至您的資料集中
1. 確認資料已成功內嵌

   ![熟客方案](assets/web-channel-loyalty-dataset.png)


### 設定Edge上主動的合併原則

所有對象都是使用合併原則建立的。 合併原則會建立設定檔的不同「檢視」、可以包含資料集的子集，並會在不同的資料集貢獻相同的設定檔屬性時指定優先順序。 若要在邊緣進行評估，對象必須使用具有&#x200B;**[!UICONTROL Edge上主動式合併原則]**&#x200B;設定的合併原則。


>[!IMPORTANT]
>
>每個沙箱只能有一個合併原則，**[!UICONTROL Edge上的Active合併原則]**&#x200B;設定


1. 開啟Experience Platform或Journey Optimizer介面，並確定您是在本教學課程使用的開發環境中。
1. 導覽至&#x200B;**[!UICONTROL 客戶]** > **[!UICONTROL 設定檔]** > **[!UICONTROL 合併原則]**&#x200B;頁面
1. 開啟&#x200B;**[!UICONTROL 預設合併原則]** （可能名為`Default Timebased`）
   ![建立客群](assets/merge-policy-open-default.png)
1. 啟用&#x200B;**[!UICONTROL Edge上主動式合併原則]**&#x200B;設定
1. 選取&#x200B;**[!UICONTROL 下一步]**

   ![建立客群](assets/merge-policy-set-active-on-edge.png)
1. 繼續選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續完成工作流程的其他步驟，並選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存您的設定
   ![建立客群](assets/merge-policy-finish.png)

您現在可以建立對象，以便在Edge上評估。

### 建立客群

對象會根據常見特徵將設定檔分組。 建立可在Real-Time CDP或Journey Optimizer中使用的簡單受眾：

1. 在Experience Platform或Journey Optimizer介面中，前往左側導覽中的&#x200B;**[!UICONTROL 客戶]** > **[!UICONTROL 對象]**
1. 選取&#x200B;**[!UICONTROL 建立對象]**
1. 選取&#x200B;**[!UICONTROL 建置規則]**
1. 選取&#x200B;**[!UICONTROL 建立]**

   ![建立客群](assets/web-campaign-create-audience.png)

1. 選取&#x200B;**[!UICONTROL 屬性]**
1. 尋找&#x200B;**[!UICONTROL 忠誠度]** > **[!UICONTROL 階層]**&#x200B;欄位，並將其拖曳至&#x200B;**[!UICONTROL 屬性]**&#x200B;區段
1. 將對象定義為`tier`為`gold`的使用者
1. 為對象命名`Luma Loyalty Rewards – Gold Status`
1. 選取&#x200B;**[!UICONTROL Edge]**&#x200B;做為&#x200B;**[!UICONTROL 評估方法]**
1. 選取&#x200B;**[!UICONTROL 儲存]**

   ![定義客群](assets/web-campaign-define-audience.png)

>[!NOTE]
>
> 由於我們已將預設的合併原則設為&#x200B;**[!UICONTROL Edge上主動式合併原則]**，因此您建立的對象會自動與此合併原則產生關聯。


由於這是非常簡單的對象，因此我們可以使用Edge評估方法。 Edge對象會在邊緣進行評估，因此在網站SDK向Platform Edge Network提出的相同請求中，我們可以評估對象定義，並立即確認使用者是否符合資格。


[下一步： ](setup-analytics.md)

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)上分享
