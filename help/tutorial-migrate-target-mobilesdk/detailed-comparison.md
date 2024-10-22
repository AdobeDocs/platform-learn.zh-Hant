---
title: Target擴充功能與決策擴充功能的比較
description: 瞭解Target擴充功能與Decisioning擴充功能之間的差異，包括功能、功能、設定和資料流程。
source-git-commit: 78d04d625aa55ce5eb76615c220b49aefd958431
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# Target擴充功能與決策擴充功能的比較

Adobe Journey Optimizer - Decisioning擴充功能與適用於行動應用程式的Adobe Target擴充功能不同。 下表為參考資料，可協助您評估在移轉程式期間可能需要著重的實作領域。

檢閱下列資訊並評估您目前的技術Target擴充功能實作後，您應該就能瞭解下列內容：

- Adobe Journey Optimizer支援哪些Target功能 — Decisioning
- 哪些Adobe Target擴充功能具有Adobe Journey Optimizer — 決策等效功能
- 如何將Target設定套用至Adobe Journey Optimizer — 決策
- Adobe Target擴充功能和Adobe Journey Optimizer — 決策擴充功能的資料流程有何不同

如果您是初次使用Platform Web SDK，別擔心，本教學課程將更詳細地介紹以下專案。

## 功能比較

| 功能 | 目標延伸功能 | 決策擴充功能(透過Edge的Target) |
|---|---|---|
| 預先擷取模式 | 支援 | 支援 |
| 執行模式 | 支援 | 不支援 |
| 自訂引數 | 支援 | 不支援每個mbox引數 |
| 登入對象 | 支援 | 支援 |
| 使用行動生命週期量度的對象細分 | 支援 | 透過資料收集規則支援 |
| thirdPartyId (mbox3rdPartyId) | 透過資料流中的身分對應和名稱空間設定提供支援 |
| 通知（顯示、按一下） | 支援 | 支援 |
| 回應Token | 支援 | 支援 |
| 動態優惠方案 | 支援 | 支援 |
| Analytics for Target (A4T) | 僅限使用者端 | 使用者端和伺服器端 |
| 行動裝置預覽（QA模式） | 支援 | 有限支援 |



## 值得注意的圖說文字

>[!NOTE]
>
>不支援將Target移轉至Platform Web SDK，同時保留指定頁面的現有AppMeasurementAdobe Analytics實施。
>
> 您可將您的at.js (和AppMeasurement.js)實作一次移轉一頁至Platform Web SDK。 如果您採取這個方法，最好使用`configure`命令將[`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled)和[`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled)選項設定為`true`。

## Target擴充功能與決策擴充功能的同等專案

許多Target擴充功能都有等同於下表所列之「決策」擴充功能的方法。 如需[函式](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)的詳細資訊，請參閱Adobe Target開發人員指南。

| 目標延伸功能 | Decisioning擴充功能 |
| --- | --- | 
| |  |

## Target擴充功能設定與決策擴充功能等同專案

Target擴充功能可以透過中的各種設定進行設定和下載……

| 目標延伸功能 | Decisioning擴充功能 |
| --- | --- | 
| |  |


## 系統圖表比較

下列圖表應可協助您瞭解使用Adobe Journey Optimizer - Decisioning擴充功能的Target實作與使用Adobe Target擴充功能的實作之間的資料流程差異。

### Target擴充功能系統圖



### 決策擴充功能系統圖




>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
