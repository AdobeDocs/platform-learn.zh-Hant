---
title: Foundation — 設定Adobe Experience Platform資料收集和Web SDK擴充功能 — 實作Adobe Target
description: Foundation — 設定Adobe Experience Platform資料收集和Web SDK擴充功能 — 實作Adobe Target
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 4aee8ae2-38ca-49a3-8f1b-57713d16f5b5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 1.6實作Adobe Target

## 1.6.更新您的Datastream以使用Adobe Target

如果您想要將Web SDK所收集的資料傳送至Adobe Target，並透過每位客戶的個人化體驗從Adobe Target取得回應，請遵循下列步驟。

前往 [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) 然後 **資料流**.

在畫面的右上角，選取沙箱名稱，名稱應為 `--aepSandboxId--`. 開啟您指定的資料流，此資料流的名稱為 `--demoProfileLdap-- - Demo System Datastream`.

![按一下左側導覽中的「邊緣設定」圖示](./images/edgeconfig1b.png)

你會看到這個。 若要啟用Adobe Target，請按一下 **+添加服務**.

![AEP Debugger](./images/aa2.png)

你會看到這個。 選擇服務 **Adobe Target**，之後您可以選擇提供其他資訊。 目前不需要儲存，因此請按一下 **取消**.

![AEP Debugger](./images/at1.png)

下一步： [1.7Adobe Experience Platform的XDM結構需求](./ex7.md)

[返回模組1](./data-ingestion-launch-web-sdk.md)

[返回所有模組](./../../overview.md)
