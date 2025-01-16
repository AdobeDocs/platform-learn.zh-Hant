---
title: 使用Photoshop API
description: 使用Photoshop API
kt: 5342
doc-type: tutorial
exl-id: 60eecc24-1713-4fec-9ffa-a3186db1a8ca
source-git-commit: a4933bd49988cd16c4382ad4327d01ae58b52bbb
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---

# 1.1.3使用Photoshop API

## 1.1.3.1更新您的Adobe I/O整合

移至[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home)。

![Adobe I/O新整合](./images/iohome.png)

移至&#x200B;**專案**，然後按一下以開啟您在上一個練習中建立的專案（稱為`--aepUserLdap-- Firefly`）。

![Azure儲存體](./images/ps1.png)

按一下&#x200B;**+新增至專案**，然後按一下&#x200B;**API**。

![Azure儲存體](./images/ps2.png)

選取&#x200B;**Creative Cloud**&#x200B;並按一下&#x200B;**Photoshop -Firefly服務**。 按一下&#x200B;**下一步**。

![Azure儲存體](./images/ps3.png)

按一下&#x200B;**下一步**。

![Azure儲存體](./images/ps4.png)

接下來，您需要選取產品設定檔，以定義此整合可用的許可權。

選取設定檔&#x200B;**預設Firefly服務組態**&#x200B;和&#x200B;**預設Creative Cloud自動化服務組態**。

按一下&#x200B;**儲存設定的API**。

![Azure儲存體](./images/ps5.png)

您的Adobe I/O專案現已更新，可搭配Photoshop和Firefly服務API使用。

![Azure儲存體](./images/ps6.png)

## 1.1.3.2以程式設計方式與PSD檔案互動

將檔案下載到[citisignal-fiber.psd](./../../../assets/ff/citisignal-fiber.psd)到您的案頭。

在Photoshop中開啟檔案&#x200B;**citisignal-fiber.psd**。 然後您應該擁有此專案。

![Azure儲存體](./images/ps7.png)

在&#x200B;**圖層**&#x200B;窗格中，您會看到檔案的設計者已為每個圖層指定唯一的名稱。 您可以在Photoshop中開啟PSD檔案來檢視圖層資訊，也可以利用程式設計方式來進行。

讓我們將您的第一個API要求傳送至Photoshop API。

前往Postman。 傳送API請求給Photoshop之前，您需要向Adobe I/O進行驗證。開啟您之前使用名稱&#x200B;**POST的要求 — 取得存取權杖**。

移至&#x200B;**Params**，並確認引數&#x200B;**Scope**&#x200B;已正確設定。 **範圍**&#x200B;的&#x200B;**值**&#x200B;應該如下所示：

`openid,session,AdobeID,read_organizations,additional_info.projectedProductContext, ff_apis, firefly_api`

然後，按一下&#x200B;**傳送**。

![Azure儲存體](./images/ps8.png)

接著，您就會具備有效的存取Token，與Photoshop API互動。

![Azure儲存體](./images/ps9.png)

### 1.1.3.2.1 Photoshop API - Hello World

接下來，讓我們向Photoshop API問好，以測試所有許可權和存取權是否已正確設定。 在集合&#x200B;**Photoshop**&#x200B;中，開啟名稱為&#x200B;**Photoshop Hello （測試驗證）的請求**。按一下&#x200B;**傳送**。

![Azure儲存體](./images/ps10.png)

您應該會收到此回應： **歡迎使用Photoshop API！**。

![Azure儲存體](./images/ps11.png)

接著，若要以程式設計方式與PSD檔案&#x200B;**citisignal-fiber.psd**&#x200B;互動，您必須將其上傳至儲存帳戶。 您可以使用Azure儲存體總管將其拖放到容器中，手動執行此操作，但這次您應透過API執行此操作。

### 1.1.3.2.2將PSD上傳至Azure

在Postman中，開啟要求&#x200B;**將PSD上傳至Azure儲存體帳戶**。 在上一個練習中，您已在Postman中設定這些環境變數，現在將使用：

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

如您在要求&#x200B;**將PSD上傳至Azure儲存體帳戶**&#x200B;中看到的，URL已設定為使用這些變數。

![Azure儲存體](./images/ps12.png)

在&#x200B;**Body**&#x200B;中，您現在應該新增選取檔案&#x200B;**citisignal-fiber.psd**。

![Azure儲存體](./images/ps13.png)

然後您應該擁有此專案。 按一下&#x200B;**傳送**。

![Azure儲存體](./images/ps14.png)

然後，您應該從Azure取得此空白回應，這表示您的檔案會儲存在Azure儲存體帳戶的容器中。

![Azure儲存體](./images/ps15.png)

如果您使用Azure儲存體總管檢視，您會在重新整理資料夾後看到檔案。

![Azure儲存體](./images/ps16.png)

### 1.1.3.2.3 Photoshop API — 取得資訊清單

接下來，您需要取得PSD檔案的資訊清單檔案。 在Postman中，開啟要求&#x200B;**Photoshop — 取得PSD資訊清單**。 移至&#x200B;**內文**。

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

按一下&#x200B;**傳送**。

在回應中，您現在會看到連結。 由於Photoshop中的作業有時需要一些時間才能完成，因此Photoshop會提供狀態檔案，以回應大部分的傳入請求。 若要瞭解您的請求正在發生什麼事，您需要讀取狀態檔案。

![Azure儲存體](./images/ps17.png)

若要讀取狀態檔案，請開啟要求&#x200B;**Photoshop — 取得PS狀態**。 接著您會看到此要求使用變數做為URL，這是由您傳送的上一個要求所設定的變數，**Photoshop — 取得PSD資訊清單**。 變數是在每個要求的&#x200B;**指令碼**&#x200B;中設定。

按一下&#x200B;**傳送**。

![Azure儲存體](./images/ps18.png)

您應該會看到此訊息。 目前，狀態設定為&#x200B;**擱置**，表示處理序尚未完成。

![Azure儲存體](./images/ps19.png)

您可以在&#x200B;**Photoshop — 取得PS Status**&#x200B;要求上再按幾次，直到狀態變更為&#x200B;**succeeded**&#x200B;為止。 這可能需要幾分鐘的時間。

當回應可用時，您會看到一個包含PSD檔案所有圖層資訊的json檔案。 這是有用的資訊，因為您可以在此處看到圖層名稱或圖層ID等內容。

![Azure儲存體](./images/ps20.png)

例如，搜尋文字`2048x2048-cta`。 您應該會看到此訊息。

![Azure儲存體](./images/ps21.png)

### 1.1.3.2.4 Photoshop API — 變更文字

接下來，您現在需要使用API變更行動號召的文字。 在Postman中，開啟請求&#x200B;**Photoshop — 變更文字**，並移至&#x200B;**內文**。

您應該會看到此訊息。 您可以看到：

- 首先，指定輸入檔案： `citisignal-fiber.psd`
- 第二，指定要變更的圖層，並將文字變更為
- 第三，指定了輸出檔案： `citisignal-fiber-changed-text.psd`

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
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

按一下&#x200B;**傳送**。

![Azure儲存體](./images/ps23.png)

就像之前一樣，回應包含一個連結，指向可追蹤進度的狀態檔案。

![Azure儲存體](./images/ps22.png)

若要讀取狀態檔，請開啟要求&#x200B;**Photoshop — 再次取得PS狀態**，然後按一下&#x200B;**傳送**。 如果狀態未立即設定為&#x200B;**成功**，請等候幾秒鐘，然後再次按一下&#x200B;**傳送**。

一旦狀態設定為&#x200B;**succeeded**，您應該就會看到這個專案。 在路徑`outputs[0]._links.renditions[0].href`中，您應該會看到Photoshop建立的輸出檔案URL，其中包含已變更的文字。

按一下URL以下載輸出檔案。

![Azure儲存體](./images/ps24.png)

檔案&#x200B;**citisignal-fiber-changed-text.psd**&#x200B;將下載到您的電腦，之後您可以開啟它。 之後，您應該會看到呼叫動作的預留位置已取代為文字&#x200B;**立即取得Fiber！**。

![Azure儲存體](./images/ps25.png)

最後，您也會使用Azure儲存體總管在容器中看到該檔案。

![Azure儲存體](./images/ps26.png)

您現在已經完成此練習。

下一步： [摘要與優點](./summary.md)

[返回模組1.1](./firefly-services.md)

[返回所有模組](./../../../overview.md)
