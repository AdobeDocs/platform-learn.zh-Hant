---
title: 建構您的資料
description: 建構您的資料
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: d300429a-5a66-4b61-97cb-b934fc8e8291
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 建構您的資料

企業有自己的語言來溝通其網域。 汽車經銷商會處理廠牌、型號和汽缸。 航空公司負責航班編號、服務類別和座位分配。 其中有些辭彙是特定公司所特有的，有些辭彙是在垂直產業中共用，有些辭彙則是由幾乎所有企業共用。 對於在垂直產業或更廣的產業之間共用的術語，當您以常見的方式命名和構建這些術語時，可以開始使用您的資料做一些強大的事情。

例如，許多企業都會處理訂單。 如果這些企業共同決定以類似的方式為訂單建模，該怎麼辦？ 例如，如果資料模型包含物件且具有 `priceTotal` 代表訂單總價的屬性。 如果該物件也有名為的屬性，該怎麼辦 `currencyCode` 和 `purchaseOrderNumber`. order物件可能包含名為的屬性 `payments` 即會是一系列付款物件。 每個物件將代表訂單的付款。 例如，客戶可能使用禮品卡支付部分訂單，而使用信用卡支付剩餘部分。 您可以開始建構類似以下的模型：

```json
{
  "order": {
    "priceTotal": 89.50,
    "currencyCode": "EUR",
    "purchaseOrderNumber": "JWN20192388410012",
    "payments": [
      {
        "paymentType": "gift_card",
        "paymentAmount": 50
      },
      {
        "paymentType": "credit_card",
        "paymentAmount": 39.50
      }
    ]
  }
}
```

如果處理訂單的所有企業都決定以一致的方式將訂單資料模型化為業界通用的辭彙，可能會開始發生神奇的事情。 您可以在組織內外更流暢地交換資訊，而不需持續解讀和翻譯資料（prop和evar，還有誰？）。 機器學習可更輕鬆地瞭解您的資料 _方法_ 並提供可操作的深入分析。 呈現相關資料的使用者介面可能會變得更直覺。 您的資料可與遵循相同模型的合作夥伴和廠商緊密整合。

## XDM

這是Adobe的目標 [體驗資料模型](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM為業界常見的資料提供規範性模型，同時也允許您擴充模型以滿足特定需求。 Adobe Experience Platform是圍繞XDM建立的，因此，傳送到Experience Platform的資料將需採用XDM格式。 與其考慮在傳送資料給Experience Platform之前將您目前的資料模型轉換為何處以及如何轉換，不如考慮更普遍地在組織內採用XDM，以便幾乎不需要翻譯。
