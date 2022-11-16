---
title: 概述
description: 概述
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 8ffa258b-6ff7-4413-aead-21b106668c65
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# 概述

收集使用者瀏覽器中發生之事件的相關資料，是行銷策略的基本原則。 Adobe提供數種工具，可協助您管理此資料。 雖然您可以個別熟悉這些工具，但本教學課程會嘗試提供更廣泛的檢視，說明每種工具的功用，以及如何共同合作以達成共同目標。

在本教學課程中，我們將討論以下策略：(1)在Adobe Experience Platform中建構並保留您的資料；(2)在瀏覽器中管理您的資料並傳達已發生某些事件，以及(3)將相關資料傳送至Adobe Experience Platform以回應這類事件。

雖然本教學課程使用Adobe用戶端資料層、Adobe Experience Platform Web SDK和標籤功能，以更規範、順暢地實作，但您也可以將這些工具與協力廠商或內部工具混合搭配，以發揮最大彈性。

## 範例案例

在本教學課程中，我們假設您正在電子商務網站上實作簡單產品頁面的資料收集。 產品頁面會載入瀏覽器中。 在此，您將追蹤使用者已檢視產品。 使用者決定購買產品，因此按一下按鈕即可將產品新增至購物車。 在此，您將透過將體驗事件傳送至Adobe Experience Platform，追蹤使用者已開啟新購物車並將產品新增至購物車。 最後，使用者點按 _下載應用程式_ 連結，因為他們對您的行動應用程式感興趣。 您會追蹤使用者是否已點按連結。
