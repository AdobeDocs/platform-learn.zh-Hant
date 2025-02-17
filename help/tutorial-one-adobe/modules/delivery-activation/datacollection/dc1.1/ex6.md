---
title: 基礎 — Adobe Experience Platform資料收集與Web SDK擴充功能的設定 — 實作Adobe Target
description: 基礎 — Adobe Experience Platform資料收集與Web SDK擴充功能的設定 — 實作Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 31cdde2f-011d-442d-8e47-15a318a6c89d
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 2%

---

# 1.1.6實作Adobe Target

## 更新您的資料流以使用Adobe Target

如果您想要將Web SDK所收集的資料傳送至Adobe Target，並從Adobe Target取得回應，為每位客戶提供個人化體驗，請依照下列步驟進行。

移至[https://experience.adobe.com/launch/](https://experience.adobe.com/launch/)並移至&#x200B;**資料串流**。

在熒幕的右上角，選取您的沙箱名稱，應為`--aepSandboxName--`。 開啟名為`--aepUserLdap-- - Demo System Datastream`的特定資料流。

![按一下左側導覽中的Edge設定圖示](./images/edgeconfig1b.png)

您將會看到此訊息。 若要啟用Adobe Target，請按一下[新增服務]。****

![AEP偵錯工具](./images/aa2.png)

您將會看到此訊息。 選取服務&#x200B;**Adobe Target**，之後您可選擇提供其他資訊。 按一下&#x200B;**儲存**。

![AEP偵錯工具](./images/at1.png)

## 後續步驟

移至Adobe Experience Platform](./ex7.md){target="_blank"}中的[1.1.7 XDM結構描述需求

返回[設定Adobe Experience Platform Data Collection和Web SDK標籤擴充功能](./data-ingestion-launch-web-sdk.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
