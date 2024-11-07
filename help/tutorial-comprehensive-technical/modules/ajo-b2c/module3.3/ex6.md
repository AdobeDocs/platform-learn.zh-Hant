---
title: offer decisioning — 使用API測試您的決定
description: 使用API測試您的決定
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# 3.3.6使用API測試您的決定

## 3.3.6.1使用Postman處理Offer Decisioning API

將[此Offer decisioning的Postman集合](./../../../assets/postman/postman_offer-decisioning.zip)下載到您的案頭並解壓縮。 之後，您將會擁有此專案：

![OD API](./images/unzip.png)

您的案頭上現在有此檔案：

- [!UICONTROL _模組14- Decisioning Service.postman_collection.json]

在[練習2.1.3中 — 您已經安裝Postman來驗證Adobe I/O](./../../../modules/rtcdp-b2c/module2.1/ex3.md) Postman。 此練習需要再次使用Postman。

開啟Postman。 按一下&#x200B;**[!UICONTROL 匯入]**。

![Adobe I/O新整合](./images/postmanui.png)

按一下&#x200B;**[!UICONTROL 上傳檔案]**。

![Adobe I/O新整合](./images/pm1.png)

選取檔案&#x200B;**[!UICONTROL _Module 14- Decisioning Service.postman_collection.json]**，然後按一下&#x200B;**[!UICONTROL 開啟]**。

![Adobe I/O新整合](./images/pm2.png)

之後，您就可以在Postman中使用此集合。

![Adobe I/O新整合](./images/pm3.png)

您現在已擁有Postman所需的一切，可開始透過API與Adobe Experience Platform互動。

### 3.3.6.1.1清單容器

按一下以開啟要求&#x200B;**[!UICONTROL GET — 清單容器]**。

在&#x200B;**[!UICONTROL 引數]**&#x200B;下，您會看到以下內容：

- 屬性： `_instance.parentName==aepenablementfy22`

在該引數中，**[!UICONTROL aepenablementfy22]**&#x200B;是Adobe Experience Platform中使用的沙箱名稱。 您應該使用的沙箱是`--aepSandboxName--`。 由`--aepSandboxName--`取代文字&#x200B;**[!UICONTROL aepenablementfy22]**。

取代沙箱名稱后，按一下&#x200B;**[!UICONTROL 傳送]**。

![OD API](./images/api2.png)

這是回應，顯示您指定的沙箱選件容器。 請複製&#x200B;**[!UICONTROL container instanceId]** （如下所示），並將其記入您電腦上的文字檔。 您需要在下一個練習中使用此&#x200B;**[!UICONTROL container instanceId]**！

![OD API](./images/api3.png)

### 3.3.6.1.2清單版位

按一下以開啟要求&#x200B;**[!UICONTROL GET — 清單版位]**。 按一下&#x200B;**[!UICONTROL 傳送]**。

![OD API](./images/api4.png)

您現在會在優惠方案容器中看到所有可用的版位。 如您在[練習3.3.1.3](./ex1.md)中所見，您所看到的版位已在Adobe Experience Platform UI中定義。

![OD API](./images/api5.png)

### 3.3.6.1.3清單決定規則

按一下以開啟要求&#x200B;**[!UICONTROL GET — 清單決定規則]**。 按一下&#x200B;**[!UICONTROL 傳送]**。

![OD API](./images/api6.png)

在回應中，您會看到在Adobe Experience Platform UI中定義的決定規則，如同您在[練習3.3.1.4](./ex1.md)中看到的一樣。

![OD API](./images/api7.png)

### 3.3.6.1.4列出個人化優惠方案

按一下以開啟要求&#x200B;**[!UICONTROL GET — 列出個人化優惠方案]**。 按一下&#x200B;**[!UICONTROL 傳送]**。

![OD API](./images/api8.png)

在回應中，您會在[練習3.3.2.1](./ex2.md)中看到您在Adobe Experience Platform UI中定義的個人化優惠。

![OD API](./images/api9.png)

### 3.3.6.1.5列出遞補優惠

按一下以開啟要求&#x200B;**[!UICONTROL GET — 列出遞補優惠]**。 按一下&#x200B;**[!UICONTROL 傳送]**。

![OD API](./images/api10.png)

在回應中，您會在[練習3.3.2.2](./ex2.md)中看到您在Adobe Experience Platform UI中定義的遞補優惠。

![OD API](./images/api11.png)

### 3.3.6.1.6清單集合

按一下以開啟請求&#x200B;**[!UICONTROL GET — 列出集合]**。

![OD API](./images/api12.png)

在回應中，您會在[練習3.3.2.3](./ex2.md)中看到您在Adobe Experience Platform UI中定義的集合。

![OD API](./images/api13.png)

### 3.3.6.1.7取得客戶設定檔的詳細優惠方案

按一下以開啟請求&#x200B;**[!UICONTROL POST — 取得客戶設定檔的詳細優惠方案]**。 此請求與上一個請求類似，但實際上會傳回影像URL、文字等詳細資訊。

![OD API](./images/api23.png)

針對此請求（類似於先前具有類似要求的練習），您需要提供&#x200B;**[!UICONTROL xdm：placementId]**&#x200B;和&#x200B;**[!UICONTROL xdm：activityId]**&#x200B;的值，以擷取客戶的特定優惠方案詳細資料。

需要填寫欄位&#x200B;**[!UICONTROL xdm：activityId]**。 您可以在Adobe Experience Platform UI中擷取該專案，如下所示。

![OD API](./images/activityid.png)

需要填寫欄位&#x200B;**[!UICONTROL xdm：placementId]**。 您可以在Adobe Experience Platform UI中擷取該專案，如下所示。 在下列範例中，您可以看到版位&#x200B;**[!UICONTROL 網路 — 影像]**&#x200B;的placementId。

![OD API](./images/placementid.png)

移至&#x200B;**[!UICONTROL 內文]**，然後輸入您要要求優惠方案的客戶電子郵件地址。 按一下&#x200B;**[!UICONTROL 傳送]**。

![OD API](./images/api24.png)

最後，您會看到哪些個人化優惠和哪些資產需要顯示給此客戶的結果。

![OD API](./images/api25.png)

您現在已經完成此練習。

下一步： [摘要與優點](./summary.md)

[返回模組3.3](./offer-decisioning.md)

[返回所有模組](./../../../overview.md)
