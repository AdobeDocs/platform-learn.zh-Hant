---
title: 區段啟動至Microsoft Azure事件中心 — 設定您的Microsoft Azure環境
description: 區段啟動至Microsoft Azure事件中心 — 設定您的Microsoft Azure環境
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 79711c1a-674c-4233-9c6c-af3bad6d0e0c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# 13.0配置環境

## 13.0.1建立Azure訂閱

>[!NOTE]
>
>如果您已有Azure訂閱，則可跳過此步驟。 請繼續執行13.0.2。

前往 [https://portal.azure.com](https://portal.azure.com) 並使用您的Azure帳戶登入。 如果您沒有，請使用您的個人電子郵件地址來建立您的Azure帳戶。

![02-azure-portal-email.png](./images/02-azure-portal-email.png)

成功登入後，您會看到下列畫面：

![03-azure-logged-in.png](./images/03-azure-logged-in.png)

按一下左側功能表，然後選取 **所有資源**，如果您尚未訂閱，則會顯示Azure訂閱畫面。 在這種情況下，請選取 **從Azure免費試用開始**.

![04-azure-start-subscribe.png](./images/04-azure-start-subscribe.png)

填寫Azure訂閱表，提供您的手機和信用卡以進行激活（您將有30天的免費套餐，除非升級，否則不會收取費用）:

![05-azure-subscription-form.png](./images/05-azure-subscription-form.png)

訂閱程式完成後，您可以立即開始：

![06-azure-subscription-ok.png](./images/06-azure-subscription-ok.png)


## 13.0.2安裝Visual Code Studio

您將使用Microsoft Visual Code Studio管理您的Azure專案。 您可以透過 [此連結](https://code.visualstudio.com/download). 請按照同一網站上特定作業系統的安裝指示操作。

## 13.0.3安裝可視化代碼擴展

從安裝Visual Studio代碼的Azure函式 [https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). 按一下「安裝」按鈕：

![07-azure-code-extension-install.png](./images/07-azure-code-extension-install.png)

安裝Azure帳戶，並從 [https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account). 按一下「安裝」按鈕：

![08-azure-account-extension-install.png](./images/08-azure-account-extension-install.png)

## 13.0.4安裝node.js

>[!NOTE]
>
>如果已安裝node.js，則可略過此步驟。 請繼續執行13.0.5。

### macOS

一定要 [荷姆布魯](https://brew.sh/) 先安裝。 遵循指示 [此處](https://brew.sh/).

![節點](./images/brew.png)

安裝Homebrew後，運行以下命令：

```javascript
brew install node
```

### Windows

下載 [Windows安裝程式](https://nodejs.org/en/#home-downloadhead) 直接從 [nodejs.org](https://nodejs.org/en/) 網站。

## 13.0.5驗證node.js版本

此模組需要安裝node.js版本12。 任何其他版本的node.js都可能在13.5版本中造成問題。

繼續之前，請立即驗證node.js的版本。

執行此命令以驗證您的node.js版本：

```javascript
node -v
```

如果您的版本低於或高於12，則需要升級或降級。

### 在macOS上升級/降級node.js版本

確認您擁有套件 **n** 已安裝。

安裝套件的方式 **n**，運行此命令：

```javascript
sudo npm install -g n
```

如果您的版本低於或高於12版，請運行以下命令以升級或降級：

```javascript
sudo n 12.6.0
```

### 在Windows上升級/降級node.js版本

從「Windows >控制面板>新增或移除程式」中解除安裝node.js。

從安裝必要的版本 [nodejs.org](https://nodejs.org/en/) 網站。

## 13.0.6安裝NPM包：請求

您需要安裝套件 **請求** 做為node.js設定的一部分。

安裝套件的方式 **請求**，運行此命令：

```javascript
npm install request
```


下一步： [13.1配置您的Microsoft Azure EventHub環境](./ex1.md)

[返回模組13](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模組](./../../overview.md)
