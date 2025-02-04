---
title: Real-time CDP — 目的地SDK
description: Real-time CDP — 目的地SDK
kt: 5342
doc-type: tutorial
exl-id: 5606ca2f-85ce-41b3-80f9-3c137f66a8c0
source-git-commit: c49b41e1b033573dbebc9ced3a3f4071bf94d04e
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 4%

---

# 2.3.6目的地SDK

## 設定您的Adobe I/O專案

在本練習中，您將再次使用Adobe I/O來查詢Adobe Experience Platform的API。如果您尚未設定Adobe I/O專案，請回到模組2.1](../module2.1/ex3.md)中的[練習3，並遵循其中的指示。

>[!IMPORTANT]
>
>如果您是Adobe員工，請依照這裡的指示使用[PostBuster](./../../../postbuster.md)。

## 驗證以Adobe I/O

在本練習中，您將再次使用Postman來查詢Adobe Experience Platform的API。如果您尚未設定Postman應用程式，請回到模組2.1](../module2.1/ex3.md)中的[練習3，並遵循其中的指示。

>[!IMPORTANT]
>
>如果您是Adobe員工，請依照這裡的指示使用[PostBuster](./../../../postbuster.md)。

## 定義端點與格式

在本練習中，您將需要端點來設定，以便在對象符合資格時，資格事件可串流至該端點。 在本練習中，您將使用[https://pipedream.com/requestbin](https://pipedream.com/requestbin)的範例端點。 移至[https://pipedream.com/requestbin](https://pipedream.com/requestbin)，建立帳戶，然後建立工作區。 建立工作區後，您會看到類似以下畫面。

按一下&#x200B;**複製**&#x200B;以複製URL。 您需要在下一個練習中指定此URL。 此範例中的URL是`https://eodts05snjmjz67.m.pipedream.net`。

![資料擷取](./images/webhook1.png)

至於格式，我們將使用標準範本，以串流方式處理對象資格或取消資格以及客戶識別碼等中繼資料。 您可以自訂範本以符合特定端點的期望，但在本練習中，我們將重複使用標準範本，這將導致類似以下的裝載將串流到端點。

```json
{
  "profiles": [
    {
      "identities": [
        {
          "type": "ecid",
          "id": "64626768309422151580190219823409897678"
        }
      ],
      "AdobeExperiencePlatformSegments": {
        "add": [
          "f58c723c-f1e5-40dd-8c79-7bb4ab47f041"
        ],
        "remove": []
      }
    }
  ]
}
```

## 建立伺服器和範本設定

在Adobe Experience Platform中建立專屬目的地的第一個步驟，是使用Postman建立伺服器和範本設定。

若要這麼做，請開啟您的Postman應用程式，並移至&#x200B;**目的地編寫API**、**目的地伺服器和範本**，然後按一下以開啟要求&#x200B;**POST — 建立目的地伺服器組態**。

>[!NOTE]
>
>如果您沒有Postman集合，請回到模組2.1](../module2.1/ex3.md)中的[練習3，並依照這裡的指示設定Postman與提供的Postman集合。

您將會看到此訊息。 在&#x200B;**Headers**&#x200B;底下，您需要手動更新機碼&#x200B;**x-sandbox-name**&#x200B;的值，並將其設定為`--aepSandboxName--`。 選取值&#x200B;**{{SANDBOX_NAME}}**。

![資料擷取](./images/sdkpm1.png)

以`--aepSandboxName--`取代。

![資料擷取](./images/sdkpm2.png)

接著，移至&#x200B;**內文**。 選取預留位置&#x200B;**{{body}}**。

![資料擷取](./images/sdkpm3.png)

您現在需要用下列程式碼取代預留位置&#x200B;**{{body}}**：

```json
{
    "name": "Custom HTTP Destination",
    "destinationServerType": "URL_BASED",
    "urlBasedDestination": {
        "url": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "yourURL"
        }
    },
    "httpTemplate": {
        "httpMethod": "POST",
        "requestBody": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{\n    \"profiles\": [\n    {%- for profile in input.profiles %}\n        {\n            \"identities\": [\n            {%- for idMapEntry in profile.identityMap -%}\n            {%- set namespace = idMapEntry.key -%}\n                {%- for identity in idMapEntry.value %}\n                {\n                    \"type\": \"{{ namespace }}\",\n                    \"id\": \"{{ identity.id }}\"\n                }{%- if not loop.last -%},{%- endif -%}\n                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\n            {% endfor %}\n            ],\n            \"AdobeExperiencePlatformSegments\": {\n                \"add\": [\n                {%- for segment in profile.segmentMembership.ups | added %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ],\n                \"remove\": [\n                {#- Alternative syntax for filtering segments by status: -#}\n                {% for segment in removedSegments(profile.segmentMembership.ups) %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ]\n            }\n        }{%- if not loop.last -%},{%- endif -%}\n    {% endfor %}\n    ]\n}"
        },
        "contentType": "application/json"
    }
}
```

貼上上述程式碼後，您必須手動更新欄位&#x200B;**urlBasedDestination.url.value**，而且您必須將其設定為您在上一步中建立的webhook的URL，在此範例中為`https://eodts05snjmjz67.m.pipedream.net`。

![資料擷取](./images/sdkpm4.png)

更新欄位&#x200B;**urlBasedDestination.url.value**&#x200B;後，它應該如下所示。 按一下&#x200B;**傳送**。

![資料擷取](./images/sdkpm5.png)

>[!NOTE]
>
>別忘了，在傳送要求給Adobe I/O之前，您必須具備有效的`access_token`。 若要取得有效的`access_token`，請執行要求&#x200B;**POST — 取得集合** AdobeIO - OAuth **中的存取權杖**。

按一下&#x200B;**傳送**&#x200B;之後，將會建立您的伺服器範本，而在回應中，您會看到名為&#x200B;**instanceId**&#x200B;的欄位。 記下它，因為您會在下一個步驟中需要它。 在此範例中，**instanceId**為
`52482c90-8a1e-42fc-b729-7f0252e5cebd`。

![資料擷取](./images/sdkpm6.png)

## 建立您的目的地設定

在Postman中的&#x200B;**目的地編寫API**&#x200B;底下，移至&#x200B;**目的地組態**&#x200B;並按一下以開啟要求&#x200B;**POST — 建立目的地組態**。 您將會看到此訊息。 在&#x200B;**Headers**&#x200B;底下，您需要手動更新機碼&#x200B;**x-sandbox-name**&#x200B;的值，並將其設定為`--aepSandboxName--`。 選取值&#x200B;**{{SANDBOX_NAME}}**&#x200B;並以`--aepSandboxName--`取代。

![資料擷取](./images/sdkpm7.png)

接著，移至&#x200B;**內文**。 選取預留位置&#x200B;**{{body}}**。

![資料擷取](./images/sdkpm9.png)

您現在需要用下列程式碼取代預留位置&#x200B;**{{body}}**：

```json
{
    "name": "--aepUserLdap-- - Webhook",
    "description": "Exports segment qualifications and identities to a custom webhook via Destination SDK.",
    "status": "TEST",
    "customerAuthenticationConfigurations": [
        {
            "authType": "BEARER"
        }
    ],
    "customerDataFields": [
        {
            "name": "endpointsInstance",
            "type": "string",
            "title": "Select Endpoint",
            "description": "We could manage several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
            "isRequired": true,
            "enum": [
                "US",
                "EU",
                "APAC",
                "NZ"
            ]
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en",
        "category": "streaming",
        "connectionType": "Server-to-server",
        "frequency": "Streaming"
    },
    "identityNamespaces": {
        "ecid": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": false
        }
    },
    "segmentMappingConfig": {
        "mapExperiencePlatformSegmentName": true,
        "mapExperiencePlatformSegmentId": true,
        "mapUserInput": false
    },
    "aggregation": {
        "aggregationType": "BEST_EFFORT",
        "bestEffortAggregation": {
            "maxUsersPerRequest": "1000",
            "splitUserById": false
        }
    },
    "schemaConfig": {
        "profileRequired": false,
        "segmentRequired": true,
        "identityRequired": true
    },
    "destinationDelivery": [
        {
            "authenticationRule": "NONE",
            "destinationServerId": "yourTemplateInstanceID"
        }
    ]
}
```

![資料擷取](./images/sdkpm11.png)

貼上上述程式碼後，您必須手動更新&#x200B;**destinationDelivery欄位。 destinationServerId**，而且您必須將它設定為您在上一步中建立的目的地伺服器範本的&#x200B;**instanceId**，在此範例中為`52482c90-8a1e-42fc-b729-7f0252e5cebd`。 接著，按一下&#x200B;**傳送**。

![資料擷取](./images/sdkpm10.png)

您會看到此回應。

![資料擷取](./images/sdkpm12.png)

您的目的地現在已建立在Adobe Experience Platform中。 讓我們到那裡檢查一下。

移至[Adobe Experience Platform](https://experience.adobe.com/platform)。 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./../../../modules/datacollection/module1.2/images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--aepSandboxName--``。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。

![資料擷取](./../../../modules/datacollection/module1.2/images/sb1.png)

在左側功能表中，移至&#x200B;**目的地**，按一下&#x200B;**目錄**，然後向下捲動至類別&#x200B;**串流**。 您現在會看到目的地可供使用。

![資料擷取](./images/destsdk1.png)

## 將您的對象連結至目的地

在&#x200B;**目的地** > **目錄**&#x200B;中，按一下目的地上的&#x200B;**設定**，開始將對象新增至您的新目的地。

![資料擷取](./images/destsdk2.png)

輸入&#x200B;**持有人權杖**&#x200B;的隨機值，例如&#x200B;**1234**。 按一下&#x200B;**連線到目的地**。

![資料擷取](./images/destsdk3.png)

您將會看到此訊息。 作為目的地的名稱，請使用`--aepUserLdap-- - Webhook`。 選取選取的端點，在此範例中為&#x200B;**EU**。 按一下&#x200B;**下一步**。

![資料擷取](./images/destsdk4.png)

您可以選擇選取資料治理原則。 按一下&#x200B;**下一步**。

![資料擷取](./images/destsdk5.png)

選取您先前建立的對象，名為`--aepUserLdap-- - Interest in Galaxy S24`。 按一下&#x200B;**下一步**。

![資料擷取](./images/destsdk6.png)

您將會看到此訊息。 確定將&#x200B;**SOURCE欄位** `--aepTenantId--.identification.core.ecid`對應到欄位`Identity: ecid`。 按一下&#x200B;**下一步**。

![資料擷取](./images/destsdk7.png)

按一下&#x200B;**完成**。

![資料擷取](./images/destsdk8.png)

您的目的地現在已上線，新的對象資格將立即串流到您的自訂webhook。

![資料擷取](./images/destsdk9.png)

## 測試您的對象啟用

移至[https://dsn.adobe.com](https://dsn.adobe.com)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案上的3個點&#x200B;**...**，然後按一下&#x200B;**執行**&#x200B;以開啟它。

![DSN](./../../datacollection/module1.1/images/web8.png)

然後您會看到示範網站已開啟。 選取URL並將其複製到剪貼簿。

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

開啟新的無痕瀏覽器視窗。

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

貼上您在上一步中複製的示範網站URL。 接著，系統會要求您使用Adobe ID登入。

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

選取您的帳戶型別並完成登入程式。

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

接著，您會在無痕瀏覽器視窗中看到您的網站已載入。 每次練習都需要使用全新的無痕瀏覽器視窗，才能載入您的示範網站URL。

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

在此範例中，您想要回應檢視特定產品的特定客戶。
從**Citi Signal**&#x200B;首頁，移至&#x200B;**手機和裝置**，然後按一下產品&#x200B;**Galaxy S24**。

![資料擷取](./images/homegalaxy.png)

Galaxy S24的產品頁面現已檢視，因此您的對象將在數分鐘內符合您的個人資料資格。

![資料擷取](./images/homegalaxy1.png)

當您開啟設定檔檢視器並移至&#x200B;**對象**&#x200B;時，您將看到對象符合資格。

![資料擷取](./images/homegalaxydsdk.png)

現在返回您在[https://eodts05snjmjz67.m.pipedream.net](https://eodts05snjmjz67.m.pipedream.net)上開啟的webhook，您應該會看到新的傳入要求，這些要求來自Adobe Experience Platform且包含對象資格事件。

![資料擷取](./images/destsdk10.png)

下一步： [摘要與優點](./summary.md)

[返回模組2.3](./real-time-cdp-build-a-segment-take-action.md)

[返回所有模組](../../../overview.md)
