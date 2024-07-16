---
title: 啟用跨網域支援 | 將Target從at.js 2.x移轉至Web SDK
description: 瞭解如何使用Experience PlatformWeb SDK為跨網域和行動應用程式設定Adobe Target以供網頁瀏覽器案例使用。
exl-id: 6ec24ddc-8f6d-4331-a3ae-bd0f3a7d6e78
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# 啟用跨網域訪客設定檔

Platform Web SDK支援訪客ID共用功能，讓客戶能在您的網域中更準確地提供個人化體驗。 此功能可讓您跨網域提供一致的個人化，並增強訪客活動報告的準確性，而不需依賴第三方Cookie。

## 先決條件

若要使用跨網域ID共用，您必須使用Platform Web SDK 2.11.0版或更新版本。 此功能也與VisitorAPI.js版本1.7.0或更新版本相容。

跨網域識別碼共用的運作方式是將特殊的`adobe_mc`查詢字串引數附加至目的地網域的URL。 此引數用於指定訪客ID，而非產生新ID或使用現有ID。

目的地網域必須使用這些資料庫中的任一資料庫進行跨網域識別碼共用，才能處理`adobe_mc`引數並正確共用訪客ID。

## 方法比較

在實作之前，請先判斷您現有的實作是否使用`visitor.appendVisitorIDsTo()`函式。 使用此函式的任何自訂程式碼都應更新為使用新的`appendIdentityToUrl` Web SDK命令。

| VisitorAPI.js | Platform Web SDK |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## 使用`appendIdentityToURL`命令

針對跨網域ID共用，Web SDK 2.11.0版新增對`appendIdentityToUrl`命令的支援。 使用此命令時，會產生`adobe_mc`查詢字串引數。

命令接受具有一個屬性`url`的物件，並傳回具有屬性URL的物件。

此命令不會等待任何同意更新。 如果尚未提供同意，則會傳回未變更的URL。

如果未提供ECID，則會呼叫`/acquire`端點來產生ECID。

以下是如何實作跨網域ID共用的範例。

此程式碼會為頁面上的所有點按新增一個事件接聽程式。 如果點按位於相符網域的連結上(在此例中為adobe.com或behance.com)，系統會將身分新增至URL並將使用者重新導向至該處。

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
>使用標籤功能（前身為Launch）實作Web SDK時，無需自訂程式碼即可完成跨網域ID共用。 如需詳細資訊，請參閱[專屬檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension)。

>[!NOTE]
>
>Platform Web SDK也支援原生行動應用程式使用案例的行動至網頁ID共用。 如需詳細資訊，請參閱關於[行動裝置對網頁和跨網域ID共用](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html)的專屬檔案。

接下來，瞭解如何[更新對象和設定檔指令碼](update-audiences.md)，以確保相容於Platform Web SDK。

>[!NOTE]
>
>我們致力協助您成功將Target從at.js移轉至Web SDK。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
