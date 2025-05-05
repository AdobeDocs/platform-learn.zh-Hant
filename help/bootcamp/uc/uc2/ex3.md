---
title: Bootcamp - Journey Optimizer建立您的歷程與電子郵件訊息
description: Bootcamp - Journey Optimizer建立您的歷程與電子郵件訊息
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: 138a70fa-fe50-4585-b47f-150db4770c3d
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 2.3建立您的歷程與電子郵件訊息

在本練習中，您將設定當有人在示範網站上建立帳戶時，需要觸發的歷程。

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`Bootcamp`。 若要從一個沙箱變更為另一個沙箱，請按一下&#x200B;**Prod**&#x200B;並從清單中選取該沙箱。 在此範例中，沙箱名為&#x200B;**Bootcamp**。 然後您就會進入沙箱`Bootcamp`的&#x200B;**首頁**&#x200B;檢視。

![ACOP](./images/acoptriglp.png)

## 2.3.1建立您的歷程

在左側功能表中，按一下&#x200B;**歷程**。 接著，按一下&#x200B;**建立歷程**&#x200B;以建立新歷程。

![ACOP](./images/createjourney.png)

接著，您會看到空白的歷程畫面。

![ACOP](./images/journeyempty.png)

在上一個練習中，您已建立新的&#x200B;**事件**。 您將其命名為`yourLastNameAccountCreationEvent`，並將`yourLastName`取代為您的姓氏。 這是建立事件的結果：

![ACOP](./images/eventdone.png)

您現在需要將此事件當作此歷程的開端。 您可以移至畫面左側，在事件清單中搜尋您的事件，以執行此操作。

![ACOP](./images/eventlist.png)

選取您的事件，將其拖放至「歷程」畫布上。 您的歷程現在看起來像這樣：

![ACOP](./images/journeyevent.png)

作為歷程的第二步，您需要新增一個短的&#x200B;**等待**&#x200B;步驟。 移至畫面左側的&#x200B;**協調流程**&#x200B;區段以尋找此專案。 您將使用設定檔屬性，而且需要確定這些屬性已填入即時客戶設定檔中。

![ACOP](./images/journeywait.png)

您的歷程現在看起來像這樣。 在畫面右側，您需要設定等待時間。 設定為1分鐘。 這會在事件觸發後，提供充足的時間讓設定檔屬性可用。

![ACOP](./images/journeywait1.png)

按一下&#x200B;**確定**&#x200B;以儲存變更。

作為歷程的第三個步驟，您需要新增&#x200B;**電子郵件**&#x200B;動作。 移至畫面左側的&#x200B;**動作**，選取&#x200B;**電子郵件**&#x200B;動作，然後將其拖放到歷程的第二個節點。 您現在看到這個了。

![ACOP](./images/journeyactions.png)

將&#x200B;**類別**&#x200B;設定為&#x200B;**行銷**，並選取可讓您傳送電子郵件的電子郵件表面。 在此情況下，要選取的電子郵件表面為&#x200B;**電子郵件**。 請確定已同時啟用&#x200B;**電子郵件**&#x200B;點按和&#x200B;**電子郵件開啟**&#x200B;的核取方塊。

![ACOP](./images/journeyactions1.png)

下一步是建立訊息。 若要這麼做，請按一下[編輯內容]。**&#x200B;**

![ACOP](./images/journeyactions2.png)

## 2.3.2建立您的訊息

若要建立您的訊息，請按一下[編輯內容]。**&#x200B;**

![ACOP](./images/journeyactions2.png)

您現在看到這個了。

![ACOP](./images/journeyactions3.png)

按一下&#x200B;**主旨列**&#x200B;文字欄位。

![Journey Optimizer](./images/msg5.png)

在文字區域中開始寫入&#x200B;**您好**

![Journey Optimizer](./images/msg6.png)

主旨列尚未完成。 接下來，您需要為&#x200B;**名字**&#x200B;欄位（儲存在`profile.person.name.firstName`下）引入個人化權杖。 在左側功能表中，向下捲動以尋找&#x200B;**人員**&#x200B;元素，然後按一下箭頭以深入瞭解。

