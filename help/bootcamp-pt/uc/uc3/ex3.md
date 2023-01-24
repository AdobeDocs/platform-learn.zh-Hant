---
title: Bootcamp — 混合物理和數位 — Journey Optimizer建立歷程並推播 — 巴西通知
description: Bootcamp — 混合物理和數位 — Journey Optimizer建立歷程並推播 — 巴西通知
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---

# 3.3建立您的歷程和推播通知

在本練習中，您將設定當使用者使用行動應用程式進入信標時需要觸發的歷程和訊息。

前往登入Adobe Journey Optimizer [Adobe Experience Cloud](https://experience.adobe.com). 按一下 **Journey Optimizer**.

![ACOP](./images/acophome.png)

系統會將您重新導向至 **首頁**  檢視。 首先，請確定您使用的沙箱正確無誤。 系統會呼叫要使用的沙箱 `Bootcamp`. 若要從一個沙箱變更為另一個沙箱，請按一下 **生產** 並從清單中選取沙箱。 在此範例中，沙箱的名稱為 **布坎普**. 那你就在 **首頁** 沙箱檢視 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1建立您的歷程

在左側功能表中，按一下 **歷程**. 下一步，按一下 **建立歷程** 來建立新歷程。

![ACOP](./images/createjourney.png)

然後您會看到空白的歷程畫面。

![ACOP](./images/journeyempty.png)

在上一個練習中，您建立了 **事件**. 你給它起了這個名字 `yourLastNameBeaconEntryEvent` 和 `yourLastName` 姓氏。 這是建立事件的結果：

![ACOP](./images/eventdone.png)

您現在需要將此活動視為此歷程的開始。 您可以前往畫面左側，並在事件清單中搜尋您的事件，以執行此操作。

![ACOP](./images/eventlist.png)

選取您的事件，將其拖放至歷程畫布上。 你的旅程現在看起來像這樣。 按一下 **確定** 來儲存變更。

![ACOP](./images/journeyevent.png)

作為歷程的第二步，您需要新增 **推播** 動作。 前往畫面左側，前往 **動作**，請選取 **推播** 動作，然後將其拖放至歷程中的第二個節點。

![ACOP](./images/journeyactions.png)

現在，您需要在畫面的右側建立推播通知。

設定 **類別** to **行銷** 和選取可讓您傳送推播通知的推播表面。 在這種情況下，要選取的推動曲面為 **mmeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2建立訊息

按一下 **編輯內容**.

![ACOP](./images/emptymsg.png)

然後您會看到：

![ACOP](./images/emailmsglist.png)

讓我們定義推播通知的內容。

按一下 **標題** 文字欄位。

![Journey Optimizer](./images/msg5.png)

在文本區域開始寫 **你好**. 按一下個人化圖示。

![Journey Optimizer](./images/msg6.png)

您現在需要為欄位帶入個人化代號 **名字** 儲存於 `profile.person.name.firstName`. 在左側功能表中，選取 **設定檔屬性**，向下捲動/導覽以尋找 **人員** 元素，然後按一下箭頭以往更深的層級，直到您到達欄位為止 `profile.person.name.firstName`. 按一下 **+** 圖示將欄位新增至畫布。 按一下「**儲存**」。

![Journey Optimizer](./images/msg7.png)

你會回來的。 按一下欄位旁的個人化圖示 **主體**.

![Journey Optimizer](./images/msg11.png)

在文本區域中，寫 `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

下一步，按一下 **內容屬性** 然後 **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

按一下 **事件**.

![ACOP](./images/jomsg4.png)

按一下事件的名稱，其應如下所示： **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

按一下 **放置內容**.

![ACOP](./images/jomsg6.png)

按一下 **POI互動**.

![ACOP](./images/jomsg7.png)

按一下 **POI詳細資料**.

![ACOP](./images/jomsg8.png)

按一下 **+** 圖示 **POI名稱**.
你會看到這個。 按一下「**儲存**」。

![ACOP](./images/jomsg9.png)

您的訊息現已準備就緒。 按一下左上角的箭頭，返回您的歷程。

![ACOP](./images/jomsg11.png)

按一下 **確定**.

![ACOP](./images/jomsg14.png)

## 3.3.2傳送訊息至畫面

作為歷程的第三步，您需要新增 **sendMessageToScreen** 動作。 前往畫面左側，前往 **動作**，請選取 **sendMessageToScreen** 動作，然後將其拖放至歷程中的第三個節點。 你會看到這個。

![ACOP](./images/jomsg15.png)

此 **sendMessageToScreen** 動作是自訂動作，會將訊息發佈至商店內顯示使用的端點。 此 **sendMessageToScreen** action需要定義許多變數。 向下捲動，直到您看到 **動作參數**.

![ACOP](./images/jomsg16.png)

您現在需要設定每個動作參數的值。 請依照下表了解需要哪些值。

| 參數 | 值 |
|:-------------:| :---------------:|
| 傳送 | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| 名字 | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| 沙箱 | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style=&quot;table-layout:auto&quot;}

若要設定這些值，請按一下 **編輯** 表徵圖。

![ACOP](./images/jomsg17.png)

下一步，選擇 **進階模式**.

![ACOP](./images/jomsg18.png)

接著，根據上表貼上值。 按一下 **確定**.

![ACOP](./images/jomsg19.png)

重複此程式為每個欄位新增值。

>[!IMPORTANT]
>
>若為欄位ECID，則會參考事件 `yourLastNameBeaconEntryEvent`. 請務必更換 `yourLastName` 姓。

最終結果應如下所示：

![ACOP](./images/jomsg20.png)

向上捲動並按一下 **確定**.

![ACOP](./images/jomsg21.png)

您仍需為歷程命名。 您可以按一下 **屬性** 圖示。

![ACOP](./images/journeyname.png)

然後，您可以在此處輸入歷程的名稱。 請使用 `yourLastName - Beacon Entry Journey`. 按一下 **確定** 來儲存變更。

![ACOP](./images/journeyname1.png)

您現在可以按一下 **發佈**.

![ACOP](./images/publishjourney.png)

按一下 **發佈** 。

![ACOP](./images/publish1.png)

接著，您會看到綠色的確認列，指出您的歷程現已發佈。

![ACOP](./images/published.png)

您的歷程現在已上線且可觸發。

你已經完成了這個練習。

下一步： [3.4測試您的歷程](./ex4.md)

[返回用戶流3](./uc3.md)

[返回所有模組](../../overview.md)
