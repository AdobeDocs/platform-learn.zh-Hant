---
title: API基本簡介
description: 應用程式寫程式介面簡介
activity: understand
doc-type: article
feature-set: Experience Platform
feature: Server API,API,Data Collection,Integrations
level: Beginner
role: User,Developer
solution: Data Collection
topic: Integrations
exl-id: 9607e641-b0d5-49c1-b319-32ed0720e715
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 0%

---

# API 101 - API的基本簡介

API代表應用程式寫程式介面。 它的含義就是 — 程式之間有介面，這些介面允許這些程式通信。 當程式設計師開發軟體應用時，他們往往需要自己的軟體來與其他軟體或硬體進行通信。 API定義這些通訊和互動的內容、方式、時間、位置及原因。

API是使用軟體解決業務難題的方法。 在大多數企業裡，這是一種合作努力。 透過對重要術語、概念和步驟的共同了解，協作總是更輕鬆。

如果您想要在網頁中按一下連結，當您按一下連結時，瀏覽器會使用幾個API。 瀏覽器可辨識點按，提出您要造訪的頁面要求，透過網際網路擷取頁面，然後在您的畫面上顯示。 中間有許多較小的步驟，但您的瀏覽器是用來與各種API通訊和互動的軟體，只是為了顯示網頁。 在本文中，我們會強調使用或討論API時非常重要的術語、概念和步驟。

在本文結尾，您應該已清楚了解這些基本術語、概念和步驟。 API檔案內容非常豐富，有關使用API處理特定使用案例的討論內容可能會非常詳細。 透過清楚的基本知識和共同了解，導覽檔案和討論API既簡單又高效。

>[!NOTE]
>
> 雖然有許多API，但此處的重點將放在網頁和瀏覽器API上：基本上，當一個軟體應用程式通過網際網路與另一個軟體應用程式交互時。

## API條款與概念

一個詞或短語是什麼意思？我如何簡單地去想？ 在API中，「應用程式」部分是指軟體應用程式或程式。 「寫程式介面」部分指的是應用程式與另一個應用程式進行特定用途交互的方式和位置。 在我們的網頁範例中，當您按一下連結時，瀏覽器會傳送網頁的要求至伺服器。

![具有目標URL的超連結影像](../assets/api101-link-destination.png)

在此螢幕擷取中，滑鼠游標將滑鼠游標暫留在Adobe Experience Platform連結上。 底部是網頁瀏覽器狀態列，顯示瀏覽器將取得之頁面的「位址」。 換句話說，按一下Adobe Experience Platform連結會告訴瀏覽器「幫我取得該頁面，以便我在畫面上看到」。

按一下連結時，瀏覽器會向伺服器要求取得頁面。 這是 `GET` 要求，此為網頁API常用的要求方法之一。 瀏覽器滿足要求時，需要用到的一項功能是頁面「地址」 — 它在網頁上的哪個位置？

### URL的部分

![具有URL的瀏覽器網址列](../assets/api101-address-bar.png)

大部分的瀏覽器都有「位址列」，顯示網頁的部分或全部「位址」。 當瀏覽器「取得」所點按連結的頁面時，就會在此位址列中顯示該頁面的「位址」。 那麼，網頁的「地址」是什麼？

那個 `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html` 以上是Web上的頁面地址，它稱為URL或統一資源定位器。 URL可以指的頁面如此一頁、影像檔案、視訊或其他檔案類型。

![URL的部分](../assets/api101-url-parts.jpg)

此位址(URL)具有與網頁和瀏覽器API非常相關的特定部分。

**方案**

此 `scheme` 上稱為 `protocol` API，且通常 `http` 或 `https`. HTTP或HyperText傳輸協定是將網頁等資源從Web伺服器傳輸到Web瀏覽器的方式。 HTTPS是安全版本，其中傳輸會透過網際網路進行，使用安全性來防止對所傳輸的資源造成干擾。 透過HTTPS檢視頁面時，瀏覽器位址列中常會出現一點鎖定圖示。

對於Web API，這些資源的傳輸會透過HTTP要求進行 — 換言之，就是透過HTTP提出要求。

**主機和網域**

此 `business.adobe.com` 是所請求資源的主機。 按一下範例連結時，瀏覽器會使用URL的這個部分來尋找托管頁面的伺服器。 它並不總是與Web伺服器完全相同，但在基本層面，我們可以將其視為瀏覽器將獲取我們請求的頁面的伺服器。

域名是域名系統的一部分，更稱為DNS。 大多數人都想 `adobe.com` 或 `example.com` 「網域名稱」，但有些部分與API相關。 `www.adobe.com` 和 `business.adobe.com` 可以稱為網域名稱，但 `www.` 和 `business.` 部分稱為子網域。 API通常會與包含子網域的URL互動，例如 `api.example.com` 或 `sub.www.example.com`.

很常見 _主機_ 指的是完整網域名稱，包括任何子網域，例如 `business.adobe.com`. 通常也會看到 _網域_ 或 _網域名稱_ 在引用沒有子網域的主機時，如 `adobe.com`. 記住每個部分的具體術語和主機的變異在這裡並不重要。 但要了解這些術語經常被使用非常重要，以便您能夠澄清有關業務和討論的任何相關細節。

**Origin**

Origin是另一個需注意的詞語，與URL的部分密切相關。 從基本層面來看，來源大致為 `scheme` 加上 `host` 加上 `domain` like `https://business.adobe.com`. 不同的值通常代表不同的原始值，例如 `https://business.adobe.com` 和 `http://business.adobe.com` 不是同一來源，因為它們有不同的方案。 `https://www.adobe.com` 和 `https://business.adobe.com` 因為子網域不同，在許多使用中也不是相同的來源。

**路徑**

上述URL範例中的最後一位是 `path` 至資源 — 此範例中的頁面。 此 `/products/experience-platform/` part通常表示web伺服器上的資料夾或目錄。 就像我們的電腦上有用於文檔和照片的資料夾或目錄一樣，我們在Web伺服器上也有資料夾來組織內容。 最後， `/adobe-experience-platform.html` part是檔案的名稱，即網頁。

URL的其他更詳細部分將在本系列的下一部分強調顯示。

### 協力廠商API

網頁API有時稱為協力廠商API。 想想交易的當事人。 在我們的連結範例中，您（更確切地說，您的瀏覽器）是頁面要求的第一方。 Web伺服器是第二方。 第三個呢？

網頁通常會包含來自其他主機或來源的內容或資源。 在這些情況下，當您的瀏覽器開始顯示頁面時，會向托管這些資源的其他主機（或「第三方」）提出另一組請求。 這是很常見的情況，尤其是影片或影像等媒體內容，也是檢視或使用時需要更新的資料。 取得特定人員的目前時間、目前天氣或個人化歡迎訊息，都是協力廠商API可在正確時間提供適當資源的範例。 來自這些協力廠商API的請求很常見。

## 網頁API的常見用途

