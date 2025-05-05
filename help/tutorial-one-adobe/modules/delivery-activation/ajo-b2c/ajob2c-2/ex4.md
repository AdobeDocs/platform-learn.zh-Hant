---
title: Adobe Journey Optimizer — 設定您的歷程和訊息
description: Adobe Journey Optimizer — 設定您的歷程和訊息
kt: 5342
doc-type: tutorial
exl-id: 687eb818-2d50-4293-88e6-7e5945b91db6
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 4%

---

# 3.2.4建立您的歷程和訊息

在本練習中，您將使用Adobe Journey Optimizer建立歷程和數則文字訊息。

在此使用案例中，目標是根據客戶位置的天氣條件傳送不同的訊息。 已定義3個案例：

- 攝氏10度以下
- 攝氏10至25度之間
- 溫度高於25攝氏度

針對這3個條件，您需要在Adobe Journey Optimizer中定義3則訊息。

## 3.2.4.1建立您的歷程

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。 然後您就會進入沙箱`--aepSandboxName--`的&#x200B;**首頁**&#x200B;檢視。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

在左側功能表中，前往&#x200B;**歷程**&#x200B;並按一下&#x200B;**建立歷程**&#x200B;以開始建立您的歷程。

![示範](./images/jocreate.png)

您應該先為您的歷程命名。

作為歷程的名稱，請使用`--aepUserLdap-- - Geofence Entry Journey`。 目前不可設定其他值。 按一下&#x200B;**儲存**。

![示範](./images/joname.png)

在熒幕左側，檢視&#x200B;**事件**。 您應該會在該清單中看到先前建立的事件。 選取它，然後將其拖放到歷程畫布上。 您的歷程隨後將如下所示。 按一下&#x200B;**儲存**。

![示範](./images/joevents.png)

接著，按一下&#x200B;**協調流程**。 您現在看到可用的&#x200B;**協調流程**&#x200B;功能。 選取「**條件**」，然後將其拖放至「歷程畫布」。

![示範](./images/jo2.png)

您現在必須為此條件設定三個路徑：

- 氣溫低於攝氏10度
- 攝氏10至25度之間
- 溫度高於25攝氏度

讓我們定義第一個條件。

### 條件1：攝氏10度以下

按一下&#x200B;**條件**。  按一下&#x200B;**Path1**&#x200B;並編輯&#x200B;**比10 C**&#x200B;還冷的路徑名稱。 按一下Path1運算式的&#x200B;**編輯**&#x200B;圖示。

![示範](./images/jo5.png)

然後您會看到空白的&#x200B;**簡單編輯器**&#x200B;畫面。 您的查詢會更進階，因此您需要&#x200B;**進階模式**。 按一下&#x200B;**進階模式**。

![示範](./images/jo7.png)

然後您會看到允許輸入程式碼的&#x200B;**進階編輯器**。

![示範](./images/jo9.png)

選取下列程式碼並將其貼到&#x200B;**進階編輯器**&#x200B;中。

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} <= 10`

您將會看到此訊息。

![示範](./images/jo10.png)

為了在此情況下擷取溫度，您需要提供客戶目前所在的城市。
**城市**&#x200B;需要連結至動態引數`q`，就像您先前在開放氣象API檔案中看到的一樣。

如熒幕擷圖所示，按一下欄位&#x200B;**動態值： q**。

![示範](./images/jo11.png)

然後，您必須在其中一個可用的資料來源中尋找包含客戶目前城市的欄位，在此情況下，您需要在&#x200B;**內容**&#x200B;下尋找該欄位。

![示範](./images/jo12.png)

您可以導覽至`--aepUserLdap--GeofenceEntry.placeContext.geo.city`找到該欄位。

按一下該欄位或按一下&#x200B;**+**，它將會新增為引數`q`的動態值。 此欄位將會填入，例如您在行動應用程式中實作的地理位置服務。 在這種情況下，您將使用示範網站的資料收集屬性來模擬此情形。 按一下&#x200B;**「確定」**。

![示範](./images/jo13.png)

### 條件2：攝氏10至25度之間

新增第一個條件後，您會看到此畫面。 按一下&#x200B;**新增路徑**。

![示範](./images/joc2.png)

連按兩下&#x200B;**Path1**&#x200B;並編輯路徑名稱&#x200B;**介於10到25 C**&#x200B;之間。 按一下此路徑運算式的&#x200B;**編輯**&#x200B;圖示。

![示範](./images/joc6.png)

然後您會看到空白的&#x200B;**簡單編輯器**&#x200B;畫面。 您的查詢會更進階，因此您需要&#x200B;**進階模式**。 按一下&#x200B;**進階模式**。

![示範](./images/jo7.png)

然後您會看到允許輸入程式碼的&#x200B;**進階編輯器**。

![示範](./images/jo9.png)

選取下列程式碼並將其貼到&#x200B;**進階編輯器**&#x200B;中。

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} > 10 and #{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} <= 25`

