---
title: 初始設定 — 從Adobe Target移轉至Adobe Journey Optimizer - Decisioning Mobile擴充功能
description: 瞭解並設定Platform Web SDK實作所需的重要基礎元素
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# 執行初始資料收集設定

從at.js移轉至Platform Web SDK時，必須進行初始設定，才能啟用Platform Web SDK的正確資料擷取、特色和功能。 必須先完成[Platform Web SDK實作教學課程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hant)中的下列步驟，才能進行任何網站實作變更：

- [在Adobe Admin Console中為資料收集設定適當的許可權](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"}
- [設定XDM結構描述](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target="_blank"}，以將結構化資料傳遞至Edge Network
- [設定身分名稱空間](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target="_blank"}，以使用跨裝置個人化和mbox3rdPartyId功能
- [建立資料串流](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target="_blank"}以啟用從Edge Network轉送資料
- [設定資料串流](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target="_blank"}以啟用將資料轉送至Adobe Target的功能

>[!CAUTION]
>
>請記住，這些設計方面應在Target、Analytics和Audience Manager移轉之間協調。

完成初始設定後，應使用Adobe Experience PlatformEdge Network啟用Target功能。

接下來，瞭解如何[取代at.js程式庫並設定基本的Platform Web SDK實作](replace-library.md)。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
