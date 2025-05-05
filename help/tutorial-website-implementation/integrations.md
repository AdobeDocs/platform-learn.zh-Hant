---
title: 實作Experience Cloud與標籤的整合
description: 瞭解如何驗證 Adobe Experience Cloud 實施中的受眾、A4T 和客戶屬性整合。本課程屬於「在網站中實作Experience Cloud」教學課程的一部分。
exl-id: 1d02efce-a50a-4f4d-a0cf-eb8275cf0faa
source-git-commit: 2182441d992aec0602d0955d78aa85407bd770c9
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 85%

---

# Experience Cloud 整合

在本課程中，將檢閱您剛剛所實施解決方案之間的主要整合。好消息是完成先前的課程後，您已實施整合的程式碼部分！除了閱讀和驗證以外，您不需要在本課程中執行任何其他工作。

## 學習目標

在本課程結束時，您將能夠：

1. 說明受眾共用、Analytics for Target (A4T) 和客戶屬性整合的基本使用案例
1. 驗證這些整合的基本用戶端實施環節

## 必要條件

您應先完成本教學課程中先前的所有課程，然後再依照本課程中的指示操作。

>[!NOTE]
>
>若要完整使用這些整合，有許多必要的使用者許可權需求、帳戶設定和布建步驟，這些不在本教學課程的討論範圍內。 如果您已在目前的 Experience Cloud 實施中使用這些整合，您應考量下列事項：
>
>* 檢視[核心服務整合](https://experienceleague.adobe.com/zh-hant/docs/core-services/interface/services/getting-started)的完整需求
>* 檢視 [Analytics for Target 整合](https://experienceleague.adobe.com/zh-hant/docs/target/using/integrate/a4t/before-implement)的完整需求

## 受眾

[受眾](https://experienceleague.adobe.com/zh-hant/docs/core-services/interface/services/audiences/overview)是 People 核心服務的一部分，可讓您在不同解決方案之間共用受眾。例如，您可以在 Audience Manager 中建立受眾，並透過 Target 使用該受眾來提供個人化內容。

實施 A4T (您已完成) 的主要需求如下：

1. 實施 Adobe Experience Platform Identity Service
1. 實施 Audience Manager
1. 實施您想要收到或建立受眾的其他解決方案，例如 Target 和 Analytics

### 驗證受眾整合

驗證受眾整合的最佳方式是實際建立受眾，將其共用給其他解決方案，然後在其他解決方案中充分使用 (例如，確認符合 AAM 區段資格的訪客，可符合目標鎖定為該區段的 Target 活動之資格)。不過，這不在本教學課程的討論範圍內。

這些驗證步驟將專注於用戶端實施中可見的關鍵部分：訪客 ID。

1. 開啟 [Luma 網站](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 如[先前的課程](switch-environments.md)所述，確認Debugger將標籤屬性對應至&#x200B;*您的*&#x200B;開發環境

   ![Debugger中顯示的標籤開發環境](images/switchEnvironments-debuggerOnWeRetail.png)

1. 前往 Debugger 的「網路」標籤

1. 按一下「**[!UICONTROL 清除所有要求]**」進行清除

1. 重新載入 Luma 頁面，確認 Debugger 中有顯示 Target 和 Analytics 請求

1. 再次重新載入 Luma 頁面

1. 您現在應該會在 Debugger 的「網路」標籤中看到四個請求：兩個針對 Target，兩個針對 Analytics

1. 查看標示為「Experience Cloud 訪客 ID」的列。所有解決方案的所有請求中的 ID 應一律相同。

   ![確認相符的 SDID](images/integrations-matchingECIDs.png)

1. 每個訪客的 ID 皆不重複，您可以請同事執行這些步驟以進行確認。

## Analytics for Target (A4T)

[Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=zh-Hant) 整合可讓您將 Analytics 資料當成 Target 中報告量度的來源。

實施 A4T (您已完成) 的主要需求如下：

1. 實施 Adobe Experience Platform Identity Service
1. 在 Analytics 頁面檢視信標之前引發 Target 頁面載入請求

A4T 的運作方式是將從 Target 傳至 Analytics 的伺服器端請求與 Analytics 頁面檢視信標拼接在一起 (我們稱為「點擊拼接」)。點擊拼接請求提供活動 (或遞增 Target 型目標量度) 的 Target 請求中，有一個參數與 Analytics 頁面檢視信標中的參數相符。此參數稱為增補資料 ID (SDID)。

### 驗證 A4T 實施

驗證 A4T 整合的最佳方式，是實際使用 A4T 建置 Target 活動並驗證報表資料，不過這不在本教學課程的討論範圍內。本教學課程將說明如何確認解決方案呼叫之間的增補資料 ID 彼此相符。

**驗證 SDID 的方式**

1. 開啟 [Luma 網站](https://luma.enablementadobe.com/content/luma/us/en.html)

1. 如[先前的課程](switch-environments.md)所述，確認Debugger將標籤屬性對應至&#x200B;*您的*&#x200B;開發環境

   ![Debugger中顯示的標籤開發環境](images/switchEnvironments-debuggerOnWeRetail.png)

1. 前往 Debugger 的「網路」標籤

1. 按一下「**[!UICONTROL 清除所有要求]**」進行清除

1. 重新載入 Luma 頁面，確認 Debugger 中有顯示 Target 和 Analytics 請求

1. 再次重新載入 Luma 頁面

1. 您現在應該會在 Debugger 的「網路」標籤中看到四個請求：兩個針對 Target，兩個針對 Analytics

1. 查看標示為「Supplemental Data ID」的這一列。來自第一個頁面載入的 ID 在 Target 與 Analytics 之間應彼此相符。來自第二個頁面載入的 ID 也應彼此相符，但與來自第一個頁面載入的 ID 不同。

   ![確認相符的 SDID](images/integrations-matchingSDIDs.png)

如果您在屬於 A4T 活動一部分的頁面載入範圍內 (不包括單頁應用程式) 提出其他 Target 請求，請將其命名為不重複名稱 (不是 target-global-mbox)，這樣其 SDID 就會繼續與初始 Target 和 Analytics 請求相同。

## 客戶屬性

[客戶屬性](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=zh-Hant??lang=zh-Hant)是 People 核心服務的一部分，可讓您從客戶關係管理 (CRM) 資料庫上傳資料，以及在 Adobe Analytics 和 Adobe Target 中運用資料。

實施客戶屬性 (您已完成) 的主要需求如下：

1. 實施 Adobe Experience Platform Identity Service
1. 在&#x200B;*之前，透過ID服務設定客戶ID* Target和Analytics引發其要求（您已使用標籤中的規則排序功能完成）

### 驗證客戶屬性實施

在先前的課程中，您已驗證客戶 ID 已同時傳遞至 Identity Service 和 Target。您也可以驗證 Analytics 點擊中的客戶 ID。目前客戶 ID 是少數不會顯示於 Experience Cloud Debugger 中的參數之一，因此您需使用瀏覽器的 JavaScript Console 進行檢視。

1. 開啟 Luma 網站
1. 開啟瀏覽器的開發人員工具
1. 前往「網路」標籤
1. 在篩選欄位中輸入 `b/ss`，即可限制您看到的 Adobe Analytics 請求內容

   ![開啟「開發人員工具」並篩選「網路」標籤，僅顯示 Analytics 請求](images/aam-openTheJSConsole.png)

1. 按一下網站右上角的&#x200B;**[!UICONTROL 登入]**&#x200B;連結

   ![按一下右上角的[登入]](images/idservice-loginNav.png)

1. 使用者名稱請輸入 `test@adobe.com`
1. 密碼請輸入 `test`
1. 按一下&#x200B;**[!UICONTROL 登入]**&#x200B;按鈕

   ![輸入認證並按一下登入](images/idservice-login.png)

1. 此時您應會返回首頁，同時也會觸發您可在開發人員工具中看到的信標。如果您進入帳戶資訊頁面，請按一下 WE.RETAIL 標誌以返回首頁。
1. 按一下請求，然後選取「標頭」標籤
1. 向下捲動，直到您看到某些巢狀參數為止
   1. cid：請求中客戶 ID 部分的標準分隔符號
   1. crm_id：這是您在 Identity Service 課程中指定的自訂整合程式碼
   1. id：來自您 `Email (Hashed)` 資料元素的客戶 ID 值
   1. as：驗證狀態，「1」表示已登入

   ![Analytics 客戶 ID 驗證](images/integrations-analyticsCustomerIDValidation.png)

[下堂課「Publish您的屬性」>](publish.md)
