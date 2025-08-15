---
title: 將同盟對象對應至S3
seo-title: Map a federated audience to S3 | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: 將同盟對象對應至S3
description: 在本練習中，我們將對應同盟對象至下游Real-Time CDP目的地，以支援個人化的離線體驗。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a47b8f7b-7bd0-43a0-bc58-8b57d331b444
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 將同盟對象對應至S3以運用對象屬性來擴充

您可以善用資料倉儲中的對象屬性，讓對象在使用RTCDP目的地的下游啟用工作流程中更加豐富。 對於SecurFinancial，這些同盟屬性可用於增強客戶受眾的離線個人化體驗。 下列，同盟對象已對應至預先設定的Amazon S3目的地。

## 步驟

1. 導覽至&#x200B;**目的地**&#x200B;入口網站。

2. 按一下預先設定的Amazon S3目的地旁的&#x200B;**3點選單**&#x200B;按鈕，然後按一下&#x200B;**啟用對象**。

   ![啟用對象](assets/activate-audiences.png)

3. 選取&#x200B;**S3目的地**，然後按一下&#x200B;**下一步**。

   ![select-s3-destination](assets/select-s3-destination.png)

4. 選取適當的對象。 在我們的範例中： **SecureFinancial客戶 — 沒有貸款，信用良好**&#x200B;個對象。

   ![select-s3-audience](assets/select-s3-audience.png)

5. 在&#x200B;**排程**&#x200B;區段中，使用預設設定並按一下&#x200B;**下一步**。

6. 在&#x200B;**對應**&#x200B;步驟中，選擇重複資料刪除索引鍵。 在我們的範例中，`xdm: personalEmail.address`被包含並選取為&#x200B;**重複資料刪除索引鍵**。 然後按一下&#x200B;**下一步**：

   ![重複資料刪除索引鍵](assets/deduplication-key.png)

7. 在對應步驟中，根據同盟對象構成中的對象欄位對應選取擴充屬性。 按一下&#x200B;**鉛筆（編輯）**&#x200B;圖示以檢視預先選取的屬性。

   ![編輯屬性](assets/edit-attributes.png)

   ![最終屬性](assets/final-attribution.png)

8. 檢閱您的對象對應並點選&#x200B;**完成**。

>[**!SUMMARY**]
>
> 我們已成功建立受眾，並輕鬆將其啟動至S3目的地。 此使用者易記介面可讓行銷團隊快速建立及啟用對象，而不需移動基礎資料。

現在我們將[建置歷程](build-journey-federated-audience.md)。
