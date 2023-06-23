---
title: 建立資料串流
description: 建立資料串流
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 52378f63-8a6d-49ed-a21a-65b74fe1ddc4
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 建立資料串流

您從網站傳送的資料會到達一組Adobe伺服器，稱為 [Adobe Experience Platform Edge](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). 此網路能夠將您的資料傳送至 [您先前建立的Adobe Experience Platform資料集](create-a-schema.md) 以及Adobe Experience Cloud中的其他產品。 這些Adobe產品也可能以資料回應您的網頁。 例如，Edge Network可能會從Adobe Target傳回個人化內容。

若要設定Edge Network往返哪些Adobe產品，您必須建立資料串流。 當Edge Network從您的網頁接收資料時，會查詢您建立的資料流、讀取其設定，然後將資料轉送至適當的Adobe產品。

若要建立資料串流，請先導覽至 [!UICONTROL 資料串流] 檢視範圍 [!UICONTROL 資料彙集]. 按一下 [!UICONTROL 建立資料串流] 右上角。 提供資料串流的名稱。

![資料流名稱和說明](../../../assets/implementation-strategy/datastream-name-description.png)

下一個畫面可讓您設定哪些Adobe產品應接收您從網站傳送的資料。 出於本教學課程的目的，請僅啟用Adobe Experience Platform，並選取您先前建立的資料集（預設為資料集） [!UICONTROL Prod] 沙箱)，然後按一下 [!UICONTROL 儲存].

![資料流產品設定](../../../assets/implementation-strategy/datastream-product-configuration.png)

已建立您的資料流。

## 資料流環境

公司通常會有促銷活動路徑，可供任何網站更新使用。 公司人員（行銷人員或工程師，視變更而定）通常會在只有該人員使用的開發環境中測試其變更。 一旦他們對變更感到滿意，就會將變更升級到中繼環境，並在該環境中接受進一步的測試。 最後，變更會發佈至使用者看到的生產網站。 資料串流支援此促銷模式。

在您按一下 [!UICONTROL 儲存]，您應該已注意到系統已自動為您建立三個資料流環境： [!UICONTROL 開發環境]， [!UICONTROL 中繼環境]、和 [!UICONTROL 生產環境].

![資料流環境](../../../assets/implementation-strategy/datastream-environments.png)

如果您按一下每個資料流環境，您會發現它們都已獲得您提供的相同設定。 不過，這些環境可個別自訂。

如果您熟悉Adobe Experience Platform標籤，可能已經熟悉開發、測試和生產環境的概念。 標籤內的環境與資料串流內的環境有關。 當您透過標籤發佈工作流程，將標籤程式庫從開發移至測試環境，再移至生產環境時，所使用的資料流環境也會自動從 [!UICONTROL 開發環境]，至 [!UICONTROL 中繼環境]，至 [!UICONTROL 生產環境]. 舉例來說，這可讓您在變更處於開發狀態時，將資料傳送至一個資料集，並在變更處於生產狀態時，將資料傳送至其他資料集。 這可讓您的生產資料免受任何您在開發過程中可能產生的垃圾資料的影響。 稍後當您在標籤屬性中設定擴充功能時，我們將討論資料流環境。

伺服器現在已完全設定為可從網頁接收資料。
