---
title: 初始設定 |將Target從at.js 2.x移轉至Web SDK
description: 了解並設定您的Platform Web SDK實作所需的重要基礎元素
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 2%

---

# 執行初始資料收集設定

從at.js移轉至Platform Web SDK需要初始設定，才能啟用Platform Web SDK的適當資料擷取、功能和函式。 下列步驟： [Platform Web SDK實作教學課程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hant) 必須先完成，才能進行任何網站實作變更：

- [設定適當的權限](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-permissions.html)Adobe Admin Console中用於資料收集的{target=&quot;_blank&quot;}
- [設定XDM結構](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target=&quot;_blank&quot;}，用於將結構化資料傳遞至邊緣網路
- [設定身分命名空間](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html)用於跨裝置個人化和mbox3rdPartyId功能的{target=&quot;_blank&quot;}
- [建立資料流](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target=&quot;_blank&quot;}啟用邊緣網路中資料的轉送
- [設定資料流](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target=&quot;_blank&quot;}啟用將資料轉送至Adobe Target

>[!CAUTION]
>
>請記住，Web SDK的這些設計層面必須在Target、Analytics和Audience Manager移轉之間進行協調。

完成初始設定後，應使用Adobe Experience Platform邊緣網路啟用Target功能。

接下來，學習如何 [取代at.js程式庫並設定基本的Platform Web SDK實作](replace-library.md).

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
