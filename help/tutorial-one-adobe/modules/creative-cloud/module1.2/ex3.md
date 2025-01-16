---
title: Firefly服務快速入門
description: Firefly服務快速入門
kt: 5342
doc-type: tutorial
exl-id: 1b7b2630-864f-4982-be5d-c46b760739c3
source-git-commit: 0fe4bbf6bcc80d4fa88bc30718a1de6621f93f17
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# 1.2.3使用Workfront Fusion實現流程自動化

您的案例現在看起來像這樣。

![WF Fusion](./images/wffusion200.png)

## 1.2.3.1反複處理多個值

到目前為止，您已變更Photoshop檔案中的文字，改為使用靜態值。 為了縮放和自動化您的內容建立工作流程，需要反複處理值清單，並將這些值動態插入Photoshop檔案中。 在接下來的步驟中，您將新增一個水來反複運算現有案例中的值。

在&#x200B;**路由器**&#x200B;節點和&#x200B;**Photoshop變更文字**&#x200B;節點之間，按一下&#x200B;**扳手**&#x200B;圖示並選取&#x200B;**新增模組**。

![WF Fusion](./images/wffusion201.png)

搜尋`flow`並選取&#x200B;**流量控制**。

![WF Fusion](./images/wffusion202.png)

選取&#x200B;**迭代器**。

![WF Fusion](./images/wffusion203.png)

然後您應該擁有此專案。

![WF Fusion](./images/wffusion204.png)

雖然您可以讀取CSV檔案之類的輸入檔案，但目前，您需要透過定義文字字串並分割該文字檔案來使用基本版本的CSV檔案。

您可以按一下&#x200B;**T**&#x200B;圖示找到&#x200B;**分割**&#x200B;函式，您可在其中看到所有可用函式來操作文字值。 按一下&#x200B;**split**&#x200B;函式，您應該會看到這個專案。

![WF Fusion](./images/wffusion206.png)

split函式預期分號前的值陣列，並預期您指定分號後的分隔符號。 對於此測試，您應該使用包含2個欄位的簡單陣列，**立即購買**&#x200B;和&#x200B;**按一下這裡**，而要使用的分隔符號為&#x200B;**，**。

透過取代目前空白的&#x200B;**分割**&#x200B;函式，在&#x200B;**陣列**&#x200B;欄位中輸入此專案： `{{split("Buy now, Click here "; ",")}}`。 按一下&#x200B;**「確定」**。

![WF Fusion](./images/wffusion205.png)

您的疊代器現在已設定，如果您現在執行情境，則會執行兩次。 不過，仍然有問題，因為您目前在&#x200B;**Photoshop變更文字**&#x200B;節點中使用靜態值。 按一下&#x200B;**Photoshop變更文字**，為輸入和輸出欄位新增部分變數，而非靜態值。

![WF Fusion](./images/wffusion207.png)

在&#x200B;**要求內容**&#x200B;中，您會看到文字&#x200B;**按一下這裡**。 此文字需要取代為來自您陣列的值。

![WF Fusion](./images/wffusion208.png)

刪除文字&#x200B;**按一下這裡**，並從&#x200B;**迭代器**&#x200B;節點選取變數&#x200B;**值**&#x200B;來取代它。 這將確保Photoshop檔案中按鈕上的文字會動態更新。

![WF Fusion](./images/wffusion209.png)

您也需要更新用來在您的Azure儲存體帳戶中寫入檔案的檔案名稱。 如果檔案名稱是靜態的，則每個新的版序都將僅覆寫先前的檔案，因此您將遺失自訂的檔案。 目前的靜態檔案名稱是&#x200B;**sevoi-psd-changed-text.psd**，您現在需要更新它。 將游標放在單字`text`後面。

![WF Fusion](./images/wffusion210.png)

首先，新增連字型大小`-`，然後選取值&#x200B;**組合訂單位置**。 這將確保對於第一次反複專案，Workfront Fusion會將`-1`新增到檔案名稱、第二次反複專案`-2`等等。 按一下&#x200B;**「確定」**。

