---
title: 對應身分
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 對應身分
description: 在本課程中，我們將建立身分識別命名空間，並將身分欄位新增至結構描述。
role: Data Architect
feature: Profiles
kt: 4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 2%

---

# 對應身分

<!-- 30 min-->

在本課程中，我們將建立身分識別命名空間，並將身分欄位新增至結構描述。 執行此動作後，我們也能完成上一堂課的架構關係。

Adobe Experience Platform Identity Service可協助您跨裝置和系統橋接身分，以便即時提供具影響力的個人數位體驗，進而更全面了解客戶及其行為。 身分欄位和命名空間是將不同資料來源連結在一起，以建立360度即時客戶設定檔的黏合劑。

**資料架構師** 需要在本教學課程之外對應身分。

開始練習之前，請觀看此短片，以進一步了解Adobe Experience Platform中的身分：
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

>[!NOTE]
>
>只有在您建立即時客戶設定檔時，才需要身分欄位。 如果您只要將資料擷取到資料湖，則不需要用到這些資料。

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## 需要權限

在 [設定權限](configure-permissions.md) 課程中，您設定了完成本課程所需的所有訪問控制。

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## 建立身分命名空間

在本練習中，我們將為Luma的自訂身分欄位建立身分識別命名空間， `loyaltyId`, `crmId`，和 `productSku`. 身分識別命名空間在建立即時客戶設定檔方面扮演關鍵角色，因為相同命名空間中的兩個相符值可讓兩個資料來源形成身分圖表。


### 在UI中建立命名空間

首先，請為Luma忠誠度結構建立命名空間：

1. 在Platform使用者介面中，前往 **[!UICONTROL 身分]** 在左側導覽列中
1. 您會發現有數個現成可用的身分識別命名空間。 選取 **[!UICONTROL 建立身分命名空間]** 按鈕
1. 提供詳細資訊，如下所示

   | 欄位 | 值 |
   |---------------|-----------|
   | 顯示名稱 | Luma忠誠度Id |
   | 標識符 | lumaLoyaltyId |
   | 類型 | 跨裝置 |

1. 選擇 **[!UICONTROL 建立]**

   ![建立命名空間](assets/identity-createNamespace.png)

現在，請為Luma產品目錄架構設定另一個命名空間，並提供下列詳細資訊：

| 欄位 | 值 |
|---------------|-----------|
| 顯示名稱 | Luma產品SKU |
| 標識符 | lumaProductSKU |
| 類型 | 非人員識別碼 |



## 使用API建立身分命名空間

我們將透過API建立CRM命名空間。

>[!NOTE]
>
>如果您偏好略過API練習，歡迎透過您與下列詳細資料搭配使用的使用者介面方法建立CRM命名空間：
>
> 1. 作為 **[!UICONTROL 顯示名稱]**，使用 `Luma CRM Id`
> 1. 作為 **[!UICONTROL 標識符]**，使用 `lumaCrmId`
> 1. 作為 **[!UICONTROL 類型]**，使用跨裝置


我們來建立身分命名空間 `Luma CRM Id`:

1. 下載 [Identity Service.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json) 至 `Luma Tutorial Assets` 資料夾
1. 將集合匯入 [!DNL Postman]
1. 如果您在過去24小時內未提出請求，則您的授權Token可能已過期。 開啟請求 **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]**，然後選取 **傳送** 請求新的JWT和存取權杖。
1. 選擇請求 **[!UICONTROL Identity服務] > [!UICONTROL 身分命名空間] > [!UICONTROL 建立新的身分命名空間].**
1. 將下列項目貼上為 [!DNL Body] 請求：

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. 按下 **傳送** 按鈕，你應該 **200 OK** 回應：

   ![身分識別命名空間](assets/identity-createUsingApi.png)

如果您返回使用者介面，現在應該會看到三個新的自訂命名空間：
![身分命名空間 ](assets/identity-newIdentities.png)


## 標籤結構中的標識欄位

現在，我們擁有了命名空間，下一步就是更新結構以標示身分欄位。


### 標示主要身分的XDM欄位

與即時客戶設定檔搭配使用的每個結構都需要指定主要身分。 而每個擷取的記錄必須有該欄位的值。

