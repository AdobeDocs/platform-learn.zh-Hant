---
title: Bootcamp - Real-time CDP — 建立區段並採取行動 — 將您的區段傳送至DV360
description: Bootcamp - Real-time CDP — 建立區段並採取行動 — 將您的區段傳送至DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5採取行動：將您的區段傳送至Facebook

前往 [Adobe Experience Platform](https://experience.adobe.com/platform). 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./images/home.png)

在繼續之前，您需要選取 **沙箱**. 要選取的沙箱已命名 ``Bootcamp``. 您可以按一下文字來執行此操作 **[!UICONTROL 生產產品]** 在熒幕上方的藍線中。 選取適當的 [!UICONTROL 沙箱]，您會看到畫面變更，現在您已進入專屬團隊 [!UICONTROL 沙箱].

![資料擷取](./images/sb1.png)

在左側功能表中，前往 **目的地**，然後前往 **目錄**. 然後您會看到 **目的地目錄**. 在 **目的地**，按一下 **啟用區段** 於 **facebook自訂對象** 卡片。

![RTCDP](./images/rtcdpgoogleseg.png)

選取目的地 **bootcamp-facebook** 並按一下 **下一個**.

![RTCDP](./images/rtcdpcreatedest2.png)

在可用區段清單中，選取您在上一個練習中建立的區段。 按&#x200B;**「下一步」**。

![RTCDP](./images/rtcdpcreatedest3.png)

於 **對應** 頁面，確認 **套用轉換** 核取方塊已啟用。 按&#x200B;**「下一步」**。

![RTCDP](./images/rtcdpcreatedest4a.png)

於 **區段排程** 頁面，選取 **您的對象來源** 並將其設定為 **直接來自客戶**. 按&#x200B;**「下一步」**。

![RTCDP](./images/rtcdpcreatedest4.png)

最後，在 **檢閱** 頁面，按一下 **完成**.

![RTCDP](./images/rtcdpcreatedest5.png)

您的區段現在已連結至Facebook自訂對象。 每次客戶符合此區段的資格時，系統都會傳送訊號至Facebook伺服器端，將該客戶納入Facebook端的自訂對象中。

在Facebook中，您會在「自訂對象」下方找到來自Adobe Experience Platform的區段：

![RTCDP](./images/rtcdpcreatedest5b.png)

您現在可以看到自訂對象出現在Facebook中：

![RTCDP](./images/rtcdpcreatedest5a.png)

[返回使用者流程1](./uc1.md)

[返回所有模組](../../overview.md)
