---
title: 建立客群
seo-title: Create an audience | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 建立客群
description: 在本課程中，我們會設定Adobe Experience Platform與您的企業Data Warehouse之間的連線，以啟用同盟對象構成。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: b5611dccdba66d31f7dfcd96506e06d1bdd5fb3d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 3%

---


# 對象建立練習

此練習會引導您使用同盟對象構成，從Data Warehouse建立對象。 我們建立受眾，以符合信貸分數為650或以上且目前在SecurFinancial投資組合中無貸款的SecurFinancial客戶的資格。

## 步驟

1. 在&#x200B;**客戶>對象**&#x200B;入口網站中，按一下&#x200B;**同盟組合**&#x200B;標籤。
2. 按一下&#x200B;**建立組合**。

   ![建立組合](assets/create-composition.png)

3. 將構成標示為`SecurFinancial Customers - No Loans, Good Credit`。 按一下&#x200B;**建立**。

4. 按一下畫布中的&#x200B;**+**&#x200B;按鈕，然後選取&#x200B;**建置對象**。 右側邊欄應會出現。

5. 按一下&#x200B;**選取結構描述**&#x200B;並選取&#x200B;**FSI_CRM**&#x200B;結構描述，然後按一下&#x200B;**確認**。

6. 按一下&#x200B;**繼續**。 在查詢產生器視窗中，按一下&#x200B;**+**&#x200B;按鈕，然後按&#x200B;**自訂條件**。 建立下列條件：

   `CURRENTPRODUCTS does not contain loan`
   `AND`
   `CREDITSCORE greater than or equal to 650`
   `AND`
   `CONSENTSMARKETINGPREFERRED equal to email`

   *最後一個條件可確保使用行銷偏好設定資料來區隔已選擇電子郵件作為其偏好通訊管道的客戶*。

   **注意：**&#x200B;值欄位區分大小寫。

   您的查詢現在應如下所示：

   ![query-builder](assets/query-builder.png)

7. 按一下下一個&#x200B;**+**&#x200B;按鈕，然後按一下&#x200B;**儲存對象**。 將此步驟標籤為`SecurFinancial Customers - No Loans, Good Credit`。 使用與對象標籤相同的值。

8. 新增下列對象對應：

   - **Source對象欄位：**&#x200B;電子郵件
   - **Source對象欄位：** CURRENTPRODUCTS
   - **Source對象欄位：**&#x200B;名字

9. 選取要用於設定檔的主要身分和名稱空間：

   - **主要身分欄位：**&#x200B;電子郵件
   - **身分名稱空間：**&#x200B;電子郵件

10. 按一下[儲存]&#x200B;**&#x200B;**，然後按一下[開始]&#x200B;**&#x200B;**，執行您剛才建置的組合查詢。

**注意：**&#x200B;我們使用產品和信用資訊來建立對象，這些對象未將敏感資料（如信用評分）移至下游平台進行啟用。

如需對象構成的詳細資訊，請造訪[Experience League](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}。

現在已建立同盟對象，我們將繼續進行[將其對應至S3帳戶](map-federated-audience-to-s3.md)。
