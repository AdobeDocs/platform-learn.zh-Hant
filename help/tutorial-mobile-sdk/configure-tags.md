---
title: 設定標籤屬性
description: 了解如何在 [!UICONTROL 資料收集] 介面。
exl-id: 0c4b00cc-34e3-4d08-945e-3fd2bc1b6ccf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 10%

---

# 設定標籤屬性

了解如何在 [!UICONTROL 資料收集] 介面。

Adobe Experience Platform 標記是新一代 Adobe 標記管理功能。標記可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告標記功能，以強化相關客戶體驗。深入了解 [標籤](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) 在產品檔案中。

## 先決條件

若要完成本課程，您必須擁有建立標籤屬性的權限。 對標籤有基準的了解也會有所幫助。

>[!NOTE]
>
> platform launch（用戶端）現在為 [標籤](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hant)

## 學習目標

在本課程中，您將：

* 安裝並設定行動標籤擴充功能。
* 產生SDK安裝指示。

## 初始設定

1. 建立新的行動標籤屬性：
   1. 在 [資料收集介面](https://experience.adobe.com/data-collection/){target=&quot;_blank&quot;}，請選取 **[!UICONTROL 標籤]** 在左側導覽列中
   1. 選擇 **[!UICONTROL 新屬性]**

      ![建立標籤屬性](assets/mobile-tags-new-property.png).
   1. 若 **[!UICONTROL 名稱]**，輸入 `Mobile SDK Course`.
   1. 若 **[!UICONTROL 平台]**，選取 **[!UICONTROL 行動]**.
   1. 選取「**[!UICONTROL 儲存]**」。

      ![設定標籤屬性](assets/mobile-tags-property-config.png)

      >[!NOTE]
      >
      > 邊緣型行動sdk實作（例如您在本教學課程中執行的實作）的預設同意設定來自 [!UICONTROL 同意擴充功能] 而不是 [!UICONTROL 隱私權] 設定。 您將在本課程稍後新增及設定「同意」擴充功能。 如需詳細資訊，請參閱 [檔案](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr).


1. 開啟新屬性
1. 建立程式庫:

   1. 前往 **[!UICONTROL 發佈流程]** 的下一頁。
   1. 選擇 **[!UICONTROL 新增程式庫]**.

      ![選擇添加庫](assets/mobile-tags-create-library.png)

   1. 若 **[!UICONTROL 名稱]**，輸入 `Initial Build`.
   1. 若 **[!UICONTROL 環境]**，選取 **[!UICONTROL 開發]**.
   1. 選擇  **[!UICONTROL 新增所有已變更的資源]**.
   1. 選擇 **[!UICONTROL 儲存並建置至開發]**.

      ![建立程式庫](assets/mobile-tags-save-library.png)

   1. 最後，將其設定為 **[!UICONTROL 工作程式庫]**.
      ![選取作為工作程式庫](assets/mobile-tags-working-library.png)
1. 選擇 **[!UICONTROL 擴充功能]**.

   行動核心和設定檔擴充功能應已預先安裝。

1. 選擇 **[!UICONTROL 目錄]**.

   ![初始設定](assets/mobile-tags-starting.png)

1. 使用 [!UICONTROL 搜尋] 功能，尋找並安裝下列擴充功能。 這些擴充功能皆不需要任何設定：
   * 身分
   * AEP保證

## 擴充功能組態

1. 安裝 **同意** 擴充功能。

   在本教學課程中，請選取 **[!UICONTROL 待定]**. 深入了解「同意」擴充功能，位於 [檔案](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network).

   ![同意設定](assets/mobile-tags-extension-consent.png)

1. 安裝 **Adobe Experience Platform Edge Network** 擴充功能。

   在 **[!UICONTROL Edge設定]** 下拉式清單，選取您在 [上一步](create-datastream.md).

1. 選擇 **[!UICONTROL 儲存至程式庫並建置]**.

   ![邊緣網路設定](assets/mobile-tags-extension-edge.png)


## 產生SDK安裝指示

1. 選擇 **[!UICONTROL 環境]**.

1. 選取 **[!UICONTROL 開發]** 「安裝」圖示。

   ![環境主畫面](assets/mobile-tags-environments.png)

1. 選擇 **[!UICONTROL iOS]**.

1. 選擇 **[!UICONTROL Swift]**.

   ![安裝指示](assets/mobile-tags-install-instructions.png)

1. 安裝指示可為您提供實作的良好起點。

   您可以找到其他資訊 [此處](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk).

   * **[!UICONTROL 環境檔案ID]**:此唯一ID指向您的開發環境，請注意此值。 生產/測試/開發都會有不同的ID值。
   * **[!UICONTROL Podfile]**:CocoaPods可用來管理SDK版本和下載。 若要進一步了解，請檢閱 [檔案](https://cocoapods.org/).
   * **[!UICONTROL 初始化程式碼]**:此程式碼區塊說明如何在啟動時匯入必要的SDK並註冊擴充功能。

>[!NOTE]
>安裝指示應視為起點，而非最終檔案。 您可以在官方 [檔案](https://aep-sdks.gitbook.io/docs/).

## 行動標籤架構

如果您熟悉標籤的網頁版本（先前稱為Launch），請務必了解行動裝置上的差異。

在Web上，標籤屬性會轉譯為JavaScript，然後（通常）托管於雲端。 網站會直接參照該JS檔案。

在行動標籤屬性中，規則和設定會轉譯為雲端中托管的JSON檔案。 JSON檔案會由行動應用程式中的行動核心擴充功能下載及讀取。 擴充功能是可搭配使用的個別SDK。 如果您將擴充功能新增至標籤屬性，您也必須更新應用程式。 如果您變更擴充功能設定或建立規則，當您發佈更新的標籤程式庫時，這些變更會反映在應用程式中。

下一個： **[安裝SDK](install-sdks.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)