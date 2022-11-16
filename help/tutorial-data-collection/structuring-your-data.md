---
title: 建立資料結構
description: 建立資料結構
exl-id: 8d176389-25a4-4718-afff-efd2f87204ed
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# 建立資料結構

企業有自己的語言來交流自己的領域。 汽車經銷商負責製造、型號和汽缸。 航空公司負責航班號、服務類別和座位分配。 這些術語中有些是特定公司特有的，有些是在垂直行業之間共用的，有些是幾乎所有公司共用的。 對於在垂直或甚至更廣泛的行業之間共用的術語，當您以通用方式命名和建構這些術語時，可以開始使用您的資料執行強大的操作。

例如，許多企業都在處理訂單。 如果這些企業集體決定以類似方式來構建一種秩序，那會怎樣？ 例如，如果資料模型包含物件，且 `priceTotal` 代表訂單總價的財產？ 如果該對象也具有已命名的屬性 `currencyCode` 和 `purchaseOrderNumber`? 或許順序物件包含的屬性名為 `payments` 就是一系列的支付對象。 每個對象都表示訂單的付款。 例如，可能是客戶用禮品卡支付部分訂單，而用信用卡支付其餘訂單。 您可以開始建立類似以下的模型：

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

如果所有處理訂單的企業都決定以一致的方式建立訂單資料模型，以獲取業內常見的條款，那麼神奇的事情就可能開始發生。 您可以更流暢地在組織內外交換資訊，而不是持續解譯和轉譯資料（Prop和evar，還有誰？）。 機器學習可更輕鬆了解您的資料 _裝置_ 並提供可操作的分析。 用於呈現相關資料的用戶介面可能更加直觀。 您的資料可以與遵循相同模型的合作夥伴和供應商無縫整合。

## XDM

這是Adobe的目標 [體驗資料模型](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM針對業界常見的資料提供規範的模型，同時也允許您根據特定需求擴充模型。 Adobe Experience Platform是以XDM為基礎而建，因此，傳送至Experience Platform的資料必須位於XDM。 在將資料傳送至Experience Platform之前，請不要考慮將目前的資料模型轉換為XDM的位置和方式，而是考慮在整個組織內更普遍地採用XDM，這樣就不需要進行翻譯。

[下一個： ](configure-the-server/create-a-schema.md)

>[!NOTE]
>
>感謝您花時間學習資料收集。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
