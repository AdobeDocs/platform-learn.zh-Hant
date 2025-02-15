---
title: 快速入門 — Adobe I/O
description: 快速入門 — Adobe I/O
kt: 5342
doc-type: tutorial
source-git-commit: 431f7696df12c8c133aced57c0f639c682304dee
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 設定您的Adobe I/O專案

## 建立您的Adobe I/O專案

在本練習中，Adobe I/O是用來查詢各種Adobe端點。 請依照下列步驟設定Adobe I/O。

移至[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}。

![Adobe I/O新整合](./images/iohome.png){zoomable="yes"}

請務必在熒幕右上角選取正確的例項。 您的執行個體是`--aepImsOrgName--`。
接著，選取**建立新專案**。

![Adobe I/O新整合](./images/iocomp.png){zoomable="yes"}

### Firefly服務API

您應該會看到此訊息。 選取&#x200B;**+新增至專案**&#x200B;並選擇&#x200B;**API**。

![Adobe I/O新整合](./images/adobe_io_access_api.png){zoomable="yes"}

您的熒幕應如下所示。

![Adobe I/O新整合](./images/api1.png){zoomable="yes"}

選取&#x200B;**Creative Cloud**&#x200B;並選擇&#x200B;**Firefly - Firefly服務**，然後選取&#x200B;**下一步**。

![Adobe I/O新整合](./images/api3.png){zoomable="yes"}

提供認證的名稱： `--aepUserLdap-- - One Adobe OAuth credential`並選取&#x200B;**下一步**。

![Adobe I/O新整合](./images/api4.png){zoomable="yes"}

選取預設設定檔&#x200B;**預設Firefly Services設定**，並選取&#x200B;**儲存設定的API**。

![Adobe I/O新整合](./images/api9.png){zoomable="yes"}

您應該會看到此訊息。

![Adobe I/O新整合](./images/api10.png){zoomable="yes"}

### PHOTOSHOP SERVICES API

選取&#x200B;**+新增至專案**，然後選取&#x200B;**API**。

![Azure儲存體](./images/ps2.png){zoomable="yes"}

選取&#x200B;**Creative Cloud**&#x200B;並選擇&#x200B;**Photoshop - Firefly服務**。 選取&#x200B;**下一步**。

![Azure儲存體](./images/ps3.png){zoomable="yes"}

選取&#x200B;**下一步**。

![Azure儲存體](./images/ps4.png){zoomable="yes"}

接下來，您需要選取產品設定檔，以定義此整合可用的許可權。

選取&#x200B;**預設Firefly服務組態**&#x200B;和&#x200B;**預設Creative Cloud自動化服務組態**。

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