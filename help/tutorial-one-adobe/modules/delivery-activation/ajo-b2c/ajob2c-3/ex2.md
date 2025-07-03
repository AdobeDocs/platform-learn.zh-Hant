---
title: 設定包含推送訊息的歷程
description: 設定包含推送訊息的歷程
kt: 5342
doc-type: tutorial
source-git-commit: 203590e3289d2e5342085bf8b6b4e3cd11859539
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---

# 3.3.2設定包含推送訊息的歷程


## 3.4.4.6建立新事件

移至&#x200B;**Journey Optimizer**。 在左側功能表中，移至&#x200B;**組態**&#x200B;並按一下&#x200B;**事件**&#x200B;底下的&#x200B;**管理**。

![ACOP](./images/acopmenu.png)

在&#x200B;**事件**&#x200B;畫面上，您會看到類似此的檢視。 按一下&#x200B;**建立事件**。

![ACOP](./images/add.png)

然後您會看到空白的事件設定。
首先，請為事件命名，如下所示： `--aepUserLdap--StoreEntryEvent`並將說明設定為`Store Entry Event`。
下一個是&#x200B;**事件型別**&#x200B;選項。 選取&#x200B;**單一**。
下一個是&#x200B;**事件ID型別**&#x200B;選擇。 選取&#x200B;**系統產生**。

![ACOP](./images/eventname.png)

接下來是「結構描述」選項。 已針對此練習準備結構描述。 請使用結構描述`Demo System - Event Schema for Mobile App (Global v1.1) v.1`。

選取結構描述後，您將會在&#x200B;**裝載**&#x200B;區段中看到一些正在選取的欄位。 您的事件現已完整設定。

按一下&#x200B;**儲存**。

![ACOP](./images/eventschema.png)

您的事件現在已設定並儲存。 再次按一下您的事件以再次開啟&#x200B;**編輯事件**&#x200B;畫面。

![ACOP](./images/eventdone.png)

將游標暫留在&#x200B;**裝載**&#x200B;欄位上，然後按一下&#x200B;**檢視裝載**&#x200B;圖示。

![ACOP](./images/hover.png)

您現在將看到預期裝載的範例。

您的事件具有獨特的協調流程eventID，您可以在該承載中向下捲動直到看到`_experience.campaign.orchestration.eventID`為止。

![ACOP](./images/payloadeventID.png)

事件ID需要傳送至Adobe Experience Platform，才能觸發您將在下一個步驟建立的歷程。 記下此eventID，因為您會在下一個步驟中需要它。
`"eventID": "89acd341ec2b7d1130c9a73535029debf2ac35f486bc99236b1a5091d6f4bc68"`

按一下&#x200B;**確定**，然後按一下&#x200B;**取消**。

## 3.4.4.7建立歷程

在功能表中，前往&#x200B;**歷程**&#x200B;並按一下&#x200B;**建立歷程**。

![DSN](./images/sjourney1.png)

您將會看到此訊息。 為您的歷程命名。 使用`--aepUserLdap-- - Store Entry journey`。 按一下&#x200B;**儲存**。

![DSN](./images/sjourney3.png)

首先，您需要新增活動作為歷程的起點。 搜尋您的活動`--aepUserLdap--StoreEntryEvent`，並將其拖放到畫布上。 按一下&#x200B;**儲存**。

![DSN](./images/sjourney4.png)

接下來，在&#x200B;**動作**&#x200B;下搜尋&#x200B;**推播**&#x200B;動作。 將&#x200B;**推播**&#x200B;動作拖放到畫布上。

將&#x200B;**類別**&#x200B;設定為&#x200B;**行銷**，並選取可讓您傳送推播通知的推播表面。 在此情況下，要選取的電子郵件表面為&#x200B;**Push-iOS-Android**。

>[!NOTE]
>
>Journey Optimizer中的管道必須存在使用&#x200B;**應用程式介面**&#x200B;且先前已檢閱過的管道。

![ACOP](./images/journeyactions1push.png)

下一步是建立訊息。 若要這麼做，請按一下[編輯內容]。**&#x200B;**

![ACOP](./images/journeyactions2push.png)

您將會看到此訊息。 按一下&#x200B;**標題**&#x200B;欄位的&#x200B;**個人化**&#x200B;圖示。

![推播](./images/bp5.png)

您將會看到此訊息。 您現在可以直接從即時客戶個人檔案中選取任何個人檔案屬性。

搜尋欄位&#x200B;**名字**，然後按一下欄位&#x200B;**名字**&#x200B;旁的&#x200B;**+**&#x200B;圖示。 接著您會看到新增的名字的個人化權杖： **{{profile.person.name.firstName}}**。

![推播](./images/bp9.png)

接下來，新增文字&#x200B;**，歡迎來到我們的商店！**&#x200B;在&#x200B;**{{profile.person.name.firstName}}**&#x200B;之後。

按一下&#x200B;**儲存**。

![推播](./images/bp10.png)

您現在擁有此專案。 按一下&#x200B;**內文**&#x200B;欄位的&#x200B;**個人化**&#x200B;圖示。

![推播](./images/bp11.png)

輸入此文字&#x200B;**按一下此處，您今天購買時可享有10%的折扣！**&#x200B;並按一下&#x200B;**儲存**。

![推播](./images/bp12.png)

您就會擁有此專案。 按一下左上角的箭頭，返回您的歷程。

![Journey Optimizer](./images/bp12a.png)

按一下&#x200B;**儲存**&#x200B;以關閉您的推送動作。

![DSN](./images/sjourney8.png)

按一下&#x200B;**發佈**。

![DSN](./images/sjourney10.png)

再按一下&#x200B;**發佈**。

![DSN](./images/sjourney10a.png)

您的歷程現已發佈。

![DSN](./images/sjourney11.png)

## 3.4.4.8測試您的歷程與推送訊息

在您的DX Demo 2.0行動應用程式中，移至&#x200B;**設定**&#x200B;畫面。 按一下&#x200B;**存放區專案**&#x200B;按鈕。

>[!NOTE]
>
>目前正在實作&#x200B;**存放區專案**&#x200B;按鈕。 您尚未在應用程式中找到。

![DSN](./images/demo1b.png)

請確定在按一下&#x200B;**市集專案**&#x200B;圖示後立即關閉應用程式，否則將不會顯示推送訊息。

幾秒後，您會看到訊息出現。

![DSN](./images/demo2.png)

您已完成此練習。

## 後續步驟

移至[3.3.3使用應用程式內訊息設定行銷活動](./ex3.md){target="_blank"}

返回[Adobe Journey Optimizer：推送和應用程式內訊息](ajopushinapp.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
