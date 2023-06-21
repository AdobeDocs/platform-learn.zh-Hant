---
title: 將範例資料匯入 Adobe Experience Platform
description: 瞭解如何使用一些範例資料設定Experience Platform沙箱環境。
role: Developer
feature: API
kt: 7349
thumbnail: 7349.jpg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: da94f4bd-0686-4d6a-a158-506f2e401b4e
source-git-commit: 60f509ef55ce121f572466a8f13953dba982a0ce
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 5%

---

# 將範例資料匯入 Adobe Experience Platform

瞭解如何設定包含範例資料的 Experience Platform 沙箱環境。您可以使用 Postman 集合來建立欄位群組、綱要、資料集，然後將範例資料匯入 Experience Platform。

## 範例資料使用案例

Experience Platform業務使用者通常必須完成一系列步驟，包括識別欄位群組、建立結構描述、準備資料、建立資料集，然後擷取資料，然後才能探索Experience Platform提供的行銷功能。 本教學課程會自動執行部分步驟，讓您儘快將資料放入Platform沙箱。

本教學課程著重於名為Luma的虛擬零售品牌。 他們投資於Adobe Experience Platform，以將忠誠度、CRM、產品目錄和離線購買資料結合到即時客戶設定檔中，並啟用這些設定檔，以將他們的行銷提升到新的境界。 我們已產生Luma的範例資料，在本教學課程的其餘部分，您會將此資料匯入您的其中一個Experience Platform沙箱環境中。

>[!NOTE]
>
>本教學課程的最終結果為沙箱，其中包含與類似的資料 [資料架構師和資料工程師專用Adobe Experience Platform快速入門教學課程](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html). 2023年4月更新以支援 [Journey Optimizer挑戰](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=zh-Hant). 2023年6月更新，將驗證方法切換至OAuth。


## 先決條件