將主要身分新增至 `Luma Loyalty Schema`:

1. 開啟 `Luma Loyalty Schema`
1. 選取 `Luma Identity profile field group`
1. 選取 `loyaltyId` 欄位
1. 檢查 **[!UICONTROL 身分]** box
1. 檢查 **[!UICONTROL 主要身分]** 框
1. 選取 `Luma Loyalty Id` 命名空間 **[!UICONTROL 身分識別命名空間]** 下拉式清單
1. 選擇 **[!UICONTROL 套用]**
1. 選擇 **[!UICONTROL 儲存]**

   ![主要身分 ](assets/identity-loyalty-primary.png)

對您的其他架構重複此程式：

1. 在 `Luma CRM Schema`，標籤 `crmId` 欄位作為主要身分，使用 `Luma CRM Id` 命名空間
1. 在 `Luma Offline Purchase Events Schema`，標籤 `loyaltyId` 欄位作為主要身分，使用 `Luma Loyalty Id` 命名空間
1. 在 `Luma Product Catalog Schema`，標籤 `productSku` 欄位作為主要身分，使用 `Luma Product SKU` 命名空間

>[!NOTE]
>
>透過Web SDK收集的資料是結構中標示身分欄位之一般實務的例外情況。 Web SDK使用「身分對應」來標示身分 *在實作端* 我們就會確定 `Luma Web Events Schema` 當我們在Luma網站上實作Web SDK時。 在稍後的課程中，我們會將Experience Cloud訪客ID(ECID)收集為主要ID，並將crmId收集為次要ID。

通過我們對主要身份的選擇，我們可以清楚地看到 `Luma CRM Schema` 可以連線至 `Luma Offline Purchase Events Schema` 因為兩者都使用 `loyaltyId` 做為識別碼。 但我們如何將線下購買與線上行為聯繫起來呢？ 如何分類隨產品目錄購買的產品？ 我們將使用其他身分欄位和結構關係。

<!--use a visual-->

### 為次要身分標示XDM欄位

可將多個身分欄位新增至結構。 非主要身分通常稱為次要身分。 若要將離線購買連線至線上行為，我們會將crmId新增為我們的 `Luma Loyalty Schema` 和更新的網頁事件資料。 讓我們更新 `Luma Loyalty Schema`:

1. 開啟 `Luma Loyalty Schema`
1. 選擇 `Luma Identity Profile Field group`
1. 選擇 `crmId` 欄位
1. 檢查 **[!UICONTROL 身分]** box
1. 選取 `Luma CRM Id` 命名空間 **[!UICONTROL 身分識別命名空間]** 下拉式清單
1. 選擇 **[!UICONTROL 套用]** ，然後選取 **[!UICONTROL 儲存]** 按鈕以保存更改

   ![次要身分](assets/identity-loyalty-secondaryId.png)

## 完成架構關係

現在，我們已將身分欄位標示為，我們可以完成Luma產品目錄與事件結構之間架構關係的設定：

1. 開啟 `Luma Offline Purchase Events Schema`
1. 選擇 **[!UICONTROL 商務詳細資訊]** 欄位群組
1. 選擇 **[!UICONTROL productListItems]** > **[!UICONTROL SKU]** 欄位
1. 檢查 **[!UICONTROL 關係]** box
1. 選擇 `Luma Product Catalog Schema` 作為 **[!UICONTROL 參考結構]**
1. `Luma Product SKU` 應會自動填入為 **[!UICONTROL 參考身分命名空間]**
1. 選擇 **[!UICONTROL 套用]**
1. 選擇 **[!UICONTROL 儲存]**

   ![參考欄位](assets/identity-offlinePurchase-relationship.png)

重複此程式，在 `Luma Web Events Schema` 和 `Luma Product Catalog Schema`.

請注意，定義關係後，會在 **[!UICONTROL 組合物]** 和 **[!UICONTROL 結構]** 綱要編輯器的區段。

![結構編輯器中的關係視覺效果](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## 其他資源

* [Identity Service 文件](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=zh-Hant)
* [Identity服務API](https://www.adobe.io/experience-platform-apis/references/identity-service/)

既然我們的身份已經確定，我們可以 [建立資料集](create-datasets.md)!
