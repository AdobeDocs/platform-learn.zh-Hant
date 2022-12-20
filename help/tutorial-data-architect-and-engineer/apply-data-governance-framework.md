---
title: 套用資料控管架構
seo-title: Apply the data governance framework | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 套用資料控管架構
description: 在本課程中，您會將資料控管架構套用至已擷取至沙箱的資料。
role: Data Architect
feature: Data Governance
kt: 4348
thumbnail: 4348-apply-data-governance-framework.jpg
exl-id: 3cc3c794-5ffd-41bf-95d8-be5bca2e3a0f
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 2%

---

# 套用資料控管架構

<!--15min-->

在本課程中，您會將資料控管架構套用至已擷取至沙箱的資料。

Adobe Experience Platform資料控管可讓您管理客戶資料，並確保符合適用於資料使用的法規、限制和政策。 它在Experience Platform內的各個層級（包括控制資料的使用）中扮演著關鍵角色。

開始練習之前，請觀看以下有關資料控管的短片：
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

## 業務方案

Luma向其忠誠計畫的成員承諾不會與任何第三方共用忠誠資料。 我們將在本課程的其餘部分中實施此情景。

## 套用資料控管標籤

資料控管程式的第一步，是將控管標籤套用至您的資料。 在執行此操作之前，請先快速了解可用的標籤：

1. 在Platform使用者介面中，選取 **[!UICONTROL 原則]** 在左側導覽列中
1. 前往 **[!UICONTROL 標籤]** 標籤，查看帳戶中的所有標籤。

有許多現成可用的標籤，而且您可以透過 [!UICONTROL 建立標籤] 按鈕。 主要有三種類型： [!UICONTROL 合約標籤], [!UICONTROL 身分標籤]，和 [!UICONTROL 敏感標籤] 與可能限制資料的常見原因對應。 每個標籤都有 [!UICONTROL 易記名稱] 和簡短 [!UICONTROL 名稱] 只是類型和數字的縮寫。 例如， [!DNL C1] 標籤是用於「無第三方匯出」，這是我們的忠誠度政策所需的項目。

![資料控管標籤](assets/governance-policies.png)

現在，是時候為我們要限制其使用情形的資料加上標籤了：

1. 在Platform使用者介面中，選取 **[!UICONTROL 資料集]** 在左側導覽列中
1. 開啟 `Luma Loyalty Dataset`
1. 前往 **[!UICONTROL 資料控管]** 標籤
1. 您可以將標籤套用至個別欄位，或套用至整個資料集。 我們會將標籤套用至整個資料集。 按一下鉛筆圖示。 如果沒有看到表徵圖，請嘗試使瀏覽器更寬或向右滾動中間面板。
   ![資料控管](assets/governance-dataset.png)
1. 在強制回應視窗中，展開 **[!UICONTROL 合約標籤]** 區段並檢查 **[!UICONTROL C2]** 標籤
1. 選取 **[!UICONTROL 儲存變更]** 按鈕
   ![資料控管](assets/governance-applyLabel.png)
1. 返回主 [!UICONTROL 資料控管] 螢幕，搭配 **[!UICONTROL 顯示繼承的標籤]** 開啟「 」，您就會看到標籤已套用至資料集中所有欄位的方式。
   ![資料控管](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## 建立資料控管原則

現在，我們的資料已經標籤了，我們可以建立策略。

1. 在Platform使用者介面中，選取 **[!UICONTROL 原則]** 在左側導覽列中
1. 在「瀏覽」標籤上，已有一個名為「第三方匯出限制」的現成可用政策，可將C2標籤與行銷動作建立關聯 [!UICONTROL 匯出至第三方] — 正是我們需要的！
1. 選取原則，然後透過 **[!UICONTROL 策略狀態]** 切換
   ![資料控管](assets/governance-enablePolicy.png)

您可以選取 **[!UICONTROL 建立原則]** 按鈕。 這會開啟精靈，讓您結合多個標籤和行銷動作限制。

## 執行治理政策

執行治理政策顯然是該框架的關鍵組成部分。 當資料啟動並從Platform傳出時，強製作業會在下游進行，尤其是透過Real-time Customer Data Platform，您可能或不可能取得授權。 無論如何，都不在本教學課程的討論範圍內。 但是，你不會被遺忘，你可以在視頻中進一步了解如何執行策略，我已經排到了相關部分。 它還將向您顯示違反策略時會發生什麼情況。

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on)


## 其他資源

* [資料控管檔案](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)
* [資料集服務API參考](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [治理策略服務API參考](https://www.adobe.io/experience-platform-apis/references/policy-service/)

現在，讓我們繼續 [查詢服務](run-queries.md).
