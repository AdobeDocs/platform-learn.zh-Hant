---
title: 發佈程式庫
description: 發佈程式庫
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 2fc072df-24f2-4fea-848f-0a973deca2f8
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 4%

---

# 發佈程式庫

現在可以將標籤程式庫部署至您的網站。

## 建立程式庫

首先，您必須建立包含您已建立的擴充功能、規則和資料元素的程式庫。 若要建立程式庫，請選取 [!UICONTROL 發佈流程] 在左側功能表中。

選取 [!UICONTROL 新增程式庫].

您應會看到程式庫建立檢視。

![標籤庫建立](../../../assets/implementation-strategy/tags-library-creation.png)

為程式庫命名，例如 _示範_. 選取 [!UICONTROL 開發] 在 [!UICONTROL 環境] 下拉式清單。 然後按一下 [!UICONTROL 新增所有變更的資源].

您現在應該會看到底下列出的所有擴充功能、規則和資料元素 [!UICONTROL 資源變更]. 按一下 [!UICONTROL 儲存並建置到開發環境].

## 將內嵌程式碼新增至您的HTML

現在，您必須將指令碼標籤新增至載入新建立標籤程式庫的產品頁面HTML。

從按一下開始 [!UICONTROL 環境] 在左側功能表中。 您應該會看到列出三個不同的環境。

![標籤環境](../../../assets/implementation-strategy/tags-environments.png)

按一下上的套件圖示 [!UICONTROL 開發] 環境列。 您應該會看到將Launch程式庫指令碼安裝到頁面上的指示。

![標籤安裝指示](../../../assets/implementation-strategy/tags-installation-instructions.png)

複製指令碼標籤（為方便起見，提供複製到剪貼簿按鈕）。 開啟您的產品頁面HTML，並將指令碼標籤插入在 `</head>` 標籤之間。 您的最終HTML應如下所示：

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
    <!--Swap this script tag with your own-->
    <script src="https://assets.adobedtm.com/xxxxxxxxxxxx/xxxxxxxxxxxx/launch-xxxxxxxxxxxx-development.min.js" async></script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```

檢視 [發佈標籤的檔案](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=zh-Hant) 如果您想進一步瞭解發佈程式。

接下來，您將測試新實作！
