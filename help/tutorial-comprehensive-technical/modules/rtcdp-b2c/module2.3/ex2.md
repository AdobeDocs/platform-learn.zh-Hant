---
title: Real-time CDP — 建立區段並採取行動 — 設定Advertising目的地，如Google DV360
description: Real-time CDP — 建立區段並採取行動 — 設定Advertising目的地，如Google DV360
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 1%

---

# 2.3.2設定Advertising目的地，例如Google DV360

>[!IMPORTANT]
>
>以下內容僅供參考 — 您&#x200B;**不**&#x200B;必須設定DV360的新目的地。 目的地已建立，您可以在下一個練習中使用它。

移至[Adobe Experience Platform](https://experience.adobe.com/platform)。 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./../../../modules/datacollection/module1.2/images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--aepSandboxName--``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。

![資料擷取](./../../../modules/datacollection/module1.2/images/sb1.png)

在左側功能表中，前往&#x200B;**目的地**，然後前往&#x200B;**目錄**。 然後您會看到&#x200B;**目的地目錄**。

![RTCDP](./images/rtcdp.png)

在&#x200B;**目的地**&#x200B;中，按一下&#x200B;**Google Display &amp; Video 360**，然後按一下&#x200B;**+設定**。

![RTCDP](./images/rtcdpgoogle.png)

您將會看到此訊息。 按一下&#x200B;**連線到目的地**。

![RTCDP](./images/rtcdpgooglecreate1.png)

在下一個畫面中，您可以將目的地設定為Google DV360。

![RTCDP](./images/rtcdpgooglecreatedest.png)

在&#x200B;**Name**&#x200B;和&#x200B;**Description**&#x200B;欄位中輸入值。

欄位&#x200B;**帳戶ID**&#x200B;是DV360帳戶的&#x200B;**廣告商ID**。 您可在這裡找到：

![RTCDP](./images/rtcdpgoogledv360advid.png)

**帳戶型別**&#x200B;應設為&#x200B;**邀請廣告商**。

現在您已擁有此專案。 按一下&#x200B;**下一步**。

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google需要允許清單Adobe，才能讓Adobe Experience Platform將資料傳送至Google DV360。 請聯絡您的Google客戶經理，以啟用此資料流。

建立目的地後，您會看到此訊息。 您可以選擇選取資料治理原則。 接著，按一下&#x200B;**儲存並結束**。

![RTCDP](./images/rtcdpcreatedest1.png)

之後，您會看到可用目的地的清單。
在下一個練習中，您會將您在上一個練習中建立的區段連線至Google DV360目的地。

下一步： [2.3.3採取動作：將您的區段傳送至DV360](./ex3.md)

[返回模組2.3](./real-time-cdp-build-a-segment-take-action.md)

[返回所有模組](../../../overview.md)
