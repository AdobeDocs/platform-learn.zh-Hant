---
title: 如何使用Adobe使用者端資料層
description: 如何使用Adobe使用者端資料層
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 33a5db8c-e49b-4073-b4d7-4abe19537fcb
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# 如何使用Adobe使用者端資料層

在 [什麼是資料層？](whats-a-data-layer.md)中，您已瞭解在討論資料層時應考量兩個部分：容器和內容。 Adobe使用者端資料層是容器。 您如何操作並不重要 [建構您的資料](../structuring-your-data.md) 或是您選擇將哪些資訊放入資料中。 資料可結構化為 [XDM](../structuring-your-data.md#xdm)，如下列範例所示，或者您可以完全建置您自己的結構。

理想情況下，貴公司的工程團隊應負責透過頁面上的程式碼，將任何必要的資料推送至資料層。 行銷團隊接著會從資料層擷取資料，最好是使用Adobe Experience Platform標籤。

## 將資料推送至資料層

Adobe使用者端資料層是JavaScript陣列。 當您建立Adobe使用者端資料層時，它一開始是空的：

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

您可以隨時呼叫，將其他資料推送至資料層 `push` 再來一次。

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

## 瞭解推送的資料

如果您已實作前兩個 `push` 呼叫，您最終會在資料層陣列中出現兩個專案。 在此狀態下，資料層並不特別有用。 通常，您會想要存取資料層的合併狀態，換句話說，就是單一物件，也就是您推送至資料層之所有資料的合併結果。 我們將在本教學課程的後面部分瞭解如何存取此合併狀態。 目前，只要瞭解兩個資料庫之後的資料層計算狀態就足夠了 `push` 呼叫如下：

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

有時您必須從資料層移除資料片段。 當使用者從一個檢視導覽到下一個檢視時，這在單頁應用程式中特別常見。 例如，如果使用者從產品檢視導覽至連絡人檢視，則清除資料層上的任何產品資料可能很有意義，因為資料層不再與作用中檢視相關。

您可以按下列的值，移除資料片段： `undefined` 用於您要移除的金鑰。 如果您想要移除，請以先前的範例為基礎 `status` 從資料層，您的程式碼如下所示：

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

資料層的計算狀態將不再包含 `status`：

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

## 將事件推播至資料層

Adobe使用者端資料層不僅用於儲存資料，也用於通訊頁面上正在發生哪些事件。 事實上，您通常會將資料推送至資料層 _因此_ 發生在頁面上的事件的。 這些事件包括(1)互動事件，例如開啟聊天機器人或在搜尋列中鍵入搜尋字詞，或(2)非互動事件，例如廣告曝光或完成網頁績效計算。

若要傳達頁面上已發生事件，請加入 `event` 鍵（在您推送至資料層的物件中）。 例如，您可能想要傳達使用者已在搜尋欄位中輸入搜尋查詢。

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

稍後，您將瞭解在特定事件推送至資料層時，如何在Adobe Experience Platform Tags中觸發規則。 另請注意 `event` 索引鍵是 _not_ 包含在計算狀態中。 它受到資料層的特殊處理。

## 將事件和資料推播至資料層

通知接聽程式使用者已輸入搜尋查詢很有幫助，但如果您想提供有關事件的其他資訊怎麼辦？ 例如，您可能想要包含使用者的搜尋查詢。 您可以透過下列兩種方式之一提供此資料：

1. 提供資料，以便 **已保留** 在資料層中，做為資料層計算狀態的一部分。
2. 提供資料，以便 **未保留** 在資料層中，做為資料層計算狀態的一部分。

是否要將資料保留在資料層中，通常取決於您是否打算在使用者停留在頁面上的整個過程中參照該資料。 如果沒有，那麼將資料保留在資料層內部可能只會造成資料層混亂。

以下是推送具有其他資料之事件的範例， **已保留** 在資料層中：

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

在此之後 `push` 發生， `siteKnowledge` 一律會顯示在資料層的計算狀態中，直到頁面解除安裝為止（除非您有意移除或覆寫） `siteKnowledge`)。

相反地，以下範例將事件與符合以下條件的其他資料一起推送： **未保留** 在資料層中：

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

請注意，在此範例中， `siteKnowledge` 包在裡面 `eventInfo`. 此 `eventInfo` key會由資料層接受特殊處理。 它會告訴資料層，此資料會 _應該_ 會包含在傳送給接聽程式的事件中，但 _不應該_ 保留在資料層內。 將事件通知聽眾後(例如Adobe Experience Platform Tags)，此資料基本上會被遺忘。 此 `siteKnowledge` 金鑰絕不會顯示在資料層的計算狀態中。

每次您呼叫 `push`，Adobe使用者端資料層會通知任何接聽程式。 稍後，我們將瞭解如何從Adobe Experience Platform Tags監聽這些通知並相應地觸發規則。
