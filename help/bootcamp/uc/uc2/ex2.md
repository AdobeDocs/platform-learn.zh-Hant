---
title: Bootcamp - Journey Optimizer建立您的活動
description: Bootcamp - Journey Optimizer建立您的活動
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 89db40ab-d4c5-4310-aca6-cb64828e7bc9
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 2.2建立事件

前往登入Adobe Journey Optimizer [Adobe Experience Cloud](https://experience.adobe.com). 按一下 **Journey Optimizer**.

![ACOP](./images/acophome.png)

系統會將您重新導向至 **首頁**  檢視。 首先，請確定您使用的沙箱正確無誤。 系統會呼叫要使用的沙箱 `Bootcamp`. 若要從一個沙箱變更為另一個沙箱，請按一下 **生產** 並從清單中選取沙箱。 在此範例中，沙箱的名稱為 **布坎普**. 那你就在 **首頁** 沙箱檢視 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

在左側功能表中，向下捲動並按一下 **配置**. 下一步，按一下 **管理** 按鈕 **事件**.

![ACOP](./images/acopmenu.png)

之後，您將會看到所有可用事件的概觀。 按一下 **建立事件** 以開始建立您自己的事件。

![ACOP](./images/emptyevent.png)

接著會出現新的空事件視窗。

![ACOP](./images/emptyevent1.png)

首先，為您的事件命名如下： `yourLastNameAccountCreationEvent` 並添加這樣的說明 `Account Creation Event`.

![ACOP](./images/eventdescription.png)

接下來，請確定 **類型** 設為 **單一**，和 **事件ID類型** 選擇，選擇 **系統生成**.

![ACOP](./images/eventidtype.png)

接下來是「結構」選項。 為本練習準備了方案。 請使用架構 `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

選取結構後，您會在 **欄位** 區段。 您現在應將滑鼠暫留在 **欄位** 區段中顯示3個圖示快顯視窗。 按一下 **編輯** 表徵圖。

![ACOP](./images/eventpayload.png)

你會看到 **欄位** 視窗快顯視窗，您需要在其中選取我們個人化電子郵件所需的一些欄位。  我們稍後會使用Adobe Experience Platform中已有的資料，選擇其他設定檔屬性。

![ACOP](./images/eventfields.png)

在物件中 `_experienceplatform.demoEnvironment`，請務必選取欄位 **brandLogo** 和 **brandName**.

![ACOP](./images/eventpayloadbr.png)

在物件中 `_experienceplatform.identification.core`，請務必選取欄位 **電子郵件**.

![ACOP](./images/eventpayloadbrid.png)

按一下 **確定** 來儲存變更。

![ACOP](./images/saveok.png)

你應該看看這個。 按一下 **儲存** 以儲存變更。

![ACOP](./images/eventsave.png)

您的事件現在已設定並儲存。

![ACOP](./images/eventdone.png)

再按一下您的事件以開啟 **編輯事件** 畫面。 暫留在 **欄位** 再看3個圖示。 按一下 **檢視裝載** 表徵圖。

![ACOP](./images/viewevent.png)

您現在會看到預期有效負載的範例。
您的事件有唯一的協調eventID，您可以在該裝載中向下捲動以找到它，直到您看到 `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

事件ID是需要傳送至Adobe Experience Platform的項目，以觸發您將在下一個練習中建立的歷程。 記住此eventID，因為您稍後可能需要它。
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

按一下 **確定**，然後按一下 **取消**.

你已經完成了這個練習。

下一步： [2.3建立您的電子郵件訊息](./ex3.md)

[返回用戶流2](./uc2.md)

[返回所有模組](../../overview.md)
