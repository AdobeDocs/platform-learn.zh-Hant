---
title: 透過Platform Web SDK將資料串流至Adobe Experience Platform
description: 瞭解如何使用Web SDK將網頁資料串流到Adobe Experience Platform。 本課程是「使用 Web SDK 實施 Adob​​e Experience Cloud」教學課程的一部分。
jira: KT-15407
exl-id: 4d749ffa-e1c0-4498-9b12-12949807b369
source-git-commit: c5318809bfd475463bac3c05d4f35138fb2d7f28
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 5%

---

# 使用Web SDK串流資料以Experience Platform

了解如何使用 Platform Web SDK 將 Web 資料串流傳輸至 Adob&#x200B;&#x200B;e Experience Platform。

Experience Platform是所有新Experience Cloud應用程式的骨幹，例如Adobe Real-time Customer Data Platform、Adobe Customer Journey Analytics和Adobe Journey Optimizer。 這些應用程式在設計上使用Platform Web SDK作為收集網頁資料的最佳方法。

![Web SDK和Adobe Experience Platform圖表](assets/dc-websdk-aep.png)

Experience Platform會使用您先前建立的相同XDM結構描述，從Luma網站擷取事件資料。 當該資料傳送至PlatformEdge Network時，資料流設定可以將其轉送至Experience Platform。

## 學習目標

在本課程結束時，您將能夠：

* 在Adobe Experience Platform中建立資料集
* 設定資料流以傳送Web SDK資料至Adobe Experience Platform
* 為即時客戶個人檔案啟用串流網頁資料
* 驗證資料已著陸Platform資料集和即時客戶設定檔中

## 先決條件

若要完成本課程，您必須先：

* 擁有Adobe Experience Platform應用程式的存取權，例如Real-time Customer Data Platform、Journey Optimizer或Customer Journey Analytics
* 完成本教學課程之初始設定和標籤設定區段中先前的課程。


## 建立資料集

所有成功內嵌至Adobe Experience Platform的資料都會以資料集的形式保留在資料湖中。 A [資料集](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/overview) 是用於資料集合的儲存和管理結構，通常是包含結構（欄）和欄位（列）的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。

讓我們為您的Luma Web事件資料設定資料集：


