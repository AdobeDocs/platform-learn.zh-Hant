---
title: Audience Activation至Microsoft Azure事件中心 — 建立對象
description: Audience Activation至Microsoft Azure事件中心 — 建立對象
kt: 5342
doc-type: tutorial
exl-id: 56f6a6dc-82aa-4b64-a3f6-b6f59c484ccb
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# 2.4.4建立對象

## 簡介

您將建立一個簡單的對象：

- 客戶造訪CitiSignal示範網站的&#x200B;**計畫**&#x200B;頁面時，將有資格對計畫&#x200B;**感興趣。**

### 很高興知道

當您符合某個受眾的資格，而該受眾屬於某個目的地的啟用清單時，Real-time CDP就會觸發該目的地的啟用。 若是如此，將傳送至該目的地的對象資格承載將包含&#x200B;**您的客戶設定檔符合資格的所有對象**。

此模組的目標是顯示您客戶設定檔的對象資格近乎即時傳送至事件中心目的地。

### 對象狀態

Adobe Experience Platform中的對象資格一律具有&#x200B;**status** — 屬性，且可為下列其中一項：

- **已實現**：這表示有新的對象資格
- **已退出**：這表示設定檔不再符合對象的資格

## 建立對象

前往此URL登入Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./../../../modules/datacollection/module1.2/images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--aepSandboxName--``。 選取適當的沙箱後，您會看到畫面變更，現在您已進入專屬沙箱。

![資料擷取](./../../../modules/datacollection/module1.2/images/sb1.png)

移至&#x200B;**對象**。 按一下&#x200B;**+建立對象**&#x200B;按鈕。

![資料擷取](./images/seg.png)

選取&#x200B;**建置規則**&#x200B;並按一下&#x200B;**建立**。

![資料擷取](./images/seg1.png)

為對象命名`--aepUserLdap-- - Interest in Plans`、將評估方法設為&#x200B;**Edge**，並從體驗事件新增頁面名稱。

按一下&#x200B;**事件**，然後拖放&#x200B;**XDM ExperienceEvent >網頁>網頁詳細資料>名稱**。 輸入&#x200B;**plans**&#x200B;作為值：

![4-05-create-ee-2.png](./images/405createee2.png)

拖放&#x200B;**XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**。 輸入`--aepUserLdap--`作為值，將比較引數設定為&#x200B;**contains**，然後按一下&#x200B;**Publish**：

![4-05-create-ee-2-brand.png](./images/405createee2brand.png)

您的對象現已發佈。

![4-05-create-ee-2-brand.png](./images/405createee2brand1.png)

下一步： [2.4.5啟用您的對象](./ex5.md)

[返回模組2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模組](./../../../overview.md)
