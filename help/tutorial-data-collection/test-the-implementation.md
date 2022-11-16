---
title: 測試實作
description: 測試實作
exl-id: 66eb1d4e-32eb-45fc-8da4-8d3c04dc3c7a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 2%

---

# 測試實作

現在您已設定網頁且部署了Adobe Experience Platform標籤程式庫，該測試實作了。

1. 在瀏覽器中開啟您的產品頁面。 您可以按一下 _檔案_ then _開啟檔案……_ 或將頁面托管在網頁伺服器上，然後輸入適當的URL。

頁面載入後，您應該會看到下列內容：
![網頁](assets/webpage.png)

這不漂亮，但是它能起到作用。

## Inspect頁面檢視和產品檢視事件

1. 在瀏覽器中開啟開發人員工具，然後按一下網路面板。 重新整理您的頁面。
此時，您應該會看到四個要求：
* product.html — 您的網頁。
* launch-##########-development.js — 您的Launch程式庫。
* interact — 傳送至伺服器的頁面檢視事件。
* interact — 要傳送至伺服器的產品檢視事件。
Inspect每個要求的裝載：
1. 第一個 `interact` 請求時，您應該會看到裝載隨 `eventType` of `web.webpagedetails.pageViews`.
   ![頁面檢視請求檢查](assets/webpage-page-viewed-inspection.png)
1. 第二個 `interact` 請求時，您應該會看到裝載隨 `eventType` of `commerce.productViews`.
   ![產品檢視請求檢查](assets/webpage-product-view-inspection.png)
1. 檢閱其餘傳送的資料，包括產品資訊。

## Inspect開啟購物車並新增至購物車事件

1. 現在按一下**_新增至購物車_**按鈕。

您應會看到兩個其他請求，第一個是 `eventType` of `commerce.productListOpens` （用於開啟新購物車）和第二個 `eventType` of `commerce.productListAdds` （用於將產品新增至購物車）。

## Inspect下載應用程式連結點擊事件

視瀏覽器而定，點選會導覽您離開目前頁面的連結，可能會清除您的網路面板。 因為您想要在離開頁面前檢查發生的連結點擊事件的網路要求，因此您需要設定瀏覽器以保留各頁面的網路記錄。

1. 通過檢查 **_保留日誌_** 核取方塊(Chrome、Safari、Edge)，或按一下齒輪圖示並勾選 **_保留日誌_** 項目(Firefox)。
1. 按一下 **_下載應用程式_** 連結。 你應該再看一次 `interact` 請求會顯示在「網路」面板中。
1. 找出具有 `eventType` of `web.webinteraction.linkClicks`，並檢閱所點按連結的詳細資訊。

## 檢查資料是否進入Adobe Experience Platform資料集

請檢查資料是否安全地送達您建立的Adobe Experience Platform資料集。

1. 導覽至 **[!UICONTROL 資料集]** 在Adobe Experience Platform內檢視。
1. 選取 [資料集](configure-the-server/create-a-dataset.md) 您為本教學課程建立的項目。
您可能需要等候幾分鐘，但很快應該會看到資料已處理並插入資料集的指示。 您也應該看到處理是否成功。 如果失敗了，你就會明白失敗的原因。 失敗通常是因為您傳送的資料不符合架構，而您需要據此調整資料或架構。
   ![資料集擷取](assets/dataset-ingestion.png)

## 使用Adobe Experience Platform Debugger擴充功能

如需進一步了解您的實作在瀏覽器和Adobe伺服器上的行為方式，請查看Adobe Experience Platform Debugger瀏覽器擴充功能！

[Adobe Experience Platform Chrome專用Debugger擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Adobe Experience Platform Firefox專用Debugger擴充功能](https://addons.mozilla.org/zh-TW/firefox/addon/adobe-experience-platform-dbg/)

[下一個： ](summary.md)

>[!NOTE]
>
>感謝您花時間學習資料收集。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)