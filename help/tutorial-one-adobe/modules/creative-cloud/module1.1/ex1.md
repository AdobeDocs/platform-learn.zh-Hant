---
title: Firefly服務快速入門
description: Firefly服務快速入門
kt: 5342
doc-type: tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: ea06ca2d05195efa57643d45d7e50d3d914081d3
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# 1.1.1Firefly服務快速入門

在本練習中，您將使用Postman和Adobe I/O來查詢Adobe Firefly服務API。

## 設定您的Adobe I/O專案

在本練習中，您將密集使用Adobe I/O來查詢Firefly服務API。 請依照下列步驟設定Adobe I/O。

移至[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home)

![Adobe I/O新整合](./images/iohome.png)

請務必在熒幕右上角選取正確的例項。 您的執行個體是`--aepImsOrgName--`。 按一下&#x200B;**建立新專案**。

![Adobe I/O新整合](./images/iocomp.png)

選取&#x200B;**+新增至專案**&#x200B;並選取&#x200B;**API**。

![Adobe I/O新整合](./images/adobe_io_access_api.png)

然後您會看到以下內容：

![Adobe I/O新整合](./images/api1.png)

選取&#x200B;**Creative Cloud**，然後按一下&#x200B;**Firefly-Firefly服務**。 按一下&#x200B;**下一步**。

![Adobe I/O新整合](./images/api3.png)

您現在將會看到此訊息。 提供認證的名稱： `--aepUserLdap-- - Firefly Services OAuth credential`。 按一下&#x200B;**下一步**。

![Adobe I/O新整合](./images/api4.png)

接下來，您需要選取產品設定檔，以定義此整合可用的許可權。

選取設定檔&#x200B;**預設Firefly服務組態**。

按一下&#x200B;**儲存設定的API**。

![Adobe I/O新整合](./images/api9.png)

您的Adobe I/O整合現已準備就緒。

![Adobe I/O新整合](./images/api11.png)

按一下「**Postman下載**」按鈕，然後按一下「**OAuth伺服器對伺服器**」以下載Postman環境。

![Adobe I/O新整合](./images/iopm.png)

您的IO專案目前有一個通用名稱。 您需要為整合提供易記名稱。 按一下所示的&#x200B;**專案X** （或類似名稱）

![Adobe I/O新整合](./images/api13.png)

按一下&#x200B;**編輯專案**。

![Adobe I/O新整合](./images/api14.png)

輸入整合的名稱： `--aepUserLdap-- Firefly`。

按一下&#x200B;**儲存**。

![Adobe I/O新整合](./images/api15.png)

您的Adobe I/O整合設定現已完成。

![Adobe I/O新整合](./images/api16.png)

## Adobe I/O的Postman驗證

移至[https://www.postman.com/downloads/](https://www.postman.com/downloads/)。

下載並安裝作業系統的相關Postman版本。

![Adobe I/O新整合](./images/getstarted.png)

安裝Postman後，請啟動應用程式。

Postman中有2個概念：「環境」和「集合」。

- 環境檔案包含您所有大致一致的環境變數。 在環境中，您會找到Adobe環境的IMSOrg之類的專案，以及使用者端ID和其他專案之類的安全性憑證。 環境檔案是您在上一個練習中的Adobe I/O設定期間下載的檔案，其名稱如下： **`oauth_server_to_server.postman_environment.json`**。

- 集合包含您可以使用的許多API請求。 我們將使用2個集合
   - 1個用於Adobe I/O驗證的集合
   - 1此單元練習的集合

請將檔案[postman.zip](./../../../assets/postman/postman-ff.zip)下載到您的本機案頭。

![Adobe I/O新整合](./images/pmfolder.png)

在此&#x200B;**postman.zip**&#x200B;檔案中，您會找到下列檔案：

- `Adobe IO - OAuth.postman_collection.json`
- `FF - Firefly Services Tech Insiders.postman_collection.json`

解壓縮&#x200B;**postman-ff.zip**&#x200B;檔案，並將這2個檔案與從Adobe I/O下載的Postman環境（即檔案`oauth_server_to_server.postman_environment.json`）一起儲存在案頭上的資料夾中。 您需要在該資料夾中有這3個檔案：

![Adobe I/O新整合](./images/pmfolder1.png)

返回Postman。 按一下&#x200B;**匯入**。

![Adobe I/O新整合](./images/postmanui.png)

按一下&#x200B;**檔案**。

![Adobe I/O新整合](./images/choosefiles.png)

導覽至您案頭上解壓縮2個下載檔案的資料夾。 同時選取這3個檔案，然後按一下[開啟]。****

![Adobe I/O新整合](./images/selectfiles.png)

按一下&#x200B;**開啟**&#x200B;後，Postman會顯示您即將匯入的環境與集合的概觀。 按一下&#x200B;**匯入**。

![Adobe I/O新整合](./images/impconfirm.png)

您現在已擁有Postman所需的一切，可開始透過API與Firefly服務互動。

首先要做的就是確保您已正確驗證。 若要進行驗證，您需要請求存取權杖。

在執行任何要求之前，請確定您已選取正確的環境。 您可以驗證右上角的環境下拉式清單，以檢查目前選取的環境。

所選環境的名稱應該與此環境類似，`--aepUserLdap-- Firefly Services OAuth Credential`。

![Postman](./images/envselemea.png)

您的Postman環境和集合現已設定完畢，可正常運作。 您現在可以從Postman驗證Adobe I/O。

在&#x200B;**AdobeIO - OAuth**&#x200B;集合中，選取名稱為&#x200B;**POST — 取得存取權杖**&#x200B;的要求。 您會在&#x200B;**引數**&#x200B;下參考2個變數： `API_KEY`和`CLIENT_SECRET`。 這些變數是從選取的環境`--aepUserLdap-- Firefly Services OAuth Credential`中取得。

按一下&#x200B;**傳送**。

![Postman](./images/ioauth.png)

按一下&#x200B;**傳送**&#x200B;後，您會在Postman的&#x200B;**內文**&#x200B;區段中看到回應：

![Postman](./images/ioauthresp.png)

如果設定成功，您應該會看到包含下列資訊的類似回應：

| 索引鍵 | 值 |
|:-------------:| :---------------:| 
| token_type | **持有人** |
| access_token | **eyJhbGciOiJSU...** |
| expires_in | **86399** |

Adobe I/O已為您提供&#x200B;**bearer**-token，具有特定值（極長的access_token）和到期視窗。

我們收到的Token現在有24小時有效。 這表示24小時後，如果您要使用Postman驗證Adobe I/O，必須再次執行此請求以產生新Token。

## Firefly服務API，文字2影像

現在您可以傳送您的第一個要求至Firefly服務API。

在&#x200B;**FF - Tech Services Tech Insiders**&#x200B;集合中，選取名稱為&#x200B;**POST- Tech-I V3**&#x200B;的FireflyFirefly。 在&#x200B;**內文**&#x200B;區段中，您會看到顯示`Horses in a field`的預設提示。 按一下&#x200B;**傳送**&#x200B;讓Firefly服務產生該影像。

![Firefly](./images/ff1.png)

然後您會看到類似的回應，其中包含影像URL。 複製影像URL並在網頁瀏覽器中開啟。

![Firefly](./images/ff2.png)

您現在將看到描繪`horses in a field`的美麗影像。

![Firefly](./images/ff3.png)

在繼續進行下一個練習之前，請隨時嘗試使用API請求。

下一步： [1.1.2使用Microsoft Azure和預先簽署的URL最佳化Firefly程式](./ex2.md)

[返回模組1.1](./firefly-services.md)

[返回所有模組](./../../../overview.md)
