---
title: Adobe Experience Platform Data Collection & Real-time Server Side Forwarding — 更新您的資料串流，使資料可用於您的Adobe Experience Platform Data Collection Server屬性
description: 更新您的資料串流，讓資料可用於您的Adobe Experience Platform資料收集伺服器屬性
kt: 5342
doc-type: tutorial
exl-id: 7b5b598e-e54c-4f0f-b260-d643600ee6ca
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---

# 2.5.2更新您的資料串流，讓資料可用於您的Adobe Experience Platform資料收集伺服器屬性

## 2.5.2.1更新您的資料流

在[快速入門](./../../gettingstarted/gettingstarted/ex2.md)中，您已建立自己的&#x200B;**[!UICONTROL 資料流]**。 您接著使用名稱`--aepUserLdap-- - Demo System Datastream`。

在本練習中，您需要設定&#x200B;**[!UICONTROL 資料串流]**&#x200B;以搭配您的&#x200B;**資料收集伺服器屬性**&#x200B;使用。

若要這麼做，請前往[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)。 您將會看到此訊息。 在左側功能表中，按一下&#x200B;**[!UICONTROL 資料串流]**。

在熒幕的右上角，選取您的沙箱名稱，應為`--aepSandboxName--`。

![按一下左側導覽中的Edge設定圖示](./images/edgeconfig1b.png)

搜尋您名為`--aepUserLdap-- - Demo System Datastream`的&#x200B;**[!UICONTROL 資料流]**。 按一下您的&#x200B;**[!UICONTROL 資料流]**&#x200B;以開啟。

![WebSDK](./images/websdk0.png)

您將會看到此訊息。 按一下&#x200B;**[!UICONTROL +新增服務]**。

![WebSDK](./images/websdk3.png)

選取服務&#x200B;**事件轉送**。 這將會顯示2個額外的設定。 選取您在上一個練習中建立且名為`--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`的「事件轉送」屬性。 然後選取&#x200B;**環境**&#x200B;下的&#x200B;**開發**。 按一下&#x200B;**儲存**。

![WebSDK](./images/websdk4.png)

您的資料流現在已更新，可以開始使用。

![WebSDK](./images/websdk8a.png)

您的資料流現在已準備好與您的&#x200B;**[!DNL Event Forwarding property]**&#x200B;搭配使用。

下一步： [2.5.3建立並設定自訂webhook](./ex3.md)

[返回模組2.5](./aep-data-collection-ssf.md)

[返回所有模組](./../../../overview.md)
