---
title: Microsoft Azure活動中心Audience Activation — 摘要與優點
description: Microsoft Azure活動中心Audience Activation — 摘要與優點
kt: 5342
doc-type: tutorial
exl-id: 3b598ffc-875e-468d-b91c-882062e8203f
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---

# 摘要與優點

恭喜並感謝您投入時間學習Microsoft Azure活動中心和Adobe Experience Platform！
在本模式中，您已瞭解如何設定Azure事件中心執行個體，以及如何將其連結至Adobe Experience Platform。

## 優點

讓我們強調整合Adobe Experience Platform與Microsoft Azure活動中心的好處：

- Microsoft Azure事件中樞作為Adobe Experience Platform目的地，可讓您即時擷取對象資格，並使用Azure事件中樞功能加以處理。 透過這類Azure事件中樞功能，您可以建置任何型別的自訂對象啟用處理常式，並進而整合任何型別的第三方目的地。

- 雖然目的地僅由指定的對象觸發，但啟用裝載將會包含特定設定檔符合資格的所有對象。

- 對象只會在狀態變更時觸發啟動。 例如，在三個月的期間內符合對象資格四次的設定檔，將只會啟用前兩個設定檔。 第一個是從&#x200B;**已實現**&#x200B;的狀態變更，第二個是由從&#x200B;**已實現**&#x200B;到&#x200B;**現有**&#x200B;的狀態變更所觸發。

- 針對已知設定檔啟用對象時，完整的身分對應會包含在啟用裝載中。 您的Azure函式可使用任何可用身分識別，將對象對應至第三方應用程式中管理的設定檔，同時使用應用程式的客戶識別碼。

- 在此模組中，事件中樞功能已部署在本機（Visual Studio Code中的偵錯模式），為您提供許多疑難排解和偵錯選項。

## 看看這個

- 不適用

[返回模組2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模組](./../../../overview.md)
