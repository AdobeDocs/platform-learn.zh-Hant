---
title: 建立合併策略
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 建立合併策略
description: 在本課程中，您將建立合併原則，以判斷資料合併至設定檔的方式。
role: Data Architect, Data Engineer
feature: Profiles
kt: 4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# 建立合併策略

<!--20 min-->

在本課程中，您將建立合併原則，以排定多個資料來源合併至設定檔的優先順序。

Adobe Experience Platform可讓您從多個來源匯整資料，並加以結合，以檢視每個客戶的完整檢視。 將這些資料集合在一起時，合併原則會決定資料的優先順序，以及結合哪些資料以建立該統一檢視。

我們將堅持使用本課程的使用者介面，但建立合併原則的API選項也存在。

**資料架構師** 需要在本教學課程之外建立合併原則。

開始練習之前，請觀看此短片，以了解有關合併策略的更多資訊：
>[!VIDEO](https://video.tv.adobe.com/v/330433?quality=12&learn=on)

## 需要權限

在 [設定權限](configure-permissions.md) 課程中，您設定了完成本課程所需的所有訪問控制。

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 關於合併策略和聯合架構

您可能會記得，在批次擷取課程中，我們為同一客戶上傳了兩筆記錄，其資訊稍有不同。 在 [!DNL Loyalty] 資料，客戶的名字是 `Daniel` 他住在 `New York City`，但在CRM資料中，客戶的名字是 `Danny` 他住在 `Portland`. 客戶資料會隨著時間而變更。 也許他從 `Portland` to `New York City`. 其他事情也會改變，例如電話號碼和電子郵件地址。 當兩個資料源為同一個用戶提供不同資訊時，合併策略可幫助您決定如何處理這些類型的衝突。

那麼，為什麼 `Danny` 以名字取勝？ 讓我們看看：

1. 在Platform使用者介面中，選取 **[!UICONTROL 設定檔]** 在左側導覽列中
1. 前往 **[!UICONTROL 合併策略]** 標籤
1. 預設的合併策略按時間戳順序排列。 因為您在忠誠度資料之後上傳了CRM資料， `Danny` 會取出為設定檔中的名字：

![「合併策略」螢幕](assets/mergepolicies-default.png)

為設定檔啟用多個結構時， [!UICONTROL 聯合架構] 會為所有啟用配置檔案的記錄架構自動建立，該架構共用一個基類。 您可以檢視 [!UICONTROL 聯合結構] 去 **[!UICONTROL 聯合架構]** 標籤。

![「合併策略」螢幕](assets/mergepolicies-unionSchema.png)

請注意，ExperienceEvent類別沒有聯合結構。 雖然ExperienceEvent資料仍會登陸設定檔，但因為資料是以時間序列為基礎，每個事件都包含時間戳記和ID，衝突不會成問題。

如果您不喜歡預設合併政策，該怎麼辦？ 如果Luma認為，當發生衝突時，他們的CRM系統應該成為真相的源泉，那會怎樣？ 為此，我們將建立合併策略。

## 在UI中建立合併原則

1. 在「合併策略」螢幕上，選擇 **[!UICONTROL 建立合併策略]** 按鈕
1. 作為 **[!UICONTROL 名稱]**，輸入 `Loyalty Prioritized`
1. 作為 **[!UICONTROL 結構]**，選取 **[!UICONTROL XDM設定檔]** (請注意，自定義類（因為它是記錄資料）也可用於合併策略)
1. 針對 **[!UICONTROL Id匯整]**，選取 **[!UICONTROL 專用圖表]**
1. 針對 **[!UICONTROL 屬性合併]**，選取 **[!UICONTROL 資料集優先順序]**
1. 拖放 `Luma Loyalty Dataset` 和 `Luma CRM Dataset` 到 **[!UICONTROL 資料集]** 中。
1. 請確定 `Luma Loyalty Dataset` 在上面拖放 `Luma CRM Dataset`
1. 選取 **[!UICONTROL 儲存]** 按鈕
<!--do i need to explain Private Graph? Is that GA?-->
![合併策略](assets/mergepolicies-newPolicy.png)

## 驗證合併策略

讓我們看看合併政策是否正如我們預期的那樣：

1. 前往 **[!UICONTROL 瀏覽]** 標籤
1. 變更 **[!UICONTROL 合併策略]** 新 `Loyalty Prioritized` 原則
1. 作為 **[!UICONTROL 身分命名空間]**，使用 `Luma CRM Id`
1. 作為 **[!UICONTROL 身分值]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. 選取 **[!UICONTROL 顯示配置檔案]** 按鈕
1. `Daniel` 回來了！

![使用不同的合併策略查看配置檔案](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## 建立包含有限資料集的合併策略

使用資料集優先順序建立合併原則時，設定檔中只會包含您右側所包含之相同基礎類別的資料集。 設定另一個合併策略

1. 在「合併策略」螢幕上，選擇 **[!UICONTROL 建立合併策略]** 按鈕
1. 作為 **[!UICONTROL 名稱]**，輸入  `Loyalty Only`
1. 作為 **[!UICONTROL 結構]**，選取 **[!UICONTROL XDM設定檔]**
1. 針對 **[!UICONTROL Id匯整]**，選取 **[!UICONTROL 無]**
1. 針對 **[!UICONTROL 屬性合併]**，選取 **[!UICONTROL 資料集優先順序]**
1. 僅拖放 `Luma Loyalty Dataset` to **[!UICONTROL 所選資料集]** 中。
1. 選取 **[!UICONTROL 儲存]** 按鈕

![僅忠誠度合併策略](assets/mergepolicies-loyaltyOnly.png)

## 驗證合併策略

現在，讓我們看看此合併政策的功用：

1. 前往 **[!UICONTROL 瀏覽]** 標籤
1. 變更 **[!UICONTROL 合併策略]** 新 `Loyalty Only` 原則
1. 作為 **[!UICONTROL 身分命名空間]**，使用 `Luma CRM Id`
1. 作為 **[!UICONTROL 身分值]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. 選取 **[!UICONTROL 顯示配置檔案]** 按鈕
1. 確認找不到任何設定檔：
   ![僅忠誠度，無CRM ID查閱。](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

CRM ID是 `Luma Loyalty Dataset`，但只能使用主要身分來查詢設定檔。 那麼，我們用主要身份查找配置檔案， `Luma Loyalty Id`&quot;

1. 變更 **[!UICONTROL 身分命名空間]** to `Luma Loyalty Id`
1. 作為 **[!UICONTROL 身分值]** use `5625458`
1. 選取 **[!UICONTROL 顯示配置檔案]** 按鈕
1. 選取要開啟設定檔的設定檔ID
1. 前往 **[!UICONTROL 屬性]** 標籤
1. 請注意，CRM資料集中的其他設定檔詳細資料（例如行動電話號碼和電子郵件地址）無法使用，因為我們
   ![無法在僅忠誠度原則中檢視CRM資料](assets/mergepolicies-loyaltyOnly-attributes.png)
1. 前往 **[!UICONTROL 事件]** 標籤
1. 儘管未將ExperienceEvent資料明確納入合併原則資料集中，仍可使用該資料：
   ![可在「僅忠誠度」政策中檢視事件](assets/mergepolicies-loyaltyOnly-events.png)

## 有關合併策略的詳細資訊

在設定檔搜尋中，將使用的合併原則變更回 `Default Timebased` ，然後選取 **[!UICONTROL 顯示配置檔案]** 按鈕。 丹尼回來了！

![使用不同的合併策略查看配置檔案](assets/mergepolicies-backToDanny.png)

怎麼回事？ 個人資料合併不是一回事。 即時客戶設定檔會根據各種因素（包括使用哪些合併政策）即時組合。 您可以建立多個合併策略以在不同上下文中使用，具體取決於您想要的客戶視圖。

合併原則的一個主要使用案例是資料控管。 例如，假設您將協力廠商資料內嵌至Platform，這無法用於個人化使用案例，但 _can_ 用於廣告使用案例。 您可以建立一個合併策略來排除此第三方資料集，並使用此合併策略來為廣告使用案例建立段。

## 其他資源

* [合併原則檔案](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [合併原則API（即時客戶設定檔API的一部分）參考](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

現在，讓我們繼續 [資料控管框架](apply-data-governance-framework.md).