* 您有權存取Experience PlatformAPI並知道如何驗證。 如果沒有，請檢閱此 [教學課程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=zh-Hant).
* 您可以存取Experience Platform開發沙箱。
* 您知道您的Experience Platform租使用者ID。 您可以透過進行驗證來取得 [API要求](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#know-your-tenant_id)
或是在您登入Platform帳戶時，從URL擷取資訊。 例如，在以下URL中，租使用者是&quot;`techmarketingdemos`&quot; `https://experience.adobe.com/#/@techmarketingdemos/sname:prod/platform/home`.

## 使用 [!DNL Postman] {#postman}

### 設定環境變數

在依照這些步驟操作之前，請確定您已下載 [Postman](https://www.postman.com/downloads/) 應用程式。 我們開始吧！

1. 下載 [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) 檔案，其中包含本教學課程所需的所有檔案。

   >[!NOTE]
   >
   >包含在「 」中的使用者資料 [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) 檔案是虛構的，僅供示範使用。

1. 從下載資料夾中，將`platform-utils-main.zip`檔案移至您電腦的所需位置，然後加以解壓縮。
1. 在 `luma-data` 資料夾，開啟所有 `json` 文字編輯器中的檔案並取代所有實體 `_yourTenantId` 擁有您自己的租使用者id，前面加上底線。
1. 開啟 `luma-offline-purchases.json`， `luma-inventory-events.json`、和 `luma-web-events.json` 並更新所有時間戳記，讓事件在上個月發生(例如，搜尋 `"timestamp":"2022-11` 和取代年和月)
1. 請記下解壓縮資料夾的位置，因為您稍後在設定 `FILE_PATH` [!DNL Postman] 環境變數：

   >[!NOTE]
   > 若要取得Mac上的檔案路徑，請導覽至 `platform-utils-main` 資料夾，以滑鼠右鍵按一下資料夾並選取 **取得資訊** 選項。
   >
   > ![Mac檔案路徑](../assets/data-generator/images/mac-file-path.png)

   >[!NOTE]
   > 若要在視窗中取得檔案路徑，請按一下以開啟所需資料夾的位置，然後在位址列中的路徑右側按一下滑鼠右鍵。 複製地址以取得檔案路徑。
   > 
   > ![Windows檔案路徑](../assets/data-generator/images/windows-file-path.png)

1. 開啟 [!DNL Postman] 並從建立工作區 **工作區** 下拉式功能表：\
   ![建立工作區](../assets/data-generator/images/create-workspace.png)
1. 輸入 **名稱** 和選填 **摘要** ，然後按一下 **建立工作區**. [!DNL Postman] 會在您建立新工作區時切換至該工作區。
   ![儲存工作區](../assets/data-generator/images/save-workspace.png)
1. 現在調整一些設定以執行 [!DNL Postman] 此工作區中的集合。 在的標題中 [!DNL Postman]，按一下齒輪圖示並選取 **設定** 以開啟設定強制回應視窗。 您也可以使用鍵盤快速鍵(CMD/CTRL + ，)來開啟強制回應視窗。
1. 在 `General` 標籤，將請求逾時（以毫秒為單位）更新為 `5000 ms` 並啟用 `allow reading file outside this directory`
   ![設定](../assets/data-generator/images/settings.png)

   >[!NOTE]
   > 如果檔案是從工作目錄內載入，如果相同的檔案儲存在其他裝置上，它將會順利地在裝置之間執行。 不過，如果您想要從工作目錄外部執行檔案，則必須開啟設定以表示相同的目的。 若您的 `FILE_PATH` 與 [!DNL Postman]的工作目錄路徑，則應啟用此選項。

1. 關閉 **設定** 面板。
1. 選取 **環境** 然後選取 **匯入**：
   ![環境匯入](../assets/data-generator/images/env-import.png)
1. 匯入下載的json環境檔案， `DataInExperiencePlatform.postman_environment`
1. 在Postman的右上角下拉式清單中選取您的環境，然後按一下眼睛圖示以檢視環境變數：
   ![環境選擇](../assets/data-generator/images/env-selection.png)

1. 請確定已填入下列環境變數。 若要瞭解如何取得環境變數的值，請檢視 [驗證Experience Platform API](/help/platform/authentication/platform-api-authentication.md) 逐步指示的教學課程。

   * `CLIENT_SECRET`
   * `API_KEY`—`Client ID` 在Adobe Developer Console中
   * `SCOPES`
   * `TECHNICAL_ACCOUNT_ID`
   * `IMS`
   * `IMS_ORG`—`Organization ID` 在Adobe Developer Console中
   * `SANDBOX_NAME`
   * `TENANT_ID` — 請務必以底線開頭，例如 `_techmarketingdemos`
   * `CONTAINER_ID`
   * `platform_end_point`
   * `FILE_PATH` — 使用您解壓縮的本機資料夾路徑 `platform-utils-main.zip` 檔案。 請確定其中包含資料夾名稱，例如 `/Users/dwright/Desktop/platform-utils-main`

1. **儲存** 更新的環境

### 匯入Postman集合

接下來，您需要將集合匯入Postman。

1. 選取 **集合** 然後選擇匯入選項：

   ![集合](../assets/data-generator/images/collections.png)

1. 匯入下列集合：

   * `0-Authentication.postman_collection.json`
   * `1-Luma-Loyalty-Data.postman_collection.json`
   * `2-Luma-CRM-Data.postman_collection.json`
   * `3-Luma-Product-Catalog.postman_collection.json`
   * `4-Luma-Offline-Purchase-Events.postman_collection.json`
   * `5-Luma-Product-Inventory-Events.postman_collection.json`
   * `6-Luma-Test-Profiles.postman_collection.json`
   * `7-Luma-Web-Events.postman_collection.json`

   ![集合匯入](../assets/data-generator/images/collection-files.png)

### 驗證

接下來，您需要驗證並產生使用者權杖。 請注意，本教學課程中使用的代號產生方法僅適用於非生產用途。 本機簽署會從協力廠商主機載入JavaScript程式庫，而遠端簽署會將私密金鑰傳送至Adobe擁有且運作的Web服務。 雖然Adobe不會儲存此私密金鑰，但生產金鑰絕不可與任何人共用。

1. 開啟 `0-Authentication` 集合，選取 `OAuth: Request Access Token` 要求，然後按一下 `SEND` 驗證及取得存取權杖。

   ![集合匯入](../assets/data-generator/images/authentication.png)

1. 檢閱環境變數，並注意 `ACCESS_TOKEN` 現已填入。

### 匯入資料

現在您可以準備資料並將其匯入您的Platform沙箱。 您匯入的Postman系列將完成所有繁重的工作！

1. 開啟 `1-Luma-Loyalty-Data` 集合併按一下 **執行** 在「概述」標籤上啟動「收集執行器」。

   ![集合匯入](../assets/data-generator/images/loyalty.png)

1. 在集合執行器視窗中，確定從下拉式選單中選取環境，更新 **延遲** 至 `4000ms`，檢查 **儲存回應** 選項，並確認執行順序正確。 按一下 **執行Luma忠誠度資料** 按鈕

   ![集合匯入](../assets/data-generator/images/loyalty-run.png)

   >[!NOTE]
   >
   >**1-Luma-Loyalty-Data** 建立客戶忠誠度資料的結構描述。 此結構描述是以XDM個別設定檔類別、標準欄位群組，以及自訂欄位群組和資料型別為基礎。 集合會使用結構描述建立資料集，並將範例客戶忠誠度資料上傳至Adobe Experience Platform。

   >[!NOTE]
   >
   >如果在Postman收集執行程式期間，有任何收集請求失敗，請停止執行並逐一執行收集請求。

1. 如果一切順利，則所有請求 `Luma-Loyalty-Data` 集合應該會通過。

   ![忠誠度結果](../assets/data-generator/images/loyalty-result.png)

1. 現在，讓我們登入 [Adobe Experience Platform介面](https://platform.adobe.com/) 和導覽至資料集。
1. 開啟 `Luma Loyalty Dataset` 在資料集活動視窗下，您可以檢視成功擷取1000筆記錄的批次執行。 您也可以按一下預覽資料集選項，驗證擷取的記錄。 您可能需要等候幾分鐘以確認1000 [!UICONTROL 新設定檔片段] 「 」已建立。
   ![熟客資料集](../assets/data-generator/images/loyalty-dataset.png)
1. 重複步驟1-3以執行其他集合：
   * `2-Luma-CRM-Data.postman_collection.json` 為客戶的CRM資料建立方案和填入的資料集。 此結構描述以XDM個人設定檔類別為基礎，其中包含人口統計詳細資料、個人聯絡詳細資料、偏好設定詳細資料和自訂身分欄位群組。
   * `3-Luma-Product-Catalog.postman_collection.json` 建立結構描述和填入的產品目錄資訊資料集。 此結構描述是以自訂產品目錄類別為基礎，並使用自訂產品目錄欄位群組。
   * `4-Luma-Offline-Purchase-Events.postman_collection.json` 為客戶離線購買事件資料建立結構描述和填入的資料集。 此結構描述以XDM ExperienceEvent類別為基礎，並包含自訂身分和商務詳細資訊欄位群組。
   * `5-Luma-Product-Inventory-Events.postman_collection.json` 會為與進貨及無庫存產品相關的事件建立方案和填入的資料集。 此結構描述是以自訂業務事件類別和自訂欄位群組為基礎。
   * `6-Luma-Test-Profiles.postman_collection.json` 建立結構描述，並填入含有測試設定檔的資料集，以便在Adobe Journey Optimizer中使用
   * `7-Luma-Web-Events.postman_collection.json` 使用簡單的歷史Web資料建立結構描述和填入的資料集。


## 驗證

範例資料的設計目的，是為了在執行集合時，建立結合來自多個系統資料的Real-Time Customer Profiles。 忠誠度、CRM和離線購買資料集的第一筆記錄就是很好的例子。 查詢該設定檔以確認資料已擷取。 在 [Adobe Experience Platform介面](https://experience.adobe.com/platform/)：

1. 前往 **[!UICONTROL 設定檔]** > **[!UICONTROL 瀏覽]**
1. 選取 `Luma Loyalty Id` 作為 **[!UICONTROL 身分名稱空間]**
1. 搜尋 `5625458` 作為 **[!UICONTROL 身分值]**
1. 開啟 `Daniel Wright` 設定檔

>[!TIP]
>
>如果您沒有看到設定檔，請檢查 [!UICONTROL 資料集] 頁面，確認已成功建立及擷取所有資料集。 如果一切正常，請等候15分鐘，然後檢視檢視器中是否有設定檔。  如果資料擷取發生問題，請檢查錯誤訊息以嘗試找出問題。 您也可以嘗試在 [!UICONTROL 資料集] 頁面，並拖放json資料檔案以重新內嵌資料。


![開啟設定檔](../assets/data-generator/images/validation-profile-open.png)

瀏覽「 」中的資料 **[!UICONTROL 屬性]** 和 **[!UICONTROL 事件]** 標籤中，您應該會看到設定檔包含來自各種資料檔案的資料：
![離線購買事件檔案中的事件資料](../assets/data-generator/images/validation-profile-events.png)

## 後續步驟

如果您想瞭解Adobe Journey Optimizer，此沙箱包含您需要採取的 [Journey Optimizer挑戰](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=zh-Hant)

如果您想瞭解合併原則、資料控管、查詢服務和區段產生器，請跳轉到 [資料架構師和資料工程師快速入門教學課程中的第11課](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-merge-policies.html?lang=en). 本其他教學課程的先前課程會讓您手動建立這些Postman集合剛才填入的所有內容 — 開門見山吧！

如果您想要建置範例Web SDK實作以連結至此沙箱，請前往
[使用Web SDK教學課程實作Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hant). 設定Web SDK教學課程的「初始設定」、「標籤設定」和「設定Experience Platform」課程後，使用中的前十個電子郵件地址登入Luma網站 `luma-crm.json` 使用密碼的檔案 `test` 以檢視設定檔片段與本教學課程中上傳的資料合併。

如果您想要建立範例行動SDK實作以連結至此沙箱，請前往
[在行動應用程式教學課程中實作Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html). 設定Web SDK教學課程的「初始設定」、「應用程式實作」和「Experience Platform」課程後，使用中的第一個電子郵件地址登入Luma網站 `luma-crm.json` 檔案以瞭解個人資料片段如何與本教學課程中上傳的資料合併。

## 重設沙箱環境 {#reset-sandbox}

重設非生產沙箱會刪除與該沙箱關聯的所有資源（結構描述、資料集等），同時維護沙箱的名稱和關聯的許可權。 此「乾淨」沙箱可繼續供擁有存取權的使用者以相同名稱使用。

請依照步驟操作 [此處](https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=en#reset-a-sandbox) 以重設沙箱環境。
