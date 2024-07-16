---
title: Bootcamp — 混合實體和數位 — Journey Optimizer建立您的活動
description: Bootcamp — 混合實體和數位 — Journey Optimizer建立您的活動
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 3d47c686-c2d8-4961-a05b-0990025392fa
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 3.2建立您的活動

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`Bootcamp`。 若要從一個沙箱變更為另一個沙箱，請按一下&#x200B;**Prod**&#x200B;並從清單中選取該沙箱。 在此範例中，沙箱名為&#x200B;**Bootcamp2**。 然後您就會進入沙箱`Bootcamp`的&#x200B;**首頁**&#x200B;檢視。

![ACOP](./images/acoptriglp.png)

在左側功能表中，向下捲動並按一下&#x200B;**組態**。 接著，按一下&#x200B;**事件**&#x200B;下的&#x200B;**管理**&#x200B;按鈕。

![ACOP](./images/acopmenu.png)

接著，您會看到所有可用事件的概觀。 按一下&#x200B;**建立事件**&#x200B;開始建立您自己的事件。

![ACOP](./images/emptyevent.png)

隨後即會出現新的空白事件視窗。

首先，請為事件命名如下： `yourLastNameBeaconEntryEvent`並新增說明，如`Beacon Entry Event`。

![ACOP](./images/eventdescription.png)

接下來，確定&#x200B;**型別**&#x200B;設定為&#x200B;**單一**，並且針對&#x200B;**事件識別碼型別**&#x200B;選取專案，選取&#x200B;**系統產生**。

![ACOP](./images/eventidtype.png)

接下來是「結構描述」選項。 已針對此練習準備結構描述。 請使用結構描述`Demo System - Event Schema for Mobile App (Global v1.1) v.1`。

![ACOP](./images/eventschema.png)

選取結構描述後，您會在&#x200B;**欄位**&#x200B;區段中看到許多選取的欄位。 您現在應該暫留在&#x200B;**欄位**&#x200B;區段上，將會看到3個圖示快顯視窗。 按一下&#x200B;**編輯**&#x200B;圖示。

![ACOP](./images/eventpayload.png)

您會看到&#x200B;**欄位**&#x200B;視窗快顯視窗，您必須在其中選取我們個人化歷程所需的一些欄位。  稍後我們將使用Adobe Experience Platform中已提供的資料，選擇其他設定檔屬性。

![ACOP](./images/eventfields.png)

向下捲動，直到您看到物件`Place context`為止，然後核取核取方塊。 透過此專案，客戶位置的所有內容都可供歷程使用。 按一下&#x200B;**確定**&#x200B;以儲存變更。

![ACOP](./images/eventpayloadbr.png)

您應該會看到此訊息。 再按一次「儲存&#x200B;****」以儲存變更。

![ACOP](./images/eventsave.png)

您的事件現在已設定並儲存。

![ACOP](./images/eventdone.png)

再次按一下您的事件以再次開啟&#x200B;**編輯事件**&#x200B;畫面。 再次將游標暫留在&#x200B;**欄位**&#x200B;上可看到3個圖示。 按一下&#x200B;**檢視**&#x200B;圖示。

![ACOP](./images/viewevent.png)

您現在將看到預期裝載的範例。
您的事件具有獨特的協調流程eventID，您可以在該承載中向下捲動直到看到`_experience.campaign.orchestration.eventID`為止。

![ACOP](./images/payloadeventID.png)

事件ID是必須傳送至Adobe Experience Platform的專案，才能觸發您將在下一個練習中建立的歷程。 記住此eventID，因為您稍後可能會需要它。
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

按一下&#x200B;**確定**，然後按一下&#x200B;**取消**。

您現在已經完成此練習。

下一步： [3.3建立您的歷程及推播通知](./ex3.md)

[返回使用者流程3](./uc3.md)

[返回所有模組](../../overview.md)
