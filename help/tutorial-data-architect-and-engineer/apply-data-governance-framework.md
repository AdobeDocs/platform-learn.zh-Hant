---
title: 套用資料治理架構
seo-title: Apply the data governance framework | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 套用資料治理架構
description: 在本課程中，您會將資料控管框架套用至您已內嵌至沙箱的資料。
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-apply-data-governance-framework.jpg
exl-id: 3cc3c794-5ffd-41bf-95d8-be5bca2e3a0f
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 1%

---

# 套用資料治理架構

<!--15min-->

在本課程中，您會將資料控管框架套用至您已內嵌至沙箱的資料。

Adobe Experience Platform資料控管可讓您管理客戶資料，並確保遵守適用於資料使用的法規、限制和政策。 在Experience Platform的各個層級上扮演關鍵角色，包括控制資料的使用方式。

在開始練習之前，請先觀看這些有關資料控管的短片：
>[!VIDEO](https://video.tv.adobe.com/v/36653?learn=on)

>[!VIDEO](https://video.tv.adobe.com/v/29708?learn=on)

<!--
## Permissions required

In the [Configure Permissions](configure-permissions.md) lesson, you set up all the access controls required to complete this lesson, specifically:

* Permission items **[!UICONTROL Data Governance]** > **[!UICONTROL Manage Usage Labels]**, **[!UICONTROL Manage Data Usage Policies]** and **[!UICONTROL View Data Usage Policies]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` Product Profile
-->

## 業務案例

Luma向其忠誠度計畫的成員承諾，忠誠度資料不會與任何第三方共用。 我們將在課程的其餘部分實作此情境。

## 套用資料治理標籤

資料控管流程的第一步，是將控管標籤套用至您的資料。 在執行此操作之前，讓我們快速瞭解可用的標籤：

1. 在Platform使用者介面中，選取左側導覽中的&#x200B;**[!UICONTROL 原則]**
1. 移至&#x200B;**[!UICONTROL 標籤]**&#x200B;標籤，檢視帳戶中的所有標籤。

有許多現成的標籤，而且您可以透過[!UICONTROL 建立標籤]按鈕建立自己的標籤。 有三種主要型別： [!UICONTROL 合約標籤]、[!UICONTROL 身分標籤]和[!UICONTROL 敏感標籤]，這些型別對應到資料可能受限制的常見原因。 每個標籤都有[!UICONTROL 易記名稱]和簡短的[!UICONTROL 名稱]，它只是型別和數字的縮寫。 例如，「[!DNL C1]」標籤是用於「無第三方匯出」，這是我們忠誠度政策所需的專案。

![資料控管標籤](assets/governance-policies.png)

現在該標籤我們要限制其使用的資料：

1. 在Platform使用者介面中，選取左側導覽中的&#x200B;**[!UICONTROL 資料集]**
1. 開啟`Luma Loyalty Dataset`
1. 前往&#x200B;**[!UICONTROL 資料控管]**&#x200B;標籤
1. 您可以將標籤套用至個別欄位，或套用至整個資料集。 我們會將標籤套用至整個資料集。 按一下鉛筆圖示。 如果沒有看見圖示，請嘗試將瀏覽器變寬或向右捲動中間面板。
   ![資料控管](assets/governance-dataset.png)
1. 在強制回應視窗中，展開&#x200B;**[!UICONTROL 合約標籤]**&#x200B;區段並檢查&#x200B;**[!UICONTROL C2]**&#x200B;標籤
1. 選取&#x200B;**[!UICONTROL 儲存變更]**按鈕
   ![資料控管](assets/governance-applyLabel.png)
1. 回到主要[!UICONTROL 資料控管]畫面，並開啟&#x200B;**[!UICONTROL 顯示繼承的標籤]**切換功能，您就可以看到標籤已套用至資料集中的所有欄位。
   ![資料控管](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## 建立資料治理原則

現在我們的資料已加上標籤，我們可以建立原則了。

1. 在Platform使用者介面中，選取左側導覽中的&#x200B;**[!UICONTROL 原則]**
1. 在「瀏覽」標籤上，已經有名為「第三方匯出限制」的現成原則，可將C2標籤與行銷動作[!UICONTROL 匯出至第三方]建立關聯 — 正是我們需要的！
1. 選取原則，然後透過&#x200B;**[!UICONTROL 原則狀態]**切換來啟用它
   ![資料控管](assets/governance-enablePolicy.png)

您可以選取&#x200B;**[!UICONTROL 建立原則]**&#x200B;按鈕，以建立您自己的原則。 這會開啟精靈，讓您結合多個標籤和行銷動作限制。

## 強制執行治理原則

執行治理政策顯然是架構的關鍵元件。 當資料啟動並從Platform傳送時，執法會發生在下游，尤其是使用Real-time Customer Data Platform （您可能正在授權或不正在授權）。 無論如何，這不在本教學課程的討論範圍內。 但您不會受影響，您可以在此影片中進一步瞭解原則如何執行，我已排入相關部分的佇列。 它也會顯示違反原則時所發生的情況。

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on)


## 其他資源

* [資料控管檔案](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)
* [資料集服務API參考](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [治理原則服務API參考](https://www.adobe.io/experience-platform-apis/references/policy-service/)

現在讓我們移至[查詢服務](run-queries.md)。
