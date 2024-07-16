---
title: 對應身分
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 對應身分
description: 在本課程中，我們將建立身分識別名稱空間，並將身分識別欄位新增至結構描述。
role: Data Architect
feature: Profiles
jira: KT-4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 6%

---

# 對應身分

<!-- 30 min-->

在本課程中，我們將建立身分識別名稱空間，並將身分識別欄位新增至結構描述。 完成此操作後，我們還將能夠完成上一個課程的結構描述關係。

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更清楚瞭解客戶及其行為。 身分欄位和名稱空間是將不同資料來源連線在一起，以建立360度即時客戶個人檔案的膠水。

**資料架構師**&#x200B;需要在本教學課程之外對應身分。

在開始練習之前，請觀看此短片，進一步瞭解Adobe Experience Platform中的身分識別：
>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on)

>[!NOTE]
>
>只有在您建立即時客戶設定檔時，才需要身分欄位。 如果您只將資料擷取到Data Lake，則不需要使用這兩項功能。

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## 需要的許可權

在[設定許可權](configure-permissions.md)課程中，您已設定完成本課程所需的所有存取控制。

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## 建立身分名稱空間

在本練習中，我們將為Luma的自訂身分識別欄位`loyaltyId`、`crmId`和`productSku`建立身分識別名稱空間。 身分識別命名空間在建立即時客戶設定檔方面扮演關鍵角色，因為相同命名空間中的兩個相符值可讓兩個資料來源形成身分識別圖表。


### 在UI中建立名稱空間

讓我們從建立Luma忠誠度方案的名稱空間開始：

1. 在Platform使用者介面中，前往左側導覽中的&#x200B;**[!UICONTROL 身分]**
1. 您會發現有多個現成的身分識別名稱空間可供使用。 選取&#x200B;**[!UICONTROL 建立身分名稱空間]**&#x200B;按鈕
1. 提供詳細資訊，如下所示

   | 欄位 | 值 |
   |---------------|-----------|
   | 顯示名稱 | Luma忠誠度Id |
   | 身分符號 | lumaLoyaltyId |
   | 類型 | 跨裝置 |

1. 選取&#x200B;**[!UICONTROL 建立]**

   ![建立命名空間](assets/identity-createNamespace.png)

現在為Luma產品目錄結構描述設定另一個名稱空間，其詳細資訊如下：

| 欄位 | 值 |
|---------------|-----------|
| 顯示名稱 | Luma產品SKU |
| 身分符號 | lumaProductSKU |
| 類型 | 非人員識別碼 |



## 使用API建立身分名稱空間

我們將透過API建立CRM名稱空間。

>[!NOTE]
>
>如果您偏好略過API練習，可以透過您使用的使用者介面方法來建立CRM名稱空間，並附上下列詳細資料：
>
> 1. 作為&#x200B;**[!UICONTROL 顯示名稱]**，請使用`Luma CRM Id`
> 1. 作為&#x200B;**[!UICONTROL 身分符號]**，請使用`lumaCrmId`
> 1. 以&#x200B;**[!UICONTROL 型別]**&#x200B;的身分，使用跨裝置

讓我們建立身分識別名稱空間`Luma CRM Id`：

1. 將[Identity Service.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json)下載至您的`Luma Tutorial Assets`資料夾
1. 將集合匯入[!DNL Postman]
1. 如果您沒有存取權杖，請開啟要求&#x200B;**[!DNL OAuth: Request Access Token]**&#x200B;並選取&#x200B;**傳送**&#x200B;以要求新的存取權杖。
1. 選取要求&#x200B;**[!UICONTROL 身分識別服務] > [!UICONTROL 身分識別名稱空間] > [!UICONTROL 建立新的身分識別名稱空間]。**
1. 將下列內容貼上為請求的[!DNL Body]：

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. 按下&#x200B;**傳送**&#x200B;按鈕，您應該會收到&#x200B;**200 OK**&#x200B;回應：

   ![身分識別命名空間](assets/identity-createUsingApi.png)

如果您返回使用者介面，現在應該會看到三個新的自訂名稱空間：
![身分識別名稱空間](assets/identity-newIdentities.png)


## 結構描述中的標籤身分欄位

現在我們有名稱空間了，下一步就是更新結構，為身分識別欄位加上標籤。


### 主要身分的標籤XDM欄位

與Real-Time Customer Profile搭配使用的每個結構描述都需要指定主要身分。 而且每個擷取的記錄都必須有該欄位的值。

將主要身分新增至`Luma Loyalty Schema`：

