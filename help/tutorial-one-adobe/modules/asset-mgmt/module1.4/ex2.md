---
title: 搭配Adobe Journey Optimizer使用您的動態媒體範本
description: 搭配Adobe Journey Optimizer使用您的動態媒體範本
kt: 5342
doc-type: tutorial
source-git-commit: 261475b85bfb15f7e9f630d1c5203732c2d4c254
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 1.4.2搭配Adobe Journey Optimizer使用您的動態媒體範本

## 1.4.2.1在Adobe Journey Optimizer中建立您的行銷活動

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。 然後您就會進入沙箱&#x200B;**的**&#x200B;首頁`--aepSandboxName--`檢視。

![ACOP](./images/acoptriglp.png)

您現在將建立行銷活動。 上一個練習的事件型歷程仰賴傳入體驗事件或對象進入或退出，以觸發1個特定客戶的歷程，而行銷活動則以唯一內容（例如電子報、一次性促銷活動或一般資訊）鎖定整個對象，或定期傳送類似內容（例如例項生日行銷活動和提醒）。

在功能表中，前往&#x200B;**行銷活動**&#x200B;並按一下&#x200B;**建立行銷活動**。

![Journey Optimizer](./images/gsemail21.png)

選取&#x200B;**排程 — 行銷**&#x200B;並按一下&#x200B;**建立**。

![Journey Optimizer](./images/gsemail22.png)

在行銷活動建立畫面上，設定下列專案：

- **名稱**： `--aepUserLdap-- - CitiSignal Fiber Max DM Email Campaign`。

按一下&#x200B;**動作**。

![Journey Optimizer](./images/gsemail23.png)

按一下&#x200B;**+新增動作**，然後選取&#x200B;**電子郵件**。

![Journey Optimizer](./images/gsemail24.png)

接著，選取現有的&#x200B;**電子郵件組態**，然後按一下&#x200B;**編輯內容**。

![Journey Optimizer](./images/gsemail25.png)

您將會看到此訊息。 對於&#x200B;**主旨列**，請使用以下專案：

```
{{profile.person.name.firstName}}, say hello to CitiSignal Fiber Max!
```

接著，按一下&#x200B;**編輯內容**。

![Journey Optimizer](./images/gsemail26.png)

選取&#x200B;**從頭開始設計**。

![Journey Optimizer](./images/gsemail27.png)

您應該會看到此訊息。

![Journey Optimizer](./images/gsemail28.png)

將2x **1:1資料行**&#x200B;新增至畫布。

![Journey Optimizer](./images/gsemail29.png)

移至&#x200B;**Fragments**，將&#x200B;**header**&#x200B;片段拖曳至第一個1:1欄，然後將&#x200B;**頁尾**&#x200B;片段拖曳至第二個1:1欄。

![Journey Optimizer](./images/gsemail30.png)

在2個片段之間新增新的1:1欄，然後將&#x200B;**影像**&#x200B;新增到該1:1欄。 然後，按一下&#x200B;**瀏覽**。

![Journey Optimizer](./images/gsemail31.png)

導覽至您儲存Dynamic Media範本的資料夾。 選取您的Dynamic Media範本，然後按一下&#x200B;**選取**。

![Journey Optimizer](./images/gsemail32.png)

您應該會看到此訊息。

![Journey Optimizer](./images/gsemail33.png)

## 後續步驟

返回[Adobe Experience Manager Assets &amp; Dynamic Media](./aemassetsdm.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}
