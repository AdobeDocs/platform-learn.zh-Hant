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
source-git-commit: d73f9b3eafb327783d6bfacaf4d57cf8881479f7
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# 建立合併原則

<!--20 min-->

在本課程中，您將建立合併原則，以排定多個資料來源合併至設定檔的優先順序。

Adobe Experience Platform可讓您將來自多個來源的資料彙集在一起，並將其結合，以檢視每個個別客戶的完整檢視。 彙總此資料時，合併原則會決定資料的優先順序，以及要合併哪些資料以建立該統一檢視。

在本課程中，我們將堅持使用使用者介面，但也會有用於建立合併原則的API選項。

**資料架構師**&#x200B;需要在本教學課程之外建立合併原則。

在開始練習之前，請觀看此短片，以進一步瞭解合併原則：
>[!VIDEO](https://video.tv.adobe.com/v/330433?learn=on&enablevpops)

## 需要的許可權

在[設定許可權](configure-permissions.md)課程中，您已設定完成本課程所需的所有存取控制。

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## 關於合併原則與聯合結構描述

您可能會記得，在批次擷取的課程中，我們上傳了兩個記錄，包含相同客戶的稍微不同的資訊。 在[!DNL Loyalty]資料中，客戶的名字是`Daniel`，而他住在`New York City`，但在CRM資料中，客戶的名字是`Danny`，而他住在`Portland`。 客戶資料會隨著時間而改變。 他可能從`Portland`移至`New York City`。 其他專案也會變更，例如電話號碼和電子郵件地址。 當兩個資料來源為同一個使用者提供不同資訊時，合併原則可協助您決定如何處理這些型別的衝突。

那麼，為什麼`Danny`會以名字取勝？ 讓我們來看一下：

1. 在Platform使用者介面中，選取左側導覽中的&#x200B;**[!UICONTROL 設定檔]**
1. 移至&#x200B;**[!UICONTROL 合併原則]**&#x200B;標籤
1. 預設的合併原則是依時間戳記排序。 由於您在忠誠度資料後上傳CRM資料，`Danny`在設定檔中勝出作為名字：

![合併原則畫面](assets/mergepolicies-default.png)

為設定檔啟用多個結構描述時，系統會自動為所有已啟用設定檔的結構描述建立[!UICONTROL 聯合結構描述]，記錄共用基底類別的結構描述。 您可以前往「**[!UICONTROL 聯合結構描述]**」標籤，檢視[!UICONTROL 聯合結構描述]。

![合併原則畫面](assets/mergepolicies-unionSchema.png)

請注意，ExperienceEvent類別沒有聯合結構描述。 雖然ExperienceEvent資料仍會出現在設定檔中，因為它是以時間序列為基礎，每個事件都包含時間戳記和ID，所以衝突並不是問題。

現在，如果您不喜歡該預設合併原則，該怎麼辦？ 如果Luma決定他們的忠誠度系統在衝突時應該是真相的來源呢？ 為此，我們將建立合併原則。

## 在UI中建立合併原則

1. 在「合併原則」畫面上，選取右上角的&#x200B;**[!UICONTROL 建立合併原則]**&#x200B;按鈕
1. 以&#x200B;**[!UICONTROL Name]**&#x200B;的身分，輸入`Loyalty Prioritized`
1. 作為&#x200B;**[!UICONTROL 結構描述]**，請選取&#x200B;**[!UICONTROL XDM設定檔]** (請注意，您的自訂類別（因為是記錄資料）也可用於合併原則)
1. 若要進行&#x200B;**[!UICONTROL Id拼接]**，請選取&#x200B;**[!UICONTROL 私人圖表]**
1. 對於&#x200B;**[!UICONTROL 屬性合併]**，請選取&#x200B;**[!UICONTROL 資料集優先順序]**
1. 將`Luma Loyalty Dataset`和`Luma CRM Dataset`拖放至&#x200B;**[!UICONTROL 資料集]**&#x200B;面板。
1. 將`Luma Loyalty Dataset`拖放到`Luma CRM Dataset`上方，確認位於頂端
1. 選取&#x200B;**[!UICONTROL 儲存]**按鈕
   <!--do i need to explain Private Graph? Is that GA?-->
   ![合併原則](assets/mergepolicies-newPolicy.png)

## 驗證合併原則

讓我們看看合併原則是否如預期般執行：

1. 前往&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤
1. 將&#x200B;**[!UICONTROL 合併原則]**&#x200B;變更為新的`Loyalty Prioritized`原則
1. 作為&#x200B;**[!UICONTROL 身分識別名稱空間]**，請使用您的`Luma CRM Id`
1. 因為&#x200B;**[!UICONTROL 身分值]**&#x200B;使用`b642b4217b34b1e8d3bd915fc65c4452`
1. 選取&#x200B;**[!UICONTROL 顯示設定檔]**&#x200B;按鈕
1. `Daniel`已回來！

![檢視具有不同合併原則的設定檔](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## 使用有限的資料集建立合併原則

使用資料集優先順序建立合併原則時，設定檔中只會包含您在右側包含的相同基底類別的資料集。 讓我們設定另一個合併原則

1. 在「合併原則」畫面上，選取右上角的&#x200B;**[!UICONTROL 建立合併原則]**&#x200B;按鈕
1. 以&#x200B;**[!UICONTROL Name]**&#x200B;的身分，輸入`Loyalty Only`
1. 作為&#x200B;**[!UICONTROL 結構描述]**，請選取&#x200B;**[!UICONTROL XDM設定檔]**
1. 對於&#x200B;**[!UICONTROL Id拼接]**，請選取&#x200B;**[!UICONTROL 無]**
1. 對於&#x200B;**[!UICONTROL 屬性合併]**，請選取&#x200B;**[!UICONTROL 資料集優先順序]**
1. 只將`Luma Loyalty Dataset`拖放至&#x200B;**[!UICONTROL 選取的資料集]**&#x200B;面板。
1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;按鈕

![僅忠誠度合併原則](assets/mergepolicies-loyaltyOnly.png)

## 驗證合併原則

現在來看看此合併原則的功用：

1. 前往&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤
1. 將&#x200B;**[!UICONTROL 合併原則]**&#x200B;變更為新的`Loyalty Only`原則
1. 作為&#x200B;**[!UICONTROL 身分識別名稱空間]**，請使用您的`Luma CRM Id`
1. 因為&#x200B;**[!UICONTROL 身分值]**&#x200B;使用`b642b4217b34b1e8d3bd915fc65c4452`
1. 選取&#x200B;**[!UICONTROL 顯示設定檔]**&#x200B;按鈕
1. 確認找不到設定檔：
   ![僅忠誠度無CRM ID查閱。](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

CRM ID是`Luma Loyalty Dataset`中的身分欄位，但只能使用主要身分來查閱設定檔。 那麼，讓我們使用主要身分`Luma Loyalty Id`來查閱設定檔。」

1. 將&#x200B;**[!UICONTROL 身分識別名稱空間]**&#x200B;變更為`Luma Loyalty Id`
1. 因為&#x200B;**[!UICONTROL 身分值]**&#x200B;使用`5625458`
1. 選取&#x200B;**[!UICONTROL 顯示設定檔]**&#x200B;按鈕
1. 選取設定檔ID以開啟設定檔
1. 前往&#x200B;**[!UICONTROL 屬性]**&#x200B;標籤
1. 請注意，CRM資料集中的其他設定檔詳細資料（例如行動電話號碼和電子郵件地址）無法使用，因為僅限
   ![CRM資料無法在僅忠誠度原則中檢視](assets/mergepolicies-loyaltyOnly-attributes.png)
1. 前往&#x200B;**[!UICONTROL 事件]**&#x200B;標籤
1. ExperienceEvent資料雖然未明確納入合併原則資料集中，但仍可供使用：
   ![事件可在僅忠誠度原則中檢視](assets/mergepolicies-loyaltyOnly-events.png)

## 深入瞭解合併原則

在設定檔搜尋中，將使用的合併原則變更回`Default Timebased`，並選取&#x200B;**[!UICONTROL 顯示設定檔]**&#x200B;按鈕。 丹尼回來了！

![檢視具有不同合併原則的設定檔](assets/mergepolicies-backToDanny.png)

這是怎麼回事？ 嗯，設定檔合併並非一次性專案。 系統會根據多種因素（包括使用何種合併原則），即時組裝即時客戶設定檔。 您可以根據想要的客戶檢視，建立要在不同內容中使用的多個合併原則。

合併原則的主要使用案例是資料治理。 例如，假設您擷取第三方資料至Platform，該資料無法用於個人化使用案例，但&#x200B;_可以_&#x200B;用於廣告使用案例。 您可以建立排除此第三方資料集的合併原則，並使用此合併原則來建立廣告使用案例的區段。

## 其他資源

* [合併原則檔案](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [合併原則API （即時客戶設定檔API的一部分）參考](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

現在讓我們移至[資料治理架構](apply-data-governance-framework.md)。
