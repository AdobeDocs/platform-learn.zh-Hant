---
title: Bootcamp — 即時客戶設定檔 — 視覺化您自己的即時客戶設定檔 — UI
description: Bootcamp — 即時客戶設定檔 — 視覺化您自己的即時客戶設定檔 — UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---

# 1.2將您自己的即時客戶設定檔視覺化 — UI

在本練習中，您將登入Adobe Experience Platform並在UI中檢視您自己的即時客戶個人檔案。

## Story

在即時客戶個人檔案中，所有個人檔案資料都會與事件資料以及現有區段會籍一起顯示。 顯示的資料可來自任何地方，包括Adobe應用程式和外部解決方案。 這是Adobe Experience Platform中最強大的檢視，真正的體驗記錄系統。

## 1.2.1在Adobe Experience Platform中使用客戶設定檔檢視

前往 [Adobe Experience Platform](https://experience.adobe.com/platform). 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./images/home.png)

在繼續之前，您需要選取 **沙箱**. 要選取的沙箱已命名 ``Bootcamp``. 您可以按一下文字來執行此操作 **[!UICONTROL 生產產品]** 在熒幕上方的藍線中。 選取適當的 [!UICONTROL 沙箱]，您會看到畫面變更，現在您已進入專屬團隊 [!UICONTROL 沙箱].

![資料擷取](./images/sb1.png)

在左側功能表中，前往 **設定檔** 和 **瀏覽**.

![客戶設定檔](./images/homemenu.png)

在您網站上的「設定檔檢視器」面板上，您可以找到身分總覽。 每個身分都會連結至名稱空間。

![客戶設定檔](./images/identities.png)

在「設定檔檢視器」面板上，您目前可以看見此身分：

| 命名空間 | 身分 |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

有了Adobe Experience Platform，所有ID都同等重要。 過去，ECID是Adobe內容中最重要的識別碼，其他所有ID都以階層式關係連結至ECID。 使用Adobe Experience Platform則不再如此，每個ID都可視為主要識別碼。

通常，主要識別碼取決於上下文。 如果您詢問客服中心， **最重要的識別碼為何？** 他們可能會回答， **電話號碼！** 但如果您詢問您的CRM團隊，他們會回答： **電子郵件地址！**  Adobe Experience Platform瞭解這種複雜性，並會為您進行管理。 每個應用程式(不論是Adobe應用程式或非Adobe應用程式)都會參照其視為主要的ID與Adobe Experience Platform交談。 而且它就是簡單的運作方式。

針對欄位 **身分名稱空間**，選取 **ECID** 欄位的and **身分值** 輸入您可在bootcamp網站的「設定檔檢視器」面板上找到的ECID。 按一下 **檢視**. 然後，您將在清單中看到您的設定檔。 按一下 **設定檔ID** 以開啟您的設定檔。

![客戶設定檔](./images/popupecid.png)

您現在看到幾項重要內容的概觀 **設定檔屬性** ，屬於您的客戶設定檔。

![客戶設定檔](./images/profile.png)

前往 **事件**，您可以在此處檢視連結至設定檔之每個體驗事件的專案。

![客戶設定檔](./images/profileee.png)

最後，前往功能表選項 **區段會籍**. 您現在會看到符合此設定檔資格的所有區段。

![客戶設定檔](./images/profileseg.png)

現在來建立一個新區段，讓您為匿名或認識的客戶個人化客戶體驗。

下一步： [1.3建立區段 — UI](./ex3.md)

[返回使用者流程1](./uc1.md)

[返回所有模組](../../overview.md)
