---
title: 安裝並配置Kafka Connect和Adobe Experience Platform Sink Connector
description: 安裝並配置Kafka Connect和Adobe Experience Platform Sink Connector
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 6a7c91c2-bc92-4b9b-bd11-18cef86294d3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 0%

---

# 15.4安裝並配置Kafka Connect和Adobe Experience Platform Sink Connector

## 15.4.1下載Adobe Experience Platform Sink Connector

前往 [https://github.com/adobe/experience-platform-streaming-connect/releases](https://github.com/adobe/experience-platform-streaming-connect/releases) 並下載最新的Adobe Experience Platform Sink Connector正式版。

![卡夫卡](./images/kc1.png)

放置下載檔案， **streaming-connect-sink-0.0.14-java-11.jar**，放在您的案頭上。

![卡夫卡](./images/kc2.png)

## 15.4.2配置Kafka Connect

轉至案頭上名為的資料夾 **Kafka_AEP** 並導覽至資料夾 `kafka_2.13-3.1.0/config`.
在該資料夾中，開啟檔案 **connect-distributed.properties** 使用任何文字編輯器。

![卡夫卡](./images/kc3a.png)

在文字編輯器中，前往第34和35行，並確定設定欄位 `key.converter.schemas.enable` 和 `value.converter.schemas.enable` to `false`

```json
key.converter.schemas.enable=false
value.converter.schemas.enable=false
```

儲存您對此檔案的變更。

![卡夫卡](./images/kc3.png)

接下來，返回資料夾 `kafka_2.13-3.1.0` 並手動建立新資料夾，然後將其命名 `connectors`.

![卡夫卡](./images/kc4.png)

以滑鼠右鍵按一下資料夾，然後按一下 **資料夾處的新終端**.

![卡夫卡](./images/kc5.png)

你會看到這個。 輸入命令 `pwd` 以檢索該資料夾的完整路徑。 選取完整路徑，並將其複製到剪貼簿。

![卡夫卡](./images/kc6.png)

返回文字編輯器，到檔案 **connect-distributed.properties** 並向下捲動至最後一行（螢幕擷取中的第86行）。 您應取消註解開頭為 `# plugin.path=` 您應將完整路徑貼入名為 `connectors`. 結果應該看起來類似這樣：

`plugin.path=/Users/woutervangeluwe/Desktop/Kafka_AEP/kafka_2.13-3.1.0/connectors`

將變更儲存至檔案 **connect-distributed.properties** 並關閉文字編輯器。

![卡夫卡](./images/kc7.png)

接下來，複製您下載到名為的資料夾中的Adobe Experience Platform Sink Connector的最新正式版本 `connectors`. 之前下載的檔案名為 **streaming-connect-sink-0.0.14-java-11.jar**，您只需將其移入 `connectors` 檔案夾。

![卡夫卡](./images/kc8.png)

接下來，在 **kafka_2.13-3.1.0** 檔案夾。 以滑鼠右鍵按一下該資料夾，然後按一下 **資料夾處的新終端**.

在「終端機」視窗中，貼上以下命令： `bin/connect-distributed.sh config/connect-distributed.properties` 按一下 **輸入**. 此命令將啟動Kafka Connect，並載入Adobe Experience Platform Sink Connector的庫。

![卡夫卡](./images/kc9.png)

幾秒後，您會看到以下畫面：

![卡夫卡](./images/kc10.png)

## 15.4.3使用Postman建立Adobe Experience Platform Sink連接器

您現在可以使用Postman與Kafka Connect互動。 若要這麼做，請下載 [此Postman集合](../../assets/postman/postman_kafka.zip) 並解壓到案頭上的本地電腦。 然後，您會有一個名為 `Kafka_AEP.postman_collection.json`.

![卡夫卡](./images/kc11a.png)

您需要在Postman中匯入此檔案。 若要這麼做，請開啟Postman，按一下 **匯入**，拖放檔案 `Kafka_AEP.postman_collection.json` 進入快顯視窗，然後按一下 **匯入**.

![卡夫卡](./images/kc11b.png)

然後，您會在Postman的左側功能表中找到此集合。 按一下第一個請求， **GET可用的Kafka Connect連接器** 來開啟它。

![卡夫卡](./images/kc11c.png)

你會看到這個。 按一下藍色 **傳送** 按鈕，之後應該會看到空回應 `[]`. 空回應是因為目前未定義Kafka Connect連接器。

![卡夫卡](./images/kc11.png)

若要建立連接器，請按一下以開啟Kafka集合中的第二個請求， **POST建立AEP Sink連接器**. 你會看到這個。 11號線，上面寫著 **&quot;aep.endpoint&quot;:&quot;**，您需要貼入在練習結束時收到的HTTP API串流端點URL [15.3](./ex3.md). HTTP API串流端點URL看起來像這樣： `https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`.

![卡夫卡](./images/kc12a.png)

貼上請求後，請求的內文應如下所示。 按一下藍色 **傳送** 按鈕來建立連接器。 建立連接器後，您會立即收到回應。

![卡夫卡](./images/kc12.png)

按一下第一個請求， **GET可用的Kafka Connect連接器** 再次開啟，然後按一下藍色 **傳送** 按鈕。 您現在會看到Kafka Connect連接器已建立。

![卡夫卡](./images/kc13.png)

接下來，開啟Kafka集合中的第三個請求， **GET檢查Kafka連接器狀態**. 按一下藍色 **傳送** 按鈕，您就會收到如下所示的回應，指出連接器執行中。

![卡夫卡](./images/kc14.png)

## 15.4.4產生體驗事件

開啟新 **終端** 按一下右鍵資料夾 **kafka_2.13-3.1.0** 按一下 **資料夾處的新終端**.

![卡夫卡](./images/kafka11.png)

輸入以下命令：

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aep`

![卡夫卡](./images/kc15.png)

你會看到這個。 按Enter按鈕後面的每一行新郵件都會導致主題中傳送新訊息 **aep**.

![卡夫卡](./images/kc16.png)

您現在可以傳送訊息，此訊息會由Adobe Experience Platform Sink Connector使用，並即時擷取至Adobe Experience Platform。

讓我們做個小演示來測試。

前往 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). 使用您的Adobe ID登入後，您會看到這個。 按一下您的網站專案以開啟。

![DSN](../module0/images/web8.png)

在 **Screens** 頁面，按一下 **執行**.

![DSN](../module1/images/web2.png)

然後，您會看到示範網站已開啟。 選取URL並複製到剪貼簿。

![DSN](../module0/images/web3.png)

開啟新的無痕瀏覽器窗口。

![DSN](../module0/images/web4.png)

貼上您在上一步複製的示範網站URL。 然後系統會要求您使用Adobe ID登入。

![DSN](../module0/images/web5.png)

選取您的帳戶類型並完成登入程式。

![DSN](../module0/images/web6.png)

然後，您會在無痕瀏覽器視窗中看到您的網站載入。 對於每個演示，您都需要使用全新的無痕瀏覽器窗口來載入演示網站URL。

![DSN](../module0/images/web7.png)

按一下螢幕左上角的Adobe標誌圖示，開啟「設定檔檢視器」。

![示範](../module2/images/pv1.png)

查看「設定檔檢視器」面板和「即時客戶設定檔」，其中 **Experience CloudID** 作為此目前未知客戶的主要識別碼。

![示範](../module2/images/pv2.png)

前往註冊/登入頁面。 按一下 **建立帳戶**.

![示範](../module2/images/pv9.png)

填寫詳細資訊，然後按一下 **註冊** 之後，系統會將您重新導向至上一頁。

![示範](../module2/images/pv10.png)

開啟「設定檔檢視器」面板，然後前往「即時客戶設定檔」。 在「設定檔檢視器」面板上，您應該會看到所有個人資料顯示，例如新新增的電子郵件和電話識別碼。

![示範](../module2/images/pv11.png)

您可能會根據過去的活動看到一些體驗事件。

![卡夫卡](./images/kc19.png)

讓我們變更，並將「呼叫中心」體驗活動從Kafka傳送至Adobe Experience Platform。

請取用下列範例體驗事件裝載，並將其複製到文字編輯器中。

```json
{
  "header": {
    "datasetId": "61fe23fd242870194a6d779c",
    "imsOrgId": "--aepImsOrgID--",
    "source": {
      "name": "Launch"
    },
    "schemaRef": {
      "id": "https://ns.adobe.com/experienceplatform/schemas/b0190276c6e1e1e99cf56c99f4c07a6e517bf02091dcec90",
      "contentType": "application/vnd.adobe.xed-full+json;version=1"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/experienceplatform/schemas/b0190276c6e1e1e99cf56c99f4c07a6e517bf02091dcec90",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
      }
    },
    "xdmEntity": {
      "eventType": "callCenterInteractionKafka",
      "_id": "",
      "timestamp": "2022-02-23T09:54:12.232Z",
      "_experienceplatform": {
        "identification": {
          "core": {
            "phoneNumber": ""
          }
        },
        "interactionDetails": {
          "core": {
            "callCenterAgent": {
              "callID": "Support Contact - 3767767",
              "callTopic": "contract",
              "callFeeling": "negative"
            }
          }
        }
      }
    }
  }
}
```

你會看到這個。 您需要手動更新2個欄位：

- **_id**:請將它設為隨機id `--demoProfileLdap--1234`
- **timestamp**:將時間戳記更新為目前的日期和時間
- **phoneNumber**:輸入剛在演示網站上建立的帳戶的phoneNumber。 您可以在「設定檔檢視器」面板的下方找到它 **身分**.

您也需要檢查並可能更新下列欄位：
- **datasetId**:您需要複製資料集示範系統的資料集ID — 客服中心（全域v1.1）的事件資料集
- **imsOrgID**:您的IMS組織ID為 `--aepImsOrgId--`

>[!NOTE]
>
>欄位 **_id** 每次資料擷取都必須是唯一的。 如果您產生多個事件，請務必更新欄位 **_id** 每次都能得到新的唯一值。

![卡夫卡](./images/kc20.png)

之後您應該有這樣的項目：

![卡夫卡](./images/kc21.png)

接下來，將您的完整體驗事件複製到剪貼簿。 您的JSON裝載的空白字元需要移除，我們將使用線上工具來移除。 前往 [http://jsonviewer.stack.hu/](http://jsonviewer.stack.hu/) 來做。

![卡夫卡](./images/kc22.png)

將體驗事件貼到編輯器中，然後按一下 **移除空白字元**.

![卡夫卡](./images/kc22a.png)

接下來，選取所有輸出文字，並將其複製到剪貼簿。

![卡夫卡](./images/kc23.png)

返回您的終端機視窗。

![卡夫卡](./images/kc16.png)

將不含空格的新裝載貼入「終端機」視窗，然後按一下 **輸入**.

![卡夫卡](./images/kc23a.png)

接下來，返回您的示範網站並重新整理頁面。 您現在應該會在設定檔下方看到體驗事件 **其他事件**，如下所示：

![卡夫卡](./images/kc24.png)

>[!NOTE]
>
>如果您希望客服中心的互動顯示在「設定檔檢視器」面板上，您必須在您的專案中新增下列標籤並篩選 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)，前往標籤 **設定檔檢視器**.

![卡夫卡](./images/kc25.png)

您已完成本練習。

下一步： [摘要和優點](./summary.md)

[返回模組15](./aep-apache-kafka.md)

[返回所有模組](../../overview.md)
