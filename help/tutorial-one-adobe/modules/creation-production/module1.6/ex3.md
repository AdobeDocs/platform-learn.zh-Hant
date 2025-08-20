---
title: 建立您的外部DAM應用程式
description: 建立您的外部DAM應用程式
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 6823e8a0-dde7-460a-a48a-6787e65e4104
source-git-commit: fe162f285d67cc2a37736f80715a5c5717835e95
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# 1.6.3建立並部署外部DAM應用程式

## 1.6.3.1下載範例應用程式檔案

移至[https://github.com/adobe/genstudio-extensibility-examples](https://github.com/adobe/genstudio-extensibility-examples)。 按一下&#x200B;**代碼**，然後選取&#x200B;**下載ZIP**。

![外部DAM](./images/extdam1.png)

將zip檔案解壓縮至案頭。

![外部DAM](./images/extdam2.png)

開啟資料夾&#x200B;**genstudio-extensibility-examples-main**。 您將會看到多個範例應用程式。 此練習的興趣是&#x200B;**genstudio-external-dam-app**。

複製該目錄並貼到您的案頭上。

![外部DAM](./images/extdam4.png)

您的案頭上現在應該有此專案：

![外部DAM](./images/extdam3.png)

在接下來的練習中，您只會使用&#x200B;**genstudio-external-dam-app**&#x200B;資料夾。

## 1.6.3.2設定Adobe Developer命令列介面

在&#x200B;**genstudio-external-dam-app**&#x200B;資料夾上按一下滑鼠右鍵，然後選取&#x200B;**資料夾的新終端機**。

![外部DAM](./images/extdam5.png)

您應該會看到此訊息。 輸入命令`aio login`。 此命令會重新導向至您的瀏覽器，並預期您會登入。

![外部DAM](./images/extdam6.png)

成功登入後，您應該會在瀏覽器中看到此資訊。

![外部DAM](./images/extdam7.png)

瀏覽器會重新導向回終端機視窗。 您應該會看到顯示&#x200B;**登入成功**&#x200B;的訊息，以及瀏覽器傳回的長權杖。

![外部DAM](./images/extdam8.png)

下一步是設定您用於外部DAM應用程式的例項和Adobe IO專案。

為此，您需要從您之前設定的Adobe IO專案下載檔案。

移至[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}，並開啟您之前建立的專案（名為`--aepUserLdap-- GSPeM EXT`）。 開啟&#x200B;**生產**&#x200B;工作區。

![外部DAM](./images/extdam9.png)

按一下&#x200B;**全部下載**。 如此將下載JSON檔案。

![外部DAM](./images/extdam10.png)

將JSON檔案從您的&#x200B;**Downloads**&#x200B;目錄複製到外部DAM應用程式的根目錄中。

![外部DAM](./images/extdam11.png)

返回您的終端機視窗。 輸入命令`aio app use XXX-YYY-Production.json`。

>[!NOTE]
>
>您需要變更檔案名稱以符合檔案名稱。

命令執行後，您的外部DAM應用程式現在會連線至使用您之前建立的App Builder的Adobe IO專案。

![外部DAM](./images/extdam12.png)

## 1.6.3.3安裝GenStudio擴充性SDK

接下來，您必須安裝&#x200B;**GenStudio擴充性SDK**。 您可以在這裡找到有關SDK的更多詳細資料： [https://github.com/adobe/genstudio-extensibility-sdk](https://github.com/adobe/genstudio-extensibility-sdk)。

若要安裝SDK，請在終端機視窗中執行此命令：

`npm install @adobe/genstudio-extensibility-sdk`

![外部DAM](./images/extdam13.png)

幾分鐘後，就會安裝SDK。

![外部DAM](./images/extdam14.png)

## 1.6.3.4在Visual Studio Code中檢閱外部DAM應用程式

開啟Visual Studio Code。 按一下&#x200B;**開啟……**&#x200B;以開啟資料夾。

![外部DAM](./images/extdam15.png)

選取包含您之前下載的應用程式的資料夾&#x200B;**genstudio-external-dam-app**。

![外部DAM](./images/extdam16.png)

按一下以開啟檔案&#x200B;**.env**。

![外部DAM](./images/extdam17.png)

**.env**&#x200B;檔案是由您在上一步中執行的命令`aio app use`所建立，包含使用App Builder連線至您的Adobe IO專案所需的資訊。

![外部DAM](./images/extdam18.png)

您現在需要在資料夾的根目錄中建立2個新檔案：

- `.env.dev`。按一下&#x200B;**新增檔案**&#x200B;按鈕，然後輸入檔案名稱`.env.dev`。

![外部DAM](./images/extdam19.png)

- `.env.prod`。  按一下&#x200B;**新增檔案**&#x200B;按鈕，然後輸入檔案名稱`.env.prod`。

![外部DAM](./images/extdam20.png)

這些檔案將包含連線至您之前建立的AWS S3儲存貯體所需的認證。

```
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=
AWS_BUCKET_NAME=
```

在上一個練習中建立IAM使用者後，欄位&#x200B;**`AWS_ACCESS_KEY_ID`**&#x200B;和&#x200B;**`AWS_SECRET_ACCESS_KEY`**&#x200B;可供使用。 系統要求您寫下這些值，您現在可以複製這些值。

![ETL](./images/cred1.png)

欄位&#x200B;**`AWS_REGION`**&#x200B;可以從AWS S3 Home檢視取得，位於您的儲存貯體名稱旁。 在此範例中，區域是&#x200B;**us-west-2**。

![ETL](./images/bucket2.png)

欄位&#x200B;**`AWS_BUCKET_NAME`**&#x200B;應為`--aepUserLdap---gspem-dam`。

此資訊可讓您更新每個變數的值。

```
AWS_ACCESS_KEY_ID=XXX
AWS_SECRET_ACCESS_KEY=YYY
AWS_REGION=us-west-2
AWS_BUCKET_NAME=--aepUserLdap---gspem-dam
```

您現在應該將此文字貼到兩個檔案中： `.env.dev`和`.env.prod`。 別忘了儲存您的變更。

![外部DAM](./images/extdam21.png)


![外部DAM](./images/extdam22.png)

接下來，返回您的終端機視窗。 執行此命令：

`export $(grep -v '^#' .env.dev | xargs)`

![外部DAM](./images/extdam23.png)

## 1.6.3.5執行您的外部DAM應用程式

在終端機視窗中，執行命令`aio app run`。 1-2分鐘後，您應該會看到此訊息。

![外部DAM](./images/extdam24.png)

您現在已確認應用程式執行中。 下一步是進行部署。

首先，按下&#x200B;**CTRL+C**&#x200B;以停止應用程式執行。 然後，輸入命令`aio app deploy`。 此命令會將您的程式碼部署至Adobe IO。

因此，您會收到類似的URL以存取已部署的應用程式：

`https://133309-201burgundyguan.adobeio-static.net/index.html`

![外部DAM](./images/extdam27.png)

為了進行測試，您現在可以將`?ext=`新增為上述URL的前置詞，將該URL作為查詢字串引數使用。 這會產生此查詢字串引數：

`?ext=https://133309-201burgundyguan.adobeio-static.net/index.html`

移至[https://experience.adobe.com/genstudio/create](https://experience.adobe.com/genstudio/create)。

![外部DAM](./images/extdam25.png)

接下來，在&#x200B;**#**&#x200B;前新增查詢字串引數。 您的新URL應如下所示：

`https://experience.adobe.com/?ext=https://133309-201burgundyguan.adobeio-static.net/index.html#/@experienceplatform/genstudio/create`

頁面會正常載入。 按一下&#x200B;**橫幅**&#x200B;開始建立新橫幅。

![外部DAM](./images/extdam26.png)

選取範本並按一下&#x200B;**使用**。

![外部DAM](./images/extdam28.png)

按一下&#x200B;**從內容選取**。

![外部DAM](./images/extdam29.png)

之後，您應該就能在下拉式清單中選取外部DAM。

![外部DAM](./images/extdam30.png)

在本機電腦上變更程式碼時，您需要重新部署應用程式。 當您重新部署時，請使用以下終端機命令：

`aio app deploy --force-build --force-deploy`

您的應用程式現已準備好發佈。

## 後續步驟

移至[私人發佈您的應用程式](./ex4.md){target="_blank"}

返回[GenStudio for Performance Marketing — 擴充性](./genstudioext.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}
