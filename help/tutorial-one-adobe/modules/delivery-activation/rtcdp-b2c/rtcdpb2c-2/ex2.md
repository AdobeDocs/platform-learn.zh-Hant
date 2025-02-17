---
title: Intelligent Services - Customer AI建立新例項（設定）
description: Customer AI — 建立新執行個體（設定）
kt: 5342
doc-type: tutorial
exl-id: faf84607-39fc-4e02-b38b-8fb0c64699e7
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---

# 2.2.2 Customer AI — 建立新執行個體（設定）

Customer AI的運作方式是藉由分析現有的消費者體驗事件資料來預測流失或轉換傾向分數。 建立新的Customer AI執行個體，讓行銷人員可定義目標和測量。

## 設定新的Customer AI執行個體

在Adobe Experience Platform中，按一下左側功能表中的&#x200B;**服務**。 **服務**&#x200B;瀏覽器會出現，並顯示您可使用的所有服務。 在Customer AI的卡片中，按一下&#x200B;**開啟**。

![服務導覽](./images/navigatetoservice.png)

按一下&#x200B;**建立執行個體**。

![建立新執行個體](./images/createnewinstance.png)

您將會看到此訊息。

![建立新執行個體](./images/custai1.png)


輸入Customer AI執行處理的必要明細：

- 名稱：使用`--aepUserLdap-- Product Purchase Propensity`
- 說明：使用： **預測客戶購買產品的可能性**
- 傾向性型別：選取&#x200B;**轉換**

按一下&#x200B;**儲存並繼續**。

![設定頁面1](./images/setuppage1.png)

您將會看到此訊息。 選取您在上一個練習中建立的資料集，名為`--aepUserLdap-- - Demo System - Customer Experience Event Dataset`。 按一下&#x200B;**新增**。

![設定頁面1](./images/custai2.png)

您將會看到此訊息。 您必須定義&#x200B;**身分**&#x200B;欄位。 按一下&#x200B;**無**。

![設定頁面1](./images/custai2a.png)

在快顯視窗中，選取&#x200B;**身分對應(identityMap)**，然後選取名稱空間&#x200B;**Demo System - CRMID (crmId)**。 接著，按一下&#x200B;**儲存**。

![設定頁面1](./images/custai2b.png)

按一下&#x200B;**儲存並繼續**。

![設定頁面1](./images/custai2c.png)

選取&#x200B;**將在您的特定資料集中發生**，並將欄位&#x200B;**commerce.purchases.value**&#x200B;定義為目標變數。

![定義CAI目標](./images/caidefinegoal.png)

接著，將排程設定為每週執行&#x200B;**次**，並將時間設定為儘可能接近目前時間。 確定已啟用設定檔&#x200B;**的**&#x200B;啟用分數切換功能。 按一下&#x200B;**儲存並繼續**。

![定義CAI進階](./images/caiadvancepage.png)

設定執行個體後，您可以在Customer AI服務清單中看到它，也可以按一下Customer AI執行個體列來預覽設定和執行詳細資訊的摘要。 如果發現錯誤，摘要面板也會顯示錯誤詳細資料。

![執行個體設定摘要](./images/caiinstancesummary.png)

>[!NOTE]
>
>只要您的Customer AI執行個體的狀態為&#x200B;**等待訓練**&#x200B;或&#x200B;**錯誤**，您就可以修改任何定義或屬性

您的模型執行後，您將會看到此訊息。

![執行個體設定摘要](./images/caiinstancesummary1.png)

## 後續步驟

移至[2.2.3 Customer AI — 評分儀表板和分段（預測並採取行動）](./ex3.md){target="_blank"}

返回[智慧型服務](./intelligent-services.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
