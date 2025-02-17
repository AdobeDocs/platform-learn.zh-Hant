---
title: Audience Activation到Microsoft Azure事件中心 — 啟用對象
description: Audience Activation到Microsoft Azure事件中心 — 啟用對象
kt: 5342
doc-type: tutorial
exl-id: e6bac0ce-4a1e-4458-af3e-3d6ac40b9cb5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 3%

---

# 2.4.5啟用您的對象

## 將對象新增至Azure事件中心目的地

在本練習中，您會將對象`--aepUserLdap-- - Interest in Plans`新增至`--aepUserLdap---aep-enablement` Azure事件中心目的地。

前往此URL登入Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--aepSandboxName--``。 選取適當的沙箱後，您會看到畫面變更，現在您已進入專屬沙箱。

![資料擷取](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

移至&#x200B;**目的地**，然後按一下&#x200B;**瀏覽**。 然後您會看到所有可用的目的地。 找到您的目的地並按一下下面所示的3個點**...**，然後按一下&#x200B;**啟用對象**。

![5-01-select-destination.png](./images/501selectdestination.png)

您將會看到此訊息。 使用您的ldap搜尋您的對象，並從對象清單中選取`--aepUserLdap-- - Interest in Plans`。

按一下&#x200B;**下一步**。

![5-04-select-segment.png](./images/504selectsegment.png)

按一下&#x200B;**新增欄位**，按一下瀏覽結構描述並選取欄位`--aepTenantId--identification.core.ecid` （刪除任何其他會自動顯示的欄位）。

按一下&#x200B;**下一步**。

![5-05-select-attributes.png](./images/505selectattributes.png)

按一下&#x200B;**完成**。

![5-06-destination-finish.png](./images/506destinationfinish.png)

您的對象現在正朝著您的Microsoft事件中心目的地啟用。

![5-07-destination-segment-added.png](./images/507destinationsegmentadded.png)

## 後續步驟

移至[2.4.6建立您的Microsoft Azure專案](./ex6.md){target="_blank"}

返回[Real-Time CDP： Audience Activation到Microsoft Azure事件中心](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
