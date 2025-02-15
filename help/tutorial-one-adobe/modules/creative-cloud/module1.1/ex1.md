---
title: Firefly服務快速入門
description: 瞭解如何使用Postman和Adobe I/O來查詢Adobe Firefly Services API
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 219945c74c620b9a4b93cb2b7462137118d42d33
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# 1.1.1 Firefly服務快速入門

瞭解如何使用Postman和Adobe I/O來查詢Adobe Firefly Services API。

## 1.1.1.1設定您的Adobe I/O專案

在本練習中，Adobe I/O是用來查詢Firefly Services API。 請依照下列步驟設定Adobe I/O。

1. 移至[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}。

![Adobe I/O新整合](./images/iohome.png){zoomable="yes"}

1. 請務必在熒幕右上角選取正確的例項。 您的執行個體是`--aepImsOrgName--`。 接著，選取&#x200B;**建立新專案**。

![Adobe I/O新整合](./images/iocomp.png){zoomable="yes"}

1. 選取&#x200B;**+新增至專案**&#x200B;並選擇&#x200B;**API**。

![Adobe I/O新整合](./images/adobe_io_access_api.png){zoomable="yes"}

您的熒幕應如下所示。

![Adobe I/O新整合](./images/api1.png){zoomable="yes"}

1. 選取&#x200B;**Creative Cloud**&#x200B;並選擇&#x200B;**Firefly - Firefly服務**，然後選取&#x200B;**下一步**。

![Adobe I/O新整合](./images/api3.png){zoomable="yes"}

1. 提供認證的名稱： `--aepUserLdap-- - Firefly Services OAuth credential`並選取&#x200B;**下一步**。

![Adobe I/O新整合](./images/api4.png){zoomable="yes"}

1. 選取預設設定檔&#x200B;**預設Firefly Services設定**，並選取&#x200B;**儲存設定的API**。

![Adobe I/O新整合](./images/api9.png){zoomable="yes"}

您的Adobe I/O整合現已準備就緒。

![Adobe I/O新整合](./images/api11.png){zoomable="yes"}

## 1.1.1.2下載Postman環境

1. 選取「下載Postman **」，然後選擇「** OAuth伺服器對伺服器&#x200B;**」以下載Postman環境。**

![Adobe I/O新整合](./images/iopm.png){zoomable="yes"}

1. 選取您的專案名稱。

![Adobe I/O新整合](./images/api13.png){zoomable="yes"}

1. 選取&#x200B;**編輯專案**。

![Adobe I/O新整合](./images/api14.png){zoomable="yes"}

1. 為您的整合輸入好記的名稱： `--aepUserLdap-- Firefly`並選取&#x200B;**儲存**。

![Adobe I/O新整合](./images/api15.png){zoomable="yes"}

您的Adobe I/O整合設定現已完成。

![Adobe I/O新整合](./images/api16.png){zoomable="yes"}

## 1.1.1.3 Postman驗證至Adobe I/O

