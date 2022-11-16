---
title: Real-time CDP — 建立區段並採取行動 — 將區段傳送至DV360
description: Real-time CDP — 建立區段並採取行動 — 將區段傳送至DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7a78260f-cd25-4ed0-801b-87174babaffe
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 2%

---

# 6.3採取行動：將段發送到DV360

前往 [Adobe Experience Platform](https://experience.adobe.com/platform). 登入後，您會登陸Adobe Experience Platform首頁。

![資料擷取](../module2/images/home.png)

繼續之前，您需要選取 **沙箱**. 要選取的沙箱已命名 ``--aepSandboxId--``. 您可以按一下文字 **[!UICONTROL 生產產品]** 在螢幕上方的藍線。 選取適當的 [!UICONTROL 沙箱]，您會看到畫面變更，現在您已進入專屬 [!UICONTROL 沙箱].

![資料擷取](../module2/images/sb1.png)

在左側功能表中，前往 **目的地**，然後前往 **目錄**. 然後您會看到 **目的地目錄**.

![RTCDP](./images/rtcdpmenudest.png)

在 **目的地**，按一下 **啟用區段** 在 **Google Display &amp; Video 360** 卡片。

![RTCDP](./images/rtcdpgoogleseg.png)

選取您的目的地，然後按一下 **下一個**.

![RTCDP](./images/rtcdpcreatedest2.png)

在可用區段清單中，選取您在上一個練習中建立的區段。 按&#x200B;**「下一步」**。

![RTCDP](./images/rtcdpcreatedest3.png)

在 **區段排程** 頁面，按一下 **下一個**.

![RTCDP](./images/rtcdpcreatedest4.png)

最後，在 **檢閱** 頁面，按一下 **完成**.

![RTCDP](./images/rtcdpcreatedest5.png)

您的區段現在已連結至Google DV360。 每當客戶符合此區段的資格時，都會傳送訊號至Google DV360，將該客戶納入Google DV360端的「對象」中。

下一步： [6.4採取行動：將區段傳送至S3目的地](./ex4.md)

[返回模組6](./real-time-cdp-build-a-segment-take-action.md)

[返回所有模組](../../overview.md)
