---
title: 更新Target對象和設定檔指令碼 — 將行動應用程式中的Adobe Target實作移轉至Offer Decisioning和Target擴充功能
description: 瞭解如何更新Adobe Target對象和設定檔指令碼，以與Offer Decisioning和Target擴充功能相容。
exl-id: de3ce2c7-0066-496a-a8a7-994d7ce3d92c
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 更新Target對象和設定檔指令碼，以瞭解Decisioning行動擴充功能相容性


在您完成將Target移轉至Offer Decisioning和Target擴充功能的技術更新後，您可能需要更新某些對象、設定檔指令碼和活動，以確保順利轉換。

>[!INFO]
>
>如果您將所有mbox引數移轉至`data.__adobe.target`物件，您就不需要更新對象、設定檔指令碼和活動，如下所示。


如果您將mbox引數移轉至`xdm`物件，則在將變更發佈至生產環境之前，您應該：

* 更新使用mbox引數的對象
* 更新使用mbox引數的設定檔指令碼
* 使用mbox引數權杖取代來更新任何優惠方案和活動（例如，`${mbox.parameter_name}`）

## 調整對象

如果您將mbox引數移轉至`xdm`物件，使用自訂mbox引數的對象應該更新為使用新的XDM引數名稱。 例如，`page_name`的自訂引數可能會對應到`web.webpagedetails.pageName`。

若要確保與Target擴充功能以及Offer Decisioning和Target擴充功能相容，一種方法是更新任何相關的對象，以便使用`OR`條件，如下所示：

![如何檢視Offer Decisioning和Target擴充功能相容性的更新Target對象](assets/target-audience-update.png){zoomable="yes"}

## 編輯個人資料指令碼

如果您將mbox引數移轉至`xdm`物件，應更新設定檔指令碼以參照新的XDM引數名稱，類似於對象。 除了mbox引數名稱的變更以外，Target和決定實作之間的設定檔指令碼運作方式並無差異。

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

如需詳細資訊和最佳實務，請參閱關於[個人資料指令碼](https://experienceleague.adobe.com/en/docs/target/using/audiences/visitor-profiles/profile-parameters)的專屬檔案。

## 更新動態內容的引數權杖

如果您將mbox引數移轉至`xdm`物件，而且您有任何使用[動態內容取代](https://experienceleague.adobe.com/en/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer)的選件、建議設計或活動，則可能需要相應更新以納入新的XDM引數名稱。

根據您使用Token取代mbox引數的方式，您或許可以增強現有設定，以處理舊引數名稱和新引數名稱。 但是，在無法執行自訂JavaScript程式碼的情況下（例如在JSON選件中），您應在移轉完成並在生產網站上即時後，建立復本和進行更新。

JSON選件範例：

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

使用XDM物件引數名稱的JSON選件範例：

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
>我們致力協助您成功將行動Target從Target擴充功能移轉至Offer Decisioning和Target擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
