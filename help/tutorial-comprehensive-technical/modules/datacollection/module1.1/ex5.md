---
title: 基礎 — Adobe Experience Platform Data Collection和Web SDK擴充功能的設定 — 實作Adobe Analytics和Adobe Audience Manager
description: 基礎 — Adobe Experience Platform Data Collection和Web SDK擴充功能的設定 — 實作Adobe Analytics和Adobe Audience Manager
kt: 5342
doc-type: tutorial
exl-id: a9022269-6db2-46c6-a82b-ec8d5b881a55
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# 1.1.5實作Adobe Analytics和Adobe Audience Manager

## 內容

您現在知道XDM資料正在流入平台。 您將深入瞭解[模組1.2](./../module1.2/data-ingestion.md)中的XDM內容，以及如何建置您自己的結構描述以追蹤自訂變數。 現在，您將瞭解當您設定資料串流將資料轉送至Analytics和Audience Manager時發生的情況。

## 在Analytics中對應變數

Adobe Experience Platform [!DNL Web SDK]會自動對應某些值，儘快透過Web SDK進行新的Analytics實作。 [這裡](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html#data-collection)列出自動對應的變數。

對於未自動對應至Adobe Analytics的XDM資料，您可以使用[內容資料](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html)來比對您的[結構描述](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hant)。 然後可以使用[處理規則](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)將其對應至Analytics以填入Analytics變數。 內容資料與處理規則將會是過去與Analytics搭配使用時熟悉的概念，但如果是新概念，目前無需擔心詳細資訊。

您也可以使用一組預設的動作和產品清單，以透過AEP Web SDK傳送或擷取資料。 若要這麼做，請參閱[產品](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en#data-collection)。

### 上下文資料

為了供Analytics使用，XDM資料會使用點標籤法扁平化，並成為可用的`contextData`。 下列值配對清單顯示`context data`的範例：

```javascript
{
    "bh": "900",
    "bw": "1680",
    "c": "24",
    "c.a.d.key.[0]": "value1",
    "c.a.d.key.[1]": "value2",
    "c.a.d.object.key1": "value1",
    "c.a.d.object.key2.[0]": "value2",
    "c.a.x.environment.browserdetails.javascriptenabled": "true",
    "c.a.x.environment.type": "browser",
    "cust_hit_time_gmt": "1579781427",
    "g": "http://example.com/home",
    "gn": "home",
    "j": "1.8.5",
    "k": "Y",
    "s": "1680x1050",
    "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:01,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
    "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
    "v": "Y"
}
```

### 處理規則

邊緣網路收集的所有資料都可以透過[處理規則](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)來存取。 在Analytics中，您可以使用處理規則將內容資料併入Analytics變數中。

## Experience PlatformEdge Network上的Audience Manager

伺服器端轉送不是Audience Manager的新概念，與之前的程式相同。 您也可以同步身分。

## 檢閱您的資料流以傳送資料至Adobe Analytics

如果您想要將Web SDK收集的資料傳送至Adobe Analytics和Adobe Audience Manager，請按照下列步驟操作。

移至[https://experience.adobe.com/launch/](https://experience.adobe.com/launch/)並移至&#x200B;**資料串流**。

在熒幕的右上角，選取您的沙箱名稱，應為`--aepSandboxName--`。 開啟名為`--aepUserLdap-- - Demo System Datastream`的特定資料流。

![按一下左側導覽中的Edge設定圖示](./images/edgeconfig1b.png)

您將會看到此訊息。 若要啟用Adobe Analytics，請按一下[新增服務]。****

![AEP偵錯工具](./images/aa2.png)

您將會看到此訊息。 選取服務&#x200B;**Adobe Analytics**，之後您需要在Adobe Analytics中新增報表套裝，才能將資料傳送到。 在本教學課程中，這不在範圍內。 按一下&#x200B;**取消**。

![AEP偵錯工具](./images/aa3.png)

## 檢閱您的資料流以傳送資料至Adobe Audience Manager

您將會看到此訊息。 若要啟用Adobe Audience Manager，請按一下[新增服務]。****

![AEP偵錯工具](./images/aa2.png)

您將會看到此訊息。 選取服務&#x200B;**Adobe Audience Manager**，之後您可以決定啟用或停用Adobe Audience Manager Cookie目的地和/或URL目的地。 在本教學課程中，此設定不在範圍內。 按一下&#x200B;**取消**。

![AEP偵錯工具](./images/aam1.png)

下一步： [1.1.6實作Adobe Target](./ex6.md)

[返回模組1.1](./data-ingestion-launch-web-sdk.md)

[返回所有模組](./../../../overview.md)
