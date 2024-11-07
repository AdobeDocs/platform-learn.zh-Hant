---
title: Real-time CDP - Destinations SDK
description: Real-time CDP - Destinations SDK
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 2%

---

# 2.3.7目的地SDK

## 2.3.7.1設定您的Adobe I/O專案

>[!IMPORTANT]
>
>如果您在2021年12月之後建立了您的Adobe I/O專案，您可以重複使用該專案、略過本練習，並立即移至練習6.7.2。
>
>如果您在2021年12月之前建立Adobe I/O專案，請建立新專案以確保其與Destinations Authoring API相容。

在本練習中，您將密集使用Adobe I/O來查詢平台的API。 請依照下列步驟設定Adobe I/O。

移至[https://developer.adobe.com/console/home](https://developer.adobe.com/console/home)

![Adobe I/O新整合](../module2.1/images/iohome.png)

請務必在熒幕右上角選取正確的Adobe Experience Platform執行個體。 您的執行個體是`--envName--`。

![Adobe I/O新整合](../module2.1/images/iocomp.png)

按一下&#x200B;**建立新專案**。

![Adobe I/O新整合](../module2.1/images/adobe_io_new_integration.png)或
![Adobe I/O新整合](../module2.1/images/adobe_io_new_integration1.png)

選取&#x200B;**+新增至專案**&#x200B;並選取&#x200B;**API**。

![Adobe I/O新整合](../module2.1/images/adobe_io_access_api.png)

然後您會看到以下內容：

![Adobe I/O新整合](../module2.1/images/api1.png)

按一下&#x200B;**Adobe Experience Platform**&#x200B;圖示。

![Adobe I/O新整合](../module2.1/images/api2.png)

按一下&#x200B;**Experience PlatformAPI**。

![Adobe I/O新整合](../module2.1/images/api3.png)

按一下&#x200B;**下一步**。

![Adobe I/O新整合](../module2.1/images/next.png)

您現在可以選擇讓Adobe I/O產生您的安全性金鑰組，或上傳現有的金鑰組。

選擇&#x200B;**選項1 — 產生金鑰組**。

![Adobe I/O新整合](../module2.1/images/api4.png)

按一下&#x200B;**產生金鑰組**。

![Adobe I/O新整合](../module2.1/images/generate.png)

您將看到旋轉圖示約30秒。

![Adobe I/O新整合](../module2.1/images/spin.png)

您會看到此訊息，而您產生的金鑰組將下載為zip檔案： **config.zip**。

在案頭上解壓縮檔案&#x200B;**config.zip**，您會看到其中包含2個檔案：

![Adobe I/O新整合](../module2.1/images/zip.png)

- **certificate_pub.crt**&#x200B;是您的公開金鑰憑證。 從安全性角度來看，這是可自由用來設定與線上應用程式整合的憑證。
- **private.key**&#x200B;是您的私密金鑰。 永遠不應與任何人共用此內容。 私密金鑰是您用來驗證API實作的金鑰，且應該是機密。 如果您與任何人共用私密金鑰，他們可能會存取您的實作，並濫用API將惡意資料擷取至Platform，並擷取Platform中的所有資料。

![Adobe I/O新整合](../module2.1/images/config.png)

請務必將&#x200B;**config.zip**&#x200B;檔案儲存在安全位置，因為您後續步驟以及日後存取Adobe I/O和Adobe Experience Platform API時都需要此檔案。

按一下&#x200B;**下一步**。

![Adobe I/O新整合](../module2.1/images/next.png)

您現在必須選取整合的&#x200B;**產品設定檔**。

選取所需的產品設定檔。

**參考資訊**：在您的Adobe Experience Platform執行個體中，產品設定檔將具有不同的命名。 您至少需要選取一個具有適當存取許可權的產品設定檔，這些設定檔是在Adobe Admin Console中設定的。

![Adobe I/O新整合](../module2.1/images/api9.png)

按一下&#x200B;**儲存設定的API**。

![Adobe I/O新整合](../module2.1/images/saveconfig.png)

您將會看到旋轉圖示幾秒鐘。

![Adobe I/O新整合](../module2.1/images/api10.png)

接下來，您將會看到您的整合。

![Adobe I/O新整合](../module2.1/images/api11.png)

按一下「下載Postman **」按鈕，然後按一下「服務帳戶(JWT)」**&#x200B;來下載Postman環境（等候下載環境，這可能需要幾秒鐘的時間）。****

![Adobe I/O新整合](../module2.1/images/iopm.png)

向下捲動，直到您看到&#x200B;**服務帳戶(JWT)**&#x200B;為止，您可在這裡找到所有用於設定與Adobe Experience Platform整合的整合詳細資訊。

![Adobe I/O新整合](../module2.1/images/api12.png)

您的IO專案目前有一個通用名稱。 您需要為整合提供易記名稱。 按一下所示的&#x200B;**專案1** （或類似名稱）

![Adobe I/O新整合](../module2.1/images/api13.png)

按一下&#x200B;**編輯專案**。

![Adobe I/O新整合](../module2.1/images/api14.png)

輸入整合的「名稱」和「說明」。 作為命名慣例，我們將使用`AEP API --aepUserLdap--`。 將ldap取代為您的ldap。
例如，如果您的ldap是vangeluw，則整合的名稱和說明會變成AEP API vangeluw。

輸入`AEP API --aepUserLdap--`作為&#x200B;**專案標題**。 按一下&#x200B;**儲存**。

![Adobe I/O新整合](../module2.1/images/api15.png)

您的Adobe I/O整合現已完成。

![Adobe I/O新整合](../module2.1/images/api16.png)

## 2.3.7.2 Postman驗證至Adobe I/O

移至[https://www.getpostman.com/](https://www.getpostman.com/)。

按一下&#x200B;**開始使用**。

![Adobe I/O新整合](../module2.1/images/getstarted.png)

接下來，下載並安裝Postman。

![Adobe I/O新整合](../module2.1/images/downloadpostman.png)

安裝Postman後，請啟動應用程式。

Postman中有2個概念：「環境」和「集合」。

- 「環境」包含您所有或多或少一致的環境變數。 在環境中，您可以找到類似平台環境的IMSOrg，以及您的私密金鑰等安全性憑證。 環境檔案是您在上一個練習中的Adobe I/O設定期間下載的檔案，其名稱如下： **service.postman_environment.json**。

- 集合包含您可以使用的許多API請求。 我們將使用2個集合
   - 1個AdobeI/0驗證的集合
   - 1此單元練習的集合
   - 1個用於Real-Time CDP模組中練習的集合，用於目的地製作

請將檔案[postman.zip](./../../../assets/postman/postman_profile.zip)下載到您的本機案頭。

在此&#x200B;**postman.zip**&#x200B;檔案中，您會找到下列檔案：

- `_Adobe I-O - Token.postman_collection.json`
- `_Adobe Experience Platform Enablement.postman_collection.json`
- `Destination_Authoring_API.json`

解壓縮&#x200B;**postman.zip**&#x200B;檔案，並將這3個檔案連同從Adobe I/O下載的Postman環境儲存在案頭上的資料夾中。您需要在該資料夾中有這4個檔案：

![Adobe I/O新整合](../module2.1/images/pmfolder.png)

返回Postman。 按一下&#x200B;**匯入**。

![Adobe I/O新整合](../module2.1/images/postmanui.png)

按一下&#x200B;**上傳檔案**。

![Adobe I/O新整合](../module2.1/images/choosefiles.png)

導覽至您案頭上解壓縮4個下載檔案的資料夾。 同時選取這4個檔案，然後按一下[開啟]。****

![Adobe I/O新整合](../module2.1/images/selectfiles.png)

按一下&#x200B;**開啟**&#x200B;後，Postman會顯示您即將匯入的環境與集合的概觀。 按一下&#x200B;**匯入**。

![Adobe I/O新整合](../module2.1/images/impconfirm.png)

您現在已擁有Postman所需的一切，可開始透過API與Adobe Experience Platform互動。

首先要做的就是確保您已正確驗證。 若要進行驗證，您需要請求存取權杖。

在執行任何要求之前，請確定您已選取正確的環境。 您可以驗證右上角的環境下拉式清單，以檢查目前選取的環境。

所選環境的名稱應類似於以下名稱：

![Postman](../module2.1/images/envselemea.png)

按一下&#x200B;**eye**&#x200B;圖示，然後按一下&#x200B;**編輯**&#x200B;以更新環境檔案中的私密金鑰。

![Postman](../module2.1/images/gear.png)

您將會看到此訊息。 除了欄位&#x200B;**PRIVATE_KEY**&#x200B;外，所有欄位都已預先填入。

![Postman](../module2.1/images/pk2.png)

私密金鑰是在您建立Adobe I/O專案時產生的。 已下載為名為&#x200B;**config.zip**&#x200B;的ZIP檔案。 將該zip檔案解壓縮至您的案頭。

![Postman](../module2.1/images/pk3.png)

開啟資料夾&#x200B;**config**，然後使用您選擇的文字編輯器開啟檔案&#x200B;**private.key**。

![Postman](../module2.1/images/pk4.png)

然後您會看到類似此內容，將所有文字複製到剪貼簿。

![Postman](../module2.1/images/pk5.png)

返回Postman，針對欄&#x200B;**INITIAL VALUE**&#x200B;和&#x200B;**CURRENT VALUE**，在變數&#x200B;**PRIVATE_KEY**&#x200B;旁的欄位中貼上私密金鑰。 按一下&#x200B;**儲存**。

![Postman](../module2.1/images/pk6.png)

您的Postman環境和集合現已設定完畢，可正常運作。 您現在可以從Postman驗證Adobe I/O。

為此，您需要載入外部程式庫，以負責通訊的加密和解密。 若要載入此程式庫，您必須執行名稱為&#x200B;**INIT：載入RS256**&#x200B;的密碼編譯程式庫的要求。 在&#x200B;**_Adobe I/O - Token集合**&#x200B;中選取此要求，您會看到它顯示在畫面中央。

![Postman](../module2.1/images/iocoll.png)

![Postman](../module2.1/images/cryptolib.png)

按一下藍色的&#x200B;**傳送**&#x200B;按鈕。 幾秒後，您應該會在Postman的&#x200B;**內文**&#x200B;區段中看到回應：

![Postman](../module2.1/images/cryptoresponse.png)

現在載入加密編譯程式庫後，我們就能向Adobe I/O進行驗證。

在&#x200B;**\_Token集合**&#x200B;中，選取名稱為&#x200B;**IMS： JWT Generate + Auth**&#x200B;的Adobe I/O。 同樣地，您會在畫面中央看到請求詳細資訊。

![Postman](../module2.1/images/ioauth.png)

按一下藍色的&#x200B;**傳送**&#x200B;按鈕。 幾秒後，您應該會在Postman的&#x200B;**內文**&#x200B;區段中看到回應：

![Postman](../module2.1/images/ioauthresp.png)

如果設定成功，您應該會看到包含下列資訊的類似回應：

| 索引鍵 | 值 |
|:-------------:| :---------------:| 
| token_type | **持有人** |
| access_token | **eyJ4NXUiOiJpbXNfbmEx...QT7mqZkumN1tdsPEioOEl4087Dg** |
| expires_in | **86399973** |

Adobe I/O已為您提供&#x200B;**bearer**-token，具有特定值（這個很長的存取權杖）和到期視窗。

我們收到的Token現在有24小時有效。 這表示24小時後，如果您要使用Postman驗證Adobe I/O，必須再次執行此請求以產生新Token。

## 2.3.7.3定義端點與格式

在本練習中，您將需要端點來設定，以便在區段符合資格時，資格事件可串流至該端點。 在本練習中，您將使用[https://webhook.site/](https://webhook.site/)的範例端點。 移至[https://webhook.site/](https://webhook.site/)，您會看到類似此內容。 按一下&#x200B;**複製到剪貼簿**&#x200B;以複製url。 您需要在下一個練習中指定此URL。 此範例中的URL是`https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a`。

![資料擷取](./images/webhook1.png)

至於格式，我們將使用標準範本，將區段資格或取消資格連同客戶識別碼等中繼資料串流。 您可以自訂範本以符合特定端點的期望，但在本練習中，我們將重複使用標準範本，這將導致類似以下的裝載將串流到端點。

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

## 2.3.7.4建立伺服器和範本設定

在Adobe Experience Platform中建立您自己的目的地的第一個步驟是建立伺服器和範本設定。

若要這麼做，請移至&#x200B;**目的地編寫API**、**目的地伺服器和範本**，然後按一下以開啟要求&#x200B;**POST — 建立目的地伺服器組態**。 您將會看到此訊息。 在&#x200B;**Headers**&#x200B;底下，您需要手動更新機碼&#x200B;**x-sandbox-name**&#x200B;的值，並將其設定為`--aepSandboxName--`。 選取值&#x200B;**{{SANDBOX_NAME}}**。

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

貼上上述程式碼後，您必須手動更新欄位&#x200B;**urlBasedDestination.url.value**，而且您必須將其設定為您在上一步中建立的webhook的URL，在此範例中為`https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a`。

![資料擷取](./images/sdkpm4.png)

更新欄位&#x200B;**urlBasedDestiantion.url.value**&#x200B;後，它應該如下所示。 按一下&#x200B;**傳送**。

![資料擷取](./images/sdkpm5.png)

按一下&#x200B;**傳送**&#x200B;之後，將會建立您的伺服器範本，而在回應中，您會看到名為&#x200B;**instanceId**&#x200B;的欄位。 記下它，因為您會在下一個步驟中需要它。 在此範例中，**instanceId**為
`eb0f436f-dcf5-4993-a82d-0fcc09a6b36c`。

![資料擷取](./images/sdkpm6.png)

## 2.3.7.5建立您的目的地設定

在Postman中的&#x200B;**目的地編寫API**&#x200B;底下，移至&#x200B;**目的地組態**&#x200B;並按一下以開啟要求&#x200B;**POST — 建立目的地組態**。 您將會看到此訊息。 在&#x200B;**Headers**&#x200B;底下，您需要手動更新機碼&#x200B;**x-sandbox-name**&#x200B;的值，並將其設定為`--aepSandboxName--`。 選取值&#x200B;**{{SANDBOX_NAME}}**。

![資料擷取](./images/sdkpm7.png)

以`--aepSandboxName--`取代。

![資料擷取](./images/sdkpm8.png)

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

貼上上述程式碼後，您必須手動更新&#x200B;**destinationDelivery欄位。 destinationServerId**，而且您必須將它設定為您在上一步中建立的目的地伺服器範本的&#x200B;**instanceId**，在此範例中為`eb0f436f-dcf5-4993-a82d-0fcc09a6b36c`。 接著，按一下&#x200B;**傳送**。

![資料擷取](./images/sdkpm10.png)

您會看到此回應。

![資料擷取](./images/sdkpm12.png)

您的目的地現在已建立在Adobe Experience Platform中。 讓我們到那裡檢查一下。

移至[Adobe Experience Platform](https://experience.adobe.com/platform)。 登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./../../../modules/datacollection/module1.2/images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--aepSandboxName--``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的[!UICONTROL 沙箱]後，您將會看到畫面變更，現在您已在專屬的[!UICONTROL 沙箱]中。

![資料擷取](./../../../modules/datacollection/module1.2/images/sb1.png)

在左側功能表中，移至&#x200B;**目的地**，按一下&#x200B;**目錄**，然後向下捲動至類別&#x200B;**串流**。 您現在會看到目的地可供使用。

![資料擷取](./images/destsdk1.png)

## 2.3.7.6將您的區段連結至目的地

在&#x200B;**目的地** > **目錄**&#x200B;中，按一下目的地上的&#x200B;**設定**，開始將區段新增至您的新目的地。

![資料擷取](./images/destsdk2.png)

輸入虛擬持有人權杖，例如&#x200B;**1234**。 按一下&#x200B;**連線到目的地**。

![資料擷取](./images/destsdk3.png)

您將會看到此訊息。 作為目的地的名稱，請使用`--aepUserLdap-- - Webhook`。 選取選取的端點，在此範例中為&#x200B;**EU**。 按一下&#x200B;**下一步**。

![資料擷取](./images/destsdk4.png)

您可以選擇選取資料治理原則。 按一下&#x200B;**下一步**。

![資料擷取](./images/destsdk5.png)

選取您先前建立的區段，名為`--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`。 按一下&#x200B;**下一步**。

![資料擷取](./images/destsdk6.png)

您將會看到此訊息。 確定將&#x200B;**SOURCE欄位** `--aepTenantId--.identification.core.ecid`對應到欄位`Identity: ecid`。 按一下&#x200B;**下一步**。

![資料擷取](./images/destsdk7.png)

按一下&#x200B;**完成**。

![資料擷取](./images/destsdk8.png)

您的目的地現已上線，新的區段資格將立即串流至您的自訂webhook。

![資料擷取](./images/destsdk9.png)

## 2.3.7.7測試您的區段啟用

移至[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案以開啟。

![DSN](../../gettingstarted/gettingstarted/images/web8.png)

您現在可以依照以下流程存取網站。 按一下&#x200B;**整合**。

![DSN](../../gettingstarted/gettingstarted/images/web1.png)

在&#x200B;**整合**&#x200B;頁面上，您必須選取在練習0.1中建立的資料收集屬性。

![DSN](../../gettingstarted/gettingstarted/images/web2.png)

然後您會看到示範網站已開啟。 選取URL並將其複製到剪貼簿。

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

開啟新的無痕瀏覽器視窗。

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

貼上您在上一步中複製的示範網站URL。 接著，系統會要求您使用Adobe ID登入。

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

選取您的帳戶型別並完成登入程式。

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

接著，您會在無痕瀏覽器視窗中看到您的網站已載入。 對於每個示範，您都需要使用全新的無痕瀏覽器視窗來載入您的示範網站URL。

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

從&#x200B;**Luma**&#x200B;首頁，前往&#x200B;**Men**，然後按一下產品&#x200B;**PROTEUS FITNESS JACKSHIRT**。

![資料擷取](./images/homenadia.png)

您現在已造訪&#x200B;**PROTEUS FITNESS JACKSHIRT**&#x200B;的產品頁面，這表示您現在符合在此練習中先前建立的區段資格。

![資料擷取](./images/homenadiapp.png)

當您開啟設定檔檢視器並移至&#x200B;**區段**&#x200B;時，您將看到該區段符合資格。

![資料擷取](./images/homenadiapppb.png)

現在返回您在[https://webhook.site/](https://webhook.site/)上開啟的webhook，您應該會看到新的傳入要求，這些要求來自Adobe Experience Platform且包含區段資格事件。

![資料擷取](./images/destsdk10.png)

下一步： [摘要與優點](./summary.md)

[返回模組2.3](./real-time-cdp-build-a-segment-take-action.md)

[返回所有模組](../../../overview.md)
