---
title: 將自訂程式碼移轉至網頁SDK
description: 瞭解如何將自訂程式碼從Analytics擴充功能中的s物件移轉至Web SDK。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16761
source-git-commit: 346d4b2965248fb34341ad464f3f126667e3d940
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 0%

---


# 將自訂程式碼移轉至網頁SDK

在本練習中，您將瞭解如何在Experience Platform標籤中，將自訂程式碼從Adobe Analytics擴充功能移轉至Adobe Experience Platform Web SDK擴充功能。

## 重大免責宣告

我敢肯定，我會在檔案中加入類似這樣的內容，告訴您使用程式碼的最佳/最簡單/最有效方式，對此您不會感到驚訝。 可以撰寫、編輯及處理程式碼的方式顯然有很多種。 在本練習中，我將提供一種方法，讓您輕鬆擷取現有規則中的程式碼，並加以複製、新增變更，使其適用於已移轉的規則。 若您想更好的做，這太棒了，我不僅歡迎您使用它，也歡迎您與我們分享，以及與Experience League社群中的同行（尤其是在有關本教學課程的社群貼文中）。 搭配實施外掛程式，頁面下半部也會有相同情況。 我在此建議一個方法，然後您做對您有益的事情。 好，讓我們進入詳細資訊。

>[!IMPORTANT]
>
>秉承上段精神，建議您藉此機會移轉至Web SDK並仔細檢視程式碼，瞭解其中是否有任何程式碼應更新或刪除，這也相當重要。 在下列段落和步驟中，您將會看到如何移轉程式碼，即使一次移動所有程式碼會更容易，但我還是建議您不要進行春季清潔（這麼說吧）。

## 移轉哪些程式碼？

我們在此章節中會先處理的程式碼，是您在任何Adobe Analytics動作（包括&#x200B;**設定變數**&#x200B;動作）的「自訂程式碼」視窗中可能擁有的程式碼。 換言之，請開啟其中一個規則，然後在動作區段中向下檢視。 如果您有「Adobe Analytics — 設定變數」動作，請按一下以開啟。

![設定變數代碼](assets/set-variables-action.jpg)

然後在右側向下捲動至底部，您會看到「自訂程式碼」視窗的「開啟編輯器」按鈕。 按一下以開啟。

![開啟自訂程式碼編輯器](assets/open-aa-custom-code-editor.jpg)

如果您有程式碼，則需要移轉，才能使用網頁SDK執行並傳送至Adobe Analytics。
這裡的主要想法是，我們將將「s」物件轉換為「內容」。__adobe.analytics」。

我們只需在第一次呼叫s物件之前新增一些其他程式碼，好讓網頁SDK可瞭解和處理它。 新增新修改程式碼的位置位於「Adobe Experience Platform Web SDK — 更新變數」動作的「自訂程式碼」視窗中。

舉例來說，假設您在自訂程式碼視窗中有以下程式碼區塊：

```javascript
const products = window.digitalData.products;
const productIndex = event.element.dataset.productIndex;
const product = products[productIndex];
s.products = [
product.cat3Tag,
product.id,
1,
product.price
].join(";");
```

您需要包含的程式碼如下：

```javascript
content.__adobe = content.__adobe || {};
content.__adobe.analytics = content.__adobe.analytics || {};
const s = content.__adobe.analytics;
```

因此，請依照下列步驟移轉自訂程式碼：

1. 在Adobe Analytics設定變數動作中，從視窗複製自訂程式碼
1. 關閉該程式碼視窗，然後關閉（取消退出）動作。
1. 開啟「網頁SDK — 更新變數」動作，方法是按一下該動作（或如果您還沒有該動作，請新增動作）。

   ![開啟更新變數動作](assets/open-sdk-update-variable.jpg)

1. 選取右側視窗頂端的分析物件

   ![選取分析物件](assets/select-analytics-object.jpg)

1. 向下捲動至底部並開啟自訂程式碼視窗

   ![開啟sdk自訂程式碼視窗](assets/open-sdk-custom-code.jpg)

1. 貼入您從Analytics自訂程式碼視窗取得的程式碼
1. 現在，將新幾行程式碼放置在現有程式碼的中央，使其位於s物件的第一個提及的上方，如下列範例所示：

![新的s程式碼](assets/new-s-code.jpg)

您現在可以在「自訂程式碼」視窗中儲存程式碼，並將變更保留在「更新變數」動作中。 您也會想要儲存規則，並將新變更發佈到工作程式庫中。

