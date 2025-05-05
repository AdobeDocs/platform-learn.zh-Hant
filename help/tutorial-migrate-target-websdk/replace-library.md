---
title: 取代資料庫 — 將Target從at.js 2.x移轉至Web SDK
description: 瞭解如何將Adobe Target實作從at.js 2.x移轉至Adobe Experience Platform Web SDK。 主題包括程式庫概述、實作差異和其他值得注意的圖說文字。
exl-id: dfafa132-376a-475d-a467-9bc2f0a414cf
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 1%

---

# 以Platform Web SDK取代at.js資料庫

瞭解如何取代頁面上的Adobe Target實作，以從at.js移轉至Platform Web SDK。 基本取代包含下列步驟：

* 檢閱您的Target管理設定，並記下您的IMS組織ID
* 以Platform Web SDK取代at.js資料庫
* 更新同步程式庫實作的預先隱藏程式碼片段
* 設定Platform Web SDK

>[!NOTE]
>
>提供的範例僅供說明用途，您實際的Target實作可能會有所不同。 如果您現有的Target實作使用Adobe的資料收集標籤管理員，您也可以參閱[Platform Web SDK Target實作教學課程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=zh-Hant)以取得其他資訊。


## 檢閱Target管理設定

將Target移轉至Platform Web SDK的第一步，是檢閱Target介面的&#x200B;**[!UICONTROL 管理]**&#x200B;區段中的設定。

### [!UICONTROL 實作]

#### [!UICONTROL 帳戶詳細資料]

* **[!UICONTROL IMS組織ID]** — 記下此值，因為設定Platform Web SDK需要此值。
* **[!UICONTROL 裝置上決策]** - Platform Web SDK不支援此功能。 若您移轉後不再在任何網站上使用at.js，或不再有任何裝置上決策的伺服器端使用案例，即可停用此設定。

#### [!UICONTROL 實作方法]

**[!UICONTROL 實作方法]**&#x200B;區段中的所有可編輯設定僅適用於at.js。 這些設定可用來產生自訂的at.js程式庫，以供您實作。 檢閱這些設定，以檢查您是否有任何自訂程式碼，或正在為跨網域使用案例設定第一方和第三方Cookie。

**[!UICONTROL 設定檔存留期]**&#x200B;設定只能由Adobe客戶服務變更。 Target訪客設定檔存留期不會受到實施方式的影響。 at.js和Platform Web SDK都使用相同的訪客設定檔存留期。

#### [!UICONTROL 隱私]

* **[!UICONTROL 模糊化訪客IP位址]** — 此設定會影響地理定位功能。 at.js和Platform Web SDK都針對地理定位使用相同的後端IP模糊化設定。

### [!UICONTROL 環境]

Platform Web SDK使用資料流設定，可讓您為個別開發、測試和生產資料流明確定義[!UICONTROL 環境ID]。 此設定的主要使用案例是用於行動應用程式實施，其中URL不存在以輕鬆區分環境。 此設定為選用，但可用於確保所有請求都與指定環境正確關聯。 這與at.js實作不同，在實作中，您必須根據網域和主機群組規則指派Target環境。

>[!NOTE]
>
>如果在資料流設定中未指定環境ID，則Target會使用&#x200B;**主機**&#x200B;區段中指定的網域對環境對應。

