---
title: 使用Platform Web SDK設定同意
description: 瞭解如何設定Experience PlatformWeb SDK標籤擴充功能的隱私權設定。 本課程屬於「使用Web SDK實作Adobe Experience Cloud」教學課程的一部分。
feature: Web SDK,Tags,Consent
source-git-commit: 695c12ab66df33af00baacabc3b69eaac7ada231
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 0%

---

# 使用Platform Web SDK設定同意

瞭解如何設定Experience PlatformWeb SDK標籤擴充功能的隱私權設定。 根據訪客與同意管理平台(CMP)的橫幅互動來設定同意。

>[!NOTE]
> 
>為了示範，本教學課程使用 [克拉羅](https://heyklaro.com/) 作為CMP。 歡迎您使用Klaro或您在網站中使用的CMP，並加以關注。


## 學習目標

在本課程結束時，您能夠：

* 使用標籤載入CMP
* 在Experience Platform Web SDK標籤擴充功能中設定隱私權設定
* 根據訪客的動作設定Experience PlatformWeb SDK的同意

## 先決條件

您應熟悉標籤以及使用Experience PlatformDebugger建立規則、資料元素、建置程式庫至環境和切換標籤程式庫的步驟。

在您開始設定隱私權設定及建立設定同意的規則之前，請確定您已將同意管理平台指令碼插入網站，且運作正常。 CMP可以在網站開發人員的協助下直接載入原始程式碼中，或是透過標籤本身載入。 本課程將展示後一種方法。
>[!NOTE]
> 
>1. 同意管理平台（或CMP）是組織用來在收集、共用或銷售來自線上來源（例如網站和應用程式）的訪客資料之前，合法記錄和管理訪客的同意選擇。
>
>2. 插入CMP的建議方法是直接透過原始程式碼在標籤管理員指令碼之前進行。

### 設定Klaro

在跳至標籤設定之前，請先進一步瞭解本教學課程Klaro中使用的同意管理平台。

1. 造訪 [克拉羅](https://heyklaro.com/) 並設定帳戶。
1. 前往 **隱私權管理員** 並根據指示建立例項。
1. 使用 **整合代碼** 將Klaro插入標籤屬性中（下一個練習將說明此內容）。
1. 略過 **掃描** 區段，因為它會偵測在Luma示範網站上以硬式編碼撰寫的標籤屬性，而非您為本教學課程建立的標籤屬性。
1. 新增名為的服務 `aep web sdk` 並開啟 **服務預設狀態**. 開啟時，預設同意值為 `true`，否則為 `false`. 如果您想要決定Web應用程式的預設同意狀態（在訪客同意前），此設定相當實用。 例如：
   * 對於CCPA，預設同意通常設定為 `true`. 您即將參考此情境為 **隱含的選擇加入** 貫穿本教學課程
   * GDPR的預設同意通常是設為 `false`. 您即將參考此情境為 **隱含的選擇退出** 貫穿本教學課程。

<!--
    This consent value can be verified by returning the JavaScript object ```klaro.getManager().consents``` in the browser's developer console.
-->
    >[！NOTE]
    >
    >通常，負責處理CMP的團隊或個人（例如OneTrust或TrustArc）會完成並謹慎執行上述步驟。

## 插入CMP

>[!WARNING]
>
>實作同意管理平台的最佳實務通常是載入CMP _早於_ 正在載入您的標籤管理員。 為了協助進行本教學課程，您將載入CMP _替換為_ 標籤管理員。 本課程旨在說明如何在Platform Web SDK中使用同意功能，請勿作為正確設定Klaro或任何其他CMP的指南。


現在，使用完Klaro的設定後，請使用以下設定來建立標籤規則：

* [!UICONTROL 名稱]：`all pages - library load - Klaro`
* [!UICONTROL 事件]： [!UICONTROL 程式庫已載入（頁面頂端）] 替換為 [!UICONTROL 進階選項] > [!UICONTROL 訂購] 設為1
* [!UICONTROL 動作]： [!UICONTROL 自訂程式碼]， [!UICONTROL 語言]：載入CMP指令碼的HTML。

![插入CMP規則](assets/consent-cmp-inject-rule-1.png)

自訂程式碼區塊看起來應該類似下列：

![插入CMP規則](assets/consent-cmp-inject-rule-2.png)

現在，請儲存此規則並建置至您的開發程式庫，將標籤程式庫從Luma網站切換至您自己的網站，以驗證是否顯示同意橫幅。 您應該會在網站上看到CMP橫幅，如下所示。 若要檢查目前訪客的同意許可權，您可在瀏覽器主控台上使用下列程式碼片段。

```javascript
    klaro.getManager().consents 
```

![同意橫幅](assets/consent-cmp-banner.png)

若要進入偵錯模式，請在Adobe Experience Platform Debugger中使用下列核取方塊。

![標籤偵錯模式](assets/consent-rule-debugging.png)

此外，在閱讀本教學課程時，您可能必須多次清除Cookie和本機存放區，因為訪客的同意值會儲存在該處。 您可以直接執行下列動作：

![正在清除儲存空間](assets/consent-clearning-cookies.png)

## 同意情境

GDPR、CCPA等隱私權行為對於您設計同意實作的方式至關重要。 在本課程中，您會探索訪客如何在兩個最顯著的隱私權行為下與同意橫幅互動。
![同意情境](assets/consent-scenarios.jpeg)


### 案例1：隱含的選擇加入

隱含的選擇加入表示在收集訪客資料前，企業不需要取得訪客的同意（或「選擇加入」），因此網站的所有訪客都會預設為選擇加入。 不過，訪客可以透過同意橫幅拒絕Cookie來選擇退出。 此使用案例類似於CCPA。

現在您將針對此情境設定並實作同意：

1. 在 **[!UICONTROL 隱私權]** Experience Platform Web SDK標籤擴充功能的區段，確認  **[!UICONTROL 預設同意]** 設為 **[!UICONTROL 在]** ：


   ![同意AEP擴充功能隱私權設定](assets/consent-web-sdk-privacy-in.png)

   >[!NOTE]
   > 
   >對於動態解決方案，請選取「提供資料元素」選項，然後傳遞傳回值的資料元素 ```klaro.getManager().consents```
   >
   >如果將CMP插入原始程式碼中，則會使用此選項 *早於* 標籤內嵌程式碼，讓使用者在Experience PlatformWeb SDK擴充功能開始載入前即取得預設同意。 在我們的範例中，我們無法使用此選項，因為CMP是透過標籤載入，而不是在標籤之前。



2. 儲存此變更並將其建置到您的標籤程式庫
3. 在Luma示範網站上載入標籤程式庫
4. 在Luma網站上啟用標籤偵錯並重新載入頁面。 在瀏覽器的開發人員主控台中，您應該會看到defaultConsent等於 **[!UICONTROL 在]**
5. 使用此設定時，Experience Platform Web SDK擴充功能會繼續提出網路要求，除非訪客決定拒絕Cookie並選擇退出：

   ![同意隱含選擇加入](assets/consent-Implied-optin-default.png)



如果訪客決定選擇退出（拒絕追蹤Cookie），您必須將同意變更為 **[!UICONTROL 輸出]**. 請依照下列步驟變更同意設定：

<!--
1. Create a data element to store the consent value of the visitor. Let's call it `klaro consent value`. Use the code snippet to create a custom code type data element:
    
    ```javascript
    return klaro.getManager().consents["aep web sdk"]
    ```

    ![Data Element consent value](assets/consent-data-element-value.png)


1. Create another custom code data element, `consent confirmed`, with the following snippet which returns ```true``` only after a visitor confirms consent:

    
    ```javascript
    return klaro.getManager().confirmed
    ```

    ![Data Element consent confirmed](assets/consent-data-element-confirmed.png)
-->

1. 建立訪客點按時觸發的規則 **我拒絕**.  將此規則命名為： `all pages - click consent banner - set consent "out"`

1. 作為 **[!UICONTROL 事件]**，使用 **[!UICONTROL 按一下]** 於 **[!UICONTROL 符合CSS選擇器的元素]** `#klaro .cn-decline`

   ![規則條件使用者點選「我拒絕」](assets/consent-optOut-clickEvent.png)

1. 現在請使用Experience Platform Web SDK， [!UICONTROL 設定同意] [!UICONTROL 動作型別] 將同意設為「out」：

   ![同意規則選擇退出動作](assets/consent-rule-optout-action.png)

1. 選取 **[!UICONTROL 儲存至程式庫並建置]**：

   ![儲存並建置程式庫](assets/consent-rule-optout-saveAndBuild.png)

現在，當訪客選擇退出時，以上述方式設定的規則會引發，並將Web SDK同意設定為 **[!UICONTROL 輸出]**.

前往Luma示範網站進行驗證，拒絕Cookie，並確認選擇退出後沒有引發任何Web SDK請求。

### 案例2：隱含的選擇退出


隱含的選擇退出表示訪客應被視為預設的選擇退出，且不應設定Cookie。 除非訪客決定透過同意橫幅來接受Cookie，以手動方式選擇加入，否則不應引發Web SDK請求。 您可能必須在適用GDPR的歐盟地區處理這類使用案例。

以下說明如何設定隱含選擇退出情境的設定：

1. 在Klaro中，將 **服務預設狀態** 在您的 `aep web sdk` 服務並儲存更新的設定。

1. 在 **[!UICONTROL 隱私權]** Experience Platform Web SDK擴充功能的區段，將預設同意設為 **[!UICONTROL 輸出]** 或 **[!UICONTROL 擱置中]** 視需要。

   ![同意AEP擴充功能隱私權設定](assets/consent-implied-opt-out.png)

1. **儲存** 更新您的標籤程式庫的設定，然後重新建置它。

   透過此設定，Experience Platform Web SDK可確保不會觸發任何要求，除非同意許可權變更為 **[!UICONTROL 在]**. 訪客透過選擇加入以手動方式接受Cookie，因此可能會發生這種情況。

1. 在Debugger中，確認Luma網站已對應至您的標籤屬性，且標籤主控台記錄已開啟。
1. 使用瀏覽器的開發人員主控台： **清除網站資料** 在 **應用** > **儲存**

1. 重新載入Luma網站，您應該會看到 `defaultConsent` 設為 **[!UICONTROL 輸出]** 且尚未提出任何Web SDK請求

   ![同意隱含選擇退出](assets/consent-implied-out-cmp.png)

如果訪客決定選擇加入（接受追蹤Cookie），您必須變更同意並將其設為 **[!UICONTROL 在]**. 以下為使用規則達成此目的的方法：

1. 建立訪客點按時觸發的規則 **沒關係**.  將此規則命名為： `all pages - click consent banner - set consent "in"`

1. 作為 **[!UICONTROL 事件]**，使用 **[!UICONTROL 按一下]** 於 **[!UICONTROL 符合CSS選擇器的元素]** `#klaro .cm-btn-success`

   ![規則條件使用者按一下「沒問題」](assets/consent-optIn-clickEvent.png)

1. 使用Experience PlatformWeb SDK新增動作 [!UICONTROL 副檔名]， **[!UICONTROL 動作型別]** 之 **[!UICONTROL 設定同意]**， **[!UICONTROL 一般同意]** 作為 **[!UICONTROL 在]**.

   ![同意規則選擇加入動作](assets/consent-rule-optin-action.png)

   這裡需要注意的一點是 [!UICONTROL 設定同意] 動作將會是第一個走出並建立身分的請求。 因此，在第一個要求本身上同步身分識別可能很重要。 身分對應可以新增到 [!UICONTROL 設定同意] 動作，方法是傳遞身分型別資料元素。

1. 選取 **[!UICONTROL 儲存至程式庫並建置]**：

   ![同意規則選擇退出](assets/consent-rule-optin-saveAndBuild.png)

1. **[!UICONTROL 儲存]** 將規則移至程式庫並重新建置。

一旦您設定好此規則，事件收集就會在訪客選擇加入時開始。

![同意貼文訪客選項](assets/consent-post-user-optin.png)


如需有關Web SDK中同意的詳細資訊，請參閱 [支援客戶同意偏好設定](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?lang=en).


如需詳細資訊，請參閱 [!UICONTROL 設定同意] 動作，請參閱 [設定同意](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/action-types.html?lang=en#set-consent).

[下一步： ](setup-event-forwarding.md)

>[!NOTE]
>
>感謝您投入時間學習Adobe Experience Platform Web SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