您將會看到此訊息。

![示範](./images/joc10.png)

為了擷取本條件中的溫度，您必須提供客戶目前所在的城市。
**City**&#x200B;需要連結至動態引數&#x200B;**q**，就像您先前在Open Weather API檔案中看到的一樣。

如熒幕擷圖所示，按一下欄位&#x200B;**動態值： q**。

![示範](./images/joc11.png)

然後，您需要在一個可用資料來源中找到包含客戶目前城市的欄位。

![示範](./images/jo12.png)

您可以導覽至`--aepUserLdap--GeofenceEntry.placeContext.geo.city`找到該欄位。 按一下該欄位，就會將其新增為引數&#x200B;**q**&#x200B;的動態值。 此欄位將會填入，例如您在行動應用程式中實作的地理位置服務。 在這種情況下，您將使用示範網站的資料收集屬性來模擬此情形。 按一下&#x200B;**「確定」**。

![示範](./images/jo13.png)

接下來，您將新增第3個條件。

### 條件3：攝氏25度以上

新增第二個條件後，您會看到此畫面。 按一下&#x200B;**新增路徑**。

![示範](./images/joct2.png)

按兩下Path1以將名稱變更為&#x200B;**比25 C**&#x200B;熱。
然後按一下此路徑之運算式的&#x200B;**編輯**&#x200B;圖示。

![示範](./images/joct6.png)

然後您會看到空白的&#x200B;**簡單編輯器**&#x200B;畫面。 您的查詢會更進階，因此您需要&#x200B;**進階模式**。 按一下&#x200B;**進階模式**。

![示範](./images/jo7.png)

然後您會看到允許輸入程式碼的&#x200B;**進階編輯器**。

![示範](./images/jo9.png)

