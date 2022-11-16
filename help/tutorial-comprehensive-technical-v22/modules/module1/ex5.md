---
title: Foundation — 設定Adobe Experience Platform資料收集和Web SDK擴充功能 — 實作Adobe Analytics和Adobe Audience Manager
description: Foundation — 設定Adobe Experience Platform資料收集和Web SDK擴充功能 — 實作Adobe Analytics和Adobe Audience Manager
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: e3ef6534-9af9-4b8c-86d0-46f413f4ff6d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 11%

---

# 1.5 — 實作Adobe Analytics和Adobe Audience Manager

## 內容

您現在知道XDM資料正流入平台。 您將進一步了解XDM的功能 [模組2](./../module2/data-ingestion.md)，以及如何建立自己的結構以追蹤自訂變數。 目前，您將審視設定資料流，將資料轉送至Analytics和Audience Manager時會發生什麼情況。

## 1.5.1 Analytics中的對應變數

Adobe Experience Platform [!DNL Web SDK] 自動對應特定值，讓Web SDK能盡快實作Analytics。 會列出自動對應的變數 [此處](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html#data-collection).

針對未自動對應至的XDM資料 [!DNL Adobe Analytics]，您可以使用 [內容資料](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=zh-Hant) 與 [綱要](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hant). 然後可將其對應至 [!DNL Analytics] 使用 [處理規則](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=zh-Hant) 填入 [!DNL Analytics] 變數。 「內容資料」和「處理規則」是過去曾與Analytics搭配使用的概念，但現在只要是新概念，不必擔心詳細資訊。

您也可以使用一組預設的動作和產品清單，透過AEP傳送或擷取資料 [!DNL Web SDK]. 若要這麼做，請參閱[產品](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en#data-collection)。

### 內容資料

供使用 [!DNL Analytics], XDM資料會使用點標籤法扁平化，並成為可用的 `contextData`. 下列值配對清單顯示 `context data` 的範例：

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

邊緣網路收集的所有資料都可透過[處理規則](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)來存取。在 [!DNL Analytics]，您可以使用處理規則將內容資料併入 [!DNL Analytics] 變數。

## 1.5.2Audience ManagerExperience Platform邊緣網路

伺服器端轉送不是Audience Manager的新概念，其程式與之前的程式相同。 您也可以同步身分。

## 1.5.3檢閱您的Datastream以傳送資料至Adobe Analytics

如果您想要將Web SDK所收集的資料傳送至Adobe Analytics和Adobe Audience Manager，請遵循下列步驟。

前往 [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) 然後 **資料流**.

在畫面的右上角，選取沙箱名稱，名稱應為 `--aepSandboxId--`. 開啟您指定的資料流，此資料流的名稱為 `--demoProfileLdap-- - Demo System Datastream`.

![按一下左側導覽中的「邊緣設定」圖示](./images/edgeconfig1b.png)

你會看到這個。 若要啟用Adobe Analytics，請按一下 **+添加服務**.

![AEP Debugger](./images/aa2.png)

你會看到這個。 選擇服務 **Adobe Analytics**，之後您需要在Adobe Analytics中新增報表套裝，才能將資料傳送至。 在本教學課程中，此課程超出範圍。 按一下 **取消**.

![AEP Debugger](./images/aa3.png)

## 1.5.4檢閱您的Datastream以傳送資料至Adobe Audience Manager

你會看到這個。 若要啟用Adobe Audience Manager，請按一下 **+添加服務**.

![AEP Debugger](./images/aa2.png)

你會看到這個。 選擇服務 **Adobe Audience Manager** 之後，您可以決定啟用或停用Adobe Audience Manager cookie目的地和/或URL目的地。 在本教學課程中，此設定超出範圍。 按一下 **取消**.

![AEP Debugger](./images/aam1.png)

下一步： [1.6實作Adobe Target](./ex6.md)

[返回模組1](./data-ingestion-launch-web-sdk.md)

[返回所有模組](./../../overview.md)
