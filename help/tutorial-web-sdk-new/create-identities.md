---
title: 建立身分
description: 瞭解如何在XDM中建立身分識別，並使用身分對應資料元素來擷取使用者ID。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
feature: Tags
source-git-commit: ef3d374f800905c49cefba539c1ac16ee88c688b
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 1%

---

# 建立身分

瞭解如何使用Experience PlatformWeb SDK擷取身分。 擷取上未驗證和已驗證的身分資料 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html). 瞭解如何使用您先前建立的資料元素，以透過稱為「身分對應」的Platform Web SDK資料元素型別來收集已驗證的資料。

本課程著重於Adobe Experience Platform Web SDK標籤擴充功能所提供的身分對應資料元素。 您可以將包含已驗證使用者ID和驗證狀態的資料元素對應至XDM。

## 學習目標

在本課程結束時，您能夠：

* 瞭解Experience CloudID (ECID)和第一方裝置ID (FPID)之間的關係
* 瞭解未驗證與已驗證ID之間的差異
* 建立身分對應資料元素

## 先決條件

您已瞭解資料層是什麼，並熟悉 [Luma示範網站](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} 資料層，並瞭解如何參照標籤中的資料元素。 您必須完成本教學課程中先前的課程：

* [設定XDM結構描述](configure-schemas.md)
* [設定身分名稱空間](configure-identities.md)
* [設定資料流](configure-datastream.md)
* [安裝在標籤屬性中的Web SDK擴充功能](install-web-sdk.md)
* [建立資料元素](create-data-elements.md)


## Experience Cloud ID

此 [Experience CloudID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) 是跨Adobe Experience Platform和Adobe Experience Cloud應用程式使用的共用身分名稱空間。 ECID是客戶身分識別的基礎，也是數位財產的預設身分識別。 這可讓ECID成為追蹤未驗證使用者行為的理想識別碼，因為它永遠存在

<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

深入瞭解如何 [使用Platform Web SDK追蹤ECID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en).

ECID是使用第一方Cookie和Platform Edge Network的組合來設定。 根據預設，第一方Cookie由Web SDK設定。 若要說明瀏覽器對Cookie有效期的限制，您可以選擇改為設定和管理您自己的第一方Cookie。 這些稱為第一方裝置ID (FPID)。

>[!IMPORTANT]
>
>此 [Experience CloudID服務擴充功能](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) 實作Adobe Experience Platform Web SDK時不需要使用，因為ID服務功能內建於Platform Web SDK中。

## 第一方裝置識別碼(FPID)

FPID是第一方Cookie _您使用自己的網頁伺服器設定_ 然後使用哪個Adobe來建立ECID，而不是使用Web SDK設定的第一方Cookie。 雖然瀏覽器支援可能有所不同，但如果第一方Cookie是由運用DNS A記錄（適用於IPv4）或AAAA記錄（適用於IPv6）的伺服器所設定，而不是由DNS CNAME或JavaScript程式碼設定，則這些支援通常更耐用。

設定FPID Cookie後，就能在收集事件資料時擷取其值並傳送至Adobe。 收集的FPID會作為種子，在Platform Edge Network上產生ECID，這繼續是Adobe Experience Cloud應用程式中的預設識別碼。

雖然本教學課程中不使用FPID，但建議您在自己的網頁SDK實作中使用FPID。 深入瞭解 [Platform Web SDK中的第一方裝置ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html?lang=zh-Hant)

>[!CAUTION]
>
> FPID是使用網頁伺服器設定的Cookie來產生ECID的替代方式。 它不會用於識別已驗證的使用者。

## 已驗證的ID

如上所述，使用Platform Web SDK時，系統會Adobe為您數位財產的所有訪客指派ECID。 如此，ECID就會成為追蹤未驗證數位行為的預設身分識別。

您也可以傳送已驗證的使用者ID，讓Platform能夠建立 [身分圖](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs.html?lang=zh-Hant) 而Target可以設定 [第三方Id](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html). 這是透過使用 [!UICONTROL 身分對應] 資料元素型別。

若要建立 [!UICONTROL 身分對應] 資料元素：

1. 前往 **[!UICONTROL 資料元素]** 並選取 **[!UICONTROL 新增資料元素]**

1. **[!UICONTROL 名稱]** 資料元素 `identityMap.loginID`

1. 作為 **[!UICONTROL 副檔名]**，選取 `Adobe Experience Platform Web SDK`

1. 作為 **[!UICONTROL 資料元素型別]**，選取 `Identity map`

1. 這會提示右側的 **[!UICONTROL 資料收集介面]** 供您設定身分識別：

   ![資料收集介面](assets/identity-identityMap-setup.png)

1. 作為  **[!UICONTROL 名稱空間]**，選取 `lumaCrmId` 您先前在中建立的名稱空間 [設定身分](configure-identities.md) 課程。

   >[!NOTE]
   >
   >    如果您沒有看到 `lumaCrmId` 名稱空間，確認您也在預設的生產沙箱中建立它。 目前，只有在預設生產沙箱中建立的名稱空間才會顯示在名稱空間下拉式清單中。

1. 在 **[!UICONTROL 名稱空間]** ，則必須設定ID。 選取 `user.profile.attributes.username` 之前在中建立的資料元素 [建立資料元素](create-data-elements.md#create-data-elements-to-capture-the-data-layer) 課程，可在使用者登入Luma網站時擷取ID。

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. 作為 **[!UICONTROL 已驗證狀態]**，選取 **[!UICONTROL 已驗證]**
1. 選取 **[!UICONTROL 主要]**

1. 選取 **[!UICONTROL 儲存]**

   ![資料收集介面](assets/identity-id-namespace.png)

>[!TIP]
>
> Adobe建議傳送代表個人的身分，例如 `Luma CRM Id`，作為 [!UICONTROL 主要] 身分。
>
> 如果身分對應包含個人識別碼(例如 `Luma CRM Id`)，則人員識別碼將變成 [!UICONTROL 主要] 身分。 否則， `ECID` 成為 [!UICONTROL 主要] 身分。




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

在這些步驟結束時，您應該建立下列資料元素：

| 核心擴充功能資料元素 | Platform Web SDK擴充功能資料元素 |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `cart.productInfo` | `xdm.variable.content` |
| `cart.productInfo.purchase` | |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `product.category` | |
| `product.productInfo.sku` | |
| `product.productInfo.title` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

備妥這些資料元素後，您就可以開始在標籤中建立規則，透過XDM物件開始將資料傳送至Platform Edge Network。

[下一步： ](create-tag-rule.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
