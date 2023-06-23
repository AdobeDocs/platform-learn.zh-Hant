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
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 2%

---

# 套用資料治理架構

<!--15min-->

在本課程中，您會將資料控管框架套用至您已內嵌至沙箱的資料。

Adobe Experience Platform資料控管可讓您管理客戶資料，並確保遵守適用於資料使用的法規、限制和原則。 它在各種層級的Experience Platform中起著關鍵作用，包括控制資料的使用情況。

在開始練習之前，請先觀看這些資料控管的短片：
>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&learn=on)

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&learn=on)

<!--
## Permissions required

In the [Configure Permissions](configure-permissions.md) lesson, you set up all the access controls required to complete this lesson, specifically:

* Permission items **[!UICONTROL Data Governance]** > **[!UICONTROL Manage Usage Labels]**, **[!UICONTROL Manage Data Usage Policies]** and **[!UICONTROL View Data Usage Policies]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` Product Profile
-->

## 業務案例

Luma向其忠誠度計畫的成員承諾，忠誠度資料不會與任何第三方共用。 我們將在課程的其餘部分實作此案例。

## 套用資料治理標籤

資料控管流程的第一步，是將控管標籤套用至您的資料。 在執行此操作之前，讓我們快速瀏覽可用的標籤：

1. 在平台使用者介面中，選取「 」 **[!UICONTROL 原則]** 在左側導覽列中
1. 前往 **[!UICONTROL 標籤]** 標籤來檢視帳戶中的所有標籤。

有許多現成的標籤，加上您可以透過 [!UICONTROL 建立標籤] 按鈕。 有三種主要型別： [!UICONTROL 合約標籤]， [!UICONTROL 身分標籤]、和 [!UICONTROL 敏感標籤] 對應至資料可能受限制的常見原因。 每個標籤都有 [!UICONTROL 易記名稱] 和簡短 [!UICONTROL 名稱] 這是型別和數字的縮寫。 例如， [!DNL C1] 標籤適用於「無第三方匯出」，這是我們忠誠度政策所需的專案。

![資料控管標籤](assets/governance-policies.png)

現在到了標籤我們想限制其使用方式的資料的時候了：

1. 在平台使用者介面中，選取「 」 **[!UICONTROL 資料集]** 在左側導覽列中
1. 開啟 `Luma Loyalty Dataset`
1. 前往 **[!UICONTROL 資料控管]** 標籤
1. 您可以將標籤套用至個別欄位，或將其套用至整個資料集。 我們會將標籤套用至整個資料集。 按一下鉛筆圖示。 如果沒有看見圖示，請嘗試將瀏覽器變寬或向右捲動中間面板。
   ![資料控管](assets/governance-dataset.png)
1. 在強制回應視窗中，展開 **[!UICONTROL 合約標籤]** 區段並檢查 **[!UICONTROL C2]** 標籤
1. 選取 **[!UICONTROL 儲存變更]** 按鈕
   ![資料控管](assets/governance-applyLabel.png)
1. 返回主要 [!UICONTROL 資料控管] 熒幕，使用 **[!UICONTROL 顯示繼承的標籤]** 切換為開啟時，您會看到標籤已套用至資料集中所有欄位的方式。
   ![資料控管](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## 建立資料治理原則

現在我們的資料已加上標籤，我們可以建立原則了。

1. 在平台使用者介面中，選取「 」 **[!UICONTROL 原則]** 在左側導覽列中
1. 在「瀏覽」標籤上，已經有名為「第三方匯出限制」的現成原則，可將C2標籤與行銷動作建立關聯 [!UICONTROL 匯出至第三方] — 完全符合我們的需求！
1. 選取原則，然後透過 **[!UICONTROL 原則狀態]** 切換
   ![資料控管](assets/governance-enablePolicy.png)

您可以選取 **[!UICONTROL 建立原則]** 按鈕。 這會開啟精靈，讓您結合多個標籤和行銷動作限制。

## 強制執行治理原則

執行治理政策顯然是架構的關鍵元件。 當資料啟動並從Platform傳送出去時，執法會發生在下游，尤其是使用Real-time Customer Data Platform （您可能正在授權或不正在授權）。 無論如何，這不在本教學課程的討論範圍內。 但您不會因此而擱置，您可以在此影片中進一步瞭解原則如何執行，我已將此影片排入相關部分的佇列。 它也會顯示違反原則時會發生什麼情況。

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on)


## 其他資源

* [資料控管檔案](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)
* [資料集服務API參考](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [治理原則服務API參考](https://www.adobe.io/experience-platform-apis/references/policy-service/)

現在，讓我們繼續前往 [查詢服務](run-queries.md).
