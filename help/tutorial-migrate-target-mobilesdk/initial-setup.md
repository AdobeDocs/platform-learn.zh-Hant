---
title: 初始設定 — 將行動應用程式中的Adobe Target實作移轉至Adobe Journey Optimizer — 決策擴充功能
description: 瞭解並設定Platform Web SDK實作所需的重要基礎元素
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: 45a47cde8bb5ac3baba24d7527fc4029ca3d6596
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 6%

---

# 執行初始資料收集設定

從Target SDK移轉至「最佳化SDK」需要初始設定，以啟用「最佳化SDK」的正確資料擷取、特色和功能。 必須先完成下列步驟，網站實施作業才會發生變更：

- [在Adobe Admin Console中為資料收集設定適當的許可權](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#permissions){target="_blank"}
- [設定XDM結構描述](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"}，以將結構化資料傳遞至Edge Network
- [設定結構描述](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema){target="_blank"}以接收Adobe Target資料
- [設定身分名稱空間](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"}，以使用跨裝置個人化和mbox3rdPartyId功能
- [建立資料串流](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"}以啟用從Edge Network轉送資料
- [設定資料串流](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"}以啟用將資料轉送至Adobe Target的功能
- [設定Decisioning延伸的Tag屬性](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension){target="_blank"}

## 擴充功能組態

>[!BEGINTABS]

>[!TAB 決策延伸]

標籤使用決策擴充功能時安裝的擴充功能：

1. Adobe Journey Optimizer - Decisioning
1. Adobe Experience Platform Edge Network
1. Mobile Core
1. 輪廓
1. 同意
1. 身分識別
1. AEP Assurance （選用，除錯所需）

使用Decisioning擴充功能時安裝的![標籤擴充功能](assets/tag-extensions-decisioning.png)

>[!TAB 目標延伸功能]

使用Target擴充功能時安裝的標籤擴充功能：

1. Adobe Target
1. Mobile Core
1. 輪廓
1. Adobe Analytics (選用，在使用Adobe Analytics做為Adobe Target活動的報表來源時需要)

使用Target擴充功能時安裝的![標籤擴充功能](assets/tag-extensions-target.png)

>[!ENDTABS]

## 資料流設定

Target擴充功能具有[可設定的設定](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui)，而決策擴充功能在datastream](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup)中已設定[。

| 目標延伸功能 | Decisioning擴充功能 | 附註 |
| --- | --- | --- | 
| 用戶端代碼 | 不適用 | 邊緣使用IMS組織詳細資料自動設定 |
| 環境ID | 目標環境ID | 在資料流中設定 |
| 目標Workspace屬性 | 屬性Token | 在資料流中設定 |
| 逾時 | 逾時 | 可在Decisioning擴充功能和最佳化SDK中設定。 預設逾時為10秒。 |
| 伺服器網域 | Edge Network網域 | 在Adobe Experience Platform Edge Network擴充功能中設定 |

接下來，瞭解如何[取代目標SDK](replace-sdk.md)。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
