---
title: 建立資料元素
description: 了解如何建立XDM物件，並在標籤中將資料元素對應至該物件。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
feature: Tags
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 4%

---

# 建立資料元素

了解如何使用Web SDK建立擷取資料所需的必要資料元素Experience Platform。 擷取 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html). 了解如何透過名為XDM物件的新資料元素類型，使用您先前建立的XDM結構，以透過Platform Web SDK收集資料。

>[!NOTE]
>
> 為了示範，本課程中的練習以 [設定結構](configure-schemas.md) 步驟；建立XDM物件範例，擷取已檢視的內容和使用者在 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>本課程的資料來自 `[!UICONTROL digitalData]` 資料層。 若要檢視資料層，請開啟開發人員主控台，然後輸入 `[!UICONTROL digitalData]` 以檢視完整的可用資料層。![digitalData資料層](assets/data-element-data-layer.png)


無論使用何種Platform Web SDK，您都必須繼續在標籤屬性內建立資料元素，這些元素會對應至您網站的資料收集變數，例如資料層、HTML屬性或其他。 建立這些資料元素後，必須將它們對應至您於 [配置結構](configure-schemas.md) 教訓。 為此，Platform Web SDK擴充功能提供名為XDM物件的新資料元素類型。 因此，建立資料元素包含兩個動作：

1. 將網站變數對應至資料元素，以及
1. 將這些資料元素對應至XDM物件

對於步驟1，您可以使用任何核心標籤擴充功能的資料元素類型，繼續將資料層對應至目前的資料元素。 針對步驟2,Platform Web SDK擴充功能會建立一組先前無法使用的新資料元素類型：

* 事件合併ID
* 身分對應
* XDM物件

本課程著重於XDM物件和身分對應資料元素類型。 您將建立XDM物件以擷取Luma訪客的活動和驗證狀態。

## 學習目標

在本課程結束時，您可以：

* 建立資料元素以擷取內容和使用者登入ID資料
* 建立身分對應資料元素
* 將資料元素對應至XDM物件資料元素


## 先決條件

您對資料層有了解，並熟悉 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;}資料層，並了解如何參考標籤中的資料元素。 您必須在教學課程中完成下列先前步驟

* [設定權限](configure-permissions.md)
* [設定XDM結構](configure-schemas.md)
* [設定身分命名空間](configure-identities.md)
* [設定資料流](configure-datastream.md)
* [Web SDK擴充功能已安裝在標籤屬性中](install-web-sdk.md)

>[!IMPORTANT]
>
>此 [Experience CloudID服務擴充功能](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) 實作Adobe Experience Platform Web SDK時不需要，因為ID服務功能內建於Platform Web SDK。

## 建立資料元素以擷取資料層

開始建立XDM物件之前，請先建立對應至的下列資料元素集 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;}資料層：

1. 前往 **[!UICONTROL 資料元素]** 選取 **[!UICONTROL 新增資料元素]** (或 **[!UICONTROL 建立新資料元素]** 如果標籤屬性中沒有現有的資料元素)

   ![建立資料元素](assets/data-element-create.jpg)

1. 將資料元素命名為 `page.pageInfo.pageName`
1. 使用 **[!UICONTROL JavaScript變數]** **[!UICONTROL 資料元素類型]** 指向Luma資料層中的值： `digitalData.page.pageInfo.pageName`

1. 勾選&#x200B;**[!UICONTROL 值強制小寫]**&#x200B;和&#x200B;**[!UICONTROL 清除文字]**&#x200B;方塊，以標準化大小寫格式並移除多餘空格

1. 離開 `None` 作為 **[!UICONTROL 儲存期間]** 設定，因為此值在每個頁面上都不同

1. 選擇 **[!UICONTROL 儲存]**

   ![頁面名稱資料元素](assets/data-element-pageName.jpg)

請依照相同的步驟建立這四個額外的資料元素：

* **`page.pageInfo.server`**  已對應至
   `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  已對應至
   `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  已對應至
   `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** 已對應至
   `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** 已對應至 `digitalData.cart.orderId` (您會在 [設定分析](setup-analytics.md) 課程)


>[!CAUTION]
>
>此 [!UICONTROL JavaScript變數] 資料元素類型會將陣列參考視為點而非方括弧，因此參考使用者名稱資料元素會視為 `digitalData.user[0].profile[0].attributes.username` **將無法運作**.

## 建立Identity Map資料元素

接下來，您可以建立「身分對應」資料元素：

1. 前往 **[!UICONTROL 資料元素]** 選取 **[!UICONTROL 新增資料元素]**

1. **[!UICONTROL 名稱]** 資料元素 `identityMap.loginID`

1. 作為 **[!UICONTROL 擴充功能]**，選取 `Adobe Experience Platform Web SDK`

1. 作為 **[!UICONTROL 資料元素類型]**，選取 `Identity map`

