---
title: 1.1設定Adobe Experience Platform資料收集和Web SDK擴充功能
description: 基礎 — Adobe Experience Platform Data Collection和Web SDK擴充功能的設定
kt: 5342
doc-type: tutorial
exl-id: 8c613648-9007-49fb-898f-039c366297da
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# 1.1設定Adobe Experience Platform資料收集和Web SDK標籤擴充功能

此基礎模組會向您介紹Adobe的資料收集願景，並說明如何透過Adobe Experience Platform Data Collection、Adobe Experience Platform SDK和Adobe Experience Platform Edge Network，將網站和行動應用程式的資料匯入Adobe Experience Platform和其他應用程式。

此單元會介紹一些概念和技術，其影響超出Adobe Experience Platform技術教學課程的範圍。 應該清楚這些練習的哪些部分是完整教學課程其他部分的基礎，這些部分會教您更多有關Edge Network及其功能的知識，以及到哪裡取得進一步的資訊和教學課程。

## 學習目標

- 瞭解品牌如何使用Adobe Experience Platform資料收集作為其Tag Management系統(TMS)。
- 瞭解品牌用來將資料擷取至其Adobe產品的資料流程。
- 瞭解如何透過Adobe Experience Platform Edge Network將資料傳送至Adobe Experience Platform和其他產品。
- 瞭解如何建立從Web和Mobile收集資料的資料元素和規則。
- 瞭解[網頁SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)追蹤事件以及如何偵錯其內容。
- 瞭解什麼是資料層，以及Adobe在實作資料層時的建議。
- 瞭解從頭開始實作[網頁SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)的步驟。
- 瞭解網頁版和行動版實作之間的差異。

## 先決條件

- 存取Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- 存取Adobe Experience Platform資料彙集： [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- 存取示範網站

>[!NOTE]
>
>別忘了安裝、設定和使用[安裝Chrome檔案的Chrome擴充功能](../../../getting-started/gettingstarted/ex1.md)中提到的Experience League擴充功能

## 練習

[1.1.1瞭解Adobe Experience Platform資料收集](./ex1.md)

在本練習中，請探索Adobe Experience Platform資料收集UI並瞭解其功能。

[1.1.2 Edge Network、資料串流和伺服器端資料收集](./ex2.md)

在本練習中，您將瞭解如何在Adobe Experience Platform資料收集介面中轉送資料至Adobe產品，並調查示範網站使用的資料串流。

[1.1.3 Adobe Experience Platform資料彙集簡介](./ex3.md)

在本練習中，您將瞭解如何設定擴充功能、建置資料元素和規則，並將其發佈至網路。

[1.1.4使用者端Web資料收集](./ex4.md)

在本練習中，請對已安裝的Web SDK進行偵錯，以瞭解其運作方式，以及未來練習中將使用哪些資料。

[1.1.5實作Adobe Analytics和Adobe Audience Manager](./ex5.md)

在本練習中，請參閱並使用在Adobe Analytics和Adobe Audience Manager中透過Web SDK收集的網頁資料。

[1.1.6實作Adobe Target](./ex6.md)

在本練習中，設定在Adobe Target中透過網頁SDK實作的活動。

[1.1.7 Adobe Experience Platform中的XDM結構描述需求](./ex7.md)

為確保網頁SDK能夠將資料擷取到Adobe Experience Platform，您需要將特定XDM Mixin納入Adobe Experience Platform的XDM結構描述。

[摘要和優點](./summary.md)

本單元摘要和優點概觀。

![技術內部人士](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform及其應用程式的所有知識。 如果您有任何問題，想要分享對未來內容有建議的一般意見回饋，請傳送電子郵件至&#x200B;**techinsiders@adobe.com**，直接連絡技術業內人士。

[返回所有模組](./../../../../overview.md)
