---
title: 區段啟動至Microsoft Azure事件中心 — 摘要和優點
description: 區段啟動至Microsoft Azure事件中心 — 摘要和優點
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 2174ac52-b5dd-4bc8-ab5f-4d84ae9ef19b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# 摘要和優點

祝賀您，感謝您花時間學習Microsoft Azure活動中心和Adobe Experience Platform!
在本模組中，您學習了如何設定Azure Event Hub執行個體，以及如何將其連線至Adobe Experience Platform。

## 優點

讓我們強調整合Adobe Experience Platform與Microsoft Azure活動中心的優點：

- Microsoft Azure事件中心作為Adobe Experience Platform目的地，可讓您即時擷取區段資格，並使用Azure事件中心功能處理。 使用此類Azure事件中心功能，您可以建立任何類型的自訂區段啟用處理常式，並因此整合任何類型的第三方目的地。

- 雖然目的地僅由指定的區段觸發，但啟動裝載將包含指定設定檔符合資格的所有區段。

- 區段只有在狀態變更時才會觸發啟動。 例如，在三個月內符合區段4次的設定檔，只會啟動前兩個區段。 第一個是狀態從變更為 **實現**，第二個則會由 **實現** to **現有**.

- 為已知設定檔啟用區段時，啟用裝載中會包含完整身分對應。 您的Azure函式可使用任何可用的身分，將區段對應至在第三方應用程式中管理的設定檔，同時使用應用程式的客戶識別碼。

- 在此模組中，事件中心函式已部署到本地（在Visual Studio代碼中為調試模式），為您提供了許多故障排除和調試選項。

## 看看這個

- 不適用

[返回模組13](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模組](./../../overview.md)
