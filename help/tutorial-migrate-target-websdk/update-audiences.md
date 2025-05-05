---
title: 更新對象和設定檔指令碼 — 將Target從at.js 2.x移轉至Web SDK
description: 瞭解如何更新Adobe Target對象和設定檔指令碼，以與Experience Platform Web SDK相容。
exl-id: 2c0f85f7-6e8c-4d0b-8ed5-53897d06e563
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# 針對Platform Web SDK相容性更新Target對象和設定檔指令碼

在您完成將Target移轉至Platform Web SDK的技術更新後，您可能需要更新某些對象、設定檔指令碼和活動，以確保順利轉換。

您必須透過Platform Web SDK實作，以XDM格式傳遞所有Target mbox引數。 將變更發佈至生產環境前，您應該：

* 更新使用mbox引數的對象
* 更新使用mbox引數的設定檔指令碼
* 使用mbox引數權杖取代來更新任何優惠方案和活動（例如，`${mbox.parameter_name}`）

## 調整對象

應更新任何使用自訂mbox引數的對象，以使用新的XDM引數名稱。 例如，`page_name`的自訂引數可能會對應到`web.webpagedetails.pageName`。

若要確保與at.js和Platform Web SDK相容，一種方法是更新任何相關的對象，以便使用`OR`條件，如下所示：

![如何檢視更新Platform Web SDK相容性的Target對象](assets/target-audience-update.png){zoomable="yes"}

## 編輯個人資料指令碼

應更新個人資料指令碼以參考類似於對象的新XDM引數名稱。 除了mbox引數名稱的變更以外，設定檔指令碼在at.js和Platform Web SDK實作之間的運作方式並無差異。

確保相容性的一個方法是使用設定檔指令碼中的`OR`條件。

範例設定檔指令碼：

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

已更新Platform Web SDK相容性的設定檔指令碼：

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

如需詳細資訊和最佳實務，請參閱關於[個人資料指令碼](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=zh-Hant)的專屬檔案。

## 更新動態內容的引數權杖

如果您有任何使用[動態內容取代](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html?lang=zh-Hant)的選件、建議設計或活動，可能需要據此更新，以考慮新的XDM引數名稱。

根據您使用Token取代mbox引數的方式，您或許可以增強現有設定，以處理舊引數名稱和新引數名稱。 但是，在無法執行自訂JavaScript程式碼的情況下（例如在JSON選件中），您應在移轉完成並在生產網站上即時後，建立復本和進行更新。

JSON選件範例：

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

使用Platform Web SDK引數名稱的JSON選件範例：

```JSON
{
  "pageName" : "${mbox.web.webPagedDetails.pageName}",
  "layoutVariation" : "grid"
}
```

如果您選擇在移轉後進行調整，以便納入新的XDM mbox引數名稱，請務必在移轉事件期間暫停任何受影響的活動，以避免活動向訪客顯示錯誤。

接下來，瞭解如何[驗證Target實作](validate.md)。

>[!NOTE]
>
>我們致力協助您成功將Target從at.js移轉至Web SDK。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
