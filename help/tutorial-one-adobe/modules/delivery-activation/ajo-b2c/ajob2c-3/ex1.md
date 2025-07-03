---
title: 開始使用推播通知
description: 開始使用推播通知
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 203590e3289d2e5342085bf8b6b4e3cd11859539
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 1%

---

# 3.3.1推播通知快速入門

若要搭配Adobe Journey Optimizer使用推播通知，有許多設定需要檢查並瞭解。

以下是要驗證的所有設定：

- Adobe Experience Platform中的資料集和結構描述
- 適用於行動裝置的資料流
- 行動裝置的資料收集屬性
- 推送憑證的應用程式表面
- 使用AEP Assurance測試推播設定

讓我們逐一檢閱這些內容。

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。 然後您就會進入沙箱&#x200B;**的**&#x200B;首頁`--aepSandboxName--`檢視。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.4.4.1推送資料集

Adobe Journey Optimizer使用資料集來儲存行動裝置的推播權杖之類的專案，或是在Adobe Journey Optimizer的資料集中與推播訊息的互動（例如：已傳送訊息、已開啟訊息等）。

您可以在畫面左側的功能表中前往&#x200B;**[!UICONTROL 資料集]**&#x200B;找到這些資料集。 若要顯示系統資料集，請按一下篩選圖示。

啟用選項&#x200B;**顯示系統資料集**&#x200B;並搜尋&#x200B;**AJO**。 然後您會看到用於推播通知的資料集。

![資料擷取](./images/menudsjo1.png)

## 行動裝置的3.4.4.2資料流

移至[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)。

在左側功能表中，移至&#x200B;**[!UICONTROL 資料流]**&#x200B;並搜尋您在[快速入門](./../../../../modules/getting-started/gettingstarted/ex2.md)中建立的資料流（名為`--aepUserLdap-- - Demo System Datastream (Mobile)`）。 按一下以開啟它。

![按一下左側導覽中的[資料流]圖示](./images/edgeconfig1a.png)

在&#x200B;**Adobe Experience Platform**&#x200B;服務上按一下&#x200B;**編輯**。

![按一下左側導覽中的[資料流]圖示](./images/edgeconfig1.png)

然後您會看到已定義的資料流設定，以及將會儲存資料集事件和設定檔屬性的資料。

您也應該啟用下列選項（如果尚未啟用）：

- **Offer Decisioning**
- **個人化目的地**
- **Adobe Journey Optimizer**

按一下&#x200B;**儲存**。

![命名資料流並儲存](./images/edgeconfig2.png)

## 3.4.4.3檢閱您的行動裝置資料收集屬性

移至[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)。 在[快速入門](./../../../../modules/getting-started/gettingstarted/ex1.md)中，已建立2個資料收集屬性。
您已在先前的模組中使用這些資料收集使用者端屬性。

按一下以開啟行動裝置的「資料收集」屬性。

![DSN](./images/launchprop.png)

在資料收集屬性中，移至&#x200B;**擴充功能**。 接著，您會看到行動應用程式所需的各種擴充功能。 按一下以開啟擴充功能&#x200B;**Adobe Experience Platform Edge Network**。

![Adobe Experience Platform資料彙集](./images/launchprop1.png)

接著，您會看到行動裝置資料流已連結至此處。 接著，按一下&#x200B;**取消**，返回您的擴充功能概觀。

![Adobe Experience Platform資料彙集](./images/launchprop2.png)

然後您會回到這裡。 您將會看到&#x200B;**AEP Assurance**&#x200B;的擴充功能。 AEP Assurance可協助您檢查、證明、模擬及驗證如何在行動應用程式中收集資料或提供體驗。 您可以在[https://aep-sdks.gitbook.io/docs/beta/project-griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon)閱讀更多有關AEP Assurance和Project Griffon的資訊。

![Adobe Experience Platform資料彙集](./images/launchprop8.png)

接著，按一下&#x200B;**設定**&#x200B;以開啟擴充功能&#x200B;**Adobe Journey Optimizer**。

![Adobe Experience Platform資料彙集](./images/launchprop9.png)

接著，您會看到追蹤推送事件的資料集已連結至此處。

![Adobe Experience Platform資料彙集](./images/launchprop10.png)

您不需要變更資料收集屬性。

## 3.4.4.4檢閱您的應用程式表面設定

移至[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)。 在左側功能表中，前往&#x200B;**應用程式表面**&#x200B;並開啟&#x200B;**DX示範應用程式APNS**&#x200B;的應用程式表面。

![Adobe Experience Platform資料彙集](./images/appsf.png)

接著，您就會看到為iOS和Android設定的應用程式表面。

![Adobe Experience Platform資料彙集](./images/appsf1.png)

## 使用AEP Assurance的3.4.4.5測試推播通知設定。

應用程式安裝後，您會在裝置的主畫面上找到。 按一下圖示以開啟應用程式。

![DSN](./../../../../modules/getting-started/gettingstarted/images/mobileappn1.png)

第一次使用應用程式時，系統會要求您使用Adobe ID登入。 完成登入程式。

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn2.png)

登入後，您會看到通知要求您傳送通知的許可權。 我們將在教學課程中傳送通知，因此請按一下[允許]。**&#x200B;**

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn3.png)