![WF Fusion](./images/wffusion211.png)

儲存您的情境，然後按一下[執行一次]****。

![WF Fusion](./images/wffusion212.png)

案例執行後，請返回Azure儲存體總管並重新整理資料夾。 之後，您應該會看到2個新建立的檔案。

![WF Fusion](./images/wffusion213.png)

下載並開啟每個檔案。 然後您應該會在按鈕上看到各種文字。 這是檔案`sevoi-psd-changed-text-1.psd`。

![WF Fusion](./images/wffusion214.png)

這是檔案`sevoi-psd-changed-text-2.psd`。

![WF Fusion](./images/wffusion215.png)

## 1.2.3.2使用webhook啟動您的情境

到目前為止，您已手動執行您的案例以進行測試。 現在來使用webhook更新您的情境，以便從外部環境啟動它。

按一下&#x200B;**+**&#x200B;圖示，搜尋&#x200B;**webhook**，然後選取&#x200B;**Webhook**。

![WF Fusion](./images/wffusion216.png)

選取&#x200B;**自訂webhook**。

拖曳並連線&#x200B;**自訂webhook**&#x200B;節點，使其連線到畫布上的第一個節點，稱為&#x200B;**初始化常數**。

![WF Fusion](./images/wffusion217.png)

按一下&#x200B;**自訂webhook**&#x200B;節點。 然後，按一下&#x200B;**新增**。

![WF Fusion](./images/wffusion218.png)

將&#x200B;**Webhook名稱**&#x200B;設定為`--aepUserLdap-- - Tutorial 1.2`。

![WF Fusion](./images/wffusion219.png)

核取&#x200B;**取得要求標題**&#x200B;的核取方塊。 按一下&#x200B;**儲存**。

![WF Fusion](./images/wffusion220.png)

您的webhook URL現已可用。 複製URL。

![WF Fusion](./images/wffusion221.png)

開啟Postman並在集合&#x200B;**FF -Firefly服務技術內幕人士**&#x200B;中新增資料夾。

![WF Fusion](./images/wffusion222.png)

為資料夾命名`--aepUserLdap-- - Workfront Fusion`。

![WF Fusion](./images/wffusion223.png)

在您剛建立的資料夾中，按一下3個點&#x200B;**...**，然後選取&#x200B;**新增要求**。

![WF Fusion](./images/wffusion224.png)

將&#x200B;**方法型別**&#x200B;設定為&#x200B;**POST**，並將webhook的URL貼到位址列。

![WF Fusion](./images/wffusion225.png)

您必須傳送自訂內文，才能從外部來源將變數元素提供給Workfront Fusion案例。 移至&#x200B;**內文**&#x200B;並選取&#x200B;**原始**。

![WF Fusion](./images/wffusion226.png)

將下列文字貼入要求內文。 按一下&#x200B;**傳送**。

```json
{
    "psdTemplate": "placeholder",
    "xlsFile": "placeholder"
}
```

![WF Fusion](./images/wffusion229.png)

返回Workfront Fusion。 您現在會在自訂webhook上看到一則訊息，顯示： **已成功判定**。

![WF Fusion](./images/wffusion227.png)

按一下&#x200B;**儲存**，然後按一下&#x200B;**執行一次**。 您的情境現在會啟用，但必須等到您再次在Postman中按一下&#x200B;**傳送**&#x200B;後才會執行。

![WF Fusion](./images/wffusion230.png)

移至Postman，然後再次按一下&#x200B;**傳送**。

![WF Fusion](./images/wffusion228.png)

您的案例將再次執行，並像之前一樣建立2個檔案。

![WF Fusion](./images/wffusion232.png)

在繼續之前，請將您的Postman請求名稱變更為`POST - Send Request to Workfront Fusion Webhook`。

![WF Fusion](./images/wffusion233.png)


下一步： [摘要與優點](./summary.md)

[返回模組1.2](./automation.md)

[返回所有模組](./../../../overview.md)
