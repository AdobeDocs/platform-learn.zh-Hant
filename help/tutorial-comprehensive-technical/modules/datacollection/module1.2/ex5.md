---
title: Foundation — 資料擷取 — 從離線來源擷取資料
description: Foundation — 資料擷取 — 從離線來源擷取資料
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 1%

---

# 1.2.5資料登陸區域

本練習的目標是設定具有Azure Blob儲存體的資料登陸區域Source聯結器。

Data Landing Zone是Adobe Experience Platform布建的Azure Blob儲存體介面，可讓您存取安全的雲端型檔案儲存設施，以將檔案帶入Platform。 Data Landing Zone支援SAS式驗證，其資料受到標準Azure Blob儲存安全性機制的保護，無論是在靜止狀態還是在傳輸中。 SAS式驗證可讓您透過公用網際網路連線，安全地存取您的資料登陸區域容器。

>[!NOTE]
>
> Adobe Experience Platform **對上傳至資料登陸區域容器的所有檔案強制實施嚴格的七天存留時間(TTL)**。 所有檔案會在七天後刪除。


## 1.2.5.1必要條件

若要將blob或檔案複製到Adobe Experience Platform資料登陸區域，您將使用命令列公用程式AzCopy。 您可以透過[https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)下載作業系統的版本。

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- 解壓縮下載檔案

![dlz-install-az-copy.png](./images/dlz1.png)

- 下載範例資料檔global-context-websiteinteractions.csv，其中包含範例網站互動，並將其儲存至您解壓縮&#x200B;**azcopy**&#x200B;的資料夾。

![dlz-install-az-copy.png](./images/dlz2.png)

- 開啟終端機視窗並導覽至案頭上的資料夾，您應該會看到下列內容（azcopy和global-context-websiteinteractions.csv），例如OSX上的內容：

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 1.2.5.2將資料登陸區域連線至Adobe Experience Platform

前往此URL登入Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--module2sandbox--``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的沙箱後，您會看到畫面變更，現在您已進入專屬沙箱。

![資料擷取](./images/sb1.png)

在左側功能表中，移至&#x200B;**來源**。 在來源目錄中，搜尋&#x200B;**資料登陸**。 在&#x200B;**資料登陸區域**&#x200B;卡片上，按一下&#x200B;**...**&#x200B;並選取&#x200B;**檢視認證**。

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

按一下tp copy **SASUri**。

![dlz-copy-sas-uri.png](./images/dlz-copy-sas-uri.png)

## 1.2.5.3將csv檔案複製到AEP資料登陸區域

您現在會使用AZCopy，透過Azure命令列工具將資料內嵌至Adobe Experience Platform。

在azcopy安裝位置開啟終端機，然後執行下列命令，將檔案複製到AEP的資料登陸區域：

``./azcopy copy <your-local-file> <your SASUri>``

請務必使用雙引號圍住您的SASUri。 將`<your-local-file>`取代為azcopy目錄中檔案&#x200B;**global-context-websiteinteractions.csv**&#x200B;的本機復本路徑，並將`<your SASUri>`取代為您從Adobe Experience Platform UI複製的&#x200B;**SASUri**&#x200B;值。 您的命令應該如下所示：

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

在終端機中執行上述命令後，您會看到以下內容：

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 1.2.5.4在您的資料登陸區域中查詢您的檔案

前往Adobe Experience Platform中的資料登陸區域。

選取&#x200B;**來源**，搜尋&#x200B;**資料登陸**，然後按一下&#x200B;**設定**&#x200B;按鈕。

![dlz-inspect-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

如此將可開啟資料登陸區域。 您會在資料登陸區域的&#x200B;**選取資料**&#x200B;面板中看到您剛才上傳的檔案。

![dlz-datalanding-zone-open.png](./images/dlz-datalanding-zone-open.png)

## 1.2.5.5處理您的檔案

選取您的檔案，然後選取&#x200B;**分隔符號**&#x200B;作為資料格式。 之後，您將會看到資料的預覽。 按一下&#x200B;**下一步**。

![dlz-datalanding-select-file.png](./images/dlz-datalanding-select-file.png)

您現在可以開始對應已上傳的資料，以符合資料集的XDM結構描述。

選取&#x200B;**現有的資料集**，然後選取資料集&#x200B;**示範系統 — 網站的事件資料集（全域v1.1）**。 按一下&#x200B;**下一步**。

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

現在，您可以將csv檔案的傳入來源資料，對應到資料集XDM結構描述的目標欄位。

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> 別介意對應可能發生的錯誤。 您將在下一個步驟中更正對應。

## 1.2.5.6地圖欄位

首先，按一下&#x200B;**清除所有對應**&#x200B;按鈕。 然後，您就可以從清除對應開始。

![dlz-clear-mappings.png](./images/mappings1.png)

接著，按一下&#x200B;**新增欄位型別**，然後選取&#x200B;**新增欄位**。

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

若要對應&#x200B;**ecid**&#x200B;來源欄位，請選取欄位&#x200B;**identities.ecid**&#x200B;並按一下&#x200B;**選取**。

![dlz-map-identity.png](./images/dlz-map-identity.png)

接著，按一下&#x200B;**對應目標欄位**。

![dlz-map-select-target-field.png](./images/dlz-map-select-target-field.png)

選取結構描述結構中的欄位``--aepTenantId--``.identification.core.ecid。

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

您需要對應幾個其他欄位，按一下&#x200B;**+新增欄位型別**，接著按一下&#x200B;**新增欄位**&#x200B;並新增此對應的欄位

| 來源 | 目標 |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| 時間戳記 | 時間戳記 |
| 時間戳記 | _id |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

完成時，您的畫面應該看起來像下面的畫面。 按一下&#x200B;**下一步**。

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

按一下&#x200B;**下一步**。

![dlz-default-scheduling.png](./images/dlz-default-scheduling.png)

按一下&#x200B;**完成**。

![dlz-import-finish.png](./images/dlz-import-finish.png)

## 1.2.5.7監視器資料流

若要監視您的資料流，請移至&#x200B;**來源**、**資料流**，然後按一下您的資料流：

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

載入資料可能需要幾分鐘的時間，若成功，您會看到&#x200B;**成功**&#x200B;的狀態：

![dlz-monitor-dataflow-result.png](./images/dlz-monitor-dataflow-result.png)

下一步： [摘要與優點](./summary.md)

[返回模組1.2](./data-ingestion.md)

[返回所有模組](../../../overview.md)
