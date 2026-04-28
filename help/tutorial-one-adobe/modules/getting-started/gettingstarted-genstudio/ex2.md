---
title: 快速入門 — Adobe I/O
description: 快速入門 — Adobe I/O
kt: 5342
doc-type: tutorial
source-git-commit: 2a552768bb4d0fcc46cb91e0e4afae247b946b16
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---

# 設定您的Adobe I/O專案

## 影片

在這段影片中，您將獲得本練習中所有步驟的說明和示範。

>[!VIDEO](https://video.tv.adobe.com/v/3476494?quality=12&learn=on)

## 建立您的Adobe I/O專案

在本練習中，Adobe I/O是用來查詢各種Adobe端點。 請依照下列步驟設定Adobe I/O。

移至[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}。

![Adobe I/O新整合](./images/iohome.png)

請務必在熒幕右上角選取正確的例項。 您的執行個體是`--aepImsOrgName--`。

>[!NOTE]
>
> 下方熒幕擷圖顯示選取的特定組織。 完成本教學課程時，您的組織很可能有不同的名稱。 當您註冊參加本教學課程時，系統已為您提供要使用的環境詳細資訊，請依照這些指示操作。

接著，選取&#x200B;**建立新專案**。

![Adobe I/O新整合](./images/iocomp.png)

### FIREFLY SERVICES API

>[!IMPORTANT]
>
>根據您選取的學習路徑，您可能無法存取Firefly Services API。 您必須位於學習路徑&#x200B;**Firefly**、**Workfront Fusion**、**全部**，或正在參加&#x200B;**現場現場研討會**，才能存取Firefly Services API。 如果您不在其中一個學習路徑上，可以略過此步驟。

您應該會看到此訊息。 選取&#x200B;**+新增至專案**&#x200B;並選擇&#x200B;**API**。

![Adobe I/O新整合](./images/adobe_io_access_api.png)

選取&#x200B;**Adobe Firefly Services**&#x200B;並選擇&#x200B;**Firefly - Firefly Services**，然後選取&#x200B;**下一步**。

![Adobe I/O新整合](./images/api3.png)

提供認證的名稱： `--aepUserLdap-- - One Adobe OAuth credential`並選取&#x200B;**下一步**。

![Adobe I/O新整合](./images/api4.png)

選取預設設定檔&#x200B;**預設Firefly Services設定**，然後選取&#x200B;**儲存設定的API**。

![Adobe I/O新整合](./images/api9.png)

您應該會看到此訊息。

![Adobe I/O新整合](./images/api10.png)

### PHOTOSHOP SERVICES API

>[!IMPORTANT]
>
>根據您選取的學習路徑，您可能無法存取Photoshop Services API。 您必須位於學習路徑&#x200B;**Firefly**、**Workfront Fusion**、**全部**，或正在參加&#x200B;**現場現場研討會**，才能存取Photoshop Services API。 如果您不在其中一個學習路徑上，可以略過此步驟。
>
>選取&#x200B;**+新增至專案**，然後選取&#x200B;**API**。

![Azure儲存空間](./images/ps2.png)

選取&#x200B;**Adobe Firefly Services**&#x200B;並選擇&#x200B;**Photoshop - Firefly Services**。 選取&#x200B;**下一步**。

![Azure儲存空間](./images/ps3.png)

選取&#x200B;**下一步**。

![Azure儲存空間](./images/ps4.png)

接下來，您需要選取產品設定檔，以定義此整合可用的許可權。

選取&#x200B;**預設Firefly Services設定**&#x200B;和&#x200B;**預設Creative Cloud Automation Services設定**。

選取&#x200B;**儲存設定的API**。

![Azure儲存空間](./images/ps5.png)

您應該會看到此訊息。

![Adobe I/O新整合](./images/ps7.png)

### ADOBE EXPERIENCE PLATFORM API

>[!IMPORTANT]
>
>根據您選取的學習路徑，您可能無法存取Adobe Experience Platform API。 You will only have access to Adobe Experience Platform API if you&#39;re on the learning path **AEP + Apps**, **ALL**, or when you&#39;re attending a **live in-person workshop**. 如果您不在其中一個學習路徑上，可以略過此步驟。

選取&#x200B;**+新增至專案**，然後選取&#x200B;**API**。

![Azure儲存空間](./images/aep1.png)

Select **Adobe Experience Platfrom** and choose **Experience Platform API**. 選取&#x200B;**下一步**。

![Azure儲存空間](./images/aep2.png)

選取&#x200B;**下一步**。

![Azure儲存空間](./images/aep3.png)

接下來，您需要選取產品設定檔，以定義此整合可用的許可權。

Select **Adobe Experience Platform - All Users - PROD**.

>[!NOTE]
>
>The name of the Product Profile for AEP is dependent on how the environment was configured. If you don&#39;t see the above mentioned product profile, you may have a product profile that is called **Default Production All Access**. If you&#39;re not sure which one to choose, ask your AEP System Admin.

選取&#x200B;**儲存設定的API**。

![Azure儲存空間](./images/aep4.png)

您應該會看到此訊息。

![Adobe I/O新整合](./images/aep5.png)

### Frame.io API

>[!IMPORTANT]
>
>Depending on the learning path that you selected, you may not have access to Frame.io API. You will only have access to Frame.io API if you&#39;re on the learning path **Workfront Fusion**, **ALL**, or when you&#39;re attending a **live in-person workshop**. 如果您不在其中一個學習路徑上，可以略過此步驟。

選取&#x200B;**+新增至專案**，然後選取&#x200B;**API**。

![Azure儲存空間](./images/fiops2.png)

Select **Creative Cloud** and choose **Frame.io API**. 選取&#x200B;**下一步**。

![Azure儲存空間](./images/fiops3.png)

選取&#x200B;**伺服器對伺服器驗證**，然後按一下&#x200B;**下一步**。

![Azure儲存空間](./images/fiops4.png)

選取&#x200B;**OAuth伺服器對伺服器**，然後按一下[下一步]&#x200B;**。**

![Azure儲存空間](./images/fiops5.png)

接下來，您需要選取產品設定檔，以定義此整合可用的許可權。

選取&#x200B;**預設Frame.io Enterprise - Prime設定**，然後按一下&#x200B;**儲存設定的API**。

![Azure儲存空間](./images/fiops6.png)

您應該會看到此訊息。

![Adobe I/O新整合](./images/fiops7.png)

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

移至[選項1： Postman設定](./ex3.md){target="_blank"}

移至[選項2： PostBuster設定](./ex4.md){target="_blank"}

返回[快速入門 — GenStudio](./getting-started-genstudio.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}