![Journey Optimizer](./images/msg7.png)

現在找到&#x200B;**全名**&#x200B;元素，然後按一下箭頭，即可深入瞭解。

![Journey Optimizer](./images/msg8.png)

最後，找到&#x200B;**名字**&#x200B;欄位，然後按一下它旁邊的&#x200B;**+**&#x200B;符號。 然後，您會看到個人化權杖出現在文字欄位中。

![Journey Optimizer](./images/msg9.png)

接下來，新增文字&#x200B;**，感謝您註冊！**。按一下&#x200B;**儲存**。

![Journey Optimizer](./images/msg10.png)

然後您就會回到這裡。 按一下&#x200B;**電子郵件Designer**&#x200B;以建立電子郵件的內容。

![Journey Optimizer](./images/msg11.png)

在下一個畫面中，系統會使用3種不同的方法來提示您提供電子郵件內容：

- **從草稿開始設計**：從空白畫布開始，並使用WYSIWYG編輯器拖放結構和內容元件，以視覺化方式建置電子郵件的內容。
- **為您自己的電子郵件編碼**：使用HTML編碼來建立您自己的電子郵件範本
- **匯入HTML**：匯入現有的HTML範本，您可以編輯該範本。

按一下&#x200B;**匯入HTML**。 或者，您可以按一下&#x200B;**儲存的範本**，然後選取範本&#x200B;**Bootcamp — 電子郵件範本**。

![Journey Optimizer](./images/msg12.png)

若您選取&#x200B;**匯入HTML**，您現在可以拖放檔案&#x200B;**mailtemplatebootcamp.html**，您可以將[下載到這裡](../../assets/html/mailtemplatebootcamp.html.zip)。 按一下「匯入」。

![Journey Optimizer](./images/msg13.png)

之後，您會看到此預設電子郵件範本：

![Journey Optimizer](./images/msg14.png)

讓我們個人化電子郵件。 按一下文字&#x200B;**嗨**&#x200B;旁的，然後按一下&#x200B;**新增Personalization**&#x200B;圖示。

![Journey Optimizer](./images/msg35.png)

接下來，您需要帶上儲存在`profile.person.name.firstName`底下的&#x200B;**名字**&#x200B;個人化權杖。 在功能表中，尋找&#x200B;**人員**&#x200B;元素，向下展開至&#x200B;**全名**&#x200B;元素，然後按一下&#x200B;**+**&#x200B;圖示，將「名字」欄位新增至運算式編輯器。

按一下&#x200B;**儲存**。

![Journey Optimizer](./images/msg36.png)

您現在會注意到個人化欄位已新增至文字的方式。

![Journey Optimizer](./images/msg37.png)

按一下&#x200B;**儲存**&#x200B;以儲存您的訊息。

![Journey Optimizer](./images/msg55.png)

按一下左上角主旨列文字旁的&#x200B;**箭頭**，返回訊息儀表板。

![Journey Optimizer](./images/msg56.png)

您現在已經完成建立註冊電子郵件。 按一下左上角的箭頭，返回您的歷程。

![Journey Optimizer](./images/msg57.png)

按一下&#x200B;**確定**。

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publish您的歷程

您仍需要提供歷程名稱。 若要這麼做，請按一下熒幕左上方的&#x200B;**鉛筆**&#x200B;圖示。

![ACOP](./images/journeyname.png)

然後，您可以在此處輸入歷程的名稱。 請使用`yourLastName - Account Creation Journey`。 按一下&#x200B;**確定**&#x200B;以儲存變更。

![ACOP](./images/journeyname1.png)

您現在可以按一下&#x200B;**Publish**&#x200B;發佈您的歷程。

![ACOP](./images/publishjourney.png)

再按一下&#x200B;**Publish**。

![ACOP](./images/publish1.png)

接著，您會看到綠色確認列，指出您的歷程已發佈。

![ACOP](./images/published.png)

您現在已經完成此練習。

下一步： [2.4測試您的歷程](./ex4.md)

[返回使用者流程2](./uc2.md)

[返回所有模組](../../overview.md)