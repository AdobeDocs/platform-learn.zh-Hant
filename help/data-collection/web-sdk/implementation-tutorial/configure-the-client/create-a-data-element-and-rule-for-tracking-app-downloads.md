---
title: 建立資料元素和規則以追蹤應用程式下載
description: 建立資料元素和規則以追蹤應用程式下載
feature: Web SDK
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: cb322540-e8ef-4226-b537-a67c7ca273f5
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# 建立資料元素和規則以追蹤應用程式下載

提醒一下，當使用者按一下 [!UICONTROL 下載應用程式] 連結時，您會推送至資料層，如下所示：

```js
window.adobeDataLayer.push({
  "event": "downloadAppClicked",
  "eventInfo": {
    "web": {
      "webInteraction": {
        "URL": "https://example.com/download",
        "name": "App Download",
        "type": "download"
      }
    }
  }
});
```

您已使用 `eventInfo` 索引鍵，它會告訴資料層將此資料與事件通訊，但 _not_ 將資料保留在資料層內。 若為連結點按，將點按連結的相關資訊新增至資料層並無用處，因為此資訊不適用於稍後頁面上可能發生的其他事件。

針對此實作，您會傳送體驗事件至Adobe Experience Platform，其中包含下列專案的合併結果：(1)資料層的計算狀態，以及(2)下列專案的內容 `eventInfo`.

若要這麼做，您首先需要建立可合併這兩個資訊區塊的資料元素。

## 建立資料元素

若要建立適當的資料元素，請按一下 [!UICONTROL 資料元素] 在左側功能表中。 接下來，按一下 [!UICONTROL 新增資料元素] 連結。

資料元素名稱請輸入 `computedStateAndEventInfo`. 對於 [!UICONTROL 副檔名] 欄位，選取 [!UICONTROL 核心] 如果尚未選取，則為。 對於 [!UICONTROL 資料元素型別] 欄位，選取 [!UICONTROL 合併的物件]. 此資料元素可讓您深度合併多個物件。 合併的結果會由資料元素傳回。

對於要包含在合併中的第一個物件，請輸入 `%event.fullState%`. 當用於由觸發的規則內時 [!UICONTROL 資料已推送] 規則事件，這會參考Adobe使用者端資料層觸發規則時的計算狀態。

按一下 [!UICONTROL 新增其他].

對於第二個物件，請輸入 `%event.eventInfo%`. 當用於由觸發的規則內時 [!UICONTROL 資料已推送] 規則事件，這會參考 `eventInfo` 推送至Adobe使用者端資料層的部分。

![computedStateAndEventInfo資料元素](../../../assets/implementation-strategy/computed-state-and-event-info-data-element.png)

資料元素已完成。 按一下「 」以儲存資料元素 [!UICONTROL 儲存] 按鈕。

## 建立規則

若要建立追蹤點選的規則，請 [!UICONTROL 下載應用程式] 連結，按一下 [!UICONTROL 規則] 在左側功能表中。

按一下[!UICONTROL 新增規則].

規則名稱請輸入 _已點按下載應用程式連結_.

## 新增事件

按一下 [!UICONTROL 新增] 按鈕於 [!UICONTROL 事件]. 您現在顯示在事件檢視上。 對於 [!UICONTROL 副檔名] 欄位，選取 [!UICONTROL Adobe使用者端資料層]. 對於 [!UICONTROL 事件型別] 欄位，選取 [!UICONTROL 資料已推送].

因為您只希望此規則在 `downloadAppClicked` 事件會推送至資料層，請選取 [!UICONTROL 特定事件] 下面的無線電 [!UICONTROL 聆聽] 和型別 _downloadAppClick_ 到 [!UICONTROL 要註冊的事件/金鑰]  顯示的文字欄位。

![下載應用程式點選事件](../../../assets/implementation-strategy/download-app-clicked-event.png)

按一下[!UICONTROL 保留變更].

## 新增動作

現在您已返回規則檢視，請按一下 [!UICONTROL 新增] 按鈕於 [!UICONTROL 動作]. 您現在應該位於動作檢視上。 對於 [!UICONTROL 副檔名] 欄位，選取 [!UICONTROL Adobe Experience Platform Web SDK]. 對於 [!UICONTROL 動作型別] 欄位，選取 [!UICONTROL 傳送事件].

在熒幕右側，找到 [!UICONTROL 型別] 欄位並選取 `web.webinteraction.linkClicks`.

對於 [!UICONTROL XDM資料] 欄位，按一下資料元素選擇器按鈕並選取 [!UICONTROL computedStateAndEventInfo]. 這是您剛才建立的資料元素。

對於此規則（與您建立的其他規則不同），您將檢查 [!UICONTROL 檔案將解除安裝] 核取方塊。 這基本上會告訴SDK，當使用者按一下連結時，他們將會離開頁面。 這點很重要，因為它可讓SDK提出請求的方式，即使使用者導覽離開頁面，請求仍會在背景執行並到達伺服器。 如果未核取此核取方塊，將不會以此方式提出請求，因此當目前檔案解除安裝時，可能會取消請求。

您可能會問自己：「聽起來不錯。 為何此選項並非一律啟用？」

嗯，有點複雜，但使用此功能時，SDK會使用名為的瀏覽器方法 [`sendBeacon`](https://developer.mozilla.org/zh-TW/docs/Web/API/Navigator/sendBeacon) 以傳送要求。 使用傳送請求時 `sendBeacon`，瀏覽器不允許SDK （或其他任何專案）存取伺服器傳回的任何資料。 如果SDK要針對每個請求使用此功能，SDK將無法從伺服器接收任何資料。 因此，請務必檢查 [!UICONTROL 檔案將解除安裝] 核取方塊只會在目前檔案將解除安裝時勾選，在此情況下，仍可捨棄回應資料。

![檔案將解除安裝核取方塊](../../../assets/implementation-strategy/document-will-unload.png)

按一下「 」以儲存動作 [!UICONTROL 保留變更] 按鈕。

## 儲存規則

您的規則現在應該已完成。

![下載應用程式連結點選規則](../../../assets/implementation-strategy/download-app-link-clicked-rule.png)

按一下以儲存規則 [!UICONTROL 儲存].
