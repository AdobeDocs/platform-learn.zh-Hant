---
title: 使用Microsoft Azure和預先簽署的URL最佳化Firefly程式
description: 瞭解如何使用Microsoft Azure和預先簽署的URL最佳化Firefly程式
role: Developer
level: Beginner
jira: KT-5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: da6917ec8c4e863e80eef91280e46b20816a5426
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 1%

---

# 1.1.2使用Microsoft Azure和預先簽署的URL最佳化Firefly程式

瞭解如何使用Microsoft Azure和預先簽署的URL最佳化Firefly程式。

## 1.1.2.1建立Azure訂閱

>[!NOTE]
>
>如果您已有現有的Azure訂閱，可以略過此步驟。 請繼續進行該案例的下一個練習。

移至[https://portal.azure.com](https://portal.azure.com){target="_blank"}並使用您的Azure帳戶登入。 如果您沒有電子郵件地址，請使用個人電子郵件地址來建立您的Azure帳戶。

![Azure儲存體](./images/02azureportalemail.png){zoomable="yes"}

成功登入後，您應該會看到下列畫面：

![Azure儲存體](./images/03azureloggedin.png){zoomable="yes"}

在左側功能表選取&#x200B;**所有資源**，如果您尚未訂閱，就會顯示Azure訂閱畫面。

如果您尚未訂閱，請選取&#x200B;**開始使用Azure免費試用**。

![Azure儲存體](./images/04azurestartsubscribe.png){zoomable="yes"}

填寫Azure訂閱表單，並提供您的行動電話和信用卡以進行啟用（您將有30天的免費套餐，除非您升級，否則不會向您收費）。

訂閱程式完成後，您就可以開始了。

![Azure儲存體](./images/06azuresubscriptionok.png){zoomable="yes"}

## 1.1.2.2建立Azure儲存體帳戶

搜尋`storage account`，然後選取&#x200B;**儲存帳戶**。

![Azure儲存體](./images/azs1.png){zoomable="yes"}

選取&#x200B;**+建立**。

![Azure儲存體](./images/azs2.png){zoomable="yes"}

選取您的&#x200B;**訂閱**，然後選取（或建立） **資源群組**。

在&#x200B;**儲存體帳戶名稱**&#x200B;下，使用`--aepUserLdap--`。

選取&#x200B;**檢閱+建立**。

![Azure儲存體](./images/azs3.png){zoomable="yes"}

選取「**建立**」。

![Azure儲存體](./images/azs4.png){zoomable="yes"}

確認後，選取&#x200B;**前往資源**。

![Azure儲存體](./images/azs5.png){zoomable="yes"}

您的Azure儲存體帳戶現在已可供使用。

![Azure儲存體](./images/azs6.png){zoomable="yes"}

選取&#x200B;**資料儲存體**，然後移至&#x200B;**容器**。 選取&#x200B;**+容器**。

![Azure儲存體](./images/azs7.png){zoomable="yes"}

使用`--aepUserLdap--`作為名稱，並選取&#x200B;**建立**。

![Azure儲存體](./images/azs8.png){zoomable="yes"}

您的容器現在已可供使用。

![Azure儲存體](./images/azs9.png){zoomable="yes"}

## 1.1.2.3安裝Azure儲存體總管

[下載Microsoft Azure Storage Explorer以管理您的檔案](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4){target="_blank"}。 選取適合您特定作業系統的正確版本，下載並安裝。

![Azure儲存體](./images/az10.png){zoomable="yes"}

開啟應用程式並選取&#x200B;**使用Azure登入**。

![Azure儲存體](./images/az11.png){zoomable="yes"}

選取&#x200B;**訂閱**。

![Azure儲存體](./images/az12.png){zoomable="yes"}

選取&#x200B;**Azure**，然後選取&#x200B;**下一步**。

![Azure儲存體](./images/az13.png){zoomable="yes"}

選取您的Microsoft Azure帳戶並完成驗證程式。

![Azure儲存體](./images/az14.png){zoomable="yes"}

驗證後，此訊息會出現。

![Azure儲存體](./images/az15.png){zoomable="yes"}

返回Microsoft Azure Storage Explorer應用程式，選取您的訂閱，然後選擇&#x200B;**開啟總管**。

>[!NOTE]
>
>如果您的帳戶未顯示，請按一下電子郵件地址旁的&#x200B;**齒輪**&#x200B;圖示，並選取&#x200B;**取消篩選**。

![Azure儲存體](./images/az16.png){zoomable="yes"}

您的儲存體帳戶出現在&#x200B;**儲存體帳戶**&#x200B;下。

![Azure儲存體](./images/az17.png){zoomable="yes"}

開啟&#x200B;**Blob容器**，然後選取您在上一個練習中建立的容器。

![Azure儲存體](./images/az18.png){zoomable="yes"}

## 1.1.2.4手動上傳檔案並使用影像檔案作為樣式參考

將您選擇的影像檔案或[此檔案](./images/gradient.jpg){target="_blank"}上傳至容器。

![Azure儲存體](./images/gradient.jpg)

上傳後，即可在容器中看到：

![Azure儲存體](./images/az19.png){zoomable="yes"}

在`gradient.jpg`上按一下滑鼠右鍵，然後選取&#x200B;**取得共用存取權簽章**。

![Azure儲存體](./images/az20.png){zoomable="yes"}

在&#x200B;**許可權**&#x200B;之下，只需要&#x200B;**讀取**。 選取「**建立**」。

![Azure儲存體](./images/az21.png){zoomable="yes"}

複製此影像檔案的預先簽署URL，以供下一個API請求傳送至Firefly。

![Azure儲存體](./images/az22.png){zoomable="yes"}

返回Postman開啟請求&#x200B;**POST - Firefly - T2I (styleref) V3**。
這會顯示在**內文**&#x200B;中。

![Azure儲存體](./images/az23.png){zoomable="yes"}

將預留位置URL取代為您的影像檔案預先簽署的URL，並選取&#x200B;**傳送**。

![Azure儲存體](./images/az24.png){zoomable="yes"}

在瀏覽器中開啟回應Firefly Services新影像。

![Azure儲存體](./images/az25.png){zoomable="yes"}

另一個影像會以`horses in a field`顯示，但這次的樣式與您提供做為樣式參考的影像檔案類似。

![Azure儲存體](./images/az26.png){zoomable="yes"}

## 1.1.2.5程式化檔案上傳

若要搭配Azure儲存體帳戶使用程式化檔案上傳，您必須建立新的&#x200B;**共用存取簽章(SAS)**&#x200B;權杖，其許可權可讓您寫入檔案。

在Azure儲存體總管中，用滑鼠右鍵按一下您的容器，然後選取&#x200B;**取得共用存取權簽章**。

![Azure儲存體](./images/az27.png){zoomable="yes"}

在&#x200B;**許可權**&#x200B;下，選取下列必要許可權：

- **讀取**
- **新增**
- **建立**
- **寫入**
- **清單**

選取「**建立**」。

![Azure儲存體](./images/az28.png){zoomable="yes"}

收到您的&#x200B;**共用存取簽章**&#x200B;後，請選取&#x200B;**複製**&#x200B;以複製URL。

![Azure儲存體](./images/az29.png){zoomable="yes"}

使用&#x200B;**SAS-token**&#x200B;將檔案上傳至您的Azure儲存體帳戶。

返回Postman，選取資料夾&#x200B;**FF - Firefly Services Tech Insiders**，然後選取&#x200B;**Firefly**&#x200B;資料夾中的&#x200B;**...**，然後選取&#x200B;**新增要求**。

![Azure儲存體](./images/az30.png){zoomable="yes"}

將空白要求的名稱變更為&#x200B;**上傳檔案至Azure儲存體帳戶**，將&#x200B;**要求型別**&#x200B;變更為&#x200B;**PUT**，並在URL區段中貼上SAS權杖URL，然後選取&#x200B;**內文**。

![Azure儲存體](./images/az31.png){zoomable="yes"}

接著，從本機電腦選取檔案，或使用其他位於[這裡](./images/gradient2-p.jpg){target="_blank"}的影像檔。

![漸層檔案](./images/gradient2-p.jpg)

在&#x200B;**內文**&#x200B;中，選取&#x200B;**二進位**，然後&#x200B;**選取檔案**，然後從本機電腦&#x200B;**選取**+新檔案。

![Azure儲存體](./images/az32.png){zoomable="yes"}

選取您選擇的檔案，並選取&#x200B;**開啟**。

![Azure儲存體](./images/az33.png){zoomable="yes"}

接下來，將游標放在問號&#x200B;**之前，以指定要在您的Azure儲存體帳戶中使用的檔案名稱？URL中的**&#x200B;如下：

![Azure儲存體](./images/az34.png){zoomable="yes"}

URL目前看起來像這樣，但需要變更。

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

將檔案名稱變更為`gradient2-p.jpg`，並將URL變更為包含檔案名稱，如下所示：

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![Azure儲存體](./images/az34a.png){zoomable="yes"}

接著，移至&#x200B;**標頭**&#x200B;手動新增標頭，如下所示：

| 索引鍵 | 值 |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![Azure儲存體](./images/az35.png){zoomable="yes"}

移至&#x200B;**授權**&#x200B;並將&#x200B;**驗證型別**&#x200B;設定為&#x200B;**無驗證**，然後選取&#x200B;**傳送**。

![Azure儲存體](./images/az36.png){zoomable="yes"}

接著，這個空白回應會顯示在Postman中，表示您的檔案上傳可以正常進行。

![Azure儲存體](./images/az37.png){zoomable="yes"}

返回Azure Storage Explorer重新整理資料夾的內容，新上傳的檔案隨即顯示。

![Azure儲存體](./images/az38.png){zoomable="yes"}

## 1.1.2.6程式化檔案使用方式

若要以程式設計方式長期讀取Azure儲存體帳戶的檔案，您必須建立新的&#x200B;**共用存取簽章(SAS)**&#x200B;權杖，其許可權可讓您讀取檔案。 技術上，您可以使用先前練習中建立的SAS-Token，但最佳實務是讓個別的Token只有&#x200B;**讀取**&#x200B;許可權，而個別的Token只有&#x200B;**寫入**&#x200B;許可權。

### 長期讀取SAS權杖

返回Azure儲存體總管，用滑鼠右鍵按一下您的容器，然後選取&#x200B;**取得共用存取權簽章**。

![Azure儲存體](./images/az27.png){zoomable="yes"}

在&#x200B;**許可權**&#x200B;下，選取下列必要許可權：

- **讀取**
- **清單**

將&#x200B;**到期時間**&#x200B;設定為從現在起的1年。

選取「**建立**」。

![Azure儲存體](./images/az100.png){zoomable="yes"}

複製URL並將其寫入您電腦上的檔案中，以取得具有讀取許可權的長期SAS權杖。

![Azure儲存體](./images/az101.png){zoomable="yes"}

您的URL應如下所示：

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

您可以從上述URL衍生出一些值：

- `AZURE_STORAGE_URL`：`https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`：`vangeluw`
- `AZURE_STORAGE_SAS_READ`：`?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### 長期寫入SAS權杖

返回Azure儲存體總管，用滑鼠右鍵按一下您的容器，然後選取&#x200B;**取得共用存取權簽章**。

![Azure儲存體](./images/az27.png){zoomable="yes"}

在&#x200B;**許可權**&#x200B;下，選取下列必要許可權：

- **讀取**
- **清單**
- **新增**
- **建立**
- **寫入**

將&#x200B;**到期時間**&#x200B;設定為從現在起的1年。

選取「**建立**」。

![Azure儲存體](./images/az102.png){zoomable="yes"}

複製URL並將其寫入您電腦上的檔案中，以取得具有讀取許可權的長期SAS權杖。

![Azure儲存體](./images/az103.png){zoomable="yes"}

您的URL應如下所示：

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

您可以從上述URL衍生出一些值：

- `AZURE_STORAGE_URL`：`https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`：`vangeluw`
- `AZURE_STORAGE_SAS_READ`：`?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`：`?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Postman中的變數

如上節所述，讀取和寫入權杖中都有一些常見的變數。

接下來，您需要在Postman中建立變數，以儲存上述SAS-Token的各種元素。 兩個URL中的某些值相同：

- `AZURE_STORAGE_URL`：`https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`：`vangeluw`
- `AZURE_STORAGE_SAS_READ`：`?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`：`?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

對於未來的API互動，主要變更的是資產名稱，而上述變數維持不變。 在此情況下，建議您在Postman中建立變數，如此您就不需要每次都手動指定它們。

在Postman中，選取&#x200B;**環境**，開啟&#x200B;**所有變數**&#x200B;並選取&#x200B;**環境**。

![Azure儲存體](./images/az104.png){zoomable="yes"}

在顯示的表格中建立這4個變數，並針對欄&#x200B;**初始值**&#x200B;和&#x200B;**目前值**，輸入您特定的個人值。

- `AZURE_STORAGE_URL`：您的url
- `AZURE_STORAGE_CONTAINER`：您的容器名稱
- `AZURE_STORAGE_SAS_READ`：您的SAS讀取權杖
- `AZURE_STORAGE_SAS_WRITE`：您的SAS寫入權杖

選取「**儲存**」。

![Azure儲存體](./images/az105.png){zoomable="yes"}

### PostBuster中的變數

如上節所述，讀取和寫入權杖中都有一些常見的變數。

接下來，您需要在PostBuster中建立變數，以儲存上述SAS-Token的各種元素。 兩個URL中的某些值相同：

- `AZURE_STORAGE_URL`：`https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`：`vangeluw`
- `AZURE_STORAGE_SAS_READ`：`?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`：`?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

開啟PostBuster。 選取&#x200B;**基本環境**，然後按一下&#x200B;**編輯**&#x200B;圖示以開啟基本環境。

![Azure儲存體](./images/pbbe1.png)

然後您會看到4個空白變數。 在這裡輸入您的Azure儲存體帳戶詳細資料。

![Azure儲存體](./images/pbbe2.png)

您的基本環境檔案現在看起來應該像這樣。 按一下 **關閉**。

![Azure儲存體](./images/pbbe3.png)

### 測試您的設定

在先前的練習中，您請求&#x200B;**Firefly - T2I (styleref) V3**&#x200B;的&#x200B;**內文**&#x200B;看起來像這樣：

`"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

![Azure儲存體](./images/az24.png){zoomable="yes"}

將URL變更為：

`"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

選取&#x200B;**傳送**&#x200B;以測試您所做的變更。

![Azure儲存體](./images/az106.png){zoomable="yes"}

如果變數已正確設定，則會傳回影像URL。

![Azure儲存體](./images/az107.png){zoomable="yes"}

開啟影像URL以驗證您的影像。

![Azure儲存體](./images/az108.jpg)

## 後續步驟

移至[使用Photoshop API](./ex3.md){target="_blank"}

返回[Adobe Firefly Services概觀](./firefly-services.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}