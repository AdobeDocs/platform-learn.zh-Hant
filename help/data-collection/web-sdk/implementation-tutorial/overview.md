---
title: 概述
description: 概述
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 8ffa258b-6ff7-4413-aead-21b106668c65
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# 概述

收集使用者瀏覽器中發生之事件的相關資料是行銷策略的基本原則。 Adobe提供了數種工具來協助您管理這些資料。 雖然您可以個別熟悉這些工具的各個部分，但本教學課程嘗試針對這些工具的功用，以及它們如何共同作業達成共同目標，提供更廣闊的視野。

在本教學課程中，我們將討論以下用途的策略：(1)在Adobe Experience Platform中建構並儲存您的資料，(2)在瀏覽器中管理您的資料並傳達某些事件發生了，以及(3)透過將相關資料傳送至Adobe Experience Platform來回應這些事件。

雖然本教學課程使用Adobe使用者端資料層、Adobe Experience Platform Web SDK和標籤功能，以實現更規範、順暢的實作，但您也可以將這些工具與第三方或內部工具混合搭配使用，以獲得最大的彈性。

## 範例情境

在本教學課程中，我們假設您正在電子商務網站上實作簡單產品頁面的資料收集。 產品頁面會載入瀏覽器。 在這裡，您將追蹤使用者是否已檢視產品。 使用者決定購買產品，因此他們點選按鈕將產品新增到購物車。 在此，您會將體驗事件傳送至Adobe Experience Platform，以追蹤使用者是否已開啟新購物車及將產品新增至購物車。 最後，使用者按一下 _下載應用程式_ 連結，因為他們對您的行動應用程式有興趣。 您將追蹤使用者是否已點按連結。
