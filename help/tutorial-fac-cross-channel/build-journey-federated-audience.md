---
title: 使用同盟受眾資料建立歷程
seo-title: Build a journey with federated audience data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: 使用同盟受眾資料建立歷程
description: 在此視覺練習中，同盟對象用於Journey Optimizer歷程中。
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-build-a-journey-with-federated-audience-data.jpg
hide: true
exl-id: a153667a-9b3a-4db7-9f58-b83e695009e0
source-git-commit: a3c8d8b03472d01f491bf787ed647a696d3a5524
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 1%

---

# 使用同盟受眾資料建立歷程

同盟受眾可用於Adobe Journey Optimizer (AJO)內的歷程。 這包括使用Federated Audience Composition的查詢屬性來個人化訊息。

為了繼續進行SecurFinancial案例，特別是客戶重新定位和個人化使用案例，我們為預先合格的客戶策劃了歷程。 目標是根據SecurFinancial的Data Warehouse所同盟的屬性來傳送個人化電子郵件。

## 步驟

### 與讀取對象建立歷程

1. 導覽至&#x200B;**歷程**&#x200B;入口網站，然後按一下&#x200B;**建立歷程**&#x200B;按鈕。

   ![建立歷程](assets/create-journey.png)

2. 以新名稱更新歷程屬性。 在我們的範例中： **`SecurFinancial - Home Loan Offer`**。

3. 按一下&#x200B;**協調流程**，然後將&#x200B;**讀取對象**&#x200B;圖磚拖放至畫布。

4. 按一下畫面右側「對象」方塊旁的&#x200B;**鉛筆圖示**。

5. 在搜尋列中搜尋對象。 在我們的範例中： **`SecureFinancial Customers - No Loans, Good Credit`**。 按一下&#x200B;**儲存**。

   ![建立歷程](assets/select-audience.png)

6. 在右側功能表中保留所有設定為預設值，然後按一下[儲存]。**&#x200B;**

   ![儲存對象設定](assets/save-audience-settings.png)

### 個人化電子郵件

1. 按一下&#x200B;**動作**，然後按一下並將&#x200B;**電子郵件**&#x200B;圖磚拖曳到畫布。

2. 在右側功能表上，按一下&#x200B;**電子郵件設定**&#x200B;並選取&#x200B;**電子郵件行銷**。 然後按一下&#x200B;**編輯內容**。

3. 新增主旨列。 在我們的範例中： **`Learn more about SecurFinancial Home Loan`**。 然後按一下&#x200B;**編輯電子郵件內文**。

4. 按一下右上角的&#x200B;**內容範本**&#x200B;按鈕。 尋找並選取適當的範本。 我們的範例使用`SecureFinancial Template`。 然後按一下&#x200B;**確認**。

   ![journey-email-config](assets/journey-email-config.png)

   ![journey-email-confirm](assets/journey-email-confirm.png)

5. 檢閱範本，然後按一下&#x200B;**使用範本**。

6. 您現在會收到電子郵件Designer。 將游標暫留在`{profile.person.name.firstName}`巨集上，然後按一下&#x200B;**個人化頭像**。

7. 在個人化視窗中，向下展開至具有已上傳同盟對象的資料夾路徑。 在我們的範例中： **`[sandbox] > audienceEnrichment > CustomerAudienceUpload`**

8. 按一下&#x200B;**讀取對象**&#x200B;資料夾。 您可在此處找到同盟對象的擴充屬性。

9. 選取運算式產生器的&#x200B;**名字**&#x200B;屬性。 電子郵件會動態地表示客戶的名字值，以便個人化電子郵件。

10. 按一下&#x200B;**儲存**。

11. 現在已新增名字個人化，請在個人化變數前新增`Hi, `。 然後按一下[儲存]。**&#x200B;**

    ![歷程 — 電子郵件 — 儲存](assets/journey-email-save.png)

12. 按兩下&#x200B;**上一步**&#x200B;按鈕以返回歷程畫布。 然後在右側的&#x200B;**動作：電子郵件**&#x200B;功能表中，按一下&#x200B;**儲存**。

   ![儲存 — 最終歷程](assets/save-final-journey.png)

我們使用同盟受眾和同盟擴充屬性在AJO中建立了歷程。

現在我們將瞭解如何透過Data Warehouse中的同盟資料[擴充Experience Platform中的現有對象](federated-audience-composition.md)。
