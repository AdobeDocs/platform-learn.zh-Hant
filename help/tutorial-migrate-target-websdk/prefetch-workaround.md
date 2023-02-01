---
title: 預先擷取的因應措施 |將Target從at.js 2.x移轉至Web SDK
description: 了解如何使用預先擷取傳遞參數的因應措施
source-git-commit: d061d2492d6d5e8e7a8a6e03ce63b9b6cd3793d8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 預先擷取的因應措施

2022年10月1日之前，未使用Experience PlatformWeb SDK生產的所有Target客戶，都會使用「預先擷取」模式，從Experience Platform邊緣網路向Target提出要求。 預先擷取可讓瀏覽器預先載入及快取Target選件，以便在訪客達到頁面的正確狀態時即可套用這些選件。 這在單頁應用程式(SPA)中是有利的，因為可以盡快呈現所需的使用者體驗，而不需要其他網路要求。 不過，這對SPA和非SPA實作都有重要影響。

現在，當網路請求中傳送選件內容時，將訪客計入活動時，將不計算活動中的訪客 `propositionDisplay` sendEvent要求由Web SDK提出。 當renderDecisions設為true，以及體驗已成功在頁面上轉譯時，可視化體驗撰寫器(VEC)活動會自動提出這些請求。 若使用自訂範圍，當renderDecisions設為false時，主張顯示請求需由實施者刻意啟動。 此外， _除了立即活動資格以外，用於其他目的的所有參數都必須透過 `propositionDisplay`  事件_.

## 為什麼需要因應措施？

在許多Target實作中，有時會提出重要的網路要求，而不預期會傳送活動。 例如，可向下列對象提出請求：

* 記錄訂單轉換
* 設定設定檔參數
* 觸發設定檔指令碼
* 傳送實體參數以填入Recommendations目錄

可惜，在預先擷取模式中，這些動作不會如預期般運作。 在預先擷取模式中，除非此資料屬於 `propositionDisplay`.

## 因應措施為何？

解決方法由三部分組成：

1. 將自訂範圍定義為 `sendEvent`
1. 在表單式活動中使用自訂範圍（活動可提供預設內容）
1. 使用回應處理常式來建立其他 `sendEvent` 對於主張顯示並包含您擷取順序、設定設定檔參數、觸發設定檔指令碼、傳送實體參數等所需的參數。

例如，以下是如何使用因應措施來傳送設定檔參數的範例：


```JavaScript
var data = {
    "__adobe": {
        "target": {
            "profile.gender": "male"
        }
    }
};
// Send the initial event with the data object and custom decision scope
alloy("sendEvent", {
    "renderDecisions": true,
    data,
    decisionScopes: ['profile-param-example']
}).then(function(result) {
    var propositions = result.propositions;
    var ctaProposition;
    if (propositions) {
        // Find the discount proposition, if it exists.
        for (var i = 0; i < propositions.length; i++) {
            var proposition = propositions[i];
            if (proposition.scope === "profile-param-example") {
                ctaProposition = proposition;
                break;
            }
        }
    }
    if (ctaProposition) {
        // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered, and includes the data object again
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: [{
                            id: ctaProposition.id,
                            scope: ctaProposition.scope,
                            scopeDetails: ctaProposition.scopeDetails
                        }]
                    }
                }
            },
            data
        });
    }
});
```

當設定檔設為postimationDisplay的一部分時，會儲存至訪客的設定檔，並可在後續請求中使用。 報表訂單轉換詳細資訊和實體參數也可使用相同的方法。

在標籤中，使用「傳送事件完成」事件類型來觸發包含其他sendEvent的事件。

## 如何知道我的實作是否使用預先擷取模式？

您必須開啟客戶服務票證，才能了解您的帳戶是否使用預先擷取模式。


>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).