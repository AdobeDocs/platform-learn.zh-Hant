---
title: 啟用跨網域支援 |將Target從at.js 2.x移轉至Web SDK
description: 了解如何使用Adobe Target Web SDK將跨網域和行動應用程式設定為網頁瀏覽器案例。
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 啟用跨網域訪客設定檔

Platform Web SDK支援訪客ID共用功能，讓客戶能在您的網域間更精確地提供個人化體驗。 此功能可讓您跨網域提供一致的個人化內容，並增強訪客活動報表的準確性，而不需依賴第三方Cookie。

## 先決條件

若要使用跨網域ID共用，您必須使用Platform Web SDK 2.11.0版或更新版本。 此功能也與VisitorAPI.js 1.7.0版或更新版本相容。

跨網域ID共用的作用是附加特殊的 `adobe_mc` 查詢字串參數至目的地網域的URL。 此參數用於指定訪客ID，而非產生新ID或使用現有ID。

目的地網域必須使用其中一個程式庫進行跨網域ID共用，才能處理 `adobe_mc` 參數並正確共用訪客ID。

## 方法比較

實作前，請先判斷您現有的實作是否使用 `visitor.appendVisitorIDsTo()` 函式。 應更新使用此函式的任何自訂程式碼，以使用新 `appendIdentityToUrl` Web SDK命令。

| VisitorAPI.js | 平台Web SDK |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## 使用 `appendIdentityToURL` 命令

為了跨網域ID共用，Web SDK 2.11.0版新增了 `appendIdentityToUrl` 命令。 使用時，此命令將生成 `adobe_mc` 查詢字串參數。

命令接受一個屬性的對象， `url`，並傳回具有屬性url的物件。

此命令不等待任何同意更新。 如果未提供同意，則會傳回URL不變。

若未提供ECID，則 `/acquire` 呼叫端點來產生ECID。

以下是如何實作跨網域ID共用的範例。

此程式碼會為頁面上的所有點按新增事件接聽程式。 如果點按是指向相符網域的連結，在此例中是adobe.com或behance.com，會將身分新增至URL，並將使用者重新導向至該處。

```Javascript
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

>[!TIP]
>
>使用標籤功能（舊稱Launch）來實作Web SDK時，無須自訂程式碼，即可完成跨網域ID共用。 請參閱 [專屬檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension) 以取得更多詳細資訊。

>[!NOTE]
>
>Platform Web SDK也支援針對原生行動應用程式使用案例進行行動對網頁ID共用。 如需詳細資訊，請參閱 [行動對網頁和跨網域ID共用](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

接下來，學習如何 [更新對象和設定檔指令碼](update-audiences.md) 確保與Platform Web SDK相容。

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).