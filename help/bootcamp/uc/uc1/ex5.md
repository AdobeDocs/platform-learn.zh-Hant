---
title: Bootcamp - Real-time CDP — 建立對象並採取行動 — 將對象傳送至DV360
description: Bootcamp - Real-time CDP — 建立對象並採取行動 — 將對象傳送至DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# 1.5採取動作：將對象傳送至Facebook

移至[Adobe Experience Platform](https://experience.adobe.com/platform)。 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``Bootcamp``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。

![資料擷取](./images/sb1.png)

在左側功能表中，前往&#x200B;**目的地**，然後前往&#x200B;**目錄**。 然後您會看到&#x200B;**目的地目錄**。 在&#x200B;**目的地**&#x200B;中，按一下&#x200B;**Facebook自訂對象**&#x200B;卡片上的&#x200B;**啟用對象**。

![RTCDP](./images/rtcdpgoogleseg.png)

選取目的地&#x200B;**bootcamp-facebook**，然後按一下&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest2.png)

在可用受眾清單中，選取您在上一個練習中建立的受眾。 按一下&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest3.png)

在&#x200B;**對應**&#x200B;頁面上，確定已啟用&#x200B;**套用轉換**&#x200B;核取方塊。 按一下&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest4a.png)

在&#x200B;**對象排程**&#x200B;頁面上，選取對象的&#x200B;**來源**，並將其設定為&#x200B;**直接來自客戶**。 按一下&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest4.png)

最後，在&#x200B;**檢閱**&#x200B;頁面上按一下&#x200B;**完成**。

![RTCDP](./images/rtcdpcreatedest5.png)

您的對象現在已連結至Facebook自訂對象。 每當客戶符合此對象的資格時，就會傳送訊號至Facebook伺服器端，將該客戶納入Facebook端的自訂對象中。

在Facebook中，您可以在Adobe Experience Platform的自訂對象下方找到您的對象：

![RTCDP](./images/rtcdpcreatedest5b.png)

您現在可以看到自訂對象出現在Facebook中：

![RTCDP](./images/rtcdpcreatedest5a.png)

[返回使用者流程1](./uc1.md)

[返回所有模組](../../overview.md)
