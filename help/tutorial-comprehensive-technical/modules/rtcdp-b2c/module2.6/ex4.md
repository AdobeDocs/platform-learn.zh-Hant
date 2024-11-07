---
title: 安裝及設定Kafka Connect和Adobe Experience Platform接收器聯結器
description: 安裝及設定Kafka Connect和Adobe Experience Platform接收器聯結器
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---

# 2.6.4安裝並設定Kafka Connect和Adobe Experience Platform接收器聯結器

## 2.6.4.1下載Adobe Experience Platform接收器聯結器

移至[https://github.com/adobe/experience-platform-streaming-connect/releases](https://github.com/adobe/experience-platform-streaming-connect/releases)並下載Adobe Experience Platform接收器聯結器的最新正式版本。

![Kafka](./images/kc1.png)

將下載檔案&#x200B;**streaming-connect-sink-0.0.14-java-11.jar**&#x200B;放到您的案頭上。

![Kafka](./images/kc2.png)

## 2.6.4.2設定Kafka Connect

移至案頭上名為&#x200B;**Kafka_AEP**&#x200B;的資料夾，並導覽至資料夾`kafka_2.13-3.1.0/config`。
在該資料夾中，使用任何文字編輯器開啟檔案**connect-distributed.properties**。

![Kafka](./images/kc3a.png)

在文字編輯器中，移至第34和35行，並確定將欄位`key.converter.schemas.enable`和`value.converter.schemas.enable`設定為`false`

```json
key.converter.schemas.enable=false
value.converter.schemas.enable=false
```

將變更儲存至此檔案。

![Kafka](./images/kc3.png)

接著，返回資料夾`kafka_2.13-3.1.0`並手動建立新資料夾，然後將其命名為`connectors`。

![Kafka](./images/kc4.png)

在資料夾上按一下滑鼠右鍵，然後按一下&#x200B;**在資料夾**&#x200B;新增終端機。

![Kafka](./images/kc5.png)

您將會看到此訊息。 輸入命令`pwd`以擷取該資料夾的完整路徑。 選取完整路徑並將其複製到剪貼簿。

![Kafka](./images/kc6.png)

返回文字編輯器，前往檔案&#x200B;**connect-distributed.properties**，然後向下捲動至最後一行（熒幕擷圖中的第86行）。 您應該取消註解以`# plugin.path=`開頭的行，並且應該貼上名稱為`connectors`的資料夾的完整路徑。 結果看起來應該類似這樣：

`plugin.path=/Users/woutervangeluwe/Desktop/Kafka_AEP/kafka_2.13-3.1.0/connectors`

儲存您對檔案&#x200B;**connect-distributed.properties**&#x200B;所做的變更，並關閉文字編輯器。

![Kafka](./images/kc7.png)

接著，複製您下載至名為`connectors`的資料夾的最新正式Adobe Experience Platform接收器聯結器版本。 您之前下載的檔案名稱為&#x200B;**streaming-connect-sink-0.0.14-java-11.jar**，您只需將其移至`connectors`資料夾即可。

![Kafka](./images/kc8.png)

接下來，在&#x200B;**kafka_2.13-3.1.0**&#x200B;資料夾的層級開啟新的「終端機」視窗。 以滑鼠右鍵按一下該資料夾，然後按一下&#x200B;**資料夾的新終端機**。

在[終端機]視窗中，貼上此命令： `bin/connect-distributed.sh config/connect-distributed.properties`並按一下&#x200B;**Enter**。 這個指令會啟動Kafka Connect並載入Adobe Experience Platform接收器聯結器的程式庫。

![Kafka](./images/kc9.png)

幾秒後，您會看到類似以下畫面：

![Kafka](./images/kc10.png)

## 2.6.4.3使用Postman建立Adobe Experience Platform接收器聯結器

您現在可以使用Postman與Kafka Connect互動。 若要這樣做，請下載[此Postman集合](./../../../assets/postman/postman_kafka.zip)，並將其解壓縮至案頭上的本機電腦。 然後，您會擁有名為`Kafka_AEP.postman_collection.json`的檔案。

![Kafka](./images/kc11a.png)

您需要在Postman中匯入此檔案。 若要這麼做，請開啟Postman，按一下&#x200B;**匯入**，將檔案`Kafka_AEP.postman_collection.json`拖放到快顯視窗中，然後按一下&#x200B;**匯入**。

![Kafka](./images/kc11b.png)

之後，您會在Postman的左側功能表中找到此集合。 按一下第一個要求&#x200B;**可用的Kafka Connect聯結器**&#x200B;以開啟GET。

![Kafka](./images/kc11c.png)

您將會看到此訊息。 按一下藍色的&#x200B;**傳送**&#x200B;按鈕，之後您應該會看到空白回應`[]`。 空白回應是因為目前未定義任何Kafka Connect聯結器。

![Kafka](./images/kc11.png)

若要建立聯結器，請按一下以開啟Kafka集合中的第二個要求，**POST建立AEP接收聯結器**。 您將會看到此訊息。 第11行顯示&#x200B;**&quot;aep.endpoint&quot;：&quot;**，您必須貼入練習[15.3](./ex3.md)結束時收到的HTTP API串流端點URL。 HTTP API串流端點URL看起來像這樣： `https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`。

![Kafka](./images/kc12a.png)

貼上要求後，其內文看起來應該像這樣。 按一下藍色的&#x200B;**傳送**&#x200B;按鈕以建立您的聯結器。 建立聯結器後，您會立即收到回應。

![Kafka](./images/kc12.png)

GET按一下第一個要求&#x200B;**可用的Kafka Connect聯結器**&#x200B;以再次開啟它，然後按一下藍色的&#x200B;**傳送**&#x200B;按鈕。 您現在會看到Kafka Connect聯結器已建立。

![Kafka](./images/kc13.png)

接下來，開啟Kafka集合中的第三個要求，**GET檢查Kafka連線聯結器狀態**。 按一下藍色的&#x200B;**傳送**&#x200B;按鈕，您將會收到如下所示的回應，表示聯結器正在執行。

![Kafka](./images/kc14.png)

## 2.6.4.4產生體驗事件

開啟新的&#x200B;**終端機**&#x200B;視窗，方法是用滑鼠右鍵按一下資料夾&#x200B;**kafka_2.13-3.1.0**，然後按一下&#x200B;**資料夾中的新終端機**。

![Kafka](./images/kafka11.png)

輸入下列命令：

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aep`

![Kafka](./images/kc15.png)

您將會看到此訊息。 按下Enter按鈕後每新增一行，就會傳送新訊息至主題&#x200B;**aep**。

![Kafka](./images/kc16.png)

您現在可以傳送訊息，訊息會由Adobe Experience Platform接收器聯結器使用，並即時擷取到Adobe Experience Platform中。

讓我們來做一些示範以測試這個。

移至[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案以開啟。

![DSN](./../../gettingstarted/gettingstarted/images/web8.png)

在&#x200B;**Screens**&#x200B;頁面上按一下&#x200B;**執行**。

![DSN](./../../gettingstarted/gettingstarted/images/web2.png)

然後您會看到示範網站已開啟。 選取URL並將其複製到剪貼簿。

![DSN](./../../gettingstarted/gettingstarted/images/web3.png)

開啟新的無痕瀏覽器視窗。

![DSN](./../../gettingstarted/gettingstarted/images/web4.png)

貼上您在上一步中複製的示範網站URL。 接著，系統會要求您使用Adobe ID登入。

![DSN](./../../gettingstarted/gettingstarted/images/web5.png)

選取您的帳戶型別並完成登入程式。

![DSN](./../../gettingstarted/gettingstarted/images/web6.png)

接著，您會在無痕瀏覽器視窗中看到您的網站已載入。 對於每個示範，您都需要使用全新的無痕瀏覽器視窗來載入您的示範網站URL。

![DSN](./../../gettingstarted/gettingstarted/images/web7.png)

按一下畫面左上角的Adobe標誌圖示，開啟設定檔檢視器。

![示範](./../../../modules/datacollection/module1.2/images/pv1.png)

請檢視「設定檔檢視器」面板和即時客戶設定檔，並將&#x200B;**Experience CloudID**&#x200B;設為此目前未知客戶的主要識別碼。

![示範](./../../../modules/datacollection/module1.2/images/pv2.png)

前往「註冊/登入」頁面。 按一下&#x200B;**建立帳戶**。

![示範](./../../../modules/datacollection/module1.2/images/pv9.png)

填寫您的詳細資料，然後按一下&#x200B;**註冊**，之後您將會被重新導向到上一頁。

![示範](./../../../modules/datacollection/module1.2/images/pv10.png)

開啟設定檔檢視器面板，然後前往即時客戶設定檔。 在「設定檔檢視器」面板上，您應該會看到所有顯示的個人資料，例如新新增的電子郵件和電話識別碼。

![示範](./../../../modules/datacollection/module1.2/images/pv11.png)

您可能會看到根據過去活動的一些體驗事件。

![Kafka](./images/kc19.png)

讓我們加以變更，並將來自Kafka的Callcenter體驗事件傳送至Adobe Experience Platform。

取得以下體驗事件裝載範例，並將其複製到文字編輯器中。

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

您將會看到此訊息。 您必須手動更新2個欄位：

- **_id**：請將其設為隨機識別碼，例如`--demoProfileLdap--1234`
- **timestamp**：將時間戳記更新為目前的日期和時間
- **phoneNumber**：輸入剛才在示範網站上建立的帳戶的phoneNumber。 您可以在「設定檔檢視器」面板的&#x200B;**身分**&#x200B;下找到它。

您也需要檢查並可能更新這些欄位：
- **datasetId**：您必須複製資料集示範系統的資料集ID — 客服中心的事件資料集（全域v1.1）
- **imsOrgID**：您的IMS組織ID為`--aepImsOrgId--`

>[!NOTE]
>
>每個資料擷取的欄位&#x200B;**_id**&#x200B;必須是唯一的。 如果您產生多個事件，請確定您每次都會將欄位&#x200B;**_id**&#x200B;更新為新的唯一值。

![Kafka](./images/kc20.png)

之後，您應該會有類似以下的專案：

![Kafka](./images/kc21.png)

接下來，將您的完整體驗事件複製到剪貼簿。 需要清除JSON裝載的空白處，我們將使用線上工具執行此操作。 請移至[http://jsonviewer.stack.hu/](http://jsonviewer.stack.hu/)進行此操作。

![Kafka](./images/kc22.png)

將您的體驗事件貼到編輯器中，然後按一下&#x200B;**移除空白字元**。

![Kafka](./images/kc22a.png)

接著，選取所有輸出文字，並將其複製到剪貼簿。

![Kafka](./images/kc23.png)

返回「終端機」視窗。

![Kafka](./images/kc16.png)

將不含空格的新裝載貼到「終端機」視窗中，然後按一下&#x200B;**Enter**。

![Kafka](./images/kc23a.png)

接著，返回示範網站並重新整理頁面。 您現在應該會在設定檔的&#x200B;**其他事件**&#x200B;底下看到體驗事件，就像下列專案一樣：

![Kafka](./images/kc24.png)

>[!NOTE]
>
>如果您希望客服中心互動顯示在「設定檔檢視器」面板上，您必須移至標籤&#x200B;**設定檔檢視器**，在[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)上的專案中新增以下標籤並篩選。

![Kafka](./images/kc25.png)

您已完成此練習。

下一步： [摘要與優點](./summary.md)

[返回模組2.6](./aep-apache-kafka.md)

[返回所有模組](../../../overview.md)
