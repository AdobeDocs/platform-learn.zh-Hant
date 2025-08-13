---
title: 使用同盟資料豐富Experience Platform閱聽眾
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 使用同盟資料豐富Experience Platform閱聽眾
description: 在此視覺化練習中，Experience Platform對象已加入同盟資料而更加豐富。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
hide: true
source-git-commit: 0bbdc93969b4716407ecf51499d572cb50f5a0d3
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 7%

---


# 使用同盟資料豐富Experience Platform受眾

同盟對象構成可讓您運用從企業資料倉儲已同盟的構成對象資料，使Adobe Experience Platform (AEP)中現有的對象更為豐富。 此資料將不會長期保存在 Adobe Experience Platform 客戶輪廓中。

## 在同盟構成中讀取AEP對象

在此視覺化練習中，我們使用儲存在AEP設定檔服務中的&#x200B;**SecurFinancial貸款申請頁面訪客**&#x200B;對象，來啟動我們的同盟構成。 它會使用Snowflake中的同盟資料，根據信用評分和貸款活動來決定預先核准。

![federated-composition-example](assets/snowflake-preapproval.png)

### 步驟

1. **將AEP對象**&#x200B;對應到同盟對象組合目的地。
2. **使用對應的對象來建置您的組合**&#x200B;做為讀取對象。
3. **調解讀取對象中的身分**，以加入同盟資料。

![federated-method-1-1](assets/federated-method-1-1.png)

![federated-method-1-2](assets/federated-method-1-2.png)

我們將檢視另一個使用同盟資料來[支援「即時」個人化的範例](drive-in-the-moment-personalization.md)！