## 外掛程式呢？

如果您有Adobe Analytics的「appMeasurement」實作，並使用Experience Platform標籤（先前稱為「Launch」）中的Analytics擴充功能，則您可能正使用一或多個JavaScript「外掛程式」來設定變數或執行其他工作。 如果這些JavaScript函式和呼叫位於規則內的程式碼視窗中，此頁面上的上述資訊應可協助您將程式碼移轉至Web SDK。
不過，您的外掛程式程式碼也更有可能在Adobe Analytics擴充功能本身設定的程式碼視窗中。 若要檢查您是否有外掛程式和其他要移轉的程式碼，請進入Data Collection and Tags開啟Analytics擴充功能、開啟您的屬性，然後按一下左側導覽中的**擴充功能**。

1. 選取頁面頂端的「**已安裝**」標籤，然後選取您的Adobe Analytics擴充功能。
1. 然後在頁面右側，按一下&#x200B;**設定**

   ![設定analytics擴充功能](assets/configure-analytics-extension.jpg)

1. 展開&#x200B;**使用自訂程式碼設定追蹤器**&#x200B;區段
1. 按一下以&#x200B;**開啟編輯器**

   ![開啟主編輯器](assets/aa-extension-custom-code-window.jpg)

此時，您將可以看到其中的程式碼，而且您可能有JavaScript的「外掛程式」，也就是協助您取得所需資料，並將其指派給自訂維度的程式碼片段等。

就最真實的Adobe Analytics概念而言，並非此程式碼視窗中的所有內容都可被視為外掛程式。 在決定如何移轉程式碼時，請務必瞭解這一點。

### 從擴充功能的主要程式碼視窗移轉程式碼的建議

同樣地，並非程式碼視窗中的所有內容都是正式的Adobe Consulting建立外掛程式。 其中有些可能是您撰寫的程式碼，無論您是否將其稱為外掛程式。 我們建議進行兩項變更。 這是為了使用新的擴充功能，以及將剩餘的程式碼複製並貼到新的位置。

**第一個**，標籤中有名為&#x200B;**常用Web SDK外掛程式**&#x200B;的擴充功能。 此擴充功能是Adobe Analytics檔案中列出之實作外掛程式總數清單的子集。 透過將此擴充功能安裝至Tags屬性，您就能安裝隨附外掛程式的程式碼。 然後，若要使用這些外掛程式，您會在建立新&#x200B;**資料元素**&#x200B;時找到它們。 稍後將提供更多相關資訊。

**秒**，在網頁SDK擴充功能的設定中有一個程式碼視窗，您可以在其中放入所有（或部分）程式碼，如果您希望該程式碼在事件傳送到Adobe Analytics之前立即執行。 尋找該程式碼視窗的步驟如下：

1. 假設您已將Web SDK擴充功能新增至屬性，請瀏覽至&#x200B;**擴充功能**&#x200B;並選取&#x200B;**已安裝**&#x200B;索引標籤
1. 選取&#x200B;**Adobe Experience Platform Web SDK擴充功能**，然後按一下右側邊欄上的&#x200B;**設定**&#x200B;以開啟它。

   ![設定Web SDK擴充功能](assets/configure-websdk-extension.jpg)

1. 向下捲動至&#x200B;**Data Collection**&#x200B;區段，然後按一下以開啟&#x200B;**onBeforeEventSend**&#x200B;的程式碼視窗。

   ![onBeforeEventSend](assets/on-before-event-send-window.jpg)

這是您要在事件從網頁SDK傳入Analytics之前貼上您要執行的任何程式碼的位置。 這基本上就是doPlugins函式在舊版Analytics實作中所執行的動作。

**好消息**&#x200B;是您傳送事件時&#x200B;**隨時都可以執行**，因此無論是在頁面載入時或自訂連結中執行，此程式碼都應該執行、設定變數等。

#### 我是否需要變更我的程式碼？

嗯，有也沒有。 是，您確實需要變更一些小專案，但不，只要您變更這些小專案，就不需要變更大量程式碼：

_**程式碼變更1：**_
在您選擇之後（或之前），將「外掛程式」程式碼貼到Web SDK擴充功能的程式碼視窗中，**從程式碼中移除**&#x200B;個「doPlugin」行。 您不需要這些引數，但會造成錯誤，因為這些引數屬於appMeasurement.js的一部分，但不屬於Web SDK程式碼。

