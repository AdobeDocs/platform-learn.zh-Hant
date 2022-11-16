---
title: Foundation — 資料擷取 — 離線來源的資料擷取
description: Foundation — 資料擷取 — 離線來源的資料擷取
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 93d9f4ef-9cbd-4310-879e-d69106b70404
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# 2.5資料登陸區

在本練習中，目標是使用Azure Blob儲存設定您的資料著陸區來源連接器。

資料著陸區是由Adobe Experience Platform布建的Azure Blob儲存介面，可讓您存取安全、雲端型的檔案儲存設施，將檔案匯入Platform。 資料著陸區支援基於SAS的身份驗證，其資料在閒置和傳輸中受到標準Azure Blob儲存安全機制的保護。 基於SAS的身份驗證允許您通過公共Internet連接安全地訪問資料著陸區容器。

>[!NOTE]
>
> Adobe Experience Platform **強制執行嚴格的七天存留時間(TTL)** 上傳至「資料著陸區」容器的所有檔案。 所有檔案會在七天後刪除。


## 2.5.1必要條件

要將Blob或檔案複製到您的Adobe Experience Platform資料登陸區，您將使用命令行實用程式AzCopy。 您可以透過 [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- 將下載的檔案解壓縮

![dlz-install-az-copy.png](./images/dlz1.png)

- 下載範例資料檔案 [global-context-websiteinteractions.csv](../../assets/csv/data-ingestion/global-context-websiteinteractions.csv)，其中包含網站互動範例，並儲存至您解壓縮的資料夾 **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- 開啟「終端機」視窗並導覽至案頭上的資料夾，您應該會看到下列內容（azcopy和global-context-websiteinteractions.csv），例如在OSX上：

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 2.5.2將資料登陸區連接至Adobe Experience Platform

前往此URL登入Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

登入後，您會登陸Adobe Experience Platform首頁。

![資料擷取](./images/home.png)

繼續之前，您需要選取 **沙箱**. 要選取的沙箱已命名 ``--module2sandbox--``. 您可以按一下文字 **[!UICONTROL 生產產品]** 在螢幕上方的藍線。 選取適當的沙箱後，畫面會變更，現在您就位於專用的沙箱中。

![資料擷取](./images/sb1.png)

在左側功能表中，前往 **來源**. 在來源目錄中，搜尋 **資料登陸**. 在 **資料登陸區** 卡片，按一下 **...** 選取 **查看憑據**.

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

按一下tp copy **沙蘇里**.

![dlz-copy-sas-uri.png](./images/dlz-copy-sas-uri.png)

## 2.5.3將csv檔案複製至AEP資料登陸區

您現在將使用Azure命令列工具，使用AZCopy將資料內嵌至Adobe Experience Platform。

在azcopy安裝位置開啟終端機，並執行下列命令將檔案複製到AEP的資料登陸區：

``./azcopy copy <your-local-file> <your SASUri>``

請務必在SASUri周圍加上雙引號。 取代 `<your-local-file>` 檔案的本機副本路徑 **global-context-websiteinteractions.csv** 在azcopy目錄中，並取代 `<your SASUri>` 按 **沙蘇里** 值(從Adobe Experience Platform UI複製)。 您的命令應如下所示：

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

在您的終端機中執行上述命令後，您會看到：

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 2.5.4在資料登陸區域查閱檔案

前往Adobe Experience Platform中的資料登陸區。

選擇 **來源**，搜尋 **資料登陸** 並按一下 **設定** 按鈕。

![dlz-inspect-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

這會開啟資料登陸區。 您會看到您剛在資料登陸區域 **選擇資料** 中。

![dlz-datalanding-zone-open.png](./images/dlz-datalanding-zone-open.png)

## 2.5.5處理您的檔案

選取您的檔案並選取 **分隔** 為資料格式。 然後您會看到資料的預覽。 按&#x200B;**「下一步」**。

![dlz-datalanding-select-file.png](./images/dlz-datalanding-select-file.png)

您現在可以開始對應已上傳的資料，以符合資料集的XDM結構。

選擇 **現有資料集** 和選取資料集 **示範系統 — 網站事件資料集（全域v1.1）**. 按&#x200B;**「下一步」**。

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

現在您已準備好將從csv檔案傳入的來源資料對應至資料集XDM結構的目標欄位。

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> 請不要管對應程式的潛在錯誤。 您將在下一步中修正對應。

## 2.5.6地圖欄位

首先，按一下 **清除所有映射** 按鈕。 然後，您就可以從乾淨的對應開始。

![dlz-clear-mappings.png](./images/mappings1.png)

下一步，按一下 **新欄位類型** 然後選取 **新增欄位**.

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

對應 **ecid** 源欄位，選擇欄位 **identities.ecid** 按一下 **選擇**.

![dlz-map-identity.png](./images/dlz-map-identity.png)

下一步，按一下 **映射目標欄位**.

![dlz-map-select-target-field-png](./images/dlz-map-select-target-field.png)

選取欄位 ``--aepTenantId--``架構結構中的.identification.core.ecid。

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

您需要映射其他幾個欄位，請按一下 **+新欄位類型** 後跟 **新增欄位** 並新增此對應的欄位

| 來源 | Target |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| timestamp | timestamp |
| timestamp | _id |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

完成後，畫面應該會顯示如下。 按&#x200B;**「下一步」**。

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

按&#x200B;**「下一步」**。

![dlz-default-scheduling.png](./images/dlz-default-scheduling.png)

按一下&#x200B;**完成**。

![dlz-import-finish.png](./images/dlz-import-finish.png)

## 2.5.7監視資料流

要監視資料流，請轉到 **來源**, **資料流** 然後按一下資料流：

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

載入資料可能需要幾分鐘的時間，如果成功，您會看到的狀態為 **成功**:

![dlz-monitor-dataflow-result.png](./images/dlz-monitor-dataflow-result.png)

下一步： [摘要和優點](./summary.md)

[返回模組2](./data-ingestion.md)

[返回所有模組](../../overview.md)