選取下列程式碼並將其貼到&#x200B;**進階編輯器**&#x200B;中。

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} > 25`

您將會看到此訊息。

![示範](./images/joct10.png)

為了擷取本條件中的溫度，您必須提供客戶目前所在的城市。
**City**&#x200B;需要連結至動態引數&#x200B;**q**，就像您先前在Open Weather API檔案中看到的一樣。

如熒幕擷圖所示，按一下欄位&#x200B;**動態值： q**。

![示範](./images/joct11.png)

然後，您需要在一個可用資料來源中找到包含客戶目前城市的欄位。

![示範](./images/jo12.png)

您可以導覽至```--aepUserLdap--GeofenceEntry.placeContext.geo.city```找到該欄位。 按一下該欄位，就會將其新增為引數&#x200B;**q**&#x200B;的動態值。 此欄位將會填入，例如您在行動應用程式中實作的地理位置服務。 在這種情況下，您將使用示範網站的資料收集屬性來模擬此情形。 按一下&#x200B;**「確定」**。

![示範](./images/jo13.png)

您現在有三個已設定的路徑。 按一下&#x200B;**儲存**。

![示範](./images/jo3path.png)

由於此歷程僅供學習之用，您現在將設定數個動作，以展示行銷人員目前必須傳送訊息的各種選項。

## 3.2.4.2傳送下列路徑的訊息：攝氏10度以下

對於每個溫度環境，您將嘗試傳送文字訊息給客戶。 在本練習中，您會傳送真實訊息至Slack頻道，而非行動電話號碼。

讓我們專注於路徑&#x200B;**比10 C**&#x200B;冷。

![示範](./images/p1steps.png)

在左側功能表中，返回&#x200B;**動作**，選取動作`--aepUserLdap--TextSlack`，然後將其拖放至&#x200B;**訊息**&#x200B;動作之後。

![示範](./images/joa18.png)

移至&#x200B;**動作引數**&#x200B;並按一下引數`textToSlack`的&#x200B;**編輯**&#x200B;圖示。

![示範](./images/joa19.png)

在快顯視窗中，按一下&#x200B;**進階模式**。

![示範](./images/joa20.png)

選取下列程式碼，複製並貼到&#x200B;**進階模式編輯器**&#x200B;中。 按一下&#x200B;**確定**。

`"Brrrr..." + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + ",  it's cold and freezing outside. Get comfortable at home with a 20% discount on a Disney+ subscription!"`

![示範](./images/joa21.png)

您將會看到已完成的動作。 按一下&#x200B;**儲存**。

![示範](./images/joa22.png)

此歷程路徑現已準備就緒。

## 3.2.4.3傳送路徑訊息：攝氏10度至25度之間

對於每個溫度環境，您都會嘗試傳送訊息給您的客戶。 在本練習中，您會傳送真實訊息至Slack頻道，而非行動電話號碼。

讓我們專注於10到25個C **路徑之間的**。

![示範](./images/p2steps.png)

在左側功能表中，返回&#x200B;**動作**，選取動作`--aepUserLdap--TextSlack`，然後將其拖放至&#x200B;**訊息**&#x200B;動作之後。

![示範](./images/jop18.png)

移至&#x200B;**動作引數**&#x200B;並按一下引數`textToSlack`的&#x200B;**編輯**&#x200B;圖示。

![示範](./images/joa19z.png)

在快顯視窗中，按一下&#x200B;**進階模式**。

![示範](./images/joa20.png)

選取下列程式碼，複製並貼到&#x200B;**進階模式編輯器**&#x200B;中。 按一下&#x200B;**確定**。

`"What nice weather for the time of year, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + " 20% discount on Apple AirPods so you can go for a walk and listen to your favorite podcast!"`

![示範](./images/jop21.png)

您將會看到已完成的動作。 按一下&#x200B;**確定**。

![示範](./images/jop22.png)

此歷程路徑現已準備就緒。

## 3.2.4.4傳送下列路徑的訊息：攝氏25度以上

對於每個溫度環境，您都會嘗試傳送訊息給您的客戶。 在本練習中，您會傳送真實訊息至Slack頻道，而非行動電話號碼。

讓我們專注於&#x200B;**比25 C**&#x200B;路徑還溫暖的路徑。

![示範](./images/p3steps.png)

在左側功能表中，返回&#x200B;**動作**，選取動作`--aepUserLdap--TextSlack`，然後將其拖放至&#x200B;**訊息**&#x200B;動作之後。

![示範](./images/jod18.png)

移至&#x200B;**動作引數**&#x200B;並按一下引數`textToSlack`的&#x200B;**編輯**&#x200B;圖示。

![示範](./images/joa19zzz.png)

在快顯視窗中，按一下&#x200B;**進階模式**。

![示範](./images/joa20.png)

選取下列程式碼，複製並貼到&#x200B;**進階模式編輯器**&#x200B;中。 按一下&#x200B;**確定**。

`"So warm, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + "! 20% discount on adding 10GB of extra data so you can get online at the beach!"`

![示範](./images/jod21.png)

您將會看到已完成的動作。 按一下&#x200B;**儲存**。

![示範](./images/jod22.png)

此歷程路徑現已準備就緒。

## 3.2.4.5發佈您的歷程

您的歷程現在已完整設定。 按一下&#x200B;**發佈**。

![示範](./images/jodone.png)

再按一下&#x200B;**發佈**。

![示範](./images/jopublish1.png)

您的歷程現已發佈。

![示範](./images/jopublish2.png)

## 後續步驟

移至[3.2.5觸發您的歷程](./ex5.md){target="_blank"}

返回[Adobe Journey Optimizer：外部資料來源和自訂動作](journey-orchestration-external-weather-api-sms.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
