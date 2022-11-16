---
title: 建立資料流
description: 建立資料流
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 52378f63-8a6d-49ed-a21a-65b74fe1ddc4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 建立資料流

您從網站傳送的資料會到達一組名為 [Adobe Experience Platform Edge](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). 此網路可將您的資料傳送至 [Adobe Experience Platform資料集](create-a-schema.md) 以及Adobe Experience Cloud內的其他產品。 這些Adobe產品也可能會對您的網頁回應資料。 例如，邊緣網路可能會從Adobe Target傳回個人化內容。

若要設定Edge Network會將資料傳輸至和傳送至哪些Adobe產品，您必須建立資料流。 當邊緣網路從您的網頁收到資料時，會諮詢您建立的資料流、讀取其設定，然後將資料轉送至適當的Adobe產品。

若要建立資料流，請先導覽至 [!UICONTROL 資料流] 檢視 [!UICONTROL 資料收集]. 按一下 [!UICONTROL 建立資料流] 在右上角。 提供資料流的名稱。

![資料流名稱和說明](../../../assets/implementation-strategy/datastream-name-description.png)

下一個畫面可讓您設定哪些Adobe產品應接收您從網站傳送的資料。 在本教學課程中，請僅啟用Adobe Experience Platform，選取您先前建立的資料集(預設為 [!UICONTROL 生產] )，然後按一下 [!UICONTROL 儲存].

![資料流產品配置](../../../assets/implementation-strategy/datastream-product-configuration.png)

您的資料流已建立。

## 資料流環境

公司通常會有任何網站更新的促銷路徑。 公司中的某個人（行銷人員或工程師，視變更而定）通常會在只有該人使用的開發環境中測試其變更。 一旦他們熟悉變更，變更就會升級至預備環境，接受進一步的測試。 最後，變更會發佈至使用者看到的生產網站。 資料流支援此促銷模式。

按一下後 [!UICONTROL 儲存]，您應該注意到已自動為您建立三個datastream環境： [!UICONTROL 開發環境], [!UICONTROL 中繼環境]，和 [!UICONTROL 生產環境].

![資料流環境](../../../assets/implementation-strategy/datastream-environments.png)

如果按一下每個資料流環境，您會發現這些環境都獲得您提供的相同設定。 不過，這些環境可以個別自訂。

如果您熟悉Adobe Experience Platform標籤，您可能已熟悉開發、測試和生產環境的概念。 標籤中的環境與資料流中的環境相關。 當您在標籤發佈工作流程中從開發、移至測試、移至生產環境時，使用的資料流環境同樣會自動從 [!UICONTROL 開發環境]，到 [!UICONTROL 中繼環境]，到 [!UICONTROL 生產環境]. 舉例來說，您可以在變更處於開發階段時將資料傳送至一個資料集，並在變更生產階段後，將資料傳送至不同的資料集。 這樣，您的生產資料就不會有開發過程中可能產生的任何垃圾資料。 我們稍後會在您的標籤屬性中設定擴充功能時，討論資料流環境。

伺服器現在已完全設定，可從您的網頁接收資料。
