---
title: 在產品頁面上實作資料層
description: 在產品頁面上實作資料層
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 在產品頁面上實作資料層

在本教學課程中，您將針對一般電子商務網站實作Adobe用戶端資料層。 如果您尚未這麼做，請閱讀 [如何使用Adobe用戶端資料層](how-to-use-the-adobe-client-data-layer.md) 首先，了解Adobe用戶端資料層的運作方式。

假設使用者瀏覽了您的產品，並點按了泡沫滾筒，以了解更多資訊。 用戶登陸泡沫輥產品詳細資訊頁面。

以下是您簡單產品詳細資料頁面的HTML:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      // Code will go here.
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

正如你所注意到的， `<head>` 標籤有 `<script>` 標籤。 這是您放置JavaScript程式碼的位置。 不需要將 `<script>` 標籤內 `<head>`，但請盡快將資料推送至資料層，可協助行銷人員在使用者離開頁面前快速將資料傳送至Adobe Experience Platform。

內 `<script>` 標籤，您會先建立 `adobeDataLayer` 陣列，然後將適當的事件和資料資訊推送至陣列。 資料符合XDM架構 [您先前建立](../configure-the-server/create-a-schema.md).

```js
window.adobeDataLayer = window.adobeDataLayer || [];
window.adobeDataLayer.push({
  "event": "pageViewed",
  "web": {
    "webPageDetails": {
      "name": "Foam Roller",
      "siteSection": "Equipment"
    },
  }
});
window.adobeDataLayer.push({
  "event": "productViewed",
  "productListItems": [
    {
      "SKU": "eqfr08",
      "currencyCode": "USD",
      "name": "Foam Roller",
      "priceTotal": 18.95
    }
  ]
});
```

在此範例中，您已進行兩次推送至資料層，每個都包含 `event` 鍵。 包括 `event` 索引鍵不僅可傳達頁面上發生的事件，而且讓行銷人員在Adobe Experience Platform標籤中建立適當規則更簡單。

第一次推送至資料層時，會通知監聽器（標籤規則）使用者已檢視頁面。 也會將頁面名稱和網站區段新增至資料層。

第二個推送至資料層會通知監聽器（標籤規則）使用者已檢視產品。 它也會將產品資訊新增至資料層。

## 新增至購物車

您也可能想要追蹤使用者點按 [!UICONTROL 新增至購物車] 按鈕。

若要這麼做，請建立當使用者按一下 [!UICONTROL 新增至購物車] 按鈕。

```js
window.onAddToCartClick = function() {
  // In a real implementation, you would change this condition to 
  // only pass if a cart doesn't already exist. You would typically 
  // do this by checking a cookie or variable value.
  if (true) {
    window.adobeDataLayer.push({
      "event": "cartOpened",
    });
  }
  window.adobeDataLayer.push({
    "event": "productAddedToCart"
  });
};
```

呼叫此函式時，會先檢查使用者是否已有購物車。 這通常會透過檢查特定Cookie或變數是否存在來完成。 如果購物車不存在，您會推送 `cartOpened` 事件移入資料層。 接著，你會推 `productAddedToCart` 事件移入資料層。 資料層中已有產品資訊，因此您不需要再次新增。

新增 `onclick` 屬性 [!UICONTROL 新增至購物車] 按鈕調用新 `onAddToCartClick` 函式。

HTML頁面的結果應如下所示：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

## 下載應用程式

最後要執行的一項動作，是追蹤使用者點按 _[!UICONTROL 下載應用程式]_ 連結。

若要這麼做，請建立當使用者按一下 _[!UICONTROL 下載應用程式]_ 連結。

```js
window.onDownloadAppClick = function(event) {
  window.adobeDataLayer.push({
    "event": "downloadAppClicked",
    "eventInfo": {
      "web": {
        "webInteraction": {
          "URL": "https://example.com/download",
          "name": "App Download",
          "type": "download"
        }
      }
    }
  });
};
```

在此情況下，連結的相關資訊會包裝在 `eventInfo` 鍵。 如 [如何使用Adobe用戶端資料層](how-to-use-the-adobe-client-data-layer.md)，這會告訴資料層與事件一併傳送此資料，但傳送至 _not_ 將資料保留在資料層內。 對於連結點按，將點按連結的相關資訊新增至資料層沒有用處，因為它整體上不屬於頁面，且不適用於可能發生的其他事件。

新增 `onclick` 屬性 [!UICONTROL 下載應用程式] 呼叫新 `onDownloadAppClick` 函式。

HTML頁面的結果應如下所示：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
      window.onDownloadAppClick = function() {
        window.adobeDataLayer.push({
          "event": "downloadAppClicked",
          "eventInfo": {
            "web": {
              "webInteraction": {
                "URL": "https://example.com/download",
                "name": "App Download",
                "type": "download"
              }
            }
          }
        });
      };
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```
