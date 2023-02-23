---
title: 更新對象和設定檔指令碼 |將Target從at.js 2.x移轉至Web SDK
description: 了解如何更新Adobe Target對象和設定檔指令碼，以與Experience PlatformWeb SDK相容。
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# 更新Target受眾和設定檔指令碼，以便與Platform Web SDK相容

完成技術更新以將Target移轉至Platform Web SDK後，您可能需要更新部分對象、設定檔指令碼和活動，以確保順暢轉換。

所有Target mbox參數都必須以XDM格式透過Platform Web SDK實作傳遞。 將變更發佈至生產環境前，您應：

* 更新使用mbox參數的對象
* 更新使用mbox參數的設定檔指令碼
* 更新任何選件和活動時都會使用mbox參數代號取代(例如 `${mbox.parameter_name}`)

## 調整對象

任何使用自訂mbox參數的對象都應更新為使用新的XDM參數名稱。 例如， `page_name` 可能會對應至 `web.webpagedetails.pageName`.

若要確保與at.js和Platform Web SDK相容，一種方法是更新任何相關對象，以便 `OR` 條件，如下所示：

![如何檢視更新Target受眾，以提升平台Web SDK相容性](assets/target-audience-update.png){zoomable=&quot;yes&quot;}

## 編輯設定檔指令碼

描述檔指令碼應更新，以參考類似於對象的新XDM參數名稱。 除了變更mbox參數名稱外，設定檔指令碼在at.js和Platform Web SDK實作之間的運作方式並無差異。

確保相容性的一種方法是使用 `OR` 設定檔指令碼程式碼中的條件。

設定檔指令碼範例：

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

更新Platform Web SDK相容性的設定檔指令碼：

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

如需詳細資訊和最佳實務，請參閱 [設定檔指令碼](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html).

## 更新動態內容的參數Token

如果您有任何使用的選件、建議設計或活動 [動態內容取代](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html)，則新XDM參數名稱可能需要相應更新。

根據您對mbox參數使用代號取代的方式，您可能可以增強現有設定，以說明新舊參數名稱。 不過，在無法使用自訂JavaScript程式碼的情況下（例如在JSON選件中），您應在移轉完成並在生產網站上上線後，建立復本並進行更新。

範例JSON選件：

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

使用Platform Web SDK參數名稱的JSON選件範例：

```JSON
{
  "pageName" : "${mbox.web.webPagedDetails.pageName}",
  "layoutVariation" : "grid"
}
```

如果您選擇在移轉後進行調整，以考慮新的XDM mbox參數名稱，請務必在移轉事件期間暫停任何受影響的活動，以防止活動對訪客顯示錯誤。

接下來，學習如何 [驗證Target實作](validate.md).

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).