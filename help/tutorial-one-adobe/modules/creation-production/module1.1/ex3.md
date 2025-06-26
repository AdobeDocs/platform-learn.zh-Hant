---
title: 使用Photoshop API
description: 瞭解如何使用Photoshop API和Firefly Services
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 60eecc24-1713-4fec-9ffa-a3186db1a8ca
source-git-commit: 2dd9c43bbf348805fe6c271d92b3db51fd25ca6f
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 0%

---

# 1.1.3使用Photoshop API

瞭解如何使用Photoshop API和Firefly Services。

## 1.1.3.1必要條件

在繼續此練習之前，您必須先完成[您的Adobe I/O專案](./../../../modules/getting-started/gettingstarted/ex6.md)的設定，而且您還需要設定應用程式以與API互動，例如[Postman](./../../../modules/getting-started/gettingstarted/ex7.md)或[PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md)。

## 1.1.3.2 Adobe I/O - access_token

在&#x200B;**Adobe IO - OAuth**&#x200B;集合中，選取名為&#x200B;**POST - Get Access Token**&#x200B;的要求，並選取&#x200B;**傳送**。 回應應包含新的&#x200B;**accestoken**。

![Postman](./images/ioauthresp.png)

## 1.1.3.3以程式設計方式與PSD檔案互動