1. 這會提示右側的螢幕區域 **[!UICONTROL 資料收集介面]** 用於配置標識：

   ![資料收集介面](assets/identity-identityMap-setup.png)

1. 作為  **[!UICONTROL 命名空間]**，請選取 `Luma CRM Id` 您先前在 [設定身分](configure-identities.md) 教訓。

   >[!NOTE]
   >
   >    如果你沒看見 `Luma CRM Id` 命名空間，確認您也已在預設的生產沙箱中建立命名空間。 目前，命名空間下拉式清單中只會顯示預設生產沙箱中建立的命名空間。

1. 在 **[!UICONTROL 命名空間]** ，則必須設定ID。 選取 `user.profile.attributes.username` 本課程先前建立的資料元素，會在使用者登入Luma網站時擷取ID。

<!--  >[!TIP]
   >
   >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
   >
   >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
-->

1. 作為 **[!UICONTROL 驗證狀態]**，選取 **[!UICONTROL 已驗證]**

1. 選擇 **[!UICONTROL 儲存]**

   ![資料收集介面](assets/identity-id-namespace.png)

>[!WARNING]
>
>傳送至Adobe Experience Platform的所有記錄都須有主要身分。 依預設，Experience CloudID(ECID)會作為Platform Web SDK的主要身分識別。 您絕不會想使用 `Luma CRM ID` 作為Web SDK的主要身分，因為它僅存在於使用者驗證之後，因此無法用於所有記錄。

<!--
1. Once the data element is configured in **[!UICONTROL Data Collection interface]**, it can be tested on the Luma web property like any other Data Element. Enter the following script in the browser developer console
   
   
   ```
   _satellite.getVar('identityMap.loginID')
   ```  

   ![Data Collection interface](assets/identity-consoleIdentityDataElement.png)
   
   >[!NOTE]
   >
   >ECID identifier will NOT populate in the Data Element, as this is configured already with Platform Web SDK.   
-->

## 將資料元素對應至XDM物件

您建立的所有資料元素都必須對應至XDM物件。 此物件應符合您在 [設定結構](configure-schemas.md) 教訓。

有不同的方式可將資料元素對應至XDM物件欄位。 只要您的資料元素符合XDM物件中出現的確切索引鍵值配對架構，您就可以將個別資料元素對應至個別XDM欄位，或將資料元素對應至整個XDM物件。 在本課程中，您將透過對應至個別欄位來擷取內容資料。 你會學會 [將資料元素對應至整個XDM物件](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) 在 [設定分析](setup-analytics.md) 教訓。

建立XDM物件以擷取內容資料：

1. 在左側導覽中，選取 **[!UICONTROL 資料元素]**
1. 選擇 **[!UICONTROL 新增資料元素]**
1. ****&#x200B;將資料元素命名為 **`xdm.content`**
1. 作為 **[!UICONTROL 擴充功能]** 選取 `Adobe Experience Platform Web SDK`
1. 作為 **[!UICONTROL 資料元素類型]** 選取 `XDM object`
1. 選取平台 **[!UICONTROL 沙箱]** 在中建立XDM架構的 [設定XDM結構](configure-schemas.md) 本範例中的課程 `DEVELOPMENT Mobile and Web SDK Courses`
1. 作為 **[!UICONTROL 結構]**，選取 `Luma Web Event Data` 方案：

   ![XDM物件](assets/data-element-xdm.content-fields.png)

   >[!NOTE]
   >
   >沙箱對應於您建立結構的Experience Platform沙箱。 您的Experience Platform例項中可能有多個沙箱，因此請務必選取正確的沙箱。 總是先在開發中工作，再在生產中工作。

1. 向下捲動，直到到達 **`web`** 物件
1. 選取以開啟

   ![Web對象](assets/data-element-pageviews-xdm-object.png)


1. 將下列Web XDM變數對應至資料元素

   * **`web.webPageDetials.name`** 到 `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** 到 `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** 到 `%page.pageInfo.hierarchie1%`

   ![XDM物件](assets/data-element-xdm.content.png)

1. 接下來，找到 `identityMap` 架構中的物件，並加以選取

1. 對應至 `identityMap.loginID` 資料元素

1. 選擇 **[!UICONTROL 儲存]**

   ![資料收集介面](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)




在這些步驟結束時，您應建立下列資料元素：

| 核心擴充功能資料元素 | Platform Web SDK資料元素 |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.content` |
| `page.pageInfo.pageName` |  |
| `page.pageInfo.server` |  |
| `user.profile.attributes.loggedIn` |  |
| `user.profile.attributes.username` |  |

備妥這些資料元素後，您就可以在標籤中建立規則，借此透過XDM物件將資料傳送至Platform Edge Network。

[下一個： ](create-tag-rule.md)

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Web SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
