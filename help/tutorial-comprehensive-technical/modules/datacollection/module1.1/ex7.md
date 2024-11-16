---
title: 基礎 — Adobe Experience Platform資料彙集的設定和Web SDK擴充功能 — Adobe Experience Platform中的XDM結構描述需求
description: 基礎 — Adobe Experience Platform資料彙集的設定和Web SDK擴充功能 — Adobe Experience Platform中的XDM結構描述需求
kt: 5342
doc-type: tutorial
exl-id: 3fc4a1d6-4130-464e-98c0-5b9cac8051a0
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 1.1.7 Adobe Experience Platform中的XDM結構描述需求

為確保Web SDK和alloy.js能夠擷取資料至Adobe Experience Platform，需將特定XDM Mixin納入Adobe Experience Platform的XDM結構描述。

前往[https://experience.adobe.com/platform](https://experience.adobe.com/platform)並登入。

![AEP偵錯工具](./images/exp1.png)

登入後，按一下熒幕上方藍線中的文字&#x200B;**Production Prod**&#x200B;以選取適當的沙箱。 選取沙箱`--aepSandboxName--`。

選取您的沙箱後，您會看到畫面變更，現在您已進入沙箱。

![AEP偵錯工具](./images/exp2.png)

在左側功能表中，前往&#x200B;**結構描述**&#x200B;並開啟網站的&#x200B;**示範系統 — 事件結構描述（全域v1.1）**&#x200B;結構描述。

![AEP偵錯工具](./images/exp3.png)

在該結構描述中，您會看到已新增欄位群組&#x200B;**AEP Web SDK ExperienceEvent**&#x200B;欄位群組。 此欄位群組會將所有最低必要欄位新增至結構描述。 Web SDK在Adobe Experience Platform中使用的每個體驗事件結構描述一律會要求該欄位群組成為結構描述的一部分。

![AEP偵錯工具](./images/exp4.png)

在[模組1.2](./../module1.2/data-ingestion.md)中，您將瞭解如何新增欄位群組至結構描述。

下一步： [摘要與優點](./summary.md)

[返回模組1.1](./data-ingestion-launch-web-sdk.md)

[返回所有模組](./../../../overview.md)
