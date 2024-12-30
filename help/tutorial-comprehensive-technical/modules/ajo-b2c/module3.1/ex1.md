---
title: Journey Optimizer建立您的活動
description: Journey Optimizer建立您的活動
kt: 5342
doc-type: tutorial
exl-id: b132ad78-aaa3-458d-9895-0935f8ba88bb
source-git-commit: f843c50af04d744a7d769f320b5b55a5e6d25ffd
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 3.1.1建立您的活動

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。

![ACOP](./images/acoptriglp.png)

在左側功能表中，向下捲動並按一下&#x200B;**組態**。 接著，按一下&#x200B;**事件**&#x200B;下的&#x200B;**管理**&#x200B;按鈕。

![ACOP](./images/acopmenu.png)

接著，您會看到所有可用事件的概觀。 按一下&#x200B;**建立事件**&#x200B;開始建立您自己的事件。

![ACOP](./images/emptyevent.png)

隨後即會出現新的空白事件視窗。

![ACOP](./images/emptyevent1.png)

首先，請為活動命名，如下所示： `--aepUserLdap--AccountCreationEvent`。
將描述設定為`Account Creation Event`，確定&#x200B;**型別**&#x200B;設定為&#x200B;**單一**，並針對&#x200B;**事件識別碼型別**&#x200B;選取專案，選取&#x200B;**系統產生**。

![ACOP](./images/eventdescription.png)

接下來是「結構描述」選項。 請使用結構描述`Demo System - Event Schema for Website (Global v1.1) v.1`。

![ACOP](./images/eventschema.png)

選取結構描述後，您將會在&#x200B;**裝載**&#x200B;區段中看到一些正在選取的欄位。 您現在應該將游標暫留在&#x200B;**裝載**&#x200B;區段上，將會看到3個圖示快顯視窗。 按一下&#x200B;**編輯**&#x200B;圖示。

![ACOP](./images/eventpayload.png)

您會看到&#x200B;**欄位**&#x200B;視窗快顯視窗，您必須在其中選取我們個人化電子郵件所需的部分欄位。  稍後我們將使用Adobe Experience Platform中已提供的資料，選擇其他設定檔屬性。

![ACOP](./images/eventfields.png)

在物件`--aepTenantId--.demoEnvironment`中，請確定選取欄位&#x200B;**brandLogo**&#x200B;和&#x200B;**brandName**。

![ACOP](./images/eventpayloadbr.png)

在物件`--aepTenantId--.identification.core`中，請確定選取欄位&#x200B;**電子郵件**。 按一下&#x200B;**確定**&#x200B;以儲存變更。

![ACOP](./images/eventpayloadbrid.png)

您應該會看到此訊息。 將&#x200B;**名稱空間**&#x200B;設定為&#x200B;**ECID (ECID)**。 按一下&#x200B;**儲存**。

![ACOP](./images/eventsave.png)

您的事件現在已設定並儲存。

![ACOP](./images/eventdone.png)

再次按一下您的事件以再次開啟&#x200B;**編輯事件**&#x200B;畫面。 再次將游標暫留在&#x200B;**承載**&#x200B;欄位上，可再次看到3個圖示。 按一下&#x200B;**檢視裝載**&#x200B;圖示。

![ACOP](./images/viewevent.png)

您現在將看到預期裝載的範例。

![ACOP](./images/fullpayload.png)

您的事件具有獨特的協調流程eventID，您可以在該承載中向下捲動直到看到`_experience.campaign.orchestration.eventID`為止。

事件ID需要傳送至Adobe Experience Platform，才能觸發您接下來要建立的歷程。 記住此eventID，因為您將在下一個練習中需要它。
`"eventID": "5ae9b8d3f68eb555502b0c07d03ef71780600c4bd0373a4065c692ae0bfbd34d"`

按一下&#x200B;**確定**。

![ACOP](./images/payloadeventID.png)

按一下&#x200B;**取消**。

![ACOP](./images/payloadeventID1.png)

您現在已經完成此練習。

下一步： [3.1.2建立要用於訊息中的片段](./ex2.md)

[返回模組3.1](./journey-orchestration-create-account.md)

[返回所有模組](../../../overview.md)
