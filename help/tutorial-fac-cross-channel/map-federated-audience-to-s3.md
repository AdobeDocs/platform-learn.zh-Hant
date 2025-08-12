---
title: 將同盟對象對應至S3
seo-title: Map a federated audience to S3 | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 將同盟對象對應至S3
description: 在本課程中，我們將對應同盟對象至下游Real-Time CDP目的地，以支援個人化的離線體驗。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: b5611dccdba66d31f7dfcd96506e06d1bdd5fb3d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# 將同盟對象對應至S3以運用對象屬性來擴充

在本練習中，您將瞭解如何在您的資料倉儲中運用對象屬性，讓您的對象在使用RTCDP目的地的下游啟用工作流程中更加豐富。 對於SecurFinancial，這些同盟屬性可用於增強客戶受眾的離線個人化體驗。 在此範例中，我們會將同盟對象對應至預先設定的Amazon S3目的地。

## 步驟

1. 導覽至&#x200B;**目的地**&#x200B;入口網站。

2. 按一下預先設定的Amazon S3目的地旁的&#x200B;**3點選單**&#x200B;按鈕，然後按一下&#x200B;**啟用對象**。

   ![啟用對象](assets/activate-audiences.png)

3. 選取&#x200B;**S3目的地**，然後按一下&#x200B;**下一步**。

   ![select-s3-destination](assets/select-s3-destination.png)

4. 選取&#x200B;**SecureFinancial客戶 — 沒有貸款，信用良好**&#x200B;對象。

   ![select-s3-audience](assets/select-s3-audience.png)

5. 在&#x200B;**排程**&#x200B;區段中，保留所有預設設定並按一下&#x200B;**下一步**。

6. 在&#x200B;**對應**&#x200B;步驟中，確定已包含`xdm: personalEmail.address`並選取為&#x200B;**重複資料刪除索引鍵**。 然後按一下&#x200B;**下一步**：

   ![重複資料刪除索引鍵](assets/deduplication-key.png)

7. 在以下對應步驟中，您可以根據同盟對象構成中的對象欄位對應來選取擴充屬性。 按一下&#x200B;**鉛筆（編輯）**&#x200B;圖示以檢視預先選取的屬性。

   ![編輯屬性](assets/edit-attributes.png)

   ![最終屬性](assets/final-attribution.png)

8. 檢閱您的對象對應並點選&#x200B;**完成**。

我們已準備好繼續進行[建置歷程](build-journey-federated-audience.md)。
