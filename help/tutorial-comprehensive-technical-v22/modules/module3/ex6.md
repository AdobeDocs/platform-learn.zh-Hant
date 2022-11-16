---
title: 在客服中心查看您的即時客戶個人檔案實際運作情況
description: 在客服中心查看您的即時客戶個人檔案實際運作情況
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 457347ca-1ce5-4699-bd30-735abdc7b450
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 3%

---

# 3.6在客服中心查看您的即時客戶個人檔案實際運作情況

在本練習中，目標是讓您逐步了解客戶歷程，並像真正的客戶一樣行事。

在這個網站上，我們實作了Adobe Experience Platform。 每個動作都會視為體驗事件，並會即時傳送至Adobe Experience Platform，加上即時客戶設定檔。

在先前的練習中，您最初是一個瀏覽網站的匿名客戶，經過幾個步驟後，您成為了已知客戶。

當同一位客戶最終拿起電話打給您的呼叫中心時，必須立即提供其他通道的資訊，以便讓呼叫中心的體驗具有相關性和個人化。

## 3.6.1使用您的CX應用

作為演示系統的一部分，我們建立了一個CX應用程式模板，可用於模擬客服中心環境。 請按照以下步驟建立此類CX應用程式項目。

前往 [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). 按一下 **新增專案**.

然後，您將看到您的CX應用程式項目。 按一下專案以開啟。

![示範](./images/cxapp3.png)

在CX應用程式項目中，轉到 **整合**. 選取在模組0中建立的Adobe Experience Platform資料收集屬性。 您需要選取具有 **（啟用）** 以其名義。 然後，按一下 **執行**.

![示範](./images/cxapp4.png)

你會看到這個。

![示範](./images/cxapp5.png)

在「設定檔檢視器」面板上，您可以看到ID和命名空間的下列組合：

![客戶設定檔](./images/identities.png)

| 身分 | 命名空間 |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 12507560687324495704459439363261812234 |
| 電子郵件ID | woutervangeluwe+06022022-01@gmail.com |
| 行動號碼ID | +32473622044+06022022-01 |

當客戶呼叫您的呼叫中心時，可使用電話號碼來識別客戶。 因此，在本練習中，您將使用電話號碼來檢索CX應用程式中的客戶配置檔案。

選擇 **電話號碼** 在下拉式清單中，輸入您在網站上使用的電話號碼。 點擊 **輸入**.

![示範](./images/19.png)

您現在會看到理想情況下會顯示在客服中心的資訊，以便客服中心員工在與客戶交談時可以立即獲得所有相關資訊。

![示範](./images/20.png)

下一步： [摘要和優點](./summary.md)

[返回模組3](./real-time-customer-profile.md)

[返回所有模組](../../overview.md)
