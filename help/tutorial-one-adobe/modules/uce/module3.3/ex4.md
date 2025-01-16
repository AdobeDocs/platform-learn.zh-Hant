---
title: Offer Decisioning — 使用示範網站測試您的決定
description: 使用示範網站測試您的決定
kt: 5342
doc-type: tutorial
source-git-commit: 926f0f1f6d6b557fd7e59a89aaa3e09d831c82a6
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%

---

# 3.3.4將Adobe Target與Offer Decisioning結合

## 3.3.4.1收集示範專案的分享連結

若要在Adobe Target中載入示範網站專案，您首先需要收集特殊連結，讓Adobe Target可載入您的示範網站專案。

若要這麼做，請前往[https://dsn.adobe.com/projects](https://builder.adobedemo.com/projects)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案以開啟。

![RTCDP](./images/builder1.png)

您現在將會看到此訊息。 移至&#x200B;**共用**。 按一下&#x200B;**產生連結**，然後將連結複製到剪貼簿。

![RTCDP](./images/builder2.png)

移至[https://bitly.com](https://bitly.com)，貼上您複製的連結，然後按一下&#x200B;**建立您的連結**。

![RTCDP](./images/builder4.png)

您現在會取得縮短的連結，如下所示： `https://adobe.ly/3PpGcFk`。 在下一個練習中，您將需要該連結。

![RTCDP](./images/builder5.png)

## 3.3.4.2收集

現在移至[https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/)，以移至Adobe Experience Cloud首頁。 按一下&#x200B;**目標**。

在&#x200B;**Adobe Target**&#x200B;首頁上，您會看到所有現有的活動。 按一下&#x200B;**建立活動**，然後按一下&#x200B;**體驗鎖定目標**。

現在選取&#x200B;**Visual**，並將您縮短的連結貼到&#x200B;**輸入活動URL**&#x200B;欄位。 按一下&#x200B;**建立**。

![RTCDP](./images/exclatcrxt1.png)

然後您會看到您的示範網站專案正載入到視覺化體驗撰寫器中。

>[!NOTE]
>
>如果您的網站未正確載入，請從Chrome網站商店安裝並啟用此Chrome擴充功能： **Adobe Target VEC Helper**，然後再試一次。

![RTCDP](./images/vec1.png)

按一下Disney+優惠方案所在的區域。 請確定選取完整的&#x200B;**容器**。 按一下&#x200B;**插入在**&#x200B;之前，然後選取&#x200B;**優惠決定**。

![RTCDP](./images/vec3.png)

然後您會看到此快顯視窗。 選取您的沙箱`--aepSandboxName--`，然後選取位置&#x200B;**網頁 — 影像**。

![RTCDP](./images/vec4.png)

接著，選取您的決定`--aepUserLdap-- - CitiSignal Decision`。 按一下&#x200B;**儲存**。

![RTCDP](./images/vec5.png)

您將會看到此訊息。 按一下&#x200B;**檢閱規則**。

![RTCDP](./images/vec5a.png)

確定新增其他範本規則&#x200B;**URL** **包含** **your-project-name**。 按一下&#x200B;**儲存**。

![RTCDP](./images/vec6.png)

您將會看到此訊息。 按一下&#x200B;**下一步**。

![RTCDP](./images/vec7.png)

輸入優惠方案名稱，使用此名稱： `--aepUserLdap-- - XT with Offers (VEC)`。 按一下&#x200B;**下一步**。

![RTCDP](./images/vec8.png)

您將會看到此訊息。 依照指示定義您的&#x200B;**目標量度**。 按一下&#x200B;**儲存並關閉**。

![RTCDP](./images/vec9.png)

您的選件現已建立並正在發佈。 您的選件發佈後，您就可以啟用它。

![RTCDP](./images/vec11.png)

下一步： [3.3.5在電子郵件和簡訊中使用您的決定](./ex5.md)

[返回模組3.3](./offer-decisioning.md)

[返回所有模組](./../../../overview.md)