然後您會看到應用程式的首頁。 移至&#x200B;**設定**。

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn4.png)

在設定中，您會看到應用程式目前已載入&#x200B;**公用專案**。 按一下&#x200B;**自訂專案**。

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn5.png)

您現在可以載入自訂專案。 按一下QR碼以輕鬆載入您的專案。

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn6.png)

完成&#x200B;**快速入門**&#x200B;區段後，您便有了此結果。 按一下以開啟為您建立的&#x200B;**行動零售專案**。

![DSN](./../../../modules/../getting-started/gettingstarted/images/dsn5b.png)

如果您不小心關閉了瀏覽器視窗，或是為了未來的示範或啟用工作階段，您也可以前往[https://dsn.adobe.com/projects](https://dsn.adobe.com/projects)存取您的網站專案。 使用Adobe ID登入後，您會看到此訊息。 按一下您的行動應用程式專案以開啟。

![DSN](./../../../modules/../getting-started/gettingstarted/images/web8a.png)

接著，按一下&#x200B;**執行**。

![DSN](./images/web8b.png)

然後您會看到這個快顯視窗，其中包含QR碼。 從行動應用程式內掃描此QR碼。

![DSN](./../../../modules/../getting-started/gettingstarted/images/web8c.png)

然後您會在應用程式中看到您的專案ID，之後您可以按一下&#x200B;**儲存**。

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn7.png)

現在，請回到應用程式中的&#x200B;**首頁**。 您的應用程式現在已可供使用。

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn8.png)

您現在需要掃描QR碼，將行動裝置連線至AEP Assurance工作階段。

若要開始AEP Assurance工作階段，請前往[https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)。 按一下左側功能表中的&#x200B;**Assurance**。 然後，按一下&#x200B;**建立工作階段**。

![Adobe Experience Platform資料彙集](./images/griffon3.png)

按一下&#x200B;**開始**。

![Adobe Experience Platform資料彙集](./images/griffon5.png)

填入值：

- 工作階段名稱：使用`--aepUserLdap-- - push debugging`並以您的ldap取代ldap
- 基底URL：使用`dxdemo://default`

按一下&#x200B;**下一步**。

![Adobe Experience Platform資料彙集](./images/griffon4.png)

接著，您會在熒幕上看到QR碼，請使用iOS裝置掃描該碼。

![Adobe Experience Platform資料彙集](./images/griffon6.png)

在行動裝置上，開啟相機應用程式並掃描AEP Assurance顯示的二維碼。

![Adobe Experience Platform資料彙集](./images/ipadPushTest8a.png)

然後您會看到快顯畫面，要求您輸入PIN碼。 從AEP Assurance畫面複製PIN碼，然後按一下&#x200B;**連線**。

![Adobe Experience Platform資料彙集](./images/ipadPushTest9.png)

您將會看到此訊息。

![Adobe Experience Platform資料彙集](./images/ipadPushTest11.png)

在Assurance中，您現在會看到裝置正在前往Assurance工作階段。 按一下&#x200B;**「完成」**。

![Adobe Experience Platform資料彙集](./images/griffon7.png)

移至&#x200B;**推送偵錯**。

>[!NOTE]
>
>如果您在左側功能表中找不到&#x200B;**推播偵錯**，請按一下畫面左下角的&#x200B;**設定**，然後新增&#x200B;**推播偵錯**&#x200B;至功能表。

您將會看到類似這樣的內容。

![Adobe Experience Platform資料彙集](./images/griffon10.png)

部分說明：

- 第一欄&#x200B;**Client**&#x200B;顯示您的iOS裝置上可用的識別碼。 您會看到ECID和推播權杖。
- 第2欄顯示&#x200B;**App Store認證與設定**，此專案是在練習&#x200B;**3.4.5.4在Launch中建立應用程式設定**&#x200B;中設定的
- 第二欄顯示&#x200B;**設定檔**&#x200B;資訊，以及推播權杖所在平台（APNS或APNSSandbox）的其他資訊。 如果您按一下&#x200B;**檢查設定檔**&#x200B;按鈕，您將會被帶到Adobe Experience Platform並看到完整的即時客戶設定檔。

若要測試推播設定設定，請移至&#x200B;**傳送測試推播設定**&#x200B;按鈕。 按一下&#x200B;**傳送測試推播通知**

![Adobe Experience Platform資料彙集](./images/griffon11.png)

您必須確定按一下&#x200B;**傳送推播通知**&#x200B;按鈕時，**DX示範**&#x200B;應用程式未開啟。 如果應用程式處於開啟狀態，系統可能會在背景收到「推播通知」，因此不會顯示。

接著，您會在行動裝置上看到類似這樣的推播通知。

![Adobe Experience Platform資料彙集](./images/ipadPush2.png)

如果您已收到推播通知，這表示您的設定正確且運作正常，您現在可以建立真正的歷程，進而從Journey Optimizer傳送推播訊息。

## 後續步驟

移至[3.3.2設定包含推送訊息的歷程](./ex2.md){target="_blank"}

返回[Adobe Journey Optimizer：推送和應用程式內訊息](ajopushinapp.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