如需詳細資訊，請參閱[資料流組態](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=zh-Hant#target)指南和Target [主機](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=zh-Hant)檔案。

## 部署Platform Web SDK

Target功能由at.js和Platform Web SDK共同提供。 如果兩個程式庫同時使用，您可能會遇到轉譯和追蹤問題。 若要成功移轉至Platform Web SDK，第一步是移除at.js，並將其取代為Platform Web SDK (alloy.js)。

假設有一個使用at.js的簡單Target實作：

* 靠近頁面頂端的資料層可提供Target和其他應用程式的資訊
* 一或多個可在Target活動中使用其功能的第三方協助程式庫（例如jQuery）
* 預先隱藏的程式碼片段可緩解閃爍問題
* Target at.js程式庫會以非同步方式載入預設設定，以自動要求及轉譯活動：

+++at.js範例在HTML頁面上實作

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>
  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
  <!--prehiding snippet for Target with asynchronous deployment-->
  <script>
    ;(function(win, doc, style, timeout) {
      var STYLE_ID = 'at-body-style';

      function getParent() {
        return doc.getElementsByTagName('head')[0];
      }

      function addStyle(parent, id, def) {
        if (!parent) {
          return;
        }
        var style = doc.createElement('style');
        style.id = id;
        style.innerHTML = def;
        parent.appendChild(style);
      }

      function removeStyle(parent, id) {
        if (!parent) {
          return;
        }
        var style = doc.getElementById(id);
        if (!style) {
          return;
        }
        parent.removeChild(style);
      }
      addStyle(getParent(), STYLE_ID, style);
      setTimeout(function() {
        removeStyle(getParent(), STYLE_ID);
      }, timeout);
    }(window, document, "body {opacity: 0 !important}", 3000));
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div>Homepage Hero Banner Content</div>
</body>
</html>
```

+++

若要升級Target以使用Platform Web SDK，請先移除at.js：

```HTML
<!--Target at.js library loaded asynchonously-->
<script src="/libraries/at.js" async></script>
```

和將取代為alloy JavsScript程式庫或您的標籤內嵌程式碼和Adobe Experience Platform Web SDK擴充功能：

>[!BEGINTABS]

>[!TAB JavaScript]

```HTML
<!--Platform Web SDK base code-->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
<script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
```

>[!TAB 標記]

```HTML
<!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
<script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
```

在標籤屬性中，新增Adobe Experience Platform Web SDK擴充功能：

![新增Adobe Experience Platform Web SDK擴充功能](assets/library-tags-addExtension.png){zoomable="yes"}


>[!ENDTABS]

預先建立的獨立版本需要直接新增至頁面的「基底程式碼」，以建立名為alloy的全域函式。 使用此函式與SDK互動。 如果您想要將全域函式命名為其他名稱，請變更`alloy`名稱。

如需其他詳細資訊和部署選項，請參閱[安裝Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=zh-Hant)檔案。


## 更新內容預先隱藏方法

視程式庫是以非同步或同步方式載入而定，Platform Web SDK實作可能需要預先隱藏程式碼片段。

### 非同步實施

就像使用at.js一樣，如果Platform Web SDK程式庫以非同步方式載入，頁面可能會在Target執行內容交換之前完成轉譯。 此行為可能會導致所謂的「閃爍」問題，發生此問題時，會先短暫地顯示預設內容，然後再更換為Target指定的個人化內容。 若要避免發生這種閃爍問題，Adobe建議在非同步Platform Web SDK指令碼參考或標籤內嵌程式碼之前，立即新增特殊的預先隱藏程式碼片段。

如果您的實作非同步（如上述範例），請將at.js預先隱藏程式碼片段取代為下列與Platform Web SDK相容的版本：

```HTML
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

預先隱藏程式碼片段會使用您選擇的CSS定義，在頁面標題中建立樣式標籤。 在收到來自Target的回應或達到逾時時間時，會移除此樣式標籤。

預先隱藏行為是由程式碼片段尾端的兩項設定所控制。

* `body { opacity: 0 !important }`會指定在Target載入之前，要用於預先隱藏的CSS定義。 依預設，會隱藏整個頁面。 您可以將此定義更新為要預先隱藏的選擇器，以及要如何隱藏它們。 您可以包含多個定義，因為此值只是插入到預先隱藏樣式標籤中的值。 如果您有可輕鬆識別的容器元素，可將內容包裝在導覽下，則可使用此設定將預先隱藏限定為該容器元素。

* `3000`指定預先隱藏的逾時時間（毫秒）。 如果逾時前未收到來自Target的回應，則會移除預先隱藏樣式標籤。 達到此逾時的情況應該很少見。

>[!IMPORTANT]
>
>請務必對Platform Web SDK使用正確的程式碼片段，因為它使用不同的樣式識別碼`alloy-prehiding`。 如果使用適用於at.js的預先隱藏程式碼片段，該程式碼片段可能無法正常運作。

### 同步實施

Adobe建議您以非同步方式實施Platform Web SDK，以獲得最佳的整體頁面效能。 不過，如果alloy.js程式庫或tags內嵌程式碼同步載入，則不需要預先隱藏程式碼片段。 而是在Platform Web SDK設定中指定預先隱藏樣式。

可以使用[`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hant#prehidingStyle)選項設定同步實施的預先隱藏樣式。 下節將介紹Platform Web SDK設定。

若要深入瞭解Platform Web SDK如何管理忽隱忽現的情形，請參閱指南章節： [管理個人化體驗的忽隱忽現情形](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html?lang=zh-Hant)

## 設定Platform Web SDK

每次載入頁面時都必須設定Platform Web SDK。 以下範例假設整個網站正在單一部署中升級為Platform Web SDK：

>[!BEGINTABS]

>[!TAB JavaScript]

`configure`命令必須一律為呼叫的第一個SDK命令。 `edgeConfigId`是[!UICONTROL 資料流識別碼]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

>[!TAB 標記]

在標籤實作中，許多欄位會自動填入或從下拉式選單中選取。 請注意，可以為每個環境選取不同的Platform [!UICONTROL 沙箱]和[!UICONTROL 資料串流]。 資料流將會根據發佈程式中標籤庫的狀態而變更。

![設定Web SDK標籤延伸模組](assets/tags-config.png){zoomable="yes"}
>[!ENDTABS]

如果您打算以逐頁方式從at.js移轉至Platform Web SDK，則需要下列設定選項：


>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled":true,
  "idMigrationEnabled":true
});
```

>[!TAB 標記]

![設定Web SDK標籤延伸移轉選項](assets/tags-config-migration.png){zoomable="yes"}

>[!ENDTABS]

以下列出與Target相關的重要設定選項：

| 選項 | 說明 | 範例值 |
| --- | --- | --- |
| `edgeConfigId` | 資料串流ID | `ebebf826-a01f-4458-8cec-ef61de241c93` |
| `orgId` | Adobe Experience Cloud組織ID | `ADB3LETTERSANDNUMBERS@AdobeOrg` |
| `targetMigrationEnabled` | 使用此選項可讓Web SDK讀取和寫入at.js使用的舊版mbox和mboxEdgeCluster Cookie。 這可協助您在從使用Web SDK的頁面移至使用at.js程式庫的頁面時，保留訪客設定檔，反之亦然。 | `true` |
| `idMigrationEnabled` | 如果為True，SDK會讀取及設定舊的AMCV Cookie。 當網站某些部分仍可能使用Visitor.js時，此選項可協助您轉換至使用Platform Web SDK。 | `true` |
| `thirdPartyCookiesEnabled` | 啟用Adobe第三方Cookie的設定。 SDK可將訪客ID儲存在協力廠商內容中，以便跨網站使用相同的訪客ID。 如果您有多個網站，請使用此選項；不過，有時基於隱私權原因不需要此選項。 | `true` |
| `prehidingStyle` | 用來建立CSS樣式定義，在從伺服器載入個人化內容時隱藏網頁的內容區域。 此僅適用於SDK的同步部署。 | `body { opacity: 0 !important }` |

如需完整的選項清單，請參閱[設定Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hant)指南。

## 實作範例

當Platform Web SDK正確就位後，範例頁面看起來會像這樣。

>[!BEGINTABS]

>[!TAB JavaScript]

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

>[!TAB 標記]

頁面代碼：

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

在標籤中，新增Adobe Experience Platform Web SDK擴充功能：

![新增Adobe Experience Platform Web SDK擴充功能](assets/library-tags-addExtension.png){zoomable="yes"}

並新增所需的設定：
![設定Web SDK標籤延伸移轉選項](assets/tags-config-migration.png){zoomable="yes"}


>[!ENDTABS]



請務必注意，僅包含並設定Platform Web SDK程式庫（如上所示）並不會執行任何對Adobe Edge網路的網路呼叫。

接下來，瞭解如何[要求並套用VEC型活動](render-vec-activities.md)至頁面。

>[!NOTE]
>
>我們致力協助您成功將Target從at.js移轉至Web SDK。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