1. 前往 [Experience Platform介面](https://experience.adobe.com/platform/)
1. 確認您是在本教學課程使用的開發沙箱中
1. 開啟 **[!UICONTROL 資料管理>資料集]** 從左側導覽
1. 選取 **[!UICONTROL 建立資料集]**

   ![建立結構描述](assets/experience-platform-create-dataset.png)

1. 選取 **[!UICONTROL 從結構描述建立資料集]** 選項

   ![從結構描述建立資料集](assets/experience-platform-create-dataset-schema.png)

1. 選取 `Luma Web Event Data` 在中建立的綱要 [先前的課程](configure-schemas.md) 然後選取 **[!UICONTROL 下一個]**

   ![資料集，選取結構描述](assets/experience-platform-create-dataset-schema-selection.png)

1. 提供 **[!UICONTROL 名稱]** 和選填 **[!UICONTROL 說明]** 用於資料集。 在本練習中，請使用 `Luma Web Event Data`，然後選取 **[!UICONTROL 完成]**

   ![資料集名稱 ](assets/experience-platform-create-dataset-schema-name.png)

資料集現在已設定為開始從Platform Web SDK實作收集資料。

## 設定資料串流

現在您可以設定 [!UICONTROL 資料流] 以傳送資料至 [!UICONTROL Adobe Experience Platform]. 資料流是標籤屬性、平台Edge Network和Experience Platform資料集之間的連結。

1. 開啟 [資料彙集](https://experience.adobe.com/#/data-collection){target="blank"} 介面
1. 選取 **[!UICONTROL 資料串流]** 從左側導覽
1. 開啟您在中建立的資料流 [設定資料串流](configure-datastream.md) 課程， `Luma Web SDK`

   ![選取Luma Web SDK資料流](assets/datastream-luma-web-sdk-development.png)

1. 選取 **[!UICONTROL 新增服務]**
   ![將服務新增至資料流](assets/experience-platform-addService.png)
1. 選取 **[!UICONTROL Adobe Experience Platform]** 作為 **[!UICONTROL 服務]**
1. 選取 `Luma Web Event Data` 作為 **[!UICONTROL 事件資料集]**

1. 選取「**[!UICONTROL 儲存]**」。

   ![資料流設定](assets/experience-platform-datastream-config.png)

當您在 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 對應至您的標籤屬性，資料會在Experience Platform中填入資料集！

## 驗證資料集

此步驟對於確保資料已抵達資料集至關重要。 驗證傳送至資料集的資料有兩個方面。

* 使用進行驗證 [!UICONTROL Experience Platform偵錯工具]
* 使用進行驗證 [!UICONTROL 預覽資料集]
* 使用進行驗證 [!UICONTROL 查詢服務]

### Experience Platform Debugger

這些步驟與您在中的操作大致相同 [偵錯工具課程](validate-with-debugger.md). 不過，由於資料只有在資料流中啟用後才會傳送至Platform，因此您必須產生更多範例資料：

1. 開啟 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html) 並選取 [!UICONTROL Experience Platform偵錯工具] 擴充功能圖示

1. 設定Debugger將標籤屬性對應至 *您的* 開發環境，如 [使用Debugger進行驗證](validate-with-debugger.md) 課程

   ![Debugger 中顯示的 Launch 開發環境](assets/experience-platform-debugger-dev.png)

1. 使用 `test@adobe.com`/`test` 憑證登入 Luma 網站

1. 返回 [Luma 首頁](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 在Debugger顯示的Platform Web SDK網路信標中，選取「事件」列以在快顯視窗中展開詳細資料

   ![Debugger中的Web SDK](assets/experience-platform-debugger-dev-eventType.png)

1. 在快顯視窗中搜尋「identityMap」。 您應該會在這裡看到lumaCrmId包含authenticatedState、id和primary的三個索引鍵
   ![Debugger中的Web SDK](assets/experience-platform-debugger-dev-idMap.png)

現在，資料應填入 `Luma Web Event Data` 資料集並準備好進行「預覽資料集」驗證。

### 預覽資料集

若要確認資料已著陸Platform的資料湖，快速選項是使用 **[!UICONTROL 預覽資料集]** 功能。 Web SDK資料會以微批次處理至資料湖，並定期在平台介面中重新整理。 您可能需要10到15分鐘的時間才能看到您產生的資料。

1. 在 [Experience Platform](https://experience.adobe.com/platform/) 介面，選取 **[!UICONTROL 資料管理>資料集]** 在左側導覽以開啟 **[!UICONTROL 資料集]** 儀表板。

   控制面板會列出貴組織的所有可用資料集。 系統會顯示每個列出資料集的詳細資訊，包括其名稱、資料集所遵守的結構描述，以及最新擷取執行的狀態。

1. 選取您的 `Luma Web Event Data` 資料集，以開啟其 **[!UICONTROL 資料集活動]** 畫面。

   ![資料集Luma Web事件](assets/experience-platform-dataset-validation-lumaSDK.png)

   活動畫麵包含以視覺效果呈現訊息使用率的圖表，以及成功和失敗批次的清單。

1. 從 **[!UICONTROL 資料集活動]** 熒幕，選取 **[!UICONTROL 預覽資料集]** 靠近熒幕右上角，可預覽最多100列資料。 如果資料集空白，則會停用預覽連結。

   ![資料集預覽](assets/experience-platform-dataset-preview.png)

   在預覽視窗中，資料集的結構描述階層檢視會顯示在右側。

   ![資料集預覽1](assets/experience-platform-dataset-preview-1.png)

>[!INFO]
>
>Adobe Experience Platform的查詢服務是驗證湖中資料的更強大方法，但不在本教學課程的討論範圍內。 如需詳細資訊，請參閱 [探索資料](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/queries/explore-data) 位於Platform教學課程區段。


## 為即時客戶個人檔案啟用資料集和結構描述

下一步是為即時客戶個人檔案啟用資料集和結構。 從Web SDK串流的資料會是流入Platform的眾多資料來源之一，而您想要將網頁資料與其他資料來源結合，以建置360度客戶設定檔。 若要深入瞭解即時客戶個人檔案，請觀看此短片：

>[!VIDEO](https://video.tv.adobe.com/v/27251?learn=on&captions=eng)

>[!CAUTION]
>
>使用您自己的網站和資料時，建議在啟用資料以用於即時客戶個人檔案之前，先對資料進行更強大的驗證。


**若要啟用資料集：**

1. 開啟您建立的資料集， `Luma Web Event Data`

1. 選取 **[!UICONTROL 設定檔切換]** 以開啟

   ![設定檔切換](assets/setup-experience-platform-profile.png)

1. 確認您要 **[!UICONTROL 啟用]** 資料集

   ![設定檔啟用切換](assets/setup-experience-platform-profile-enable.png)

**啟用綱要：**

1. 開啟您建立的結構描述， `Luma Web Event Data`

1. 選取 **[!UICONTROL 設定檔切換]** 以開啟

   ![設定檔切換](assets/setup-experience-platform-profile-schema.png)

1. 選取 **[!UICONTROL 此結構描述的資料將在identityMap欄位中包含主要身分。]**

   >[!IMPORTANT]
   >
   >    傳送到Real-Time Customer Profile的每個記錄都需要主要身分。 一般而言，身分欄位會在結構描述中加上標籤。 但是，使用身分對應時，結構描述中不會顯示身分欄位。 此對話方塊是確認您心中有一個主要身分，且您會在傳送資料時，在身分對應中指定該身分。 如您所知，Web SDK使用身分對應，而Experience CloudID (ECID)是預設的主要身分。


1. 選取 **[!UICONTROL 啟用]**

   ![設定檔啟用切換](assets/setup-experience-platform-profile-schema-enable.png)

1. 選取 **[!UICONTROL 儲存]** 儲存更新的結構描述

現在結構描述也針對設定檔啟用。

>[!IMPORTANT]
>
>    為設定檔啟用結構描述後，就無法停用或刪除它。 此外，此時之後無法從結構描述中移除欄位。 當您在生產環境中使用自己的資料時，請務必牢記這些含意。 在本教學課程中，您應該使用開發沙箱，您可以隨時將其刪除。
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

首先，您必須產生更多範例資料。 重複本課程中先前步驟以在Luma網站對應至您的標籤屬性時登入。 Inspect Platform Web SDK請求以確定其傳送資料時包含 `lumaCRMId`.

1. 在 [Experience Platform](https://experience.adobe.com/platform/) 介面，選取 **[!UICONTROL 設定檔]** 在左側導覽列中

1. 作為 **[!UICONTROL 身分名稱空間]** 使用 `lumaCRMId`
1. 複製並貼上 `lumaCRMId` 已在您在Experience Platform Debugger中檢查的呼叫中傳遞，此案例中為 `112ca06ed53d3db37e4cea49cc45b71e`.

   ![個人資料](assets/experience-platform-validate-dataset-profile.png)

1. 如果設定檔中有有效的值， `lumaCRMId`，設定檔ID會填入主控台中：

   ![個人資料](assets/experience-platform-validate-dataset-profile-set.png)

1. 若要檢視完整的 **[!UICONTROL 客戶設定檔]** 針對每個ID，選取 **[!UICONTROL 設定檔ID]** 在主視窗中。

   >[!NOTE]
   >
   >請注意，您可以選取「設定檔ID」的超連結，或者如果您選取該列，則會開啟右邊的功能表，您可以在其中選取「設定檔ID」超連結
   > ![客戶設定檔](assets/experience-platform-select-profileId.png)

   在這裡，您可以看到連結至的所有身分識別 `lumaCRMId`，例如 `ECID`.

   ![客戶設定檔](assets/experience-platform-validate-dataset-custProfile.png)

您現已啟用適用於Experience Platform的Platform Web SDK (以及Real-Time CDP！ 以及Journey Optimizer！ 和Customer Journey Analytics！)。

### 建立忠誠度方案並擷取範例資料

Real-time Customer Data Platform和Journey Optimizer的客戶可望完成此練習。

將Web SDK資料擷取至Adobe Experience Platform後，您即可將資料擷取至Platform的其他資料來源加以擴充。 例如，當使用者登入Luma網站時，身分圖表會在Experience Platform中建構，而所有其他已啟用設定檔的資料集可能會連結在一起，以建置即時客戶設定檔。 若要實際瞭解此情況，請在Adobe Experience Platform中快速建立另一個資料集，其中包含一些忠誠度資料範例，以便您可以搭配Real-time Customer Data Platform和Journey Optimizer使用即時客戶設定檔。 由於您已完成類似的練習，因此會提供簡短的指示。

建立熟客方案：

1. 建立新結構描述
1. 選擇 **[!UICONTROL 個別設定檔]** 作為 [!UICONTROL 基底類別]
1. 為結構命名 `Luma Loyalty Schema`
1. 新增 [!UICONTROL 熟客方案細節] 欄位群組
1. 新增 [!UICONTROL 人口統計細節] 欄位群組
1. 選取 `Person ID` 欄位並標籤為 [!UICONTROL 身分] 和 [!UICONTROL 主要身分] 使用 `Luma CRM Id` [!UICONTROL 身分名稱空間].
1. 為以下專案啟用結構描述： [!UICONTROL 個人資料]

   ![熟客方案](assets/web-channel-loyalty-schema.png)

若要建立資料集並擷取範例資料：

1. 從建立新資料集 `Luma Loyalty Schema`
1. 為資料集命名 `Luma Loyalty Dataset`
1. 為以下專案啟用資料集 [!UICONTROL 個人資料]
1. 下載範例檔案 [luma-loyalty-forWeb.json](assets/luma-loyalty-forWeb.json)
1. 將檔案拖放至您的資料集中
1. 確認資料已成功內嵌

   ![熟客方案](assets/web-channel-loyalty-dataset.png)

### 建立對象

對象會根據常見特徵將設定檔分組。 建立可在網路行銷活動中使用的快速受眾：

1. 在Experience Platform介面中，前往 **[!UICONTROL 受眾]** 在左側導覽列中
1. 選取 **[!UICONTROL 建立對象]**
1. 選取 **[!UICONTROL 建置規則]**
1. 選取 **[!UICONTROL 建立]**

   ![建立受眾](assets/web-campaign-create-audience.png)

1. 選取 **[!UICONTROL 屬性]**
1. 尋找 **[!UICONTROL 忠誠度]** > **[!UICONTROL 階層]** 欄位並將其拖曳至 **[!UICONTROL 屬性]** 區段
1. 將對象定義為使用者，其 `tier` 是 `gold`
1. 為對象命名 `Luma Loyalty Rewards – Gold Status`
1. 選取 **[!UICONTROL Edge]** 作為 **[!UICONTROL 評估方法]**
1. 選取 **[!UICONTROL 儲存]**

   ![定義對象](assets/web-campaign-define-audience.png)

由於這是非常簡單的對象，因此我們可以使用Edge評估方法。 Edge對象會在Edge進行評估，因此在Web SDK對平台Edge Network發出的相同請求中，我們可以評估對象定義，並立即確認使用者是否符合條件。


[下一步： ](setup-analytics.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