將[citisignal-fiber.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"}下載到您的案頭。

在Photoshop中開啟&#x200B;**citisignal-fiber.psd**。

![Azure儲存體](./images/ps7.png)

在&#x200B;**圖層**&#x200B;窗格中，檔案的設計者已為每個圖層指定唯一的名稱。 您可以在Photoshop中開啟PSD檔案，檢視圖層資訊，也可以使用程式設計方式執行此操作。

讓我們將您的第一個API要求傳送至Photoshop API。

### Photoshop API - Hello World

接下來，讓我們向Photoshop API問好，以測試所有許可權和存取權是否已正確設定。

在集合&#x200B;**Photoshop**&#x200B;中，開啟要求&#x200B;**Photoshop Hello （測試驗證）。**。選取&#x200B;**傳送**。

![Azure儲存體](./images/ps10.png)

您應該會收到回應&#x200B;**歡迎使用Photoshop API！**。

![Azure儲存體](./images/ps11.png)

接著，若要以程式設計方式與PSD檔案&#x200B;**citisignal-fiber.psd**&#x200B;互動，您必須將其上傳至儲存帳戶。 您可以使用Azure儲存體總管將其拖放到容器中，手動執行此操作，但這次您應透過API執行此操作。

### 將PSD上傳至Azure

在Postman中，開啟要求&#x200B;**將PSD上傳至Azure儲存體帳戶**。 在上一個練習中，您已在Postman中設定這些環境變數，現在將使用：

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

如您在要求&#x200B;**將PSD上傳至Azure儲存體帳戶**&#x200B;中看到的，URL已設定為使用這些變數。

![Azure儲存體](./images/ps12.png)

在&#x200B;**主體**&#x200B;中，選取檔案&#x200B;**citisignal-fiber.psd**。

![Azure儲存體](./images/ps13.png)

您的熒幕應如下所示。 選取&#x200B;**傳送**。

![Azure儲存體](./images/ps14.png)

您應該從Azure取得此空白回應，這表示您的檔案儲存在Azure儲存體帳戶的容器中。

![Azure儲存體](./images/ps15.png)

如果您使用Azure Storage Explorer檢視檔案，請務必重新整理資料夾。

![Azure儲存體](./images/ps16.png)

### Photoshop API — 取得資訊清單

接下來，您需要取得PSD檔案的資訊清單檔案。

在Postman中，開啟要求&#x200B;**Photoshop — 取得PSD資訊清單**。 移至&#x200B;**內文**。

內文看起來應該像這樣：

```json
  {
    "inputs": [
      {
        "storage": "external",
        "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
      }
    ],
    "options": {
      "thumbnails": {
        "type": "image/jpeg"
      }
    }
  }
```

選取&#x200B;**傳送**。

在回應中，您現在會看到連結。 由於Photoshop中的作業有時需要一些時間才能完成，因此Photoshop會提供狀態檔案來回應大多數傳入的請求。 若要瞭解您的請求正在發生什麼事，您需要讀取狀態檔案。

![Azure儲存體](./images/ps17.png)

若要讀取狀態檔案，請開啟要求&#x200B;**Photoshop — 取得PS狀態**。 您可以看到此請求正在使用變數做為URL，這是由您傳送的上一個請求所設定的變數，**Photoshop — 取得PSD資訊清單**。 變數是在每個要求的&#x200B;**指令碼**&#x200B;中設定。 選取&#x200B;**傳送**。

![Azure儲存體](./images/ps18.png)

您的熒幕應如下所示。 目前，狀態設定為&#x200B;**擱置**，表示處理序尚未完成。

![Azure儲存體](./images/ps19.png)

在&#x200B;**Photoshop — 取得PS Status**&#x200B;上再選取傳送幾次，直到狀態變更為&#x200B;**succeeded**。 這可能需要幾分鐘的時間。

當回應可用時，您可以看到json檔案包含PSD檔案所有圖層的資訊。 這是有用的資訊，因為可以識別圖層名稱或圖層ID等。

![Azure儲存體](./images/ps20.png)

例如，搜尋文字`2048x2048-cta`。 您的畫面應如下所示：

![Azure儲存體](./images/ps21.png)


### Photoshop API - SmartObject取代

接下來，您需要使用您在前一個練習中使用Firefly產生的影像，變更檔案citisignal-fiber.psd的背景。

在Postman中，開啟要求&#x200B;**Photoshop - SmartObject Replace**，並移至&#x200B;**Body**。

您的畫面應如下所示：

- 首先，指定輸入檔案： `citisignal-fiber.psd`
- 第二，指定要變更的圖層，並使用新的背景檔案
- 第三，指定了輸出檔案： `citisignal-fiber-replacedbg.psd`

```json
  {
    "inputs": [
        {
            "storage": "azure",
            "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
        }
    ],
    "options": {
        "layers": [
            {
                "name": "2048x2048-image",
                "input": {
                    "href": "{{FIREFLY_COMPLETED_ASSET_URL}}",
                    "storage": "external"
                }
            }
        ]
    },
    "outputs": [
        {
            "storage": "azure",
            "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-replacedbg.psd{{AZURE_STORAGE_SAS_WRITE}}",
            "type": "vnd.adobe.photoshop",
            "overwrite": true
        }
    ]
}
```

輸出檔案的名稱不同，因為您不想覆寫原始輸入檔案。

選取&#x200B;**傳送**。

![Azure儲存體](./images/psbg23.png)

就像之前一樣，回應包含一個連結，指向可追蹤進度的狀態檔案。

![Azure儲存體](./images/psbg22.png)

若要讀取狀態檔，請開啟要求&#x200B;**Photoshop — 取得PS狀態**，然後選取&#x200B;**傳送**。 如果狀態未立即設定為&#x200B;**成功**，請等待幾秒鐘，然後再次選取&#x200B;**傳送**。

選取要下載輸出檔案的URL。

![Azure儲存體](./images/psbg24.png)

將檔案下載到您的電腦後，開啟&#x200B;**citisignal-fiber-replacedbg.psd**。 您應該會看到背景影像已變更為類似影像，如下所示：

![Azure儲存體](./images/psbg25.png)

您也可以使用Azure儲存體總管在容器中檢視此檔案。

![Azure儲存體](./images/psbg26.png)

### Photoshop API — 變更文字

接下來，您需要使用API變更call to action的文字。

在Postman中，開啟請求&#x200B;**Photoshop — 變更文字**，並移至&#x200B;**內文**。

您的畫面應如下所示：

- 首先，指定輸入檔案： `citisignal-fiber-replacedbg.psd`，這是您變更背景影像時，在上一步驟中產生的檔案
- 第二，指定要變更的圖層，並將文字變更為
- 第三，指定了輸出檔案： `citisignal-fiber-changed-text.psd`

```json
  {
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-replacedbg.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Get Fiber now!"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

輸出檔案的名稱不同，因為您不想覆寫原始輸入檔案。

選取&#x200B;**傳送**。

![Azure儲存體](./images/ps23.png)

就像之前一樣，回應包含一個連結，指向可追蹤進度的狀態檔案。

![Azure儲存體](./images/ps22.png)

若要讀取狀態檔，請開啟要求&#x200B;**Photoshop — 取得PS狀態**，然後選取&#x200B;**傳送**。 如果狀態未立即設定為&#x200B;**成功**，請等待幾秒鐘，然後再次選取&#x200B;**傳送**。

選取要下載輸出檔案的URL。

![Azure儲存體](./images/ps24.png)

將檔案下載到您的電腦後，開啟&#x200B;**citisignal-fiber-changed-text.psd**。 您應該會看到call to action的預留位置已被文字&#x200B;**立即取得Fiber！**&#x200B;取代。

![Azure儲存體](./images/ps25.png)

您也可以使用Azure儲存體總管在容器中檢視此檔案。

![Azure儲存體](./images/ps26.png)

## 後續步驟

移至[Firefly自訂模型API](./ex4.md){target="_blank"}

返回[Adobe Firefly Services概觀](./firefly-services.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}