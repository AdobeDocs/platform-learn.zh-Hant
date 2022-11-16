---
title: 概述
description: 概述
exl-id: 527d8f73-33d0-45a6-b7a4-5e46cdb7c138
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 1%

---

# 使用Adobe Experience Platform資料收集

收集使用者瀏覽器中發生之事件的相關資料，是行銷策略的基本原則。 Adobe提供數種工具，可協助您管理此資料。 雖然您可以個別熟悉這些工具，但本教學課程會嘗試提供更廣泛的檢視，說明每種工具的功用，以及如何共同合作以達成共同目標。

在本教學課程中，我們將討論以下策略：

1. 在Adobe Experience Platform中建構資料並保留資料，
1. 在瀏覽器中管理資料並傳達已發生特定事件，以及
1. 透過傳送相關資料至Adobe Experience Platform回應此類事件。

本教學課程使用Adobe用戶端資料層、Adobe Experience Platform Web SDK和 [!DNL Tags] 功能可提供更規範、順暢的實作，您也可以將這些工具與協力廠商或內部工具混合搭配，以發揮最大彈性。

## 範例案例

在本教學課程中，您會為電子商務網站上的簡單產品頁面實作資料收集：

1. 產品頁面會載入瀏覽器中。 您可以在此追蹤使用者已檢視產品。
1. 使用者決定購買產品，因此按一下按鈕即可將產品新增至購物車。 在此，您可以追蹤使用者是否已開啟新購物車，並將體驗事件傳送至Adobe Experience Platform以將產品新增至購物車。
1. 最後，使用者點按 _下載應用程式_ 連結，因為他們對您的行動應用程式感興趣。 您可追蹤使用者是否已點按連結。

我們開始吧！

[下一個： ](structuring-your-data.md)

>[!NOTE]
>
>感謝您花時間學習資料收集。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
