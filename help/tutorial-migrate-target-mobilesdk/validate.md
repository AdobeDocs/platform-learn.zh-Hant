---
title: 驗證和疑難排解決策擴充功能實施
description: 瞭解如何使用Decisioning擴充功能來驗證Adobe Target行動實作並進行疑難排解。
exl-id: edc6e25a-58d7-4145-97c3-bf48e980914f
source-git-commit: a4fe85580776e5d84f6deaf3c0224f0513ba8415
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 驗證和疑難排解決策擴充功能實施

將Target實作從Target擴充功能移轉至Decisioning擴充功能後，請務必驗證一切都正常運作，然後再將任何變更發佈至生產應用程式。 Adobe建議進行下列事項，本頁將詳細介紹這些事項：

* 執行技術驗證，以確保基本實作和Platform Mobile SDK請求與回應看起來正確無誤
* 確保Target活動已正確傳送和呈現
* 檢查報表是否正常運作
* 重新造訪對象和個人資料指令碼，以確保其與Platform Mobile SDK和Optimize擴充功能相容
* 確保與Adobe或協力廠商應用程式的整合可正常運作

每個Target實作會因使用的網站架構和功能而異。 您可使用下清單格作為起點，並新增實作專用的任何專案。

## 技術驗證和疑難排解

透過Assurance，Platform Mobile SDK和Decisioning擴充功能的技術驗證和疑難排解功能已大幅增強。 請參閱以下檔案頁面，以瞭解此基本工具的相關資訊：

* [在Assurance中設定決策外掛程式](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/assurance-setup/){target=_blank}

* [正在驗證最佳化SDK設定](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/optimize-configuration-view/){target=_blank}

* [檢閱要求並模擬不同的體驗](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/review-simulate/){target=_blank}

執行上述驗證步驟後，您完全可以放心，含Decisioning擴充功能的Platform Mobile SDK實作已準備好投入生產環境。

恭喜，您已結束本教學課程！ 祝您將Adobe Target實作移轉至Decisioning擴充功能好運！

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
