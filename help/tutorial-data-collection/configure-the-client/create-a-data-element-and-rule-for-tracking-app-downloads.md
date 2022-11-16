---
title: 建立資料元素和規則以追蹤應用程式下載
description: 建立資料元素和規則以追蹤應用程式下載
feature: Web SDK
exl-id: 8012ba48-38ac-4fb5-9876-8f57d1c5da5d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 4%

---

# 建立資料元素和規則以追蹤應用程式下載

提醒您，當使用者點按 [!UICONTROL 下載應用程式] 連結時，您推送至資料層的方式如下：

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

您使用 `eventInfo` 索引鍵，可告知資料層將此資料與事件一併傳送，但傳送至 _not_ 將資料保留在資料層內。 對於連結點按，將點按連結的相關資訊新增至資料層並沒有用，因為這不適用於頁面稍後可能發生的其他事件。

針對此實作，您會傳送體驗事件至Adobe Experience Platform，其中包含(1)資料層的計算狀態和(2) `eventInfo`.

若要這麼做，您需要建立資料元素，以合併這兩個資訊區塊。

## 建立資料元素

若要建立適當的資料元素：

1. 按一下 [!UICONTROL 資料元素] 的上界。
1. 下一步，按一下 [!UICONTROL 建立新資料元素] 連結。
1. 輸入資料元素名稱， `computedStateAndEventInfo`.
1. 若 [!UICONTROL 擴充功能] 欄位，選擇 [!UICONTROL 核心] 如果尚未選取。
1. 若 [!UICONTROL 資料元素類型] 欄位，選擇 **[!UICONTROL 合併的對象]**. 此資料元素可讓您合併多個物件。 資料元素會傳回合併的結果。
1. 新增您要納入合併的第一個物件。 輸入 `%event.fullState%` 在 [!UICONTROL 物件（必要）] 欄位。 在由 [!UICONTROL 資料推送] 規則事件，則會參照觸發規則時Adobe用戶端資料層的計算狀態。
1. 按一下  **[!UICONTROL 新增其他]** 命令。
1. 新增第二個物件。 輸入 `%event.eventInfo%` 在 [!UICONTROL 物件（必要）] 欄位。 在由 [!UICONTROL 資料推送] 規則事件，這會參考 `eventInfo` 推送至Adobe用戶端資料層的部分。
1. 按一下 [!UICONTROL 儲存] 按鈕。
   ![computedStateAndEventInfo資料元素](../assets/computed-state-and-event-info-data-element.png)

資料元素已完成。

## 建立規則

若要建立規則以追蹤 [!UICONTROL 下載應用程式] 連結：

1. 按一下 **[!UICONTROL 規則]** 的上界。
1. 按一下&#x200B;**[!UICONTROL 新增規則]**.
1. 輸入 **_已點按下載應用程式連結_** 在 [!UICONTROL 名稱] 欄位。

## 新增事件

1. 按一下 **[!UICONTROL 新增]** 按鈕 [!UICONTROL 事件]. 您現在會顯示在事件檢視上。
1. 若 [!UICONTROL 擴充功能] 欄位，選擇 **[!UICONTROL Adobe用戶端資料層]**.
1. 若 [!UICONTROL 事件類型] 欄位，選擇 **[!UICONTROL 資料推送]**.
1. 按一下&#x200B;**[!UICONTROL 保留變更]**.
   ![下載應用程式點擊事件](../assets/download-app-clicked-event.png)
因為您只希望此規則在 `downloadAppClicked` 事件推送至資料層，請選取 **[!UICONTROL 特定事件]** 無線電 [!UICONTROL 聽] 和類型 **_downloadAppClicked_** 進入 [!UICONTROL 要註冊的事件/密鑰]  顯示的文字欄位。

## 新增動作

現在您又回到規則檢視：

1. 按一下&#x200B;**[!UICONTROL 「動作」]**&#x200B;中的[!UICONTROL 「新增」]按鈕。
1. 您現在應該位於動作檢視上。 若 [!UICONTROL 擴充功能] 欄位，選擇 **[!UICONTROL Adobe Experience Platform Web SDK]**. 若 [!UICONTROL 動作類型] 欄位，選擇 **[!UICONTROL 傳送事件]**.
1. 在 [!UICONTROL 類型] 欄位，選擇 `web.webinteraction.linkClicks`.
1. 若 [!UICONTROL XDM資料] 欄位中，按一下右側的資料元素選取器按鈕並選取 **[!UICONTROL computedStateAndEventInfo]**. 這是您最近建立的資料元素。
1. 針對此規則（不同於您已建立的其他規則），請檢查 **[!UICONTROL 文檔將卸載]** 核取方塊。
   ![文檔將卸載複選框](../assets/document-will-unload.png)
1. 按一下 **[!UICONTROL 保留變更]** 按鈕。

>[!TIP]
>
>此 [!UICONTROL 文檔將卸載功能] 會告知SDK使用者在點按連結時離開頁面進行導覽。 這點很重要，因為即使使用者離開頁面進行導覽，SDK仍可提出請求，因為請求會持續在背景執行並連線至伺服器。 如果取消勾選此核取方塊，就不會以此方式提出要求，因此，當目前檔案卸載時，可能會取消要求。
>
>你可能會問自己，「聽起來不錯。 那麼，為何不一律啟用此選項？」
>
>嗯，這有點複雜，但使用此功能時，SDK會使用瀏覽器方法，稱為 [`sendBeacon`](https://developer.mozilla.org/zh-TW/docs/Web/API/Navigator/sendBeacon) 來傳送要求。 使用 `sendBeacon`，瀏覽器不會允許SDK（或其他任何項目）存取從伺服器傳回的任何資料。 如果SDK要對每個請求使用此功能，SDK將永遠無法從伺服器接收任何資料。 因此，請務必檢查 [!UICONTROL 文檔將卸載] 核取方塊，僅在目前檔案將卸載時進行，在此情況下，仍可捨棄回應資料。

## 儲存規則

您的規則現在應已完成。

1. 按一下 **[!UICONTROL 儲存]** 在右上角。
   ![下載應用程式連結點擊規則](../assets/download-app-link-clicked-rule.png)

[下一個： ](publish-the-library.md)

>[!NOTE]
>
>感謝您花時間學習資料收集。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)