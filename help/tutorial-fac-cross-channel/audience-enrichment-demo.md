---
title: 使用同盟資料豐富Experience Platform閱聽眾
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 使用同盟資料豐富Experience Platform閱聽眾
description: 在本課程中，我們使用同盟資料讓Experience Platform對象更加豐富。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 5%

---


# 聯合客群構成

同盟對象構成可讓您運用從企業資料倉儲已同盟的構成對象資料，使Adobe Experience Platform (AEP)中現有的對象更為豐富。 此資料將不會長期保存在 Adobe Experience Platform 客戶輪廓中。

## 豐富同盟受眾構成的方法

有兩種主要方法可豐富同盟受眾構成。

### 1.在同盟構成中讀取AEP對象

在第一個範例中，我們將使用儲存在AEP的設定檔服務中的&#x200B;**SecurFinancial貸款申請頁面訪客**&#x200B;對象，以啟動我們的同盟構成。 我們將使用Snowflake中的同盟資料豐富閱聽眾，以根據信用評分和貸款活動決定預先核准。

![federated-composition-example](assets/snowflake-preapproval.png)

1. **將AEP對象**&#x200B;對應到同盟對象組合目的地。
2. **使用對應的對象來建置您的組合**&#x200B;做為讀取對象。
3. **調解讀取對象中的身分**，以加入同盟資料。

![federated-method-1-1](assets/federated-method-1-1.png)

![federated-method-1-2](assets/federated-method-1-2.png)

### 2.透過同盟受眾豐富Experience Platform受眾規則

在第二個範例中，我們將使用查詢信用評分和貸款活動的同盟對象，以豐富貸款應用程式網頁訪客的行為對象。

透過Edge評估此對象，我們可以立即在網站上使用個人化優惠重新鎖定預先核准的貸款申請頁面訪客。

![邊緣受眾擴充](assets/edge-audience-enrich.png)

1. **儲存並開始**&#x200B;您的同盟對象組合。 執行構成後，您的同盟對象將顯示在對象入口網站中。
2. **使用個人資料服務的個人資料屬性和體驗事件來建立對象規則**，並合併您的同盟對象。

讓我們用[學習與最終收穫](conclusion.md)的摘要來總結！