除了一天中的某天、天氣或個人化內容外，網頁API有許多用途。 twitter、TikTok、Facebook、LinkedIn、Snapchat、Pinterest等社交媒體平台，都有各種API，程式設計師可搭配其應用程式使用。 當然，Adobe也 [各種API](https://developer.adobe.com/apis) 程式設計師使用這些軟體，以便與Adobe產品和服務進行互動。 軟體產品和服務可透過這些API存取其他軟體產品和服務。

## 範例API

瀏覽器API可讓程式設計人員直接與瀏覽器的功能互動。 電池API允許軟體檢查設備的電池狀態，以便根據需要提醒您。 剪貼簿API可讓軟體複製或貼上您裝置的剪貼簿。 全螢幕API可讓軟體呈現將檢視展開至裝置全螢幕的選項，例如YouTube。

Adobe Experience Platform資料存取API是網頁API，可讓程式設計人員從Adobe Experience Platform存取和下載資料集檔案，以便在自己的程式中使用客戶設定檔資料。 這類API在軟體自動化過程中很常見，軟體被寫程式以組合使用多個API執行一系列步驟。 與手動執行這些相同步驟相比，這通常可大幅節省成本。

## API端點

程式設計師在程式中「使用」瀏覽器或網頁API時，通常會提出傳送或接收資源的要求，例如要求網頁的範例瀏覽器。 API檔案通常會列出這些請求的「端點」，例如： `https://platform.adobe.io/data/foundation/export/files/{dataSetFileId}`. 這是程式設計師用來取得資料集檔案的Platform Data Access API的特定模式或「端點」。

此 `{dataSetFileId}` 由這些大括弧包圍，代表程式設計師需要在請求中發送的值。 因此，實際API請求中的URL看起來會像 `https://platform.adobe.io/data/foundation/export/files/xyz123brb` 其中 `xyz123brb` 必須是程式設計師要接收的資料集檔案的有效ID。

換言之，就像瀏覽器在特定URL取得頁面一樣，API請求也會從特定端點（如此資料集範例）取得資源，或將資源傳送至。

## HTTP要求方法

此時應清楚，Web API會要求網頁或資料集等資源。 與大多數軟體概念一樣，這些HTTP請求遵循可重複的模式。 請求從軟體應用程式發送到另一個軟體應用程式，該軟體應用程式評估請求，然後響應：瀏覽器向Web伺服器請求頁面，並使用頁面內容進行回應。

從請求到響應的整個過程涉及許多較小且非常詳細的步驟，但請求方法是直接的。 請求方法會定義要求的操作。

**`GET`**

此 `GET` 要求提供資源的回應時會使用request方法，例如我們的網頁和資料集範例。 當我們在瀏覽器中按一下連結，或在行動裝置上點選連結時，會產生 `GET` 在幕後請求。

**`POST`**

此 `POST` 方法會隨請求傳送資料。 「要求」傳送資料聽起來可能有些奇怪，但提出API要求的想法是要求端點（即接收軟體）接受要求，而在 `POST`，也接受要傳送的資料。 傳送的資料通常會寫入資料存放區，例如資料庫或檔案，以便儲存。

**`PUT`**

此 `PUT` 要求方法類似於 `POST` 因為會傳送資料，但如果要傳送的資料已存在於端點，則 `PUT` 會以取代的方式更新現有資料。 A `POST` 不更新，只會傳送，因此多個 `POST` 請求可以建立已傳送資料的多個記錄，而不需更新任何現有記錄。

**`PATCH`**

此 `PATCH` request方法可用來傳送更新部分現有記錄的資料，例如透過更新帳戶設定檔來變更地址時。 使用 `POST` 請求可建立其他設定檔，並使用 `PUT`，可以取代現有設定檔，但使用 `PATCH` 方法我們只需更新現有記錄的相關部分，如地址。

**`DELETE`**

此 `DELETE` request方法會移除請求中指定的資源，就像我們按一下連結以完全刪除帳戶設定檔一樣。

還有其他幾項，但這是使用API時最常見方法的清單。

### 請求範例

現在您已具備與API相關的基本術語、概念和步驟，我們可以在實務中查看API要求範例。

瀏覽器範例中的頁面URL為 `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html`. 按一下Adobe Experience Platform連結時，瀏覽器會 `GET` 請求。 由於我們有瀏覽器可為我們執行工作，因此我們只需按一下，但如果程式設計師希望該請求在軟體應用程式中發生，他們必須提供API請求的所有必要詳細資訊才能成功完成。

以下是程式碼中的顯示方式：

```js
fetch(
  "https://business.adobe.com/products/experience-platform/adobe-experience-platform.html",
  {
    headers: {
      accept:
        "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
      "accept-language": "en-US,en;q=0.9",
      "sec-ch-ua":
        '" Not A;Brand";v="99", "Chromium";v="101", "Microsoft Edge";v="101"',
      "sec-fetch-dest": "document",
      "sec-fetch-mode": "navigate",
      "sec-fetch-site": "none",
      "sec-fetch-user": "?1",
      "upgrade-insecure-requests": "1",
    },
    referrerPolicy: "strict-origin-when-cross-origin",
    body: null,
    method: "GET",
    mode: "cors",
    credentials: "include",
  }
);
```

在上方的程式碼中，您可以看到 `URL` 瀏覽器會提出請求，而底部附近 `method: "GET"` 要求方法。 其他幾行代碼也是請求的一部分，但不在本文的討論範圍內。


*[API]:應用程式寫程式介面*[URL]:統一資源定位器*[HTTP]:超文本傳輸協定*[DNS]:域名系統
