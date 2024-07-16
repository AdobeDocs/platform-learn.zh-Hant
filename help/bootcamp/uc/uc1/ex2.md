---
title: Bootcamp — 即時客戶設定檔 — 視覺化您自己的即時客戶設定檔 — UI
description: Bootcamp — 即時客戶設定檔 — 視覺化您自己的即時客戶設定檔 — UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 1.2視覺化您自己的即時客戶設定檔 — UI

在本練習中，您將登入Adobe Experience Platform並在UI中檢視您自己的即時客戶個人檔案。

## Story

在即時客戶個人檔案中，所有個人檔案資料都會與事件資料一起顯示，以及顯示現有的受眾會籍。 顯示的資料可來自任何地方，包括Adobe應用程式和外部解決方案。 這是Adobe Experience Platform中最強大的檢視畫面，真正的體驗記錄系統。

## 1.2.1在Adobe Experience Platform中使用客戶設定檔檢視

移至[Adobe Experience Platform](https://experience.adobe.com/platform)。 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``Bootcamp``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。



在左側功能表中，移至&#x200B;**設定檔**&#x200B;和&#x200B;**瀏覽**。

![客戶設定檔](./images/homemenu.png)

您可以在網站上的「設定檔檢視器」面板上找到身分總覽。 每個身分都會連結至名稱空間。

![客戶設定檔](./images/identities.png)




有了Adobe Experience Platform，所有ID都同等重要。 之前，ECID是Adobe內容中最重要的訪客ID，其他所有ID都是以階層式關係連結至ECID。 使用Adobe Experience Platform後，情況已完全不同，每個ID都可視為主要識別碼。

通常，主要識別碼取決於內容。 如果您詢問客服中心，**最重要的識別碼是什麼？**&#x200B;他們可能會接聽，**電話號碼！**，但如果您詢問您的CRM團隊，他們會回答，**電子郵件地址！** Adobe Experience Platform瞭解這項複雜性，並為您管理它。 每個應用程式(不論是Adobe應用程式或非Adobe應用程式)都會參照其視為主要的ID與Adobe Experience Platform交談。 而且它就是這麼運作的。

對於&#x200B;**身分名稱空間**&#x200B;欄位，請選取&#x200B;**ECID**，對於&#x200B;**身分值**&#x200B;欄位，請輸入您可以在bootcamp網站的[設定檔檢視器]面板上找到的ECID。 按一下&#x200B;**檢視**。 然後，您將在清單中看到您的設定檔。 按一下&#x200B;**設定檔識別碼**&#x200B;以開啟您的設定檔。

![客戶設定檔](./images/popupecid.png)

您現在可以看到客戶設定檔的一些重要&#x200B;**設定檔屬性**&#x200B;的概觀。

![客戶設定檔](./images/profile.png)

移至&#x200B;**事件**，您可在其中檢視連結至設定檔之每個體驗事件的專案。

![客戶設定檔](./images/profileee.png)

最後，移至功能表選項&#x200B;**對象會籍**。 您現在會看到符合此設定檔資格的所有對象。

![客戶設定檔](./images/profileseg.png)

現在，讓我們建立新的對象，好讓您為匿名或認識的客戶個人化客戶體驗。

下一步： [1.3建立對象 — UI](./ex3.md)

[返回使用者流程1](./uc1.md)

[返回所有模組](../../overview.md)
