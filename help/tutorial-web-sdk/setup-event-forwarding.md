---
title: 使用Platform Web SDK資料設定事件轉送
description: 瞭解如何使用Experience Platform Web SDK資料的事件轉送屬性。 本課程是「使用 Web SDK 實施 Adob​​e Experience Cloud」教學課程的一部分。
feature: Web SDK,Tags,Event Forwarding
jira: KT-15414
exl-id: 5a306609-2c63-42c1-8beb-efa412b8efe4
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '1872'
ht-degree: 3%

---

# 使用Platform Web SDK資料設定事件轉送

了解如何將事件轉送與 Adob&#x200B;&#x200B;e Experience Platform Web SDK 資料一起使用。

事件轉寄是「資料收集」中可用的全新屬性型別。 事件轉送可讓您直接從Adobe Experience Platform Edge Network （而非傳統使用者端瀏覽器）將資料傳送至第三方非Adobe廠商。 在[事件轉送概觀](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)中進一步瞭解事件轉送的優點。


![網頁SDK和事件轉送圖表](assets/dc-websdk-eventforwarding.png)

若要在Adobe Experience Platform中使用事件轉送，必須先使用下列一個或多個選項，將資料傳送至Adobe Experience Platform Edge Network：

* [Adobe Experience Platform Web SDK](overview.md)
* [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)
  <!--* [Server-to-Server API](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s)-->


>[!NOTE]
>Platform Web SDK和Platform Mobile SDK不要求透過標籤進行部署，但建議使用標籤來部署這些SDK。

完成本教學課程中先前的課程後，您應使用網頁SDK傳送資料至Platform Edge Network。 資料傳入Platform Edge Network後，您就可以啟用事件轉送，並使用事件轉送屬性將資料傳送至非Adobe解決方案。

## 學習目標

在本課程結束時，您將能夠：

* 建立事件轉送屬性
* 將事件轉送屬性連結至Platform Web SDK資料流
* 瞭解標籤屬性資料元素與規則之間的差異，以及事件轉送屬性資料元素與規則
* 建立事件轉送資料元素
* 設定事件轉送規則
* 驗證事件轉送屬性是否成功傳送資料


## 先決條件

