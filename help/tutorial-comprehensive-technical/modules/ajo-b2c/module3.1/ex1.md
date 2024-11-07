---
title: Journey Optimizer建立您的活動
description: Journey Optimizer建立您的活動
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 3.1.1建立您的活動

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。 若要從一個沙箱變更為另一個沙箱，請按一下&#x200B;**PRODUCTION Prod (VA7)**，然後從清單中選取沙箱。 在此範例中，沙箱名為&#x200B;**AEP Enablement FY22**。 然後您就會進入沙箱`--aepSandboxName--`的&#x200B;**首頁**&#x200B;檢視。

![ACOP](./images/acoptriglp.png)

在左側功能表中，向下捲動並按一下&#x200B;**組態**。 接著，按一下&#x200B;**事件**&#x200B;下的&#x200B;**管理**&#x200B;按鈕。

![ACOP](./images/acopmenu.png)

接著，您會看到所有可用事件的概觀。 按一下&#x200B;**建立事件**&#x200B;開始建立您自己的事件。

![ACOP](./images/emptyevent.png)

隨後即會出現新的空白事件視窗。

![ACOP](./images/emptyevent1.png)

首先，請為活動命名，如下所示： `--aepUserLdap--AccountCreationEvent`。

![ACOP](./images/eventname.png)

接下來，新增類似此`Account Creation Event`的說明。

![ACOP](./images/eventdescription.png)

接下來，確定&#x200B;**型別**&#x200B;設定為&#x200B;**單一**，並且針對&#x200B;**事件識別碼型別**&#x200B;選取專案，選取&#x200B;**系統產生**。

![ACOP](./images/eventidtype.png)

接下來是「結構描述」選項。 已針對此練習準備結構描述。 請使用結構描述`Demo System - Event Schema for Website (Global v1.1) v.1`。

![ACOP](./images/eventschema.png)

選取結構描述後，您將會在&#x200B;**裝載**&#x200B;區段中看到一些正在選取的欄位。 您現在應該將游標暫留在&#x200B;**裝載**&#x200B;區段上，將會看到3個圖示快顯視窗。 按一下&#x200B;**編輯**&#x200B;圖示。

![ACOP](./images/eventpayload.png)

您會看到&#x200B;**欄位**&#x200B;視窗快顯視窗，您必須在其中選取我們個人化電子郵件所需的部分欄位。  稍後我們將使用Adobe Experience Platform中已提供的資料，選擇其他設定檔屬性。

![ACOP](./images/eventfields.png)

在物件`--aepTenantId--.demoEnvironment`中，請確定選取欄位&#x200B;**brandLogo**&#x200B;和&#x200B;**brandName**。

![ACOP](./images/eventpayloadbr.png)

在物件`--aepTenantId--.identification.core`中，請確定選取欄位&#x200B;**電子郵件**。

![ACOP](./images/eventpayloadbrid.png)

按一下&#x200B;**確定**&#x200B;以儲存變更。

![ACOP](./images/saveok.png)

您應該會看到以下內容：

![ACOP](./images/eventsave.png)

再按一次「儲存&#x200B;****」以儲存變更。

![ACOP](./images/save1.png)

您的事件現在已設定並儲存。

![ACOP](./images/eventdone.png)

再次按一下您的事件以再次開啟&#x200B;**編輯事件**&#x200B;畫面。 再次將游標暫留在&#x200B;**承載**&#x200B;欄位上，可再次看到3個圖示。 按一下&#x200B;**檢視裝載**&#x200B;圖示。

![ACOP](./images/viewevent.png)

您現在將看到預期裝載的範例。

![ACOP](./images/fullpayload.png)

您的事件具有獨特的協調流程eventID，您可以在該承載中向下捲動直到看到`_experience.campaign.orchestration.eventID`為止。

![ACOP](./images/payloadeventID.png)

事件ID需要傳送至Adobe Experience Platform，才能觸發您將在練習7.2中建立的歷程。請記住此eventID，因為您會在練習7.3中需要它。
`"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`

按一下&#x200B;**確定**，然後按一下&#x200B;**取消**。

您現在已經完成此練習。

下一步： [3.1.2 Journey Optimizer：建立您的歷程與電子郵件訊息](./ex2.md)

[返回模組3.1](./journey-orchestration-create-account.md)

[返回所有模組](../../../overview.md)