1. 在[Postman下載](https://www.postman.com/downloads/){target="_blank"}下載並安裝作業系統的相關Postman版本。

![Adobe I/O新整合](./images/getstarted.png){zoomable="yes"}

1. 啟動應用程式。

Postman中有2個概念：「環境」和「集合」。

- 環境檔案包含您所有大致一致的環境變數。 在環境中，您可以找到Adobe環境的IMSOrg之類的專案，以及使用者端ID和其他專案之類的安全性憑證。 您先前在Adobe I/O設定期間下載了名為&#x200B;**`oauth_server_to_server.postman_environment.json`**&#x200B;的環境檔案。

- 集合包含您可以使用的許多API請求。 我們將使用2個集合
   - 1個用於驗證Adobe I/O的集合
   - 1此單元練習的集合

1. 將[postman-ff.zip](./../../../assets/postman/postman-ff.zip)下載到您的本機案頭。

![Adobe I/O新整合](./images/pmfolder.png){zoomable="yes"}

在&#x200B;**postman.zip**&#x200B;檔案中有以下檔案：

    - &#39;Adobe IO - OAuth.postman_collection.json&#39;
    - &#39;FF - Firefly服務技術內部人員.postman_collection.json&#39;

1. 解壓縮&#x200B;**postman-ff.zip**，並將下列2個檔案儲存在您案頭的資料夾中：
- Adobe IO - OAuth.postman_collection.json
- FF - Firefly服務技術內幕人士.postman_collection.json
- oauth_server_to_server.postman_environment.json

![Adobe I/O新整合](./images/pmfolder1.png){zoomable="yes"}

1. 在Postman中，選取&#x200B;**匯入**。

![Adobe I/O新整合](./images/postmanui.png){zoomable="yes"}

1. 選取&#x200B;**檔案**。

![Adobe I/O新整合](./images/choosefiles.png){zoomable="yes"}

1. 從資料夾中選擇三個檔案，然後選取&#x200B;**開啟**&#x200B;和&#x200B;**匯入**。

![Adobe I/O新整合](./images/selectfiles.png){zoomable="yes"}

![Adobe I/O新整合](./images/impconfirm.png){zoomable="yes"}

沒有，您已擁有Postman中所需的一切，可以開始透過API與Firefly服務互動。

## 1.1.1.4要求存取權杖

接下來，為確保您經過正確驗證，您需要請求存取權杖。

1. 請確認右上角的環境下拉式清單，在執行任何要求之前，請確定您已選取正確的環境。 所選環境的名稱應該與此環境類似，`--aepUserLdap-- Firefly Services OAuth Credential`。

![Postman](./images/envselemea1.png){zoomable="yes"}

所選環境的名稱應該與此環境類似，`--aepUserLdap-- Firefly Services OAuth Credential`。

![Postman](./images/envselemea.png){zoomable="yes"}

現在您的Postman環境和集合已設定好並正常運作，您可以從Postman向Adobe I/O進行驗證。

1. 在&#x200B;**Adobe IO - OAuth**&#x200B;集合中，選取名為&#x200B;**POST - Get Access Token**&#x200B;的要求，並選取&#x200B;**傳送**。

請注意，在&#x200B;**查詢引數**&#x200B;下，參考了兩個變數： `API_KEY`和`CLIENT_SECRET`。 這些變數是從選取的環境`--aepUserLdap-- Firefly Services OAuth Credential`中取得。

![Postman](./images/ioauth.png){zoomable="yes"}

如果成功，Postman的&#x200B;**內文**&#x200B;區段中會顯示包含持有人權杖、存取權杖和到期時間視窗的回應。

![Postman](./images/ioauthresp.png){zoomable="yes"}


您應該會看到包含下列資訊的類似回應：

| 索引鍵 | 值 |
|:-------------:| :---------------:| 
| token_type | **持有人** |
| access_token | **eyJhbGciOiJSU...** |
| expires_in | **86399** |

Adobe I/O **bearer-token**&#x200B;具有特定值（極長的access_token）和到期視窗，現在有效期為24小時。 這表示24小時後，如果您要使用Postman驗證Adobe I/O，必須再次執行此請求以產生新Token。

## 1.1.1.5 Firefly Services API，文字2影像

現在您已準備好將您的第一個要求傳送至Firefly Services API。

1. 從&#x200B;**FF - Firefly服務技術內部人士**&#x200B;集合中選取名為&#x200B;**POST - Firefly - T2I V3**&#x200B;的請求。

![Firefly](./images/ff1.png){zoomable="yes"}

1. 從回應中複製影像URL，然後在您的網頁瀏覽器中開啟以檢視影像。

![Firefly](./images/ff2.png){zoomable="yes"}

您應該會看到描繪`horses in a field`的美麗影像。

![Firefly](./images/ff3.png){zoomable="yes"}

在繼續進行下一個練習之前，請隨時嘗試使用API請求。

## 後續步驟

移至[使用Microsoft Azure和預先簽署的URL最佳化您的Firefly程式](./ex2.md){target="_blank"}

返回[Adobe Firefly服務總覽](./firefly-services.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}
