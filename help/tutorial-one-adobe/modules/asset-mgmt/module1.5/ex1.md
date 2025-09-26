---
title: Adobe Commerce as a Cloud Service快速入門
description: Adobe Commerce as a Cloud Service快速入門
kt: 5342
doc-type: tutorial
exl-id: 8603c8e2-c3ba-4976-9703-cef9e63924b8
source-git-commit: 7280f6b7d3579226f2d8c7f94e75ca8d3f2941cc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 1.5.1 Adobe Commerce as a Cloud Service快速入門

移至[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 確定您處於正確的環境，應該命名為`--aepImsOrgName--`。 按一下&#x200B;**Commerce**。

![AEM Assets](./images/accs1.png)

## 1.5.1.1建立您的ACCS執行個體

您應該會看到此訊息。 按一下&#x200B;**+新增執行個體**。

![AEM Assets](./images/accs2.png)

填寫欄位，如下所示：

- **執行個體名稱**： `--aepUserLdap-- - ACCS`
- **環境**： `Sandbox`
- **地區**： `North America`

按一下&#x200B;**新增執行個體**。

![AEM Assets](./images/accs3.png)

正在建立您目前的執行個體。 這可能需要5到10分鐘。

![AEM Assets](./images/accs4.png)

執行個體準備就緒後，按一下您的執行個體以開啟它。

![AEM Assets](./images/accs5.png)

## 1.5.1.2設定您的CitiSignal存放區

您應該會看到此訊息。 按一下&#x200B;**使用Adobe ID**&#x200B;登入，然後登入。

![AEM Assets](./images/accs6.png)

登入後，您應該會看到此首頁。 第一步是在Commerce中設定CitiSignal商店。 按一下&#x200B;**商店**。

![AEM Assets](./images/accs7.png)

按一下&#x200B;**所有商店**。

![AEM Assets](./images/accs8.png)

按一下&#x200B;**建立網站**。

![AEM Assets](./images/accs9.png)

填寫欄位，如下所示：

- **名稱**： `CitiSignal`
- **代碼**： `citisignal`

按一下&#x200B;**儲存網站**。

![AEM Assets](./images/accs10.png)

然後您應該會回到這裡。 按一下&#x200B;**建立存放區**。

![AEM Assets](./images/accs11.png)

填寫欄位，如下所示：

- **網站**： `CitiSignal`
- **名稱**： `CitiSignal`
- **代碼**： `citisignal`
- **根類別**： `Default Category`

按一下&#x200B;**儲存存放區**。

![AEM Assets](./images/accs12.png)

然後您應該會回到這裡。 按一下&#x200B;**建立存放區檢視**。

![AEM Assets](./images/accs13.png)

填寫欄位，如下所示：

- **存放區**： `CitiSignal`
- **名稱**： `CitiSignal`
- **代碼**： `citisignal`
- **狀態**： `Enabled`

按一下&#x200B;**儲存存放區檢視**。

![AEM Assets](./images/accs14.png)

之後，您應該會看到此訊息。 按一下&#x200B;**「確定」**。

![AEM Assets](./images/accs15.png)

然後您應該會回到這裡。 按一下&#x200B;**CitiSignal**&#x200B;網站以開啟。

![AEM Assets](./images/accs16.png)

核取核取方塊以將此網站設為預設網站。

按一下&#x200B;**儲存網站**。

![AEM Assets](./images/accs16a.png)

然後您應該會回到這裡。

![AEM Assets](./images/accs16.png)

## 1.5.1.3設定類別和產品

移至&#x200B;**目錄**，然後選取&#x200B;**類別**。

![AEM Assets](./images/accs17.png)

選取&#x200B;**預設類別**，然後按一下&#x200B;**新增子類別**。

![AEM Assets](./images/accs18.png)

輸入名稱`Phones`，然後按一下&#x200B;**儲存**。

![AEM Assets](./images/accs19.png)

選取&#x200B;**預設類別**，然後再次按一下&#x200B;**新增子類別**。

![AEM Assets](./images/accs20.png)

輸入名稱`Watches`，然後按一下&#x200B;**儲存**。

![AEM Assets](./images/accs21.png)

之後，您應該會建立2個類別。

![AEM Assets](./images/accs22.png)

接著，移至&#x200B;**目錄**，然後選取&#x200B;**產品**。

![AEM Assets](./images/accs23.png)

您應該會看到此訊息。 按一下&#x200B;**新增產品**。

![AEM Assets](./images/accs24.png)

設定您的產品，如下所示：

- **產品名稱**： `iPhone Air`
- **SKU**： `iPhone-Air`
- **價格**： `999`
- **數量**： `10000`
- **類別**：選取`Phones`

按一下&#x200B;**儲存**。

![AEM Assets](./images/accs25.png)

向下捲動至&#x200B;**組態**&#x200B;並按一下&#x200B;**建立組態**。

![AEM Assets](./images/accs26.png)

您應該會看到此訊息。 按一下&#x200B;**建立新屬性**。

![AEM Assets](./images/accs27.png)

將&#x200B;**預設標籤**&#x200B;設定為`Storage`，然後按一下&#x200B;**管理選項**&#x200B;下的&#x200B;**新增選項**。

![AEM Assets](./images/accs28.png)

在全部3個資料行中使用名稱`256GB`設定第一個選項，然後再次按一下&#x200B;**新增選項**。

![AEM Assets](./images/accs29.png)

在全部3個資料行中使用名稱`512GB`設定第二個選項，然後再次按一下&#x200B;**新增選項**。

![AEM Assets](./images/accs30.png)

在全部3個資料行中使用名稱`1TB`設定第三個選項。

![AEM Assets](./images/accs31.png)

向下捲動至&#x200B;**店面內容**。 將下列選項設定為&#x200B;**是**：

- **用於搜尋**
- **允許Storefront上的HTML標籤**
- **顯示在店面的目錄頁面上**
- **用於產品清單**

![AEM Assets](./images/accs32.png)

向上捲動並按一下&#x200B;**儲存屬性**。

![AEM Assets](./images/accs33.png)

您應該會看到此訊息。 選取&#x200B;**色彩**&#x200B;和&#x200B;**儲存**&#x200B;的兩個屬性，然後按一下&#x200B;**下一步**。

![AEM Assets](./images/accs34.png)

您應該會看到此訊息。 您現在需要新增可用的色彩選項。 若要這麼做，請按一下&#x200B;**建立新值**。

![AEM Assets](./images/accs35.png)

輸入值`Sky-Blue`並按一下&#x200B;**建立新值**。

![AEM Assets](./images/accs36.png)

輸入值`Light-Gold`並按一下&#x200B;**建立新值**。

![AEM Assets](./images/accs37.png)

輸入值`Cloud-White`並按一下&#x200B;**建立新值**。

![AEM Assets](./images/accs38.png)

輸入值`Space-Black`。 按一下&#x200B;**全選**

![AEM Assets](./images/accs39.png)

選取&#x200B;**儲存體**&#x200B;下的全部3個選項，然後按一下&#x200B;**下一步**。

![AEM Assets](./images/accs40.png)

保留預設設定，然後按一下&#x200B;**下一步**。

![AEM Assets](./images/accs41.png)

您應該會看到此訊息。 按一下&#x200B;**產生產品**。

![AEM Assets](./images/accs42.png)

將每個產品的&#x200B;**數量**&#x200B;設定為`10000`。 按一下&#x200B;**儲存**。

![AEM Assets](./images/accs43.png)

向下捲動至網站中的&#x200B;**產品**，並勾選&#x200B;**CitiSignal**&#x200B;的核取方塊。

按一下&#x200B;**儲存**。

![AEM Assets](./images/accs44.png)

按一下「**確認**」。

![AEM Assets](./images/accs45.png)

您應該會看到此訊息。 按一下&#x200B;**上一步**。

![AEM Assets](./images/accs46.png)

您現在在產品目錄中看到產品&#x200B;**iPhone Air**&#x200B;及其變數。

![AEM Assets](./images/accs47.png)

下一步：[將ACCS連線至AEM Sites CS/EDS店面](./ex2.md){target="_blank"}

返回[Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}
