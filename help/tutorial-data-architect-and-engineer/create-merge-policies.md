---
title: 建立合併原則
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 建立合併原則
description: 在本課程中，您將建立合併原則，以決定資料合併至設定檔的方式。
role: Data Architect, Data Engineer
feature: Profiles
jira: KT-4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: 915502e54365eedb09b12a92aa3b1af71f6de1f4
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# 建立合併原則

<!--20 min-->

在本課程中，您將建立合併原則，以排定多個資料來源合併至設定檔的優先順序。

Adobe Experience Platform可讓您將來自多個來源的資料彙集在一起，並將其結合，以檢視每個個別客戶的完整檢視。 彙總此資料時，合併原則會決定資料的優先順序，以及要合併哪些資料以建立該統一檢視。

在本課程中，我們將堅持使用使用者介面，但也會有用於建立合併原則的API選項。

**資料架構師** 將需要在本教學課程之外建立合併原則。

在開始練習之前，請觀看此短片，以進一步瞭解合併原則：
>[!VIDEO](https://video.tv.adobe.com/v/330433?learn=on)

## 需要的許可權

在 [設定許可權](configure-permissions.md) 課程，您已設定完成本課程所需的所有存取控制項。

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 關於合併原則與聯合結構描述

您可能會記得，在批次擷取的課程中，我們上傳了兩個記錄，包含相同客戶的稍微不同的資訊。 在 [!DNL Loyalty] 資料，客戶的名字是 `Daniel` 他住在 `New York City`，但在CRM資料中，客戶的名字是 `Danny` 他住在 `Portland`. 客戶資料會隨著時間而改變。 也許他從 `Portland` 至 `New York City`. 其他專案也會變更，例如電話號碼和電子郵件地址。 當兩個資料來源為同一個使用者提供不同資訊時，合併原則可協助您決定如何處理這些型別的衝突。

那麼，為什麼會 `Danny` 以名字勝出？ 讓我們來看一下：

1. 在Platform使用者介面中選取 **[!UICONTROL 設定檔]** 在左側導覽列中
1. 前往 **[!UICONTROL 合併原則]** 標籤
1. 預設的合併原則是依時間戳記排序。 因為您已在忠誠度資料之後上傳CRM資料， `Danny` 勝出為設定檔中的名字：

![「合併原則」畫面](assets/mergepolicies-default.png)

為設定檔啟用多個方案時， [!UICONTROL 聯合結構描述] 會為所有已啟用設定檔的記錄結構描述自動建立，這些記錄結構描述共用一個基底類別。 您可以檢視 [!UICONTROL 聯合結構描述] 前往 **[!UICONTROL 聯合結構描述]** 標籤。

![「合併原則」畫面](assets/mergepolicies-unionSchema.png)

請注意，ExperienceEvent類別沒有聯合結構描述。 雖然ExperienceEvent資料仍會出現在設定檔中，因為它是以時間序列為基礎，每個事件都包含時間戳記和ID，所以衝突並不是問題。

現在，如果您不喜歡該預設合併原則，該怎麼辦？ 如果Luma決定他們的忠誠度系統在衝突時應該是真相的來源呢？ 為此，我們將建立合併原則。

## 在UI中建立合併原則

1. 在「合併原則」畫面上，選取 **[!UICONTROL 建立合併原則]** 右上角的按鈕
1. 作為 **[!UICONTROL 名稱]**，輸入 `Loyalty Prioritized`
1. 作為 **[!UICONTROL 結構描述]**，選取 **[!UICONTROL XDM設定檔]** (請注意，您的自訂類別（由於是記錄資料）也可用於合併原則)
1. 的 **[!UICONTROL Id拼接]**，選取 **[!UICONTROL 私人圖表]**
1. 的 **[!UICONTROL 屬性合併]**，選取 **[!UICONTROL 資料集優先順序]**
1. 拖放 `Luma Loyalty Dataset` 和 `Luma CRM Dataset` 至 **[!UICONTROL 資料集]** 面板。
1. 確定 `Luma Loyalty Dataset` 在上方，將其拖放至 `Luma CRM Dataset`
1. 選取 **[!UICONTROL 儲存]** 按鈕
   <!--do i need to explain Private Graph? Is that GA?-->
   ![合併原則](assets/mergepolicies-newPolicy.png)

## 驗證合併原則

讓我們看看合併原則是否如預期般執行：

1. 前往 **[!UICONTROL 瀏覽]** 標籤
1. 變更 **[!UICONTROL 合併原則]** 至您的新檔案 `Loyalty Prioritized` 原則
1. 作為 **[!UICONTROL 身分名稱空間]**，使用您的 `Luma CRM Id`
1. 作為 **[!UICONTROL 身分值]** 使用 `112ca06ed53d3db37e4cea49cc45b71e`
1. 選取 **[!UICONTROL 顯示設定檔]** 按鈕
1. `Daniel` 回來了！

![檢視具有不同合併原則的設定檔](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## 使用有限的資料集建立合併原則

使用資料集優先順序建立合併原則時，設定檔中只會包含您在右側包含的相同基底類別的資料集。 讓我們設定另一個合併原則

1. 在「合併原則」畫面上，選取 **[!UICONTROL 建立合併原則]** 右上角的按鈕
1. 作為 **[!UICONTROL 名稱]**，輸入  `Loyalty Only`
1. 作為 **[!UICONTROL 結構描述]**，選取 **[!UICONTROL XDM設定檔]**
1. 的 **[!UICONTROL Id拼接]**，選取 **[!UICONTROL 無]**
1. 的 **[!UICONTROL 屬性合併]**，選取 **[!UICONTROL 資料集優先順序]**
1. 僅拖放 `Luma Loyalty Dataset` 至 **[!UICONTROL 選取的資料集]** 面板。
1. 選取 **[!UICONTROL 儲存]** 按鈕

![僅限熟客的合併原則](assets/mergepolicies-loyaltyOnly.png)

## 驗證合併原則

現在來看看此合併原則的功用：

1. 前往 **[!UICONTROL 瀏覽]** 標籤
1. 變更 **[!UICONTROL 合併原則]** 至您的新檔案 `Loyalty Only` 原則
1. 作為 **[!UICONTROL 身分名稱空間]**，使用您的 `Luma CRM Id`
1. 作為 **[!UICONTROL 身分值]** 使用 `112ca06ed53d3db37e4cea49cc45b71e`
1. 選取 **[!UICONTROL 顯示設定檔]** 按鈕
1. 確認找不到設定檔：
   ![僅忠誠度無CRM Id查閱。](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

CRM ID是 `Luma Loyalty Dataset`，但僅主要身分可用於查詢設定檔。 那麼，讓我們使用主要身分來查詢設定檔， `Luma Loyalty Id`&quot;

1. 變更 **[!UICONTROL 身分名稱空間]** 至 `Luma Loyalty Id`
1. 作為 **[!UICONTROL 身分值]** 使用 `5625458`
1. 選取 **[!UICONTROL 顯示設定檔]** 按鈕
1. 選取設定檔ID以開啟設定檔
1. 前往 **[!UICONTROL 屬性]** 標籤
1. 請注意，CRM資料集中的其他設定檔詳細資料（例如行動電話號碼和電子郵件地址）無法使用，因為僅限
   ![無法在僅忠誠度原則中檢視CRM資料](assets/mergepolicies-loyaltyOnly-attributes.png)
1. 前往 **[!UICONTROL 活動]** 標籤
1. ExperienceEvent資料雖然未明確納入合併原則資料集中，但仍可供使用：
   ![事件可在「僅限熟客」原則中檢視](assets/mergepolicies-loyaltyOnly-events.png)

## 深入瞭解合併原則

在設定檔搜尋中，將使用的合併原則變更回 `Default Timebased` 並選取 **[!UICONTROL 顯示設定檔]** 按鈕。 丹尼回來了！

![檢視具有不同合併原則的設定檔](assets/mergepolicies-backToDanny.png)

這是怎麼回事？ 嗯，設定檔合併並非一次性專案。 系統會根據多種因素（包括使用何種合併原則），即時組裝即時客戶設定檔。 您可以根據想要的客戶檢視，建立要在不同內容中使用的多個合併原則。

合併原則的主要使用案例是資料治理。 例如，假設您將第三方資料擷取至Platform，這些資料無法用於個人化使用案例，但 _可以_ 用於廣告使用案例。 您可以建立排除此第三方資料集的合併原則，並使用此合併原則來建立廣告使用案例的區段。

## 其他資源

* [合併原則檔案](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [合併原則API （即時客戶設定檔API的一部分）參考](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

現在，讓我們繼續進行 [資料治理框架](apply-data-governance-framework.md).
