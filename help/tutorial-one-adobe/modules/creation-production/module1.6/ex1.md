---
title: Adobe IO與App Builder
description: Adobe IO與App Builder
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: 52234e7b3b6743db79dec570b1a1f2d3ac4cf1ab
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 1%

---

# 1.6.1 Adobe IO和App Builder

## 1.6.1.1建立您的Adobe I/O專案

移至[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}。

![GSPeM擴充性](./images/gspemext1.png)

請務必在熒幕右上角選取正確的例項。 您的執行個體是`--aepImsOrgName--`。

>[!NOTE]
>
> 下方熒幕擷圖顯示選取的特定組織。 完成本教學課程時，您的組織很可能有不同的名稱。 當您註冊參加本教學課程時，系統已為您提供要使用的環境詳細資訊，請依照這些指示操作。

接著，選取&#x200B;**從範本**&#x200B;建立專案。

![GSPeM擴充性](./images/gspemext2.png)

選取&#x200B;**App Builder**。

![GSPeM擴充性](./images/gspemext4.png)

輸入名稱`--aepUserLdap-- GSPeM EXT`。 按一下&#x200B;**儲存**。

![GSPeM擴充性](./images/gspemext5.png)

您應該會看到類似這樣的內容。

![GSPeM擴充性](./images/gspemext6.png)

## 1.6.1.2設定您的開發環境

為了建立、提交和部署可擴充的應用程式，您電腦上的本機開發環境應已安裝下列應用程式和套件：

- Node.js （20.x版或更新版本）
- npm （與Node.js封裝）
- Adobe Developer命令列介面(CLI)

如果您的電腦尚未安裝這些應用程式或套件，請遵循這些步驟。

### Node.js和npm

移至[https://nodejs.org/en/download](https://nodejs.org/en/download)。 之後，您應該會看到這個畫面，其中包含許多需要執行才能安裝Node.js和npm的終端機命令。 此處顯示的指令適用於MacBook。

![GSPeM擴充性](./images/gspemext7.png)

首先，開啟新的終端機視窗。 貼上並執行熒幕擷圖第2行提及的命令：

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash`

接下來，在熒幕擷圖的第5行執行命令：

`\. "$HOME/.nvm/nvm.sh"`

成功執行兩個命令後，請執行此命令：

`node -v`

您應該會看到傳回的版本號碼。

![GSPeM擴充性](./images/gspemext8.png)

接下來，執行此命令：

`npm -v`

您應該會看到傳回的版本號碼。

![GSPeM擴充性](./images/gspemext9.png)

如果最後2個命令成功傳回版本號碼，則表示這2個功能的設定成功。

### Adobe Developer命令列介面(CLI)

若要安裝Adobe Developer命令列介面(CLI)，請在終端機視窗中執行以下命令：

`npm install -g @adobe/aio-cli`

執行此命令可能需要幾分鐘的時間，最終結果應類似如下：

![GSPeM擴充性](./images/gspemext10.png)

Adobe Developer命令列介面(CLI)現在也已成功安裝。

您現在已設定基本元素，以便執行App Builder專案。

## 後續步驟

移至[建立您的AWS S3 Bucket](./ex2.md){target="_blank"}

返回[GenStudio for Performance Marketing — 擴充性](./genstudioext.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}