* 包含事件轉送的軟體授權。 事件轉寄是資料收集的付費功能。 如需詳細資訊，請聯絡您的Adobe客戶團隊。
* 已在您的Experience Cloud組織中啟用事件轉送。
* 事件轉送的使用者許可權。 (在[Admin Console](https://adminconsole.adobe.com/)中，在Adobe Experience Platform Launch產品底下，[!UICONTROL 平台] > [!UICONTROL Edge]的許可權專案以及所有[!UICONTROL 屬性權利])。 授與後，您應該會在Data Collection介面的左側導覽中看到[!UICONTROL 事件轉送]：
  ![事件轉送屬性](assets/event-forwarding-menu.png)

* Adobe Experience Platform Web或Mobile SDK已設定為傳送資料至Edge Network。 您必須完成本教學課程的下列課程：

   * 初始設定

      * [設定XDM結構描述](configure-schemas.md)
      * [設定身分名稱空間](configure-identities.md)
      * [設定資料流](configure-datastream.md)

   * 標籤設定

      * [安裝 Web SDK 擴充功能](install-web-sdk.md)
      * [建立資料元素](create-data-elements.md)
      * [建立身分](create-identities.md)
      * [建立標籤規則](create-tag-rule.md)
      * [使用Adobe Experience Platform Debugger進行驗證](validate-with-debugger.md)


## 建立事件轉送屬性

從建立事件轉送屬性開始：

1. 開啟[資料收集介面](https://experience.adobe.com/#/data-collection)
1. 從左側導覽中選取&#x200B;**[!UICONTROL 事件轉送]**
1. 選取&#x200B;**[!UICONTROL 新屬性]**。
   ![事件轉送屬性](assets/event-forwarding-new.png)

1. 為屬性命名。 在此案例中，`Server-Side - Web SDK Course`

1. 選取「**[!UICONTROL 儲存]**」。
   ![事件轉送屬性儲存](assets/event-forwarding-save.png)

## 設定資料串流

若要讓事件轉送使用您傳送至Platform Edge Network的資料，您必須將新建立的事件轉送屬性連結至用來將資料傳送至Adobe解決方案的相同資料流。

若要在資料流中設定Target：

1. 移至[資料彙集](https://experience.adobe.com/#/data-collection){target="blank"}介面
1. 在左側導覽中，選取&#x200B;**[!UICONTROL 資料串流]**
1. 選取先前建立的`Luma Web SDK: Development Environment`資料流

   ![選取Luma Web SDK資料流](assets/datastream-luma-web-sdk-development.png)

1. 選取&#x200B;**[!UICONTROL 新增服務]**
   ![新增服務至資料流](assets/event-forwarding-datastream-addService.png)
1. 選取&#x200B;**[!UICONTROL 事件轉送]**&#x200B;做為&#x200B;**[!UICONTROL 服務]**

1. 在&#x200B;**[!UICONTROL 屬性ID]**&#x200B;下拉式清單中，選取您為事件轉送屬性指定的名稱，在此案例中為`Server-Side - Web SDK Course`

1. 在&#x200B;**[!UICONTROL 環境ID]**&#x200B;下拉式清單中，選取您要連結事件轉送環境的標籤環境，在此案例中為`Development`

   >[!TIP]
   >
   >    若要將資料傳送至Adobe組織以外的事件轉送環境，請選取&#x200B;**[!UICONTROL 手動輸入ID]**&#x200B;並貼入ID。 建立event-forwarding屬性時，系統就會提供ID。

1. 選取「**[!UICONTROL 儲存]**」。

   ![事件轉送資料流啟用](assets/event-forwarding-datastream-enable.png)

當您準備好透過發佈流程提升您的變更時，請針對中繼和生產資料串流重複這些步驟。

## 將資料從Platform Edge Network轉送至非Adobe解決方案

在本練習中，您將瞭解如何設定事件轉送資料元素、設定事件轉送規則，以及使用名為[Webhook.site](https://webhook.site/)的第三方工具進行驗證。

>[!NOTE]
>
>webhook是以半即時方式整合不同系統的方式。 [Webhook.site](https://webhook.site/)是協力廠商工具，可讓您輕鬆檢查、測試和自動化（使用視覺化自訂動作產生器或WebhookScript）任何傳入的HTTP要求或電子郵件。

>[!IMPORTANT]
>
>您必須已建立資料元素並將元素對應至XDM物件，且已設定標籤規則，並在程式庫中將這些變更建立至標籤環境，才能繼續進行。 若尚未設定，請參閱&#x200B;**先決條件**&#x200B;區段中的[標籤組態](setup-event-forwarding.md#prerequisites)步驟。 這些步驟可確保將資料傳送至Platform Edge Network，且您可以從中設定事件轉送屬性，以將資料轉送至非Adobe解決方案。


### 建立事件轉送資料元素

您先前使用Platform Web SDK標籤擴充功能設定的XDM物件，會成為事件轉送屬性中資料元素的資料來源。 您可以使用已在標籤屬性中設定的相同資料作為事件轉送的資料來源。

>[!IMPORTANT]
>
>在事件轉送中參照XDM欄位與其他內容時，有一個關鍵語法差異。 若要參考事件轉送屬性中的資料，資料元素路徑必須包含`arc.event`首碼：
>
> * 其中 `arc` 代表 Adobe Response Context。
> * 例如︰`arc.event.xdm.web.webPageDetails.URL`
>
>如果未正確指定此路徑，則不會收集資料。

在本練習中，您會將瀏覽器檢視區高度和Experience Cloud ID從XDM物件轉送至webhook。 XDM欄位路徑是由[設定XDM結構描述](configure-schemas.md)課程期間建立的XDM結構描述所決定。

>[!TIP]
>
>您也可以使用網頁瀏覽器網路工具、篩選`/ee`要求、開啟信標&#x200B;[!UICONTROL **裝載**]並向下展開至您要尋找的變數，以尋找XDM物件路徑。 然後以滑鼠右鍵按一下，並選取「複製屬性路徑」。 以下是瀏覽器檢視區高度的範例：
>> ![事件轉送XDM路徑](assets/event-forwarding-xdm-path.png)

1. 前往您最近建立的&#x200B;**[!UICONTROL 事件轉送]**&#x200B;屬性

1. 在左側導覽中，選取&#x200B;**[!UICONTROL 資料元素]**

1. 選取以&#x200B;**[!UICONTROL 建立新資料元素]**

   ![事件轉寄新資料元素](assets/event-forwarding-new-dataelement.png)

1. **[!UICONTROL Name]**&#x200B;資料元素`environment.browserDetails.viewportHeight`

1. 在&#x200B;**[!UICONTROL 副檔名]**&#x200B;下，離開`CORE`

1. 在&#x200B;**[!UICONTROL 資料元素型別]**&#x200B;下，選取`Path`

1. 輸入包含瀏覽器檢視區高度`arc.event.xdm.environment.browserDetails.viewportHeight`的XDM物件路徑

1. 選取&#x200B;**[!UICONTROL 儲存]**

   ![事件轉送ECID路徑](assets/event-forwarding-browser-viewpoirt-height.png)


1. 建立其他資料元素

1. **[!UICONTROL 名稱]**，它`ecid`

1. 在&#x200B;**[!UICONTROL 副檔名]**&#x200B;下，離開`CORE`

1. 在&#x200B;**[!UICONTROL 資料元素型別]**&#x200B;下，選取`Path`

1. 輸入包含Experience Cloud ID `arc.event.xdm.identityMap.ECID.0.id`的XDM物件路徑

1. 選取&#x200B;**[!UICONTROL 儲存]**

   ![事件轉送ECID路徑](assets/event-forwarding-ecid.png)

   >[!CAUTION]
   >
   > 請務必在路徑中加入`arc.event.`首碼。 此外，請確保遵循與XDM物件欄位名稱完全相同的大小寫，ECID名稱空間必須全部大寫。


   >[!TIP]
   >
   >使用您自己的網站時，您可以透過網頁瀏覽器網路工具找到XDM物件路徑、篩選`/ee`請求、開啟信標&#x200B;[!UICONTROL **裝載**]並向下展開至您要尋找的變數。 然後以滑鼠右鍵按一下，並選取「複製屬性路徑」。 以下是瀏覽器檢視區高度的範例：
   > ![事件轉送XDM路徑](assets/event-forwarding-xdm-path.png)

### 安裝Adobe Cloud Connector擴充功能

若要將資料傳送至協力廠商位置，您必須先安裝[!UICONTROL Adobe Cloud Connector]擴充功能。

1. 在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**

1. 選取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤

1. 搜尋&#x200B;**[!UICONTROL Adobe Cloud Connector]**，選取&#x200B;**[!UICONTROL 安裝]**

   ![事件轉送ECID路徑](assets/event-forwarding-adobe-cloud-connector.png)

不需要擴充功能設定。 透過此擴充功能，您現在可以將資料轉送至非Adobe解決方案！

### 建立事件轉送規則

在標籤屬性中設定規則與事件轉送屬性中設定規則之間有幾個主要差異：

* **[!UICONTROL 事件]和[!UICONTROL 條件]**：

   * **標籤**：所有規則都是由必須在規則中指定的事件所觸發，例如`Library Loaded - Page Top`。 條件為選用。
   * **事件轉送**：假設每個傳送至Platform Edge Network的事件都是轉送資料的觸發條件。 因此，在事件轉送規則中沒有必須選取的[!UICONTROL 事件]。 若要管理哪些事件會觸發事件轉送規則，您必須設定條件。

* **資料元素代碼化**：

   * **標籤**：資料元素名稱在規則中使用時，會在名稱的頭尾分別加上`%`，加以代碼化， 例如 `%viewportHeight%`。

   * **事件轉送**：在規則中使用資料元素名稱時，資料元素名稱的開頭有`{{`，結尾有`}}`，因此會加以代碼化。 例如 `{{viewportHeight}}`。

* **規則動作順序**：

   * 事件轉送規則的「動作」區段一律依序執行。 儲存規則時，請確認動作順序正確。 此執行序列無法像標籤一樣以非同步方式執行。

<!--
  * **Tags**: Rule actions can easily be reordered using drag-and-drop functionality.
  * **Event forwarding**: Rule actions are always executed sequentially. Make sure the order of actions is correct when you save a rule.
-->

若要設定將資料轉送至webhook的規則，您必須先取得個人webhook：

1. 移至[Webhook.site](https://webhook.site)

1. 尋找&#x200B;**您的唯一URL**，將此作為事件轉送規則中的URL要求

1. 選取&#x200B;**[!UICONTROL 複製到剪貼簿]**

1. 保持此視窗開啟，因為您將能夠驗證Webhook即時擷取的事件轉送資料

   ![複製Webhook URL](assets/event-forwarding-webhook.png)

1. 從左側導覽返回&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 事件轉送]** > **[!UICONTROL 規則]**

1. 選取&#x200B;**[!UICONTROL 建立新規則]**

   ![事件轉寄新規則](assets/event-forwarding-new-rules.png)

1. 將其命名為`all events - ad cloud connector - webhook`

1. 新增動作

1. 在&#x200B;**[!UICONTROL 擴充功能]**&#x200B;底下，選取&#x200B;**[!UICONTROL Adobe Cloud Connector]**

1. 在&#x200B;**[!UICONTROL 動作型別]**&#x200B;下，選取&#x200B;**[!UICONTROL 進行擷取呼叫]**

1. 將您的Webhook URL貼到&#x200B;**[!UICONTROL URL]**&#x200B;欄位中

   ![複製Webhook URL](assets/event-forwarding-rule.png)

1. 在&#x200B;**[查詢引數]**&#x200B;下，您將新增您先前建立的兩個資料元素。

1. 在&#x200B;**[!UICONTROL 中的]**&#x200B;索引鍵`viewPortHeight`資料行型別上。 在&#x200B;**[!UICONTROL 值]**&#x200B;欄中，輸入`{{environment.browserDetails.viewportHeight}}`資料元素，方法為輸入或從資料元素選取器圖示中選取

1. 選取&#x200B;[!UICONTROL **+新增其他**]&#x200B;以新增其他查詢引數

1. 在&#x200B;**[!UICONTROL 中的]**&#x200B;索引鍵`ecid`資料行型別上。 在值欄中，輸入`{{ecid}}`資料元素

1. 選取&#x200B;**[!UICONTROL 保留變更]**

   ![新增查詢引數](assets/event-forwarding-rule-query-parameter.png)

1. 您的規則應如下所示

1. 選取&#x200B;**[!UICONTROL 儲存]**

   ![儲存事件轉送規則](assets/event-forwarding-rule-save.png)

### 建立及建置程式庫

建立程式庫，並建置事件轉送開發環境的所有變更，如同您在標籤屬性中一般的作法。

>[!NOTE]
>
>如果您尚未將測試和生產事件轉送屬性連結至資料流，您會看到開發環境是建立程式庫的唯一選項。

![儲存事件轉送規則](assets/event-forwarding-initial-build.png)

## 驗證事件轉送規則

現在您可以使用Platform Debugger和Webhook.site來驗證事件轉送屬性：

1. 請依照步驟[將](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property)Luma示範網站[上的標籤庫](https://luma.enablementadobe.com/content/luma/us/en/men.html)切換為您在資料流中將事件轉送屬性對應到的Web SDK標籤屬性。

1. 在您重新載入頁面之前，請在Experience Platform Debugger上從左側導覽開啟&#x200B;**[!UICONTROL 記錄檔]**

1. 選取&#x200B;**[!UICONTROL Edge]**&#x200B;標籤，然後選取&#x200B;**[!UICONTROL 連線]**&#x200B;以檢視Platform Edge Network請求

   ![事件轉送邊緣網路工作階段](assets/event-forwarding-edge-session.png)

1. 重新載入頁面

1. 您會看到其他要求，讓您瞭解Platform Edge Network傳送給WebHook的伺服器端要求

1. 焦點驗證的要求是顯示Edge網路所傳送之完整建構URL的要求

   ![事件轉送偵錯工具](assets/event-forwarding-debugger.png)


1. 請注意viewPortHeight和ecid查詢字串引數

   ![事件轉寄驗證查詢字串](assets/event-forwarding-validate-data.png)

1. 它們符合XDM物件中看到的資料

   ![事件轉寄符合資料](assets/event-forwarding-matching-data.png)

1. 最後，檢視您開啟的Webhook視窗，以驗證[Webhook.site](https://webhook.site)中的資料相符

   ![事件轉送webhook網站資料](assets/event-forwarding-webhook-data.png)

恭喜！您已設定事件轉送！

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想分享一般意見或有關於未來內容的建議，請在這篇[Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)上分享
