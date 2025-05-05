---
title: Real-time CDP — 建立對象並採取行動 — 建立對象
description: Real-time CDP — 建立對象並採取行動 — 建立對象
kt: 5342
doc-type: tutorial
exl-id: a46b1640-769d-4fb3-97e6-beaf9706efbf
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 2%

---

# 2.3.1建立對象

在本練習中，您將使用Adobe Experience Platform的對象產生器來建立對象。

## 內容

回應客戶興趣必須是即時的。 即時回應客戶行為的其中一個方式是使用對象，但前提是對象符合即時資格。 在本練習中，您需要建立受眾，考量我們一直在使用的網站上的實際活動。

## 識別您要回應的行為

移至[https://dsn.adobe.com](https://dsn.adobe.com)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案上的3個點&#x200B;**...**，然後按一下&#x200B;**執行**&#x200B;以開啟它。

![DSN](./../../datacollection/module1.1/images/web8.png)

然後您會看到示範網站已開啟。 選取URL並將其複製到剪貼簿。

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

開啟新的無痕瀏覽器視窗。

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

貼上您在上一步中複製的示範網站URL。 接著，系統會要求您使用Adobe ID登入。

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

選取您的帳戶型別並完成登入程式。

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

接著，您會在無痕瀏覽器視窗中看到您的網站已載入。 每次練習都需要使用全新的無痕瀏覽器視窗，才能載入您的示範網站URL。

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

在此範例中，您想要回應檢視特定產品的特定客戶。
從&#x200B;**Citi Signal**&#x200B;首頁，移至&#x200B;**手機和裝置**，然後按一下產品&#x200B;**Galaxy S24**。

![資料擷取](./images/homegalaxy.png)

所以當有人造訪&#x200B;**Galaxy S24**&#x200B;的產品頁面時，您想要能夠採取行動。 要採取行動，首先要定義對象。

![資料擷取](./images/homegalaxy1.png)

## 建立對象

移至[Adobe Experience Platform](https://experience.adobe.com/platform)。 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./../../../modules/datacollection/module1.2/images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--aepSandboxName--``。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。

![資料擷取](./../../../modules/datacollection/module1.2/images/sb1.png)

在左側的功能表中，前往&#x200B;**對象**，然後前往&#x200B;**瀏覽**，您可以在其中檢視所有現有對象的概觀。 按一下&#x200B;**建立對象**&#x200B;按鈕以開始建立新對象。

![區段](./images/menuseg.png)

選取&#x200B;**建置規則**&#x200B;並按一下&#x200B;**建立**。

![區段](./images/menuseg1.png)

如上所述，您必須從已檢視產品&#x200B;**Galaxy S24**&#x200B;的所有客戶中建立對象。

若要建立此對象，您必須新增事件。 按一下&#x200B;**受眾**&#x200B;功能表列中的&#x200B;**事件**&#x200B;圖示，即可找到所有事件。

接下來，您將會看到頂層&#x200B;**XDM ExperienceEvent**&#x200B;節點。

若要尋找已造訪&#x200B;**Galaxy S24**&#x200B;產品的客戶，請按一下&#x200B;**XDM ExperienceEvent**。

![區段](./images/findee.png)

向下捲動至&#x200B;**產品清單專案**，然後按一下它。

![區段](./images/see.png)

選取「**名稱**」，然後從左側「**產品清單專案**」功能表將「**名稱**」物件拖放至對象產生器畫布的「**事件**」區段。

![區段](./images/eewebpdtlname1.png)

比較引數應為&#x200B;**等於**，並在輸入欄位中輸入`Galaxy S24`。

![區段](./images/pv.png)

您的&#x200B;**事件規則**&#x200B;現在看起來應該像這樣。 每次將元素新增至對象產生器時，您都可以按一下&#x200B;**重新整理預估值**&#x200B;按鈕，以取得對象中母體的新預估值。

![區段](./images/ldap4.png)

提供對象名稱，並將&#x200B;**評估方法**&#x200B;設定為&#x200B;**Edge**。

作為命名慣例，請使用：

- `--aepUserLdap-- - Interest in Galaxy S24`

接著，按一下&#x200B;**Publish**&#x200B;按鈕以儲存您的對象。

![區段](./images/segmentname.png)

您現在將返回對象總覽頁面。

![區段](./images/savedsegment.png)

下一步： [2.3.2檢閱如何使用目的地](./ex2.md)設定DV360目的地

[返回模組2.3](./real-time-cdp-build-a-segment-take-action.md)

[返回所有模組](../../../overview.md)
