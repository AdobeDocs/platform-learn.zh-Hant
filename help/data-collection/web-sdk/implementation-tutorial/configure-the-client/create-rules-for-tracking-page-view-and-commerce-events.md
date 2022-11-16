---
title: 建立追蹤頁面檢視和商務事件的規則
description: 建立追蹤頁面檢視和商務事件的規則
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 2dd02462-ddb5-4f67-8b0f-4a5bf5f7d655
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 建立追蹤頁面檢視和商務事件的規則

若要追蹤使用者已檢視產品頁面，請在Adobe Experience Platform標籤中建立規則。 按一下 [!UICONTROL 規則] 在左側功能表中，按一下 [!UICONTROL 新增規則].

對於規則名稱，請輸入 _已檢視的頁面_.

## 新增事件

按一下 [!UICONTROL 新增] 按鈕 [!UICONTROL 事件]. 您現在會顯示在事件檢視上。 若 [!UICONTROL 擴充功能] 欄位，選擇 [!UICONTROL Adobe用戶端資料層]. 若 [!UICONTROL 事件類型] 欄位，選擇 [!UICONTROL 資料推送].

因為您只希望此規則在 `pageViewed` 事件推送至資料層，請選取 [!UICONTROL 特定事件] 在 [!UICONTROL 聽] 和類型 _pageViewed_ 進入 [!UICONTROL 要註冊的事件/密鑰] 文字欄位。

![頁面檢視事件](../../../assets/implementation-strategy/page-viewed-event.png)

按一下[!UICONTROL 保留變更].

## 新增動作

現在您回到規則檢視，請按一下 [!UICONTROL 新增] 按鈕 [!UICONTROL 動作]. 您現在應該位於動作檢視上。 若 [!UICONTROL 擴充功能] 欄位，選擇 [!UICONTROL Adobe Experience Platform Web SDK]. 若 [!UICONTROL 動作類型] 欄位，選擇 [!UICONTROL 傳送事件]. 此動作可讓您將體驗事件傳送至Adobe Experience Platform Edge Network。

在畫面的右側，尋找 [!UICONTROL 類型] 欄位和選取 `web.webpagedetails.pageViews`. 這是Adobe Experience Platform現成可用的標準體驗事件類型之一。 它代表頁面檢視。

若 [!UICONTROL XDM資料] 欄位，輸入 `%event.fullState%`. 這表示資料層的計算狀態（也稱為完整狀態）應在觸發規則時擷取，並應隨體驗事件傳送。

![已檢視頁面動作](../../../assets/implementation-strategy/page-viewed-action.png)

如果您從網站推送至資料層的資料不符合XDM架構，或您只想傳送資料層運算狀態的一部分，請使用 [!UICONTROL XDM物件] 資料元素類型(由Adobe Experience Platform Web SDK擴充功能提供)，以建立符合您結構的適當物件。

按一下[!UICONTROL 保留變更]按鈕.

## 儲存規則

您的規則現在應已完成。

![頁面檢視規則](../../../assets/implementation-strategy/page-viewed-rule.png)

按一下「 [!UICONTROL 儲存].

## 重複此程式

重複上述流程，為檢視產品、開啟購物車和將產品新增至購物車時建立規則。 規則之間的唯一差異將是規則名稱，也就是在 [!UICONTROL 要註冊的事件/密鑰] 欄位 [!UICONTROL 資料推送] 事件和 [!UICONTROL 類型] 欄位 [!UICONTROL 傳送事件] 動作。 以下是每個規則的值：

產品檢視規則：

* **規則名稱**: _已檢視的產品_
* **要註冊的事件/密鑰** with [!UICONTROL 資料推送] 事件： `productViewed`
* **類型** with [!UICONTROL 傳送事件] 動作： `commerce.productViews`

購物車開啟規則：

* **規則名稱**: _購物車已開啟_
* **要註冊的事件/密鑰** with [!UICONTROL 資料推送] 事件： `cartOpened`
* **類型** with [!UICONTROL 傳送事件] 動作： `commerce.productListOpens`

新增至購物車規則的產品：

* **規則名稱**: _新增至購物車的產品_
* **要註冊的事件/密鑰** with [!UICONTROL 資料推送] 事件： `productAddedToCart`
* **類型** with [!UICONTROL 傳送事件] 動作： `commerce.productListAdds`

接下來，我們將處理 [!UICONTROL 下載應用程式] 連結。
