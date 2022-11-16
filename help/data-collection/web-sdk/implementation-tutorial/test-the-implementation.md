---
title: 測試實作
description: 測試實作
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: e2213c23-d395-4c57-8c6c-0319cd0fb0ac
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# 測試實作

現在您已設定網頁且部署了Adobe Experience Platform標籤程式庫，該測試實作了。

在瀏覽器中開啟您的產品頁面。 您可以按一下 _檔案_ then _開啟檔案……_ 或將頁面托管在網頁伺服器上，然後輸入適當的URL。

頁面載入後，您應該會看到下列內容：

![網頁](../../assets/implementation-strategy/webpage.png)

這不漂亮，但它能做到。

## Inspect頁面檢視和產品檢視事件

在瀏覽器中開啟開發人員工具，然後按一下網路面板。 重新整理您的頁面。

此時，您應該會看到四個要求：

1. product.html — 您的網頁。
2. launch-##########-development.js — 您的Launch程式庫。
3. interact — 傳送至伺服器的頁面檢視事件。
4. interact — 要傳送至伺服器的產品檢視事件。

歡迎檢查每個要求的裝載。 第一個 `interact` 請求時，您應該會看到裝載隨 `eventType` of `web.webpagedetails.pageViews`.

![頁面檢視請求檢查](../../assets/implementation-strategy/webpage-page-viewed-inspection.png)

第二個 `interact` 請求時，您應該會看到裝載隨 `eventType` of `commerce.productViews`.

![產品檢視請求檢查](../../assets/implementation-strategy/webpage-product-view-inspection.png)

歡迎隨意探查其餘傳送的資料，包括產品資訊。

## Inspect開啟購物車並新增至購物車事件

現在按一下 _新增至購物車_ 按鈕。

您應會看到兩個其他請求，第一個是 `eventType` of `commerce.productListOpens` （用於開啟新購物車）和第二個 `eventType` of `commerce.productListAdds` （用於將產品新增至購物車）。

## Inspect下載應用程式連結點擊事件

視瀏覽器而定，點選會導覽您離開目前頁面的連結，可能會清除您的網路面板。 因為您想要在離開頁面前檢查發生的連結點擊事件的網路要求，因此您需要設定瀏覽器以保留各頁面的網路記錄。 這可透過勾選 _保留日誌_ 核取方塊(Chrome、Safari、Edge)，或按一下齒輪圖示並勾選 _保留日誌_ 項目(Firefox)。

現在按一下 _下載應用程式_ 連結。

你應該再看一次 `interact` 請求會顯示在「網路」面板中。 如果您檢查請求，應會找到 `eventType` of `web.webinteraction.linkClicks` 以及所點按連結的詳細資訊。

## 檢查資料是否進入Adobe Experience Platform資料集

請求一經傳送後，您也會想要檢查資料是否安全地送達您建立的Adobe Experience Platform資料集。 首先，導覽至 [!UICONTROL 資料集] 在Adobe Experience Platform內檢視。

選取您先前建立的資料集。

您可能需要等候幾分鐘，但很快應該會看到資料已處理並插入資料集的指示。 您也應該看到處理是否成功。 如果失敗，您將能看出失敗的原因。 失敗通常是因為您傳送的資料不符合架構，而您需要據此調整資料或架構。

![資料集擷取](../../assets/implementation-strategy/dataset-ingestion.png)

## 使用Adobe Experience Platform Debugger擴充功能

如需進一步了解您的實作在瀏覽器和Adobe伺服器上的行為方式，請查看Adobe Experience Platform Debugger瀏覽器擴充功能！

[Adobe Experience Platform Chrome專用Debugger擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Adobe Experience Platform Firefox專用Debugger擴充功能](https://addons.mozilla.org/zh-TW/firefox/addon/adobe-experience-platform-dbg/)
