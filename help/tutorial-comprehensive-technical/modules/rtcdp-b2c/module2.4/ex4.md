---
title: Microsoft Azure事件中心的區段啟用 — 啟用區段
description: Microsoft Azure事件中心的區段啟用 — 啟用區段
kt: 5342
doc-type: tutorial
exl-id: 56f6a6dc-82aa-4b64-a3f6-b6f59c484ccb
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 1%

---

# 2.4.4啟動區段

## 2.4.4.1將區段新增至Azure事件中心目的地

在本練習中，您會將區段`--aepUserLdap-- - Interest in Equipment`新增至`--aepUserLdap---aep-enablement` Azure事件中心目的地。

前往此URL登入Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./../../../modules/datacollection/module1.2/images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--aepSandboxName--``。 選取適當的沙箱後，您會看到畫面變更，現在您已進入專屬沙箱。

![資料擷取](./../../../modules/datacollection/module1.2/images/sb1.png)

移至&#x200B;**目的地**，然後按一下&#x200B;**瀏覽**。 然後您會看到所有可用的目的地。 找到您的目的地，然後如下所示按一下&#x200B;**+**&#x200B;圖示。

![5-01-select-destination.png](./images/5-01-select-destination.png)

您將會看到此訊息。 使用您的ldap搜尋您的區段，並從區段清單中選取`--aepUserLdap-- - Interest in Equipment`。

按一下&#x200B;**下一步**。

![5-04-select-segment.png](./images/5-04-select-segment.png)

Adobe Experience Platform Real-time CDP可將裝載傳送至兩種型別的目的地：區段目的地和設定檔目的地。

區段目的地會收到預先定義的區段資格裝載，稍後將討論。 這類裝載包含&#x200B;**所有**&#x200B;特定設定檔的區段資格。 即使區段不在目的地的啟用清單中。 **Azure事件中樞**&#x200B;和&#x200B;**AWS Kinesis**&#x200B;就是這類區段目的地的範例。

以設定檔為基礎的目的地可讓您從XDM設定檔聯合結構描述中挑選任何屬性(firstName、lastName、...)，並將其包含在啟動裝載中。 **電子郵件行銷**&#x200B;就是這類目的地的範例。

由於您的Azure事件中心目的地是&#x200B;**區段**&#x200B;目的地，請選取欄位`--aepTenantId--.identification.core.ecid`作為範例。

按一下&#x200B;**新增欄位**，按一下瀏覽結構描述並選取欄位`--aepTenantId--identification.core.ecid` （刪除任何其他會自動顯示的欄位）。

按一下&#x200B;**下一步**。

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

按一下&#x200B;**完成**。

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

您的區段現在已對Microsoft事件中心目的地啟用。

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

下一步： [2.4.5建立您的Microsoft Azure專案](./ex5.md)

[返回模組2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模組](./../../../overview.md)
