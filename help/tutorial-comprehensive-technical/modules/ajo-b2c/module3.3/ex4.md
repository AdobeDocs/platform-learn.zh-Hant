---
title: Offer Decisioning — 使用示範網站測試您的決定
description: 使用示範網站測試您的決定
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# 3.3.4將Adobe Target與Offer Decisioning結合

## 3.3.4.1收集示範專案的分享連結

若要在Adobe Target中載入示範網站專案，您首先需要收集特殊連結，讓Adobe Target可載入您的示範網站專案。

若要這麼做，請前往[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案以開啟。

![RTCDP](./images/builder1.png)

您現在將會看到此訊息。 按一下&#x200B;**共用**。

![RTCDP](./images/builder2.png)

按一下&#x200B;**產生連結**，然後將連結複製到剪貼簿。

![RTCDP](./images/builder3.png)

移至[https://bitly.com](https://bitly.com)，貼上您複製的連結，然後按一下&#x200B;**縮短**。 您現在會取得縮短的連結，如下所示： `https://bit.ly/3JxN7aG`。 在下一個練習中，您將需要該連結。

![RTCDP](./images/builder4.png)

## 3.3.4.2收集

現在移至[https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/)，以移至Adobe Experience Cloud首頁。 按一下&#x200B;**目標**。

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/excl.png)

在&#x200B;**Adobe Target**&#x200B;首頁上，您會看到所有現有的活動。

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/exclatov.png)

按一下&#x200B;**+建立活動**&#x200B;以建立新活動。

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/exclatcr.png)

選取&#x200B;**體驗鎖定目標**。

![RTCDP](./images/exclatcrxt.png)

現在選取&#x200B;**Visual**，並將您縮短的連結貼到&#x200B;**輸入活動URL**&#x200B;欄位。 按一下&#x200B;**下一步**。

![RTCDP](./images/exclatcrxt1.png)

然後您會看到您的示範網站專案正載入到視覺化體驗撰寫器中。

![RTCDP](./images/vec1.png)

移至&#x200B;**瀏覽**&#x200B;模式，在Cookie同意快顯視窗中按一下&#x200B;**全部允許**。

![RTCDP](./images/vec2.png)

按一下包含文字&#x200B;**精選類別**&#x200B;的區域。 按一下&#x200B;**插入在**&#x200B;之前，然後選取&#x200B;**優惠決定**。

![RTCDP](./images/vec3.png)

然後您會看到此快顯視窗。 選取您的沙箱`--aepSandboxName--`，然後選取位置&#x200B;**網頁 — 影像**。

![RTCDP](./images/vec4.png)

接著，選取您的決定`--aepUserLdap-- - Luma Decision`。 按一下&#x200B;**儲存**。

![RTCDP](./images/vec5.png)

您將會看到此訊息。 確定新增其他範本規則&#x200B;**URL** **包含** **your-project-name**。 按一下&#x200B;**儲存**。

![RTCDP](./images/vec6.png)

您將會看到此訊息。 按一下&#x200B;**下一步**。

![RTCDP](./images/vec7.png)

輸入優惠方案名稱，使用此名稱： `--aepUserLdap-- - XT with Offers (VEC)`。 按一下&#x200B;**下一步**。

![RTCDP](./images/vec8.png)

您將會看到此訊息。 依照指示定義您的&#x200B;**目標量度**。 按一下&#x200B;**儲存並關閉**。

![RTCDP](./images/vec9.png)

您的選件現已建立並正在發佈。

![RTCDP](./images/vec10.png)

您的選件發佈後，您就可以啟用它。

下一步： [3.3.5在電子郵件和簡訊中使用您的決定](./ex5.md)

[返回模組3.3](./offer-decisioning.md)

[返回所有模組](./../../../overview.md)
