---
title: 傳送引數 — 從Adobe Target移轉至Adobe Journey Optimizer — 決策行動擴充功能
description: 瞭解如何使用Experience PlatformWeb SDK將mbox、設定檔和實體引數傳送至Adobe Target。
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 使用Adobe Journey Optimizer - Decisioning Mobile擴充功能傳送引數至Target

由於網站架構、業務需求及使用的功能，Target實施在各網站間會有所不同。 大部分的Target實作包括傳遞內容資訊、受眾和內容推薦的各種引數。

讓我們使用簡單的產品詳細資訊頁面和訂單確認頁面，示範將引數傳遞至Target時擴充功能之間的差異。


| at.js引數範例 | Platform Web SDK選項 | 附註 |
| --- | --- | --- |
| `at_property` | 不適用 | 屬性Token是在[資料流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target)中設定，無法在`sendEvent`呼叫中設定。 |
| `pageName` | `xdm.web.webPageDetails.name` | 所有Target mbox引數都必須作為`xdm`物件的一部分傳遞，並符合使用XDM ExperienceEvent類別的結構描述。 Mbox引數無法當作`data`物件的一部分傳遞。 |
| `profile.gender` | `data.__adobe.target.profile.gender` | 所有Target設定檔引數都必須作為`data`物件的一部分傳遞，且前置詞為`profile.`才能正確對應。 |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | 用於目標類別相關性功能的保留引數，必須作為`data`物件的一部分傳遞。 |
| `entity.id` | `data.__adobe.target.entity.id` <br>或<br> `xdm.productListItems[0].SKU` | 實體ID可用於Target Recommendations行為計數器。 這些實體ID可以作為`data`物件的一部分傳遞，或者如果您的實作使用該欄位群組，則會自動從`xdm.productListItems`陣列中的第一個專案進行對應。 |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | 實體類別ID可作為`data`物件的一部分傳遞。 |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | 自訂實體引數可用來更新Recommendations產品目錄。 這些自訂引數必須作為`data`物件的一部分傳遞。 |
| `cartIds` | `data.__adobe.target.cartIds` | 用於Target的購物車型建議演演算法。 |
| `excludedIds` | `data.__adobe.target.excludedIds` | 用來防止特定實體ID在建議設計中傳回。 |
| `mbox3rdPartyId` | 在`xdm.identityMap`物件中設定 | 用於跨裝置和客戶屬性同步Target設定檔。 必須在資料流](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html)的[Target設定中指定用於客戶ID的名稱空間。 |
| `orderId` | `xdm.commerce.order.purchaseID` | 用於識別Target轉換追蹤的唯一訂單。 |
| `orderTotal` | `xdm.commerce.order.priceTotal` | 用於追蹤Target轉換和最佳化目標的訂單總計。 |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>或<br> `xdm.productListItems[0-n].SKU` | 用於Target轉換追蹤和建議演演算法。 如需詳細資訊，請參閱下方的[實體引數](#entity-parameters)區段。 |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | 用於[自訂評分](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html)活動目標。 |

{style="table-layout:auto"}

## 自訂引數

自訂mbox引數必須以XDM或資料物件搭配`sendEvent`命令來傳遞。 請務必確保XDM結構描述包含Target實作所需的所有欄位。


## 輪廓參數

必須傳遞目標設定檔引數……

## 實體引數

實體引數可用來傳遞行為資料和Target Recommendations的補充目錄資訊。 at.js支援的所有[實體引數](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html)也受Platform Web SDK支援。 與設定檔引數類似，所有實體引數都應在Platform Web SDK `sendEvent`命令承載中的`data.__adobe.target`物件下傳遞。

特定專案的實體引數必須以`entity.`為前置詞，才能正確擷取資料。 建議演演算法的保留`cartIds`和`excludedIds`引數不應加上前置詞，而且每個引數的值都必須包含以逗號分隔的實體ID清單。



## 購買引數

成功訂單後，購買引數會在訂單確認頁面上傳遞，並用於Target轉換和最佳化目標。 透過使用決策擴充功能的Platform Mobile SDK實作，這些引數和會自動從作為`commerce`欄位群組的一部分傳遞的XDM資料進行對應。


當`commerce`欄位群組將`purchases.value`設定為`1`時，購買資訊會傳遞至Target。 訂單識別碼與訂單總計會自動從`order`物件對應。 如果`productListItems`陣列存在，則`SKU`值會用於`productPurchasedId`。


## 客戶ID (mbox3rdPartyId)

Target允許使用單一客戶ID跨裝置和系統同步設定檔。



接下來，瞭解如何使用Platform Web SDK [追蹤Target轉換事件](track-events.md)。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
