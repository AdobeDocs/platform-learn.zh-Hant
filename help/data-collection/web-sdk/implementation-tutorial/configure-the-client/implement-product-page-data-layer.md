---
title: 在產品頁面上實作資料層
description: 在產品頁面上實作資料層
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 在產品頁面上實作資料層

在本教學課程中，您將針對典型的電子商務網站實作Adobe Client Data Layer 。 如果您尚未這樣做，請閱讀 [如何使用Adobe使用者端資料層](how-to-use-the-adobe-client-data-layer.md) 首先瞭解Adobe使用者端資料層的運作方式。

假設使用者瀏覽您的產品，然後按一下泡沫膠捲以瞭解更多資訊。 使用者登陸泡沫壓路機產品詳細資訊頁面。

以下是您簡單產品詳細資料頁面的HTML：

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

如您所見，在 `<head>` 標籤中有一個 `<script>` 標籤之間。 您可以在此處放置JavaScript程式碼。 不需要放置 `<script>` 標籤範圍 `<head>`，但儘快將資料推播至資料層有助於確保行銷人員在使用者離開頁面之前可以快速將資料傳送至Adobe Experience Platform。

內部 `<script>` 標籤之前，請先建立 `adobeDataLayer` 陣列，然後將適當的事件和資料資訊推送至陣列。 資料符合XDM結構描述 [您先前已建立](../configure-the-server/create-a-schema.md).

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

在此範例中，您已對資料層進行兩次推送，每次都包含 `event` 金鑰。 包含 `event` key不僅可傳達頁面上已發生的事件，而且可讓行銷人員更輕鬆地在Adobe Experience Platform標籤內建立適當規則。

第一次推送至資料層時，會通知接聽程式（標籤規則）使用者已檢視頁面。 它也會將頁面名稱和網站區段新增至資料層。

第二次推送至資料層時，會通知接聽程式（標籤規則）使用者已檢視產品。 它也會將產品資訊新增至資料層。

## 加入購物車

您可能也想要追蹤使用者何時點選 [!UICONTROL 加入購物車] 按鈕。

若要這麼做，請建立一個函式，當使用者按一下 [!UICONTROL 加入購物車] 按鈕。

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

呼叫此函式時，會先檢查購物車是否已供使用者使用。 通常可透過檢查特定Cookie或變數是否存在來完成。 如果購物車不存在，您將推送 `cartOpened` 事件放入資料層。 之後，您將推送 `productAddedToCart` 事件放入資料層。 產品資訊已存在於資料層中，因此您不需要再次新增。

新增 `onclick` 屬性至 [!UICONTROL 加入購物車] 呼叫您新專案的按鈕 `onAddToCartClick` 函式。

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

最後要做的就是追蹤使用者何時點選 _[!UICONTROL 下載應用程式]_ 連結。

若要這麼做，請建立一個函式，當使用者按一下 _[!UICONTROL 下載應用程式]_ 連結。

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

在此情況下，連結的相關資訊會包裝在 `eventInfo` 金鑰。 如中所述 [如何使用Adobe使用者端資料層](how-to-use-the-adobe-client-data-layer.md)，這會告知資料層將此資料與事件通訊，但會 _not_ 將資料保留在資料層內。 若為連結點按，將點按連結的資訊新增至資料層並無用處，因為此資訊與頁面整體無關，也不適用於可能發生的其他事件。

新增 `onclick` 屬性至 [!UICONTROL 下載應用程式] 呼叫您新連結的連結 `onDownloadAppClick` 函式。

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
