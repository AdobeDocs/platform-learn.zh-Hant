---
title: 更新對象和設定檔指令碼 — 將Target從at.js 2.x移轉至Web SDK
description: 瞭解如何更新Adobe Target對象和設定檔指令碼，以與Experience Platform Web SDK相容。
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 針對Platform Web SDK相容性更新Target對象和設定檔指令碼


## 調整對象


如需詳細資訊和最佳實務，請參閱關於[個人資料指令碼](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)的專屬檔案。

## 更新動態內容的引數權杖



如果您選擇在移轉後進行調整，以便納入新的XDM mbox引數名稱，請務必在移轉事件期間暫停任何受影響的活動，以避免活動向訪客顯示錯誤。

接下來，瞭解如何[驗證Target實作](validate.md)。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Optimize擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
