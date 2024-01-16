---
title: 使用Platform Web SDK設定Audience Manager
description: 瞭解如何使用Platform Web SDK設定Adobe Audience Manager，並使用Cookie目的地驗證實作。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
solution: Data Collection, Audience Manager
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 1%

---

# 使用Platform Web SDK設定Audience Manager

瞭解如何使用Platform Web SDK設定Adobe Audience Manager，並使用Cookie目的地驗證實作。

[Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html) 是Adobe Experience Cloud解決方案，提供收集網站訪客之商業相關資訊、建立可行銷區段，以及將目標定位廣告和內容提供給適當對象所需的一切。


## 學習目標

在本課程結束時，您將能夠：

* 設定資料流以啟用Audience Manager
* 在Audience Manager中啟用Cookie目的地
* 透過確認具有Adobe Experience Platform Debugger的對象資格來驗證Audience Manager實施

## 先決條件

若要完成本課程，您必須先：

* 完成本教學課程之初始設定和標籤設定區段中先前的課程。
* 擁有Adobe Audience Manager的存取權，以及建立、讀取和寫入特徵、區段和目的地的適當許可權。 如需詳細資訊，請檢閱 [Audience Manager的角色型存取控制](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).

## 設定資料串流

使用Platform Web SDK的Audience Manager實作與使用 [伺服器端轉送(SSF)](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html?lang=zh-Hant). 伺服器端轉送會將Adobe Analytics請求資料傳遞給Audience Manager。 Platform Web SDK實作會將傳送至Platform Edge Network的XDM資料傳遞至Audience Manager。 已在資料流中啟用Audience Manager：

1. 前往 [資料彙集](https://experience.adobe.com/#/data-collection){target="blank"} 介面
1. 在左側導覽中選取 **[!UICONTROL 資料串流]**
1. 選取先前建立的 `Luma Web SDK` 資料流

   ![選取Luma Web SDK資料流](assets/datastream-luma-web-sdk.png)

1. 選取 **[!UICONTROL 新增服務]**
   ![將服務新增至資料流](assets/aam-datastream-addService.png)
1. 選取 **[!UICONTROL Adobe Audience Manager]** 作為 **[!UICONTROL 服務]**
1. 確認 **[!UICONTROL Cookie目的地已啟用]** 和 **[!UICONTROL 已啟用URL目的地]** 已選取
1. 選取 **[!UICONTROL 儲存]**
   ![確認Audience Manager資料流設定並儲存](assets/aam-datastream-save.png)

## 建立資料來源

接下來，建立 [資料來源](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-sources/datasources-list-and-settings.html?lang=en)，在Audience Manager中組織資料的基本工具：

1. 前往 [Audience Manager](https://experience.adobe.com/#/audience-manager/) 介面
1. 選取 **[!UICONTROL 對象資料]** 從頂端導覽
1. 選取 **[!UICONTROL 資料來源]** 從下拉式功能表
1. 選取 **[!UICONTROL 新增]** 「資料來源」頁面頂端的按鈕

   ![Adobe Experience PlatformAudience Manager資料來源](assets/data-sources-list.jpg)

1. 為資料來源提供好記的名稱和說明。 對於初始設定，您可以命名此`Platform Web SDK tutorial`.
1. 設定 **[!UICONTROL ID型別]** 至 **[!UICONTROL Cookie]**
1. 在 **[!UICONTROL 資料匯出控制]** 區段，選取 **[!UICONTROL 無限制]**

   ![Adobe Experience PlatformAudience Manager資料來源設定](assets/data-source-details.png)

1. **[!UICONTROL 儲存]** 資料來源


## 建立特徵

在儲存資料來源後，設定 [特徵](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/traits-overview.html?lang=zh-Hant). 特徵是Audience Manager中一或多個訊號的組合。 為首頁訪客建立特徵。

>[!NOTE]
>
>所有XDM資料都會傳送至Audience Manager （如果在資料流中啟用），不過資料可能需要24小時才能在「未使用的訊號」報表中使用。 為您要立即在Audience Manager中使用的XDM資料建立明確特徵，如本練習所述。

1. 選取 **[!UICONTROL 對象資料]** >  **[!UICONTROL 特徵]**
1. 選取 **[!UICONTROL 新增]** >  **[!UICONTROL Rule-Based]** 特徵

   ![Adobe Experience PlatformAudience Manager規則型特徵](assets/rule-based-trait.jpg)

1. 為您的特徵提供好記的名稱和說明， `Luma homepage view`
1. 選取 **[!UICONTROL 資料來源]** 您在上一節中建立。
1. **[!UICONTROL 選取資料夾]** 將您的特徵儲存在右側窗格中的位置。 建立資料夾的方法有： **選取+圖示** 位於現有父資料夾旁。 您可以命名這個新資料夾 `Platform Web SDK tutorial`.
1. 展開 **[!UICONTROL 特徵運算式]** 插入號並選取 **[!UICONTROL 運算式產生器]** 您必須提供表示首頁造訪的金鑰值組。
1. 開啟 [Luma首頁](https://luma.enablementadobe.com/content/luma/us/en.html) （對應至您的標籤屬性）和 **Adobe Experience Platform Debugger** 並重新整理頁面。
1. 檢視Platform Web SDK的網路要求和事件詳細資訊，以尋找首頁的索引鍵和名稱值。
   ![Adobe Experience PlatformAudience ManagerXDM資料](assets/xdm-keyvalue.jpg)
1. 返回Audience ManagerUI中的運算式產生器，並輸入索引鍵為 **`web.webPageDetails.name`** 和的值 **`content:luma:us:en`**. 此步驟可確保您每次載入首頁時都會引發特徵。
1. **[!UICONTROL 儲存]** 特徵。


## 建立區段

下一步是建立 **區段**，並將您新定義的特性指派給此區段。

1. 選取 **[!UICONTROL 對象資料]** 在頂端導覽列中，並選取 **[!UICONTROL 區段]**
1. 選取 **[!UICONTROL 新增]** 以開啟區段產生器
1. 為您的區段提供好記的名稱和說明，例如 `Platform Web SDK - Homepage visitors`
1. **[!UICONTROL 選取資料夾]** 您的區段將儲存在右側窗格中的位置。 建立資料夾的方法有： **選取+圖示** 位於現有父資料夾旁。 您可以命名這個新資料夾 `Platform Web SDK tutorial`.
1. 新增整合程式碼，在此例中是隨機數字集。
1. 在 **[!UICONTROL 資料來源]** 區段，選取 **[!UICONTROL Audience Manager]** 以及您先前建立的資料來源
1. 展開 **[!UICONTROL 特徵]** 區段並搜尋您建立的特徵
1. 選取 **[!UICONTROL 新增特徵]**.
1. 選取 **[!UICONTROL 儲存]** 在頁面底部

   ![Adobe Experience PlatformAudience Manager新增特徵](assets/add-trait-segment.jpg)

   ![Adobe Experience PlatformAudience Manager新增特徵](assets/saved-segment.jpg)

## 建立目的地

接下來，建立 **Cookie型目的地** 使用 **目的地產生器**. 目的地產生器可讓您建立和管理Cookie、URL和伺服器對伺服器目的地。

1. 選取「 」以開啟「目的地產生器」 **[!UICONTROL 目的地]** 在 **對象資料** 頂端導覽列中的功能表
1. 選取 **[!UICONTROL 建立目的地]**
1. 輸入名稱和說明， `Platform Web SDK tutorial`
1. 作為 **[!UICONTROL 類別]**，選取 **[!UICONTROL 自訂]**
1. 作為 **[!UICONTROL 型別]**，選取 **[!UICONTROL Cookie]**

   ![Adobe Experience PlatformAudience Manager新增特徵](assets/destination-settings.jpg)

1. 開啟 **[!UICONTROL 設定]** 區段，以輸入有關Cookie目的地的詳細資訊
1. 為您的Cookie提供好記的名稱， `platform_web_sdk_tutorial`
1. 作為 **[!UICONTROL Cookie網域]**，新增您計畫整合之網站的網域，針對教學課程輸入Luma網域， `luma.enablementadobe.com`
1. 作為 **[!UICONTROL 將資料發佈至]** 選項，選取 **[!UICONTROL 僅限選取的網域]**
1. 選取您的網域（如果尚未新增）
1. 作為 **[!UICONTROL 資料格式]**，選取 **[!UICONTROL 單一金鑰]** 並給您的Cookie金鑰。 用於本教學課程 `segment` 做為機碼值。
1. 最後，選取 **[!UICONTROL 儲存]** 以儲存目的地組態詳細資訊。

   ![「Audience Manager目的地組態」段落](assets/aam-destination-config-dw.png)

<!--
   ![Adobe Experience Platform Audience Manager Add Trait](assets/aam-destination-config.jpg)


   ![Adobe Experience Platform Audience Manager Add Trait](assets/cookie-destination-config.jpg)
-->

1. 在 **[!UICONTROL 區段對應]** 區段，使用 **[!UICONTROL 搜尋和新增區段]** 功能，可搜尋您先前建立的 `Platform Web SDK - Homepage visitors` 並選取 **[!UICONTROL 新增]**.


1. 新增區段後，快顯視窗隨即開啟，您必須提供Cookie的預期值。 對於此練習，請輸入「hpvisitor」值。

1. 選取 **[!UICONTROL 儲存]**

1. 選取 **[!UICONTROL 完成]**
   ![Adobe Experience PlatformAudience Manager新增特徵](assets/luma-cookie-segment-dw.png)

區段對應期間需要數小時才能啟用。 完成後，您可以重新整理Audience Manager介面，並檢視 **對應的區段** 清單已更新。

## 驗證區段

在最初建立區段數小時後，您可以驗證其是否正常運作。

首先，確認您符合區段的資格

1. 開啟 [Luma示範網站首頁](https://luma.enablementadobe.com/content/luma/us/en.html) 將區段對應至您的標籤屬性，以符合新建立區段的資格。
1. 開啟瀏覽器的 **開發人員工具**  > **網路** 標籤
1. 使用以下專案篩選至Platform Web SDK請求 `interact` 做為文字篩選
1. 選取呼叫並開啟 **預覽** 標籤以檢視回應詳細資料
1. 展開 **裝載** 以檢視預期Cookie詳細資訊，如先前在Audience Manager中所設定。 在此範例中，您會看到預期的Cookie名稱 `platform_web_sdk_tutorial`.

   ![Adobe Experience PlatformAudience Manager新增特徵](assets/segment-validate-response.jpg)

1. 開啟 **應用** 標籤，並開啟 **Cookie** 從 **儲存** 功能表。
1. 選取 **`https://luma.enablementadobe.com`** 網域，並確認您的Cookie已正確寫入清單中

   ![Adobe Experience PlatformAudience Manager新增特徵](assets/validate-cookie.jpg)


最後，您應該在Audience Manager介面中開啟區段，並確定 **區段母體** 已增加：

![Adobe Experience PlatformAudience Manager新增特徵](assets/segment-population.jpg)


現在您已完成本課程，應該能夠瞭解Platform Web SDK如何將資料傳遞至Audience Manager，以及如何透過Cookie目的地設定區段特定的第一方Cookie。

[下一步： ](setup-target.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
