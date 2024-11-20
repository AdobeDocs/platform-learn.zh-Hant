---
title: Microsoft Azure事件中樞的區段啟用 — 設定您的Microsoft Azure環境
description: Microsoft Azure事件中樞的區段啟用 — 設定您的Microsoft Azure環境
kt: 5342
doc-type: tutorial
exl-id: 772b4d2b-144a-4f29-a855-8fd3493a85d2
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 2.4.1設定環境

## 建立Azure訂閱

>[!NOTE]
>
>如果您已有Azure訂閱，可以略過此步驟。 請繼續進行該案例的下一個練習。

移至[https://portal.azure.com](https://portal.azure.com)並使用您的Azure帳戶登入。 如果您沒有電子郵件地址，請使用個人電子郵件地址來建立您的Azure帳戶。

![02-azure-portal-email.png](./images/02azureportalemail.png)

成功登入後，您會看到下列畫面：

![03-azure-logged-in.png](./images/03azureloggedin.png)

按一下左側功能表並選取&#x200B;**所有資源**，如果您尚未訂閱，將會顯示Azure訂閱畫面。 在這種情況下，請選取&#x200B;**開始使用Azure免費試用**。

![04-azure-start-subscribe.png](./images/04azurestartsubscribe.png)

填寫Azure訂閱表單，提供您的行動電話和信用卡以進行啟用（您將有30天的免費套餐，除非您升級，否則不會向您收費）。

訂閱程式完成後，您就可以開始了：

![06-azure-subscription-ok.png](./images/06azuresubscriptionok.png)

## 安裝Visual Code Studio

您將使用Microsoft Visual Code Studio來管理您的Azure專案。 您可以透過[此連結](https://code.visualstudio.com/download)下載。 請遵循同一網站上特定作業系統的安裝指示。

## 安裝視覺化程式碼擴充功能

從[https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)安裝適用於Visual Studio Code的Azure函式。 按一下安裝按鈕：

![07-azure-code-extension-install.png](./images/07azurecodeextensioninstall.png)

安裝Azure帳戶並從[https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account)登入Visual Studio Code。 按一下安裝按鈕：

![08-azure-account-extension-install.png](./images/08azureaccountextensioninstall.png)

## 安裝節點.js

>[!NOTE]
>
>如果您已安裝node.js，則可以略過此步驟。 請繼續進行該案例的下一個練習。

### macOS

確定先安裝[Homebrew](https://brew.sh/)。 請依照指示[這裡](https://brew.sh/)。

![節點](./images/brew.png)

安裝Homebrew後，請執行此命令：

```javascript
brew install node
```

### Windows

直接從[nodejs.org](https://nodejs.org/en/)網站下載[Windows Installer](https://nodejs.org/en/#home-downloadhead)。

## 驗證node.js版本

此模組需要安裝node.js版本18。 任何其他版本的node.js都可能會導致此練習發生問題。

在繼續之前，請立即驗證您的node.js版本。

執行此命令以驗證您的node.js版本：

```javascript
node -v
```

如果您的版本低於或高於18，則需要升級或降級。

### 在macOS上升級/降級node.js版本

確定您已安裝封裝&#x200B;**n**。

若要安裝封裝&#x200B;**n**，請執行此命令：

```javascript
sudo npm install -g n
```

如果您版本低於或高於版本12，請執行此命令以升級或降級：

```javascript
sudo n 18
```

### 在Windows上升級/降級node.js版本

從「Windows >控制檯>新增或移除程式」解除安裝node.js。

正在從[nodejs.org](https://nodejs.org/en/)網站安裝所需版本。

## 安裝NPM套件：要求

您必須在node.js安裝程式中安裝封裝&#x200B;**要求**。

若要安裝封裝&#x200B;**要求**，請執行此命令：

```javascript
npm install request
```

## 安裝Azure函式核心工具：

```
brew tap azure/functions
brew install azure-functions-core-tools@4
```

下一步： [2.4.2設定您的Microsoft Azure EventHub環境](./ex2.md)

[返回模組2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模組](./../../../overview.md)
