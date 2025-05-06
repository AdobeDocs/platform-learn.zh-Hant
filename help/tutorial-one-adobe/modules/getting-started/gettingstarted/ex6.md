---
title: 快速入門 — Adobe I/O
description: 快速入門 — Adobe I/O
kt: 5342
doc-type: tutorial
exl-id: 00f17d4f-a2c8-4e8e-a1ff-556037a60629
source-git-commit: cc8efbdbcf90607f5a9bc98a2e787b61b4cd66d9
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 設定您的Adobe I/O專案

## 建立您的Adobe I/O專案

在本練習中，Adobe I/O是用來查詢各種Adobe端點。 請依照下列步驟設定Adobe I/O。

移至[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}。

![Adobe I/O新整合](./images/iohome.png){zoomable="yes"}

請務必在熒幕右上角選取正確的例項。 您的執行個體是`--aepImsOrgName--`。

>[!NOTE]
>
> 下方熒幕擷圖顯示選取的特定組織。 完成本教學課程時，您的組織很可能有不同的名稱。 當您註冊參加本教學課程時，系統已為您提供要使用的環境詳細資訊，請依照這些指示操作。

接著，選取&#x200B;**建立新專案**。

![Adobe I/O新整合](./images/iocomp.png){zoomable="yes"}

### FIREFLY SERVICES API

您應該會看到此訊息。 選取&#x200B;**+新增至專案**&#x200B;並選擇&#x200B;**API**。

![Adobe I/O新整合](./images/adobe_io_access_api.png){zoomable="yes"}

您的熒幕應如下所示。

![Adobe I/O新整合](./images/api1.png){zoomable="yes"}

選取&#x200B;**Creative Cloud**&#x200B;並選擇&#x200B;**Firefly - Firefly Services**，然後選取&#x200B;**下一步**。

![Adobe I/O新整合](./images/api3.png){zoomable="yes"}

提供認證的名稱： `--aepUserLdap-- - One Adobe OAuth credential`並選取&#x200B;**下一步**。

![Adobe I/O新整合](./images/api4.png){zoomable="yes"}

選取預設設定檔&#x200B;**預設Firefly Services設定**，然後選取&#x200B;**儲存設定的API**。

![Adobe I/O新整合](./images/api9.png){zoomable="yes"}

您應該會看到此訊息。

![Adobe I/O新整合](./images/api10.png){zoomable="yes"}

### PHOTOSHOP SERVICES API

選取&#x200B;**+新增至專案**，然後選取&#x200B;**API**。

![Azure儲存體](./images/ps2.png){zoomable="yes"}

選取&#x200B;**Creative Cloud**&#x200B;並選擇&#x200B;**Photoshop - Firefly Services**。 選取&#x200B;**下一步**。

![Azure儲存體](./images/ps3.png){zoomable="yes"}

選取&#x200B;**下一步**。

![Azure儲存體](./images/ps4.png){zoomable="yes"}

接下來，您需要選取產品設定檔，以定義此整合可用的許可權。

選取&#x200B;**預設Firefly Services設定**&#x200B;和&#x200B;**預設Creative Cloud Automation Services設定**。

選取&#x200B;**儲存設定的API**。

![Azure儲存體](./images/ps5.png){zoomable="yes"}

您應該會看到此訊息。

![Adobe I/O新整合](./images/ps7.png){zoomable="yes"}

### ADOBE EXPERIENCE PLATFORM API

選取&#x200B;**+新增至專案**，然後選取&#x200B;**API**。

![Azure儲存體](./images/aep1.png){zoomable="yes"}

選取&#x200B;**Adobe Experience Platform**&#x200B;並選擇&#x200B;**Experience Platform API**。 選取&#x200B;**下一步**。

![Azure儲存體](./images/aep2.png){zoomable="yes"}

選取&#x200B;**下一步**。

![Azure儲存體](./images/aep3.png){zoomable="yes"}

接下來，您需要選取產品設定檔，以定義此整合可用的許可權。

選取&#x200B;**Adobe Experience Platform — 所有使用者 — PROD**。

選取&#x200B;**儲存設定的API**。

![Azure儲存體](./images/aep4.png){zoomable="yes"}

您應該會看到此訊息。

![Adobe I/O新整合](./images/aep5.png){zoomable="yes"}

### 專案名稱

按一下您的專案名稱。

![Adobe I/O新整合](./images/api13.png){zoomable="yes"}

選取&#x200B;**編輯專案**。

![Adobe I/O新整合](./images/api14.png){zoomable="yes"}

為您的整合輸入好記的名稱： `--aepUserLdap-- One Adobe tutorial`並選取&#x200B;**儲存**。

![Adobe I/O新整合](./images/api15.png){zoomable="yes"}

您的Adobe I/O專案設定現已完成。

![Adobe I/O新整合](./images/api16.png){zoomable="yes"}

## 後續步驟

移至[選項1： Postman設定](./ex7.md){target="_blank"}

移至[選項2： PostBuster設定](./ex8.md){target="_blank"}

返回[快速入門](./getting-started.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}
