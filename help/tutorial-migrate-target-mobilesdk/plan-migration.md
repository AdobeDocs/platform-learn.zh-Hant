---
title: 規劃 — 從Adobe Target移轉至Adobe Journey Optimizer - Decisioning行動擴充功能
description: 瞭解如何針對從at.js 2.x到Adobe Experience Platform Web SDK的Adobe Target實作進行規劃。
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 規劃Target移轉至Decisioning擴充功能

在行動應用程式中將Target從Target擴充功能升級為Decisioning擴充功能之前，您應該先評估目前的實施情形。

## 評估目前的Target擴充功能實作

成功移轉的第一步，就是要清楚瞭解您目前的Target擴充功能實作。 有些您可能會使用的功能、函式及自訂程式碼需要更新。 評估時請考量下列事項：

### 支援哪些功能？

<!--Platform Web SDK is under continuous active development and features and enhancements are added regularly. As you evaluate your current at.js implementation, refer to the [supported use cases](https://github.com/orgs/adobe/projects/18/views/1) page for the latest information.-->

### 您現在使用哪些功能？

<!--Platform Web SDK is a new library that consolidates all Adobe solutions for the websites into a single SDK. This enables tighter integration and enables new capabilities unique to Adobe Experience Platform. However, this also means at.js functions are not backwards compatible with Platform Web SDK. As you evaluate your current implementation, make note of the following:

- at.js functions such as `getOffer()` and `applyOffer()`
- Modifications to Target's global settings
- Integration with Adobe Analytics
- Use of a flicker mitigation script
- Use of response tokens
- Use of mbox, profile, and entity parameters
- Custom code unique to your implementation-->

### 您將採取哪種移轉方法？

<!--Once you have revisited your at.js implementation, you need to determine a migration approach. There are two options:

- Migrate all Adobe applications at once across the entire site
- Migrate on a page-by-page basis

Because Platform Web SDK combines and enables multiple Adobe applications, you must coordinate the Target migration of other Adobe applications like Analytics and Audience Manager. All Adobe libraries on a given page should be migrated at the same time. A mixed implementation of Platform Web SDK for Target and AppMeasurement for Analytics on a particular page is not supported. However, a mixed implementation across different pages is supported, for example Platform Web SDK on page A, and at.js with AppMeasurement on page B.

As you migrate, you should plan on following your company's process for testing and releasing new code and use things like development, qa, and staging environments before you release to production.-->

<!--
>[!CAUTION]
>
>Redirect offers are not supported in page-by-page migrations if redirecting from a page with one library to a page with a different library
-->


接下來，檢閱Target擴充功能與Decisioning擴充功能](detailed-comparison.md)的詳細[比較，以更清楚瞭解技術差異，並找出需要額外關注的領域。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
