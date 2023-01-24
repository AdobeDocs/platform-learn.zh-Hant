---
title: Bootcamp — 即時客戶設定檔 — 視覺化您自己的即時客戶設定檔 — UI — 巴西
description: Bootcamp — 即時客戶設定檔 — 視覺化您自己的即時客戶設定檔 — UI — 巴西
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# 1.2將您自己的即時客戶個人檔案視覺化 — UI

在本練習中，您將登入Adobe Experience Platform，並在UI中檢視您自己的即時客戶個人檔案。

## Story

在即時客戶設定檔中，所有設定檔資料會與事件資料以及現有區段成員資格一起顯示。 顯示的資料可以來自任何位置、Adobe應用程式和外部解決方案。 這是Adobe Experience Platform最強大的觀點，也是真正的體驗系統。

## 1.2.1使用Adobe Experience Platform中的「客戶個人檔案檢視」

前往 [Adobe Experience Platform](https://experience.adobe.com/platform). 登入後，您會登陸Adobe Experience Platform首頁。

![資料擷取](./images/home.png)

繼續之前，您需要選取 **沙箱**. 要選取的沙箱已命名 ``Bootcamp``. 您可以按一下文字 **[!UICONTROL 生產產品]** 在螢幕上方的藍線。 選取適當的 [!UICONTROL 沙箱]，您會看到畫面變更，現在您已進入專屬 [!UICONTROL 沙箱].

![資料擷取](./images/sb1.png)

在左側功能表中，前往 **設定檔** 和 **瀏覽**.

![客戶設定檔](./images/homemenu.png)

在您網站的「設定檔檢視器」面板上，您可以找到身分概述。 每個身分都會連結至命名空間。

![客戶設定檔](./images/identities.png)

在「設定檔檢視器」面板上，您目前可以看到此身分：

| 命名空間 | 身分 |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

有了Adobe Experience Platform，所有ID都同樣重要。 過去，ECID是Adobe內容中最重要的ID，而所有其他ID則以階層關係連結至ECID。 有了Adobe Experience Platform，情況就不再如此，每個ID都可視為主要識別碼。

主要識別碼通常取決於內容。 如果你問問你的呼叫中心， **最重要的ID為何？** 他們很可能會回答， **電話號碼！** 但如果你問你的CRM團隊，他們會回答， **電子郵件地址！**  Adobe Experience Platform了解這種複雜性，並為您管理。 每個應用程式(無論是Adobe應用程式或非Adobe應用程式)都會參照其視為主要的ID，與Adobe Experience Platform通話。 它就是有效的。

針對欄位 **身分命名空間**，選取 **ECID** 和 **身分值** 在bootcamp網站的「配置檔案查看器」面板上輸入可以找到的ECID。 按一下 **檢視**. 然後，您會在清單中看到您的個人資料。 按一下 **設定檔ID** 來開啟您的個人資料。

![客戶設定檔](./images/popupecid.png)

您現在會看到以下幾個重要項目的概述 **設定檔屬性** 客戶個人檔案。

![客戶設定檔](./images/profile.png)

前往 **事件**，您可以在其中看到連結至您設定檔之每個體驗事件的項目。

![客戶設定檔](./images/profileee.png)

最後，移至功能表選項 **區段成員資格**. 您現在會看到所有符合此設定檔資格的區段。

![客戶設定檔](./images/profileseg.png)

現在來建立新區段，讓您為匿名或了解的客戶個人化客戶體驗。

下一步： [1.3建立區段 — UI](./ex3.md)

[返回用戶流1](./uc1.md)

[返回所有模組](../../overview.md)
