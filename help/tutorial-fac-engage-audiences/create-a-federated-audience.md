---
title: 建立同盟對象
seo-title: Create a federated audience | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: 建立同盟對象
description: 在本練習中，我們會設定Adobe Experience Platform與您的企業Data Warehouse之間的連線，以啟用同盟對象構成。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a507cab5-dba9-4bf7-a043-d7c967e9e07d
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 建立同盟受眾

接下來，我們將引導您使用同盟受眾構成，從Data Warehouse建立受眾。 受眾包括信用積分為650或以上且目前其SecurFinancial投資組合中沒有貸款的SecurFinancial客戶。

## 步驟

1. 在&#x200B;**客戶>對象**&#x200B;入口網站中，按一下&#x200B;**同盟組合**&#x200B;標籤。
2. 按一下&#x200B;**建立組合**。

   ![建立組合](assets/create-composition.png)

3. 標籤您的組合。 在我們的範例中： `SecurFinancial Customers - No Loans, Good Credit`。 按一下&#x200B;**建立**。

4. 按一下畫布中的&#x200B;**+**&#x200B;按鈕，然後選取&#x200B;**建置對象**。 右側邊欄隨即顯示。

5. 按一下&#x200B;**選取結構描述**，選取適當的結構描述，然後按一下&#x200B;**確認**。

6. 按一下&#x200B;**繼續**。 在查詢產生器視窗中，按一下&#x200B;**+**&#x200B;按鈕，然後按&#x200B;**自訂條件**。 撰寫條件。 我們的範例使用：

   `CURRENTPRODUCTS does not contain loan`
   `AND`
   `CREDITSCORE greater than or equal to 650`
   `AND`
   `CONSENTSMARKETINGPREFERRED equal to email`

   *最後一個條件可確保使用行銷偏好設定資料來區隔已選擇電子郵件作為其偏好通訊管道的客戶*。

   **注意：**&#x200B;值欄位區分大小寫。

   ![query-builder](assets/query-builder.png)

7. 按一下下一個&#x200B;**+**&#x200B;按鈕，然後按一下&#x200B;**儲存對象**。 標籤此步驟。 在我們的範例中，我們會將其標示為`SecurFinancial Customers - No Loans, Good Credit`。

8. 新增相關的對象對應。 在此範例中：

   - **Source對象欄位：**&#x200B;電子郵件
   - **Source對象欄位：** CURRENTPRODUCTS
   - **Source對象欄位：**&#x200B;名字

9. 選取要用於設定檔的主要身分和名稱空間。 這些是用於資料的身分和欄位：

   - **主要身分欄位：**&#x200B;電子郵件
   - **身分名稱空間：**&#x200B;電子郵件

10. 按一下[儲存]****，然後按一下[開始]****&#x200B;以執行構成查詢。

>[**摘要**]
>
> 在此範例中，我們使用產品和信用資訊來建立受眾，方法是從Snowflake直接存取企業資料，而不需在Adobe Experience Platform中複製。 外部系統處理查詢後，只有相關的電子郵件、目前產品和名字值會帶入對象定義以進行下游啟用。 這適用於RTCDP支援的所有目的地。

如需對象構成的詳細資訊，請造訪[Experience League](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}。

現在已建立同盟對象，我們會將其對應至S3帳戶[。](map-federated-audience-to-s3.md)
