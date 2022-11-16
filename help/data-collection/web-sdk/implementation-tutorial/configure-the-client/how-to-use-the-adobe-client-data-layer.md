---
title: 如何使用Adobe用戶端資料層
description: 如何使用Adobe用戶端資料層
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 33a5db8c-e49b-4073-b4d7-4abe19537fcb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# 如何使用Adobe用戶端資料層

在 [什麼是資料層？](whats-a-data-layer.md)，您得知討論資料層時需考慮兩個部分：容器和內容。 Adobe用戶端資料層是容器。 不管你怎麼 [建構資料](../structuring-your-data.md) 或者你選擇將哪些資訊放入資料中。 資料可結構化為 [XDM](../structuring-your-data.md#xdm)，如下列範例所示，或您可以完全建立自己的結構。

理想情況下，貴公司的工程團隊應負責透過頁面程式碼，將任何必要資料推送至資料層。 然後行銷團隊會從資料層擷取資料，最好使用Adobe Experience Platform標籤。

## 推送資料至資料層

Adobe用戶端資料層是JavaScript陣列。 建立Adobe用戶端資料層時，其開始為空：

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

若要將資料放入資料層，請呼叫 `push` 資料層陣列上的方法：

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

您可以隨時透過呼叫將其他資料推送至資料層 `push` 。

```js
window.adobeDataLayer.push({
  "claims": {
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
});
```

## 了解推送資料

如果您已實作前兩個 `push` 呼叫時，資料層陣列中會出現兩個項目。 資料層在此狀態中並非特別有用。 通常，您會想要存取資料層的合併狀態，換言之，您要存取的是單一物件，這是您推送至資料層之所有資料的合併結果。 我們稍後將在教學課程中學習如何存取此合併狀態。 目前，只要了解資料層在我們兩個 `push` 呼叫如下：

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## 移除資料

有時，您必須從資料層中移除資料片段。 當使用者從一個檢視導覽至下一個檢視時，這在單頁應用程式中尤其常見。 例如，如果使用者從產品檢視導覽至連絡人檢視，則清除資料層上的任何產品資料可能是可行的，因為它不再與使用中檢視相關。

您可以推送 `undefined` 針對您要移除的金鑰。 根據先前的範例，如果您要移除 `status` 從資料層，您的程式碼如下所示：

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

資料層的計算狀態將不再包含 `status`:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## 推送事件至資料層

Adobe用戶端資料層不僅用於儲存資料，還用於傳達頁面上發生的事件。 事實上，您通常會將資料推送至資料層 _結果_ 在頁面上發生的事件。 這些事件包括(1)互動事件，例如開啟聊天機器人或在搜尋列中輸入搜尋詞，或(2)非互動事件，例如廣告曝光或完成網頁效能計算。

若要傳達頁面上已發生事件，請包含 `event` 推送至資料層的物件中的索引鍵。 例如，您可能想要通知用戶已在搜索欄位中輸入了搜索查詢。

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

稍後，您將學習如何在特定事件推送至資料層時，觸發Adobe Experience Platform標籤中的規則。 另請注意， `event` key _not_ 包含在計算狀態中。 它受到資料層的特殊處理。

## 推送事件和資料至資料層

通知偵聽器用戶已輸入搜索查詢是有用的，但是，如果您想提供有關該事件的其他資訊，該怎麼辦？ 例如，您可能想要包含使用者的搜尋查詢。 您可以透過下列兩種方式之一提供此資料：

1. 提供資料以便 **保留** 作為資料層計算狀態的一部分。
2. 提供資料以便 **未保留** 作為資料層計算狀態的一部分。

是否要保留資料層中的資料，通常取決於您是否打算在使用者在頁面上的整個期間參照該資料。 若非如此，則將資料保留在資料層內可能只會導致資料層雜亂。

以下是推送包含其他資料之事件的範例，這些資料 **保留** 在資料層：

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "siteKnowledge": {
    "supportSiteSearch": {
      "term": "roller",
      "locationInPage": "topSearchBar"
    }
  }
});
```

之後 `push` 發生， `siteKnowledge` 在頁面卸載前（除非您故意移除或覆寫），資料層的計算狀態一律會顯示 `siteKnowledge`)。

相反地，以下是推送事件與其他資料的範例，這些資料 **未保留** 在資料層：

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "eventInfo": {
    "siteKnowledge": {
      "supportSiteSearch": {
        "term": "roller",
        "locationInPage": "topSearchBar"
      }
    }
  }
});
```

在此範例中，請注意 `siteKnowledge` 包在裡面 `eventInfo`. 此 `eventInfo` 密鑰受到資料層的特殊處理。 它會告訴資料層此資料 _show_ 包含在傳送給聽眾的事件中，但 _不應_ 保留在資料層內。 接到事件通知後(例如Adobe Experience Platform標籤)，系統就會基本忘記這些資料。 此 `siteKnowledge` 金鑰永遠不會顯示在資料層的計算狀態內。

每次您呼叫 `push`,Adobe用戶端資料層會通知任何監聽器。 稍後，我們將學習如何從Adobe Experience Platform標籤接聽這些通知並據以觸發規則。
