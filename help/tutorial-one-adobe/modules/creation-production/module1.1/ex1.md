---
title: Firefly服務快速入門
description: 瞭解如何使用Postman和Adobe I/O來查詢Adobe Firefly Services API
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: c5a80b87ac8e997922cb8c69b4180c4220dd9862
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# 1.1.1 Firefly服務快速入門

瞭解如何使用Postman和Adobe I/O來查詢Adobe Firefly Services API。

## 1.1.1.1必要條件

在繼續此練習之前，您必須先完成[您的Adobe I/O專案](./../../../modules/getting-started/gettingstarted/ex6.md)的設定，而且您還需要設定應用程式以與API互動，例如[Postman](./../../../modules/getting-started/gettingstarted/ex7.md)或[PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md)。

## 1.1.1.2 firefly.adobe.com

移至[https://firefly.adobe.com](https://firefly.adobe.com)。 按一下&#x200B;**設定檔**&#x200B;圖示，確定您已登入正確的&#x200B;**帳戶**，應該是`--aepImsOrgName--`。 如有需要，請按一下&#x200B;**切換設定檔**&#x200B;以切換至該帳戶。

![Postman](./images/ffui1.png){zoomable="yes"}

輸入提示`Horses in a field`並按一下&#x200B;**產生**。

![Postman](./images/ffui2.png){zoomable="yes"}

之後，您應該會看到類似以下內容。

![Postman](./images/ffui3.png){zoomable="yes"}

接下來，在您的瀏覽器中開啟&#x200B;**開發人員工具**。

![Postman](./images/ffui4.png){zoomable="yes"}

您應該會看到此訊息。 移至&#x200B;**網路**&#x200B;標籤。

![Postman](./images/ffui5.png){zoomable="yes"}

輸入搜尋字詞&#x200B;**產生**，然後按一下[產生&#x200B;**]。**&#x200B;您應該會看到名稱為&#x200B;**generate-async**&#x200B;的請求。 選取該專案，然後移至&#x200B;**裝載**，您將在其中檢視要求的詳細資料。

![Postman](./images/ffui6.png){zoomable="yes"}

您在此看到的要求是傳送至Firefly服務伺服器端後端的要求。 它包含數個重要引數：

- **prompt**：這是您的提示，要求Firefly應該產生何種影像

- **種子**：在此要求中，種子是以隨機方式產生。 每當Firefly產生影像時，預設會透過挑選稱為種子的隨機數字來開始流程。 這個隨機數字有助於讓每個影像具有唯一性，如果您想要產生多種影像，這是很不錯的做法。 不過，您有時可能會想要產生多個請求中彼此相似的影像。 例如，當Firefly產生您要使用Firefly的其他選項（例如樣式預設集、參考影像等）修改的影像時，請在未來的HTTP要求中使用該影像的種子，以限制未來影像的隨機性，並接觸您想要的影像。

![Postman](./images/ffui7.png){zoomable="yes"}

請再次檢視UI。 將&#x200B;**外觀比例**&#x200B;變更為橫向(4:3)**。**

![Postman](./images/ffui8.png){zoomable="yes"}

向下捲動至&#x200B;**效果**，移至&#x200B;**主題**&#x200B;並選取效果，例如&#x200B;**漫畫書**。

![Postman](./images/ffui9.png){zoomable="yes"}

再次在瀏覽器中開啟&#x200B;**開發人員工具**。 然後，按一下[產生] **並檢查正在傳送的網路要求。**

![Postman](./images/ffui10.png){zoomable="yes"}

當您檢查網路請求的詳細資訊時，您現在會看到以下內容：

- 與先前的要求相比，**prompt**&#x200B;未變更
- 與先前的請求相比，**種子**&#x200B;尚未變更
- 根據&#x200B;**外觀比例**&#x200B;的變更，**大小**&#x200B;已變更。
- 已新增&#x200B;**樣式**，並參考您選取的&#x200B;**comic_book**&#x200B;效果

![Postman](./images/ffui11.png){zoomable="yes"}

若要進行下一個練習，您需要使用&#x200B;**seed**&#x200B;數字之一。 寫下選擇的種子編號。

在下一個練習中，您將使用Firefly Services完成類似工作，但接著使用API而非UI。 在此範例中，種子編號為&#x200B;**45781**。

## 1.1.1.3 Adobe I/O - access_token

在&#x200B;**Adobe IO - OAuth**&#x200B;集合中，選取名為&#x200B;**POST - Get Access Token**&#x200B;的要求，並選取&#x200B;**傳送**。 回應應包含新的&#x200B;**accestoken**。

![Postman](./images/ioauthresp.png){zoomable="yes"}

## 1.1.1.4 Firefly Services API，文字2影像

現在您已具備有效且新的access_token，接下來可以將第一個要求傳送至Firefly Services API。

從&#x200B;**FF - Firefly服務技術內部人士**&#x200B;集合中選取名為&#x200B;**POST - Firefly - T2I V3**&#x200B;的請求。

![Firefly](./images/ff1.png){zoomable="yes"}

從回應中複製影像URL，然後在您的網頁瀏覽器中開啟以檢視影像。

![Firefly](./images/ff2.png){zoomable="yes"}

您應該會看到描繪`horses in a field`的美麗影像。

![Firefly](./images/ff3.png){zoomable="yes"}

在您的請求&#x200B;**POST - Firefly - T2I V3**&#x200B;的&#x200B;**內文**&#x200B;中，在欄位`"promptBiasingLocaleCode": "en-US"`下新增下列內容，並以Firefly服務UI隨機使用的其中一個種子數字取代變數`XXX`。 在此範例中，**seed**&#x200B;編號為`45781`。

```json
,
  "seeds": [
    XXX
  ]
```

按一下&#x200B;**傳送**。 之後，您會收到包含Firefly服務產生之新影像的回應。 開啟影像進行檢視。

![Firefly](./images/ff4.png){zoomable="yes"}

之後，您應該會根據使用的&#x200B;**seed**，看到稍有差異的新影像。

![Firefly](./images/ff5.png){zoomable="yes"}

接著，在您的要求&#x200B;**POST - Firefly - T2I V3**&#x200B;的&#x200B;**內文**&#x200B;中，將下列&#x200B;**樣式**&#x200B;物件貼到&#x200B;**seed**&#x200B;物件下。 這會將產生的影像樣式變更為&#x200B;**comic_book**。

```json
,
  "contentClass": "art",
  "styles": {
    "presets": [
      "comic_book"
    ],
    "strength": 50
  }
```

然後您應該擁有此專案。 按一下&#x200B;**傳送**。

![Firefly](./images/ff6.png){zoomable="yes"}

按一下影像URL以開啟。

![Firefly](./images/ff7.png){zoomable="yes"}

您的影像現在已變更了一點。 套用樣式預設集時，種子影像的套用方式不再與之前相同。

![Firefly](./images/ff8.png){zoomable="yes"}

從您請求的&#x200B;**Body**&#x200B;移除&#x200B;**seed**&#x200B;物件的程式碼。 按一下&#x200B;**傳送**，然後按一下您從回應中取得的影像URL。

```json
,
  "seeds": [
    XXX
  ]
```

![Firefly](./images/ff9.png){zoomable="yes"}

您的影像現在已再次變更。

![Firefly](./images/ff10.png){zoomable="yes"}


## 1.1.1.5 Firefly Services API，一般擴充

從&#x200B;**FF - Firefly服務技術內部人員**&#x200B;集合中選取名為&#x200B;**POST - Firefly - Gen Expand**&#x200B;的請求，並移至請求的&#x200B;**Body**。

- **大小**：輸入所需的解析度。 此處輸入的值應大於影像的原始大小，且不能大於4096。
- **image.source.url**：此欄位需要需要需要展開影像的連結。 在此範例中，變數是用來參照上一個練習中產生的影像。

- **水準對齊**：接受的值為： `"center"`、`"left`、`"right"`。
- **垂直對齊**：接受的值為： `"center"`、`"top`、`"bottom"`。

![Firefly](./images/ff11.png){zoomable="yes"}

按一下回應中的影像URL。

![Firefly](./images/ff12.png){zoomable="yes"}

您現在會看到上一個練習產生的影像現在已擴展到3999x3999的解析度。

![Firefly](./images/ff13.png){zoomable="yes"}

當您變更位置對齊方式時，輸出也會稍有不同。 在此範例中，位置已變更為左下&#x200B;**的**。 按一下&#x200B;**傳送**，然後按一下以開啟產生的影像URL。

![Firefly](./images/ff14.png){zoomable="yes"}

然後您應該會看到原始影像已用於不同的位置，這會影響整個影像。

![Firefly](./images/ff15.png){zoomable="yes"}

## 後續步驟

移至[使用Microsoft Azure和預先簽署的URL最佳化您的Firefly程式](./ex2.md){target="_blank"}

返回[Adobe Firefly服務總覽](./firefly-services.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}