![移除doPlugins程式碼行](assets/remove-doplugins.jpg)

_**程式碼變更2：**_
您需做的另一個變更是新增一些程式碼，以便定義「s」物件，其內容與前述有關規則動作中程式碼的內容非常類似。 在這種情況下，我們需要以稍微不同的方式定義程式碼，新增已在規則動作中定義的「資料」節點，但此處不適用。
此定義應放置在程式碼視窗的頂端。 需要在中複製的程式碼(將程式碼放入Web SDK擴充功能時)如下所示：

```javascript
content.data.__adobe = content.data.__adobe || {};
content.data.__adobe.analytics = content.data.__adobe.analytics || {};
const s = content.data.__adobe.analytics;
```

_**同時變更兩個程式碼：**_
以下是上面列出的程式碼，但我們剛才已討論這兩項變更：

![已更新代碼](assets/update-code.jpg)

### 將主要擴充功能程式碼移轉至Web SDK的步驟

如上所述，建議包含兩個方面：使用新的「常用Web SDK外掛程式」擴充功能，以及從Analytics擴充功能設定復製程式碼並貼到Web SDK擴充功能設定中。 請記住這一點，以及頁面頂端的重要附註來清理您的程式碼，以下是高層級的建議步驟：

1. 從Analytics擴充功能的設定程式碼視窗複製所有程式碼，並將其貼到Web SDK擴充功能設定的onBeforeEventSend視窗中（雖然我們可能會複製需要移除或更新之程式碼，但我們會在新視窗中執行幾次程式碼）。
1. 現在在Web SDK擴充功能中檢視您的程式碼，並針對在&#x200B;**常見Web SDK外掛程式**&#x200B;擴充功能中定義的外掛程式，尋找外掛程式呼叫或函式定義。 安裝外掛程式擴充功能後，您可以在Web SDK資料元素定義視窗中找到外掛程式清單。 您也可以在該擴充功能](https://exchange.adobe.com/apps/ec/108520)的[檔案中找到它。
1. 對於您在新Web SDK外掛程式擴充功能中找到的每個外掛程式，請從程式碼中移除擴充功能及其呼叫，然後建立資料元素，接著在適當的規則中呼叫該資料元素以設定變數等，以確定您補償該移除。
1. 接下來，請傳遞程式碼，以檢視是否有任何呼叫已在appMeasurement.js檔案中定義的函式。 **以上程式碼變更1**&#x200B;即為此範例，此時您可以移除doPlugins程式碼（如果尚未移除）。 對於其他執行個體，當呼叫的函式未在程式碼的任何位置定義時，就會最明顯地顯示此方法。 您也可以向Adobe客戶支援或Experience League社群中的同儕確認，確保該程式碼為此案例。
1. 接下來，請依照本頁頂端的建議，傳遞您的程式碼，以更新或刪除任何不再適用於您分析需求的舊程式碼。
1. 現在，請執行上面列出的&#x200B;**程式碼變更2**，新增額外的行，以便對s物件的任何參考都不會在您的程式碼中造成錯誤。
1. 最後但同樣重要的是，測試、測試及再測試一些專案。 之後，請再次測試。 請確定您的程式碼在Experience Platform Debugger和Adobe Analytics的報表中提供您預期的結果。

>[!NOTE]
>
>關於上述步驟的最後兩個想法。
>首先，您可能會認為將外掛程式的程式碼全部留在其中會比較容易，而不用移除並使用新的「常用Web SDK外掛程式」擴充功能。 這是正確且正確的，但透過使用擴充功能，您可獲得使用UI、定義可重複使用的資料元素，以及自動接收未來任何程式碼更新的優點。 切換可能值得一試。
>
>第二，談到「進行切換」，您現在也可以決定更新所有的自訂程式碼，使其完全不參考舊的「s」物件（亦即上述步驟5的延伸）。 當然，這完全可以接受，而且是個好主意。 此移轉教學課程只是為了讓您移轉自訂程式碼更容易，以防您有大量程式碼且沒有資源可立即更新所有程式碼。 由您決定。

我們會以開始的方式結束本課程，確認有許多方式可撰寫程式碼，而本檔案會提供您一些步驟，供您依此方式進行。 主要問題是程式碼運作正常，而且會得到您預期的結果，因此您可以按照自己的方式行事，我是否說過您應該進行測試？
