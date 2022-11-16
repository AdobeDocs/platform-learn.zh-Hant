---
title: offer decisioning — 使用API測試您的決策
description: 使用API測試您的決策
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 0091c31f-0b54-4d40-a82b-3bf688db8a1f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# 9.6使用API測試您的決策

## 9.6.1使用Offer decisioningAPI，使用Postman

下載 [此Postman集合供Offer decisioning](./../../assets/postman/postman_offer-decisioning.zip) 將檔案解壓縮至案頭。 然後，您會擁有此功能：

![OD API](./images/unzip.png)

您的案頭上現在有此檔案：

- [!UICONTROL _Module 14 — 決策服務.postman_collection.json]

在 [練習3.3.3 -Postman驗證以Adobe I/O](./../../modules/module3/ex3.md) 您已安裝Postman。 在本練習中，您需要再次使用Postman。

開啟Postman。 按一下&#x200B;**[!UICONTROL 「匯入」]**。

![Adobe I/O新整合](./images/postmanui.png)

按一下 **[!UICONTROL 上傳檔案]**.

![Adobe I/O新整合](./images/pm1.png)

選取檔案 **[!UICONTROL _Module 14 — 決策服務.postman_collection.json]** 按一下 **[!UICONTROL 開啟]**.

![Adobe I/O新整合](./images/pm2.png)

之後，您就能在Postman中取得此集合。

![Adobe I/O新整合](./images/pm3.png)

現在，Postman提供您開始透過API與Adobe Experience Platform互動所需的一切。

### 9.6.1.1清單容器

按一下以開啟請求 **[!UICONTROL GET — 清單容器]**.

在 **[!UICONTROL Params]**，您會看到以下內容：

- 屬性： `_instance.parentName==aepenablementfy22`

在那個參數里， **[!UICONTROL aepenablementfy22]** 是Adobe Experience Platform中使用的沙箱名稱。 您應使用的沙箱為 `--aepSandboxId--`. 取代文字 **[!UICONTROL aepenablementfy22]** by `--aepSandboxId--`.

取代沙箱名稱后，按一下 **[!UICONTROL 傳送]**.

![OD API](./images/api2.png)

此為回應，會顯示您指定之沙箱的優惠方案容器。 請複製 **[!UICONTROL container instanceId]** 如下所示，並在電腦的文字檔案中記下來。 你需要用這個 **[!UICONTROL container instanceId]** 下次練習！

![OD API](./images/api3.png)

### 9.6.1.2清單位置

按一下以開啟請求 **[!UICONTROL GET — 清單位置]**. 按一下 **[!UICONTROL 傳送]**.

![OD API](./images/api4.png)

您現在可以在優惠方案容器中看到所有可用版位。 您看到的版位是在Adobe Experience Platform UI中定義，如 [練習9.1.3](./ex1.md).

![OD API](./images/api5.png)

### 9.6.1.3清單決定規則

按一下以開啟請求 **[!UICONTROL GET — 清單決策規則]**. 按一下 **[!UICONTROL 傳送]**.

![OD API](./images/api6.png)

在回應中，您會在Adobe Experience Platform UI中看到您定義的決策規則，如 [練習9.1.4](./ex1.md).

![OD API](./images/api7.png)

### 9.6.1.4列出個人化優惠方案

按一下以開啟請求 **[!UICONTROL GET — 列出個人化優惠方案]**. 按一下 **[!UICONTROL 傳送]**.

![OD API](./images/api8.png)

在回應中，您會在Adobe Experience Platform UI中看到您定義的個人化優惠方案，位於 [練習9.2.1](./ex2.md).

![OD API](./images/api9.png)

### 9.6.1.5列出回退優惠方案

按一下以開啟請求 **[!UICONTROL GET — 列出回退優惠方案]**. 按一下 **[!UICONTROL 傳送]**.

![OD API](./images/api10.png)

在回應中，您會看到您在Adobe Experience Platform UI中定義的備援優惠方案(位於 [練習9.2.2](./ex2.md).

![OD API](./images/api11.png)

### 9.6.1.6清單集合

按一下以開啟請求 **[!UICONTROL GET — 清單集合]**.

![OD API](./images/api12.png)

在回應中，您會在Adobe Experience Platform UI中看到您定義的集合，位於 [練習9.2.3](./ex2.md).

![OD API](./images/api13.png)

### 9.6.1.7取得客戶設定檔的詳細優惠方案

按一下以開啟請求 **[!UICONTROL POST — 取得客戶設定檔的詳細優惠方案]**. 此請求與上一個類似，但實際上會傳回影像URL、文字等詳細資訊。

![OD API](./images/api23.png)

對於此請求，與先前有類似需求的練習類似，您需要提供 **[!UICONTROL xdm:placementId]** 和 **[!UICONTROL xdm:activityId]** 以擷取客戶的特定優惠方案詳細資訊。

欄位 **[!UICONTROL xdm:activityId]** 需要填。 您可以在Adobe Experience Platform UI中擷取，如下所示。

![OD API](./images/activityid.png)

欄位 **[!UICONTROL xdm:placementId]** 需要填。 您可以在Adobe Experience Platform UI中擷取，如下所示。 在以下範例中，您可以看到版位的placementId **[!UICONTROL Web — 影像]**.

![OD API](./images/placementid.png)

前往 **[!UICONTROL 主體]** 並輸入您想要向其申請優惠方案的客戶的電子郵件地址。 按一下 **[!UICONTROL 傳送]**.

![OD API](./images/api24.png)

最後，您將會看到哪些個人化優惠方案的結果，以及需要向此客戶顯示哪些資產。

![OD API](./images/api25.png)

您已完成本練習。

下一步： [摘要和優點](./summary.md)

[返回模組9](./offer-decisioning.md)

[返回所有模組](./../../overview.md)
