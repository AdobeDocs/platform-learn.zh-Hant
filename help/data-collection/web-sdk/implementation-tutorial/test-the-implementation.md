---
title: 測試實作
description: 測試實作
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: e2213c23-d395-4c57-8c6c-0319cd0fb0ac
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# 測試實作

現在您已設定好網頁並部署Adobe Experience Platform標籤程式庫，您可以開始測試實作了。

在瀏覽器中開啟您的產品頁面。 您可以按一下「 」來完成此操作 _檔案_ 則 _開啟檔案……_ 或是在網頁伺服器上託管網頁，然後輸入適當的URL。

頁面載入後，您應會看到類似以下畫面：

![網頁](../../assets/implementation-strategy/webpage.png)

雖然不漂亮，但能勝任工作。

## Inspect頁面檢視和產品檢視事件

在瀏覽器中開啟開發人員工具，然後按一下「網路」面板。 重新整理您的頁面。

此時，您應該會看到四個請求：

1. product.html — 您的網頁。
2. launch-##########-development.js — 您的Launch程式庫。
3. interact — 傳送至伺服器的頁面檢視事件。
4. interact — 傳送至伺服器的產品檢視事件。

請隨時檢查每個請求的裝載。 第一個 `interact` 要求，您應該能夠看到隨傳送的裝載 `eventType` 之 `web.webpagedetails.pageViews`.

![頁面檢視請求檢查](../../assets/implementation-strategy/webpage-page-viewed-inspection.png)

第二個 `interact` 要求，您應該能夠看到隨傳送的裝載 `eventType` 之 `commerce.productViews`.

![產品檢視請求檢查](../../assets/implementation-strategy/webpage-product-view-inspection.png)

您可以隨意瀏覽其餘的傳送資料，包括產品資訊。

## Inspect開啟的購物車並新增至購物車事件

現在按一下 _加入購物車_ 按鈕。

您應該會看到兩個其他請求，第一個是 `eventType` 之 `commerce.productListOpens` （用於開啟新購物車）和具有 `eventType` 之 `commerce.productListAdds` （用於將產品新增至購物車）。

## Inspect下載應用程式連結點選事件

視瀏覽器而定，按一下將您導覽至目前頁面的連結可能會清除您的網路面板。 由於您要在離開頁面之前檢查發生之連結點選事件的網路要求，因此您必須設定瀏覽器以保留各頁面的網路記錄檔。 這可透過勾選 _保留記錄_ 核取方塊(Chrome、Safari、Edge)，或按一下齒輪圖示並勾選 _保留記錄檔_ 專案(Firefox)。

現在按一下 _下載應用程式_ 連結。

您應該會再看到一個 `interact` 要求會顯示在網路面板中。 如果您檢查請求，應該會找到 `eventType` 之 `web.webinteraction.linkClicks` 以及所點按連結的詳細資訊。

## 檢查資料是否送達Adobe Experience Platform資料集

現在已傳送請求，您也會想要檢查資料是否已安全地送達您建立的Adobe Experience Platform資料集。 首先，瀏覽至 [!UICONTROL 資料集] 在Adobe Experience Platform中檢視。

選取您先前建立的資料集。

您可能需要等待幾分鐘，但很快您應該會看到有資料正在處理並插入資料集的指示。 您也應該檢視處理成功或失敗。 如果失敗，您將能夠檢視失敗的原因。 失敗通常是因為您傳送的資料不符合結構描述，且您需要相應地調整資料或結構描述。

![資料集擷取](../../assets/implementation-strategy/dataset-ingestion.png)

## 使用Adobe Experience Platform Debugger擴充功能

若要進一步瞭解您的實作在瀏覽器和Adobe伺服器上的表現，請檢視Adobe Experience Platform Debugger瀏覽器擴充功能！

[Chrome的Adobe Experience Platform Debugger擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Firefox的Adobe Experience Platform Debugger擴充功能](https://addons.mozilla.org/zh-TW/firefox/addon/adobe-experience-platform-dbg/)