1. 開啟`Luma Loyalty Schema`
1. 選取`Luma Identity profile field group`
1. 選取`loyaltyId`欄位
1. 檢查&#x200B;**[!UICONTROL 身分]**&#x200B;方塊
1. 也請勾選&#x200B;**[!UICONTROL 主要身分]**&#x200B;方塊
1. 從&#x200B;**[!UICONTROL 身分識別名稱空間]**&#x200B;下拉式清單中選取`Luma Loyalty Id`名稱空間
1. 選取&#x200B;**[!UICONTROL 套用]**
1. 選取&#x200B;**[!UICONTROL 儲存]**

   ![主要身分](assets/identity-loyalty-primary.png)

對部分其他結構描述重複此程式：

1. 在`Luma CRM Schema`中，使用`Luma CRM Id`名稱空間將`crmId`欄位標示為主要身分
1. 在`Luma Offline Purchase Events Schema`中，使用`Luma Loyalty Id`名稱空間將`loyaltyId`欄位標示為主要身分
1. 在`Luma Product Catalog Schema`中，使用`Luma Product SKU`名稱空間將`productSku`欄位標示為主要身分

>[!NOTE]
>
>透過Web SDK收集的資料是架構中標籤身分欄位典型做法的例外情況。 Web SDK使用身分對應來標籤實作端&#x200B;*的身分識別*，因此我們將在Luma網站上實作Web SDK時決定`Luma Web Events Schema`的身分識別。 在稍後的課程中，我們會將Experience Cloud訪客ID (ECID)收集為主要ID，並將crmId收集為次要ID。

透過我們選取的主要身分，可清楚瞭解`Luma CRM Schema`如何連線至`Luma Offline Purchase Events Schema`，因為它們都使用`loyaltyId`做為識別碼。 但我們如何將離線購買與線上行為聯絡起來？ 如何分類隨產品目錄一起購買的產品？ 我們將使用其他身分欄位和結構描述關係。

<!--use a visual-->

### 標示次要身分的XDM欄位

可以將多個身分欄位新增到結構描述。 非主要身分通常稱為次要身分。 若要將離線購買連結至線上行為，我們會將crmId作為次要識別碼新增至`Luma Loyalty Schema`，並於稍後新增至我們的網頁事件資料。 讓我們更新`Luma Loyalty Schema`：

1. 開啟`Luma Loyalty Schema`
1. 選取`Luma Identity Profile Field group`
1. 選取`crmId`欄位
1. 檢查&#x200B;**[!UICONTROL 身分]**&#x200B;方塊
1. 從&#x200B;**[!UICONTROL 身分識別名稱空間]**&#x200B;下拉式清單中選取`Luma CRM Id`名稱空間
1. 選取&#x200B;**[!UICONTROL 套用]**，然後選取&#x200B;**[!UICONTROL 儲存]**&#x200B;按鈕以儲存您的變更

   ![次要身分](assets/identity-loyalty-secondaryId.png)

## 完成結構描述關係

現在我們的身分欄位已加上標籤，我們可以完成Luma產品目錄與事件結構描述之間的結構描述關係設定：

1. 開啟`Luma Offline Purchase Events Schema`
1. 選取&#x200B;**[!UICONTROL Commerce詳細資料]**&#x200B;欄位群組
1. 選取&#x200B;**[!UICONTROL productListItems]** > **[!UICONTROL SKU]**&#x200B;欄位
1. 檢查&#x200B;**[!UICONTROL Relationship]**&#x200B;方塊
1. 選取`Luma Product Catalog Schema`做為&#x200B;**[!UICONTROL 參考結構描述]**
1. `Luma Product SKU`應該自動填入為&#x200B;**[!UICONTROL 參考身分名稱空間]**
1. 選取&#x200B;**[!UICONTROL 套用]**
1. 選取&#x200B;**[!UICONTROL 儲存]**

   ![參考欄位](assets/identity-offlinePurchase-relationship.png)

重複此程式以建立`Luma Web Events Schema`與`Luma Product Catalog Schema`之間的關係。

請注意，定義關聯性後，結構描述編輯器的&#x200B;**[!UICONTROL 構成]**&#x200B;和&#x200B;**[!UICONTROL 結構]**&#x200B;區段中都會指出關聯性。

結構描述編輯器中的![關係視覺效果](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## 其他資源

* [Identity Service檔案](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hant)
* [身分識別服務API](https://www.adobe.io/experience-platform-apis/references/identity-service/)

現在我們的身分已準備就緒，我們可以[建立資料集](create-datasets.md)！
