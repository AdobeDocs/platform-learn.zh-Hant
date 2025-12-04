---
title: 在您的網站上實作Brand Concierge
description: 在您的網站上實作Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: ea5fa4694205a94f63d277fdcf2018951fa31fbc
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 0%

---

# 1.4.2在您的網站上實作Brand Concierge

>[!IMPORTANT]
>
>為了完成此練習，您需要存取運作中的AEM Assets CS Author環境和AEM CS/EDS網站。
>
>如果您沒有這類環境，請前往[Adobe Experience Manager Cloud Service和Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}。 按照這裡的指示操作，您將可以存取這樣的環境。

>[!IMPORTANT]
>
>如果您先前已使用AEM Assets CS環境設定AEM CS計畫，可能是您的AEM CS沙箱已休眠。 鑑於讓這樣的沙箱解除休眠需要10-15分鐘，最好現在開始解除休眠過程，這樣以後就不必等待了。

## 1.4.2.1設定您的網站以顯示Brand Concierge - AEM Author

為了讓Brand Concierge出現在您的網站上，您需要建立需要新增至新頁面的新自訂區塊，而且您將需要確保新頁面已新增至網站的導覽中。

您現在需要依此順序設定下列專案：

- 建立新的自訂區塊，用於將Brand Concierge載入您的網站。
- 在您的網站上為Brand Concierge建立新頁面。
- 在新建立的Brand Concierge頁面上連結新建立的自訂區塊。
- 新增參考以導覽至網站導覽標頭檔案中新建立的Brand Concierge頁面。

### 建立新的自訂區塊

若要建立新的自訂區塊，請導覽至連結至您網站的GitHub存放庫。

![區塊](./images/block1.png)

#### component-definition.json

向下捲動，直到您看到檔案&#x200B;**component-definition.json**&#x200B;並開啟為止

![區塊](./images/block8.png)

按一下&#x200B;**pencl**&#x200B;圖示以開始編輯檔案。

![區塊](./images/block8a.png)

向下捲動，直到您看到&#x200B;**區塊**&#x200B;為止。 將游標設定在元件&#x200B;**卡片**&#x200B;的右方括弧下

![區塊](./images/block9.png)

貼上此程式碼，並在程式碼區塊後面輸入逗號&#x200B;**，**：

```json
{
  "title": "BrandConcierge",
  "id": "brandconcierge",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "BrandConcierge",
          "model": "brandconcierge"
        }
      }
    }
  }
},
```

按一下&#x200B;**認可變更……**。

![區塊](./images/block10.png)

按一下&#x200B;**認可變更**。

![區塊](./images/block10a.png)

#### component-models.json

向下捲動直到您看到檔案&#x200B;**component-models.json**&#x200B;為止，然後按一下&#x200B;**鉛筆**&#x200B;圖示以開始編輯檔案。

![區塊](./images/block11.png)

向下捲動，直到您看到最後一個專案為止。 將游標設定在最後一個元件的右方括弧旁。

![區塊](./images/block12.png)

輸入逗號&#x200B;**，**，然後推入，並在下一行貼上此代碼：

```json
{
  "id": "brandconcierge",
  "fields": []
}
```

按一下&#x200B;**認可變更……**。

![區塊](./images/block13.png)

按一下&#x200B;**認可變更**。

![區塊](./images/block13a.png)

#### component-filters.json

向下捲動，直到您看到檔案&#x200B;**component-filters.json**&#x200B;為止，然後按一下&#x200B;**鉛筆**&#x200B;圖示以開始編輯檔案。

![區塊](./images/block14.png)

您應該會看到此訊息。

![區塊](./images/block14a.png)

在&#x200B;**區段**&#x200B;下方，輸入逗號`,`，並將元件`"brandconcierge"`的識別碼貼到目前最後一行之後。

按一下&#x200B;**認可變更……**。

![區塊](./images/block15.png)

按一下&#x200B;**認可變更**。

![區塊](./images/block15a.png)

#### brandconcierge.css

建立區塊時，最佳實務是建立區塊樣式的檔案，且檔案名稱應與區塊相同。 您現在應該建立該檔案，我們現在將保留空白。

移至&#x200B;**區塊**&#x200B;資料夾。 然後，按一下[新增檔案]&#x200B;**&#x200B;**&#x200B;並選取[建立新檔案]&#x200B;**&#x200B;**。

![區塊](./images/css1.png)

在文字方塊中，輸入`brandconcierge/brandconcierge.css`。 檔案目前可以保持空白。 按一下&#x200B;**認可變更……**。

![區塊](./images/css2.png)

按一下&#x200B;**認可變更**。

![區塊](./images/css3.png)

#### brandconcierge.js

建立區塊時，最佳實務是為與區塊相關的JavaScript建立檔案，且檔案名稱應與區塊相同。

按一下&#x200B;**新增檔案**&#x200B;並選取&#x200B;**建立新檔案**。

![區塊](./images/js1.png)

在文字方塊中，輸入`brandconcierge.js`。 檔案目前可以保持空白。 按一下&#x200B;**認可變更……**。

```javascript
export default function decorate(block) {
  block.setAttribute('id', 'brand-concierge-mount');
}
```

![區塊](./images/js2.png)

按一下&#x200B;**認可變更**。

![區塊](./images/js3.png)

### 建立新頁面並連結新的自訂區塊

移至[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。 按一下您的&#x200B;**程式**&#x200B;以開啟。

![AEMCS](./images/aemcs6.png)

接著，按一下&#x200B;**環境**&#x200B;標籤上的3個點&#x200B;**...**，然後按一下&#x200B;**檢視詳細資料**。

![AEMCS](./images/aemcs9.png)

然後您會看到環境詳細資料。 按一下&#x200B;**作者**&#x200B;環境的URL。

>[!NOTE]
>
>您的環境可能已休眠。 如果是這種情況，您需要先解除環境休眠。

![AEMCS](./images/aemcs10.png)

之後，您應該會看到您的AEM作者環境。 移至&#x200B;**網站**。

![AEMCS](./images/block21.png)

移至&#x200B;**花旗訊號**。 按一下&#x200B;**建立**&#x200B;並選取&#x200B;**頁面**。

![AEMCS](./images/block23.png)

選取&#x200B;**頁面**&#x200B;並按一下&#x200B;**下一步**。

![AEMCS](./images/block24.png)

輸入下列值：

- 標題： **Brand Concierge**
- 名稱： **brandconcierge**
- 頁面標題： **Brand Concierge**

按一下&#x200B;**建立**。

![AEMCS](./images/block25.png)

選取&#x200B;**開啟**。

![AEMCS](./images/block22.png)

您應該會看到此訊息。

![AEMCS](./images/block26.png)

按一下空白區域以選取&#x200B;**section**&#x200B;元件。 然後，按一下右側功能表中的加號&#x200B;**+**&#x200B;圖示。

![AEMCS](./images/block27.png)

之後，您應該會在可用區塊清單中看到自訂區塊。 按一下以選取它。

![AEMCS](./images/block28.png)

之後，您應該會看到有空白區塊新增至此頁面。 此區塊將使用您將在下一個步驟中新增的JavaScript程式庫動態載入。

按一下&#x200B;**發佈**。

![AEMCS](./images/block29.png)

再按一下&#x200B;**發佈**。

![AEMCS](./images/block30.png)

您的新頁面現已發佈，並可在下一步中新增至導覽標頭。

### 更新導覽標頭檔案

在您的AEM Sites總覽中，移至&#x200B;**CitiSignal**&#x200B;並勾選檔案&#x200B;**Header/nav**&#x200B;的核取方塊。 按一下&#x200B;**編輯**。

![AEMCS](./images/nav0.png)

在預覽畫面中選取&#x200B;**文字**&#x200B;欄位，然後按一下畫面右側的&#x200B;**文字**&#x200B;欄位以進行編輯。

![AEMCS](./images/nav0a.png)

在導覽功能表中建立新的功能表選項，文字為`Brand Concierge`。 然後，選取文字&#x200B;**Brand Concierge**&#x200B;並按一下&#x200B;**連結**&#x200B;圖示。

![AEMCS](./images/nav1.png)

請為欄位&#x200B;**路徑或URL** `/content/CitiSignal/brandconcierge.html`輸入此專案，並為欄位`Brand Concierge`標題&#x200B;**輸入**。 按一下&#x200B;**儲存**。

![AEMCS](./images/nav3.png)

然後您應該擁有此專案。 按一下「**完成**」。

![AEMCS](./images/nav4.png)

然後您應該擁有此專案。 按一下&#x200B;**發佈**。

![AEMCS](./images/nav4a.png)

再按一下&#x200B;**發佈**。

![AEMCS](./images/nav5.png)

您的新頁面現在已新增至功能表。

## 1.4.2.2設定您的網站以顯示Brand Concierge - GitHub

使用您的AEM製作環境更新內容後，您現在需要更新網站所用的GitHub存放庫中的部分程式碼。

### Javascript程式庫

若要在AEM CS/EDS上執行的網站上實作Brand Concierge，需要下列程式庫：

- [styleconfigurations.js](./assets/styleconfigurations.js)
- [alloy.js](./assets/alloy.js)
- [brandconciergemain.js](./assets/brandconciergemain.js)

將全部3個檔案下載到您的案頭。

![Brand Concierge](./images/aem0.png)

前往AEM CS/EDS網站的GitHub專案。 移至&#x200B;**指令碼**。

![Brand Concierge](./images/aem1.png)

按一下&#x200B;**新增檔案**，然後選取&#x200B;**上傳檔案**。

![Brand Concierge](./images/aem3.png)

按一下&#x200B;**選擇您的檔案**。

![Brand Concierge](./images/aem3a.png)

從您的案頭選取全部3個檔案&#x200B;**styleConfigurations.js、alloy.js和brandconciergemain.js**，然後按一下&#x200B;**開啟**。

![Brand Concierge](./images/aem4.png)

按一下&#x200B;**認可變更**。

![Brand Concierge](./images/aem5.png)

### 更新head.html

在上一步中，您已上傳3個新程式庫。 現在載入您的網站時，需要載入這些程式庫，方法是在檔案&#x200B;**head.html**&#x200B;中新增對這些檔案的參照。

此外，您也需要在&#x200B;**head.html**&#x200B;檔案中提供指示，以確保程式庫以正確的順序和正確的方式載入。

若要這麼做，請按一下&#x200B;**代碼**，前往AEM CS/EDS網站的GitHub專案。

![Brand Concierge](./images/aem6.png)

向下捲動一點。 開啟檔案&#x200B;**head.html**。

![Brand Concierge](./images/aem7.png)

按一下&#x200B;**鉛筆**&#x200B;圖示以編輯此檔案。

![Brand Concierge](./images/aem8.png)

您應該會看到此訊息。

![Brand Concierge](./images/aem9.png)

向下捲動至第43行並貼上下列內容：

下列程式碼中有2個欄位需要更新：

>[!IMPORTANT]
>
>- **datastreamId**&#x200B;目前設為&quot;XXXXX&quot;，必須由您在上一步建立的資料流識別碼取代。
>- **orgId**&#x200B;需要取代為您Adobe Experience Cloud執行個體的IMS組織ID。

```javascript
<script src="/scripts/styleconfigurations.js"></script>

<script>
		!function (n, o) {
      o.forEach(function (o) {
        n[o] || ((n.__alloyNS = n.__alloyNS ||
          []).push(o), n[o] = function () {
            var u = arguments; return new Promise(
              function (i, l) { n[o].q.push([i, l, u]) })
          }, n[o].q = [])
      })
    }
      (window, ["alloy"]);
	</script>


<script src="/scripts/alloy.js"></script>

<script>
	alloy("configure", {
		defaultConsent: "in",
        edgeDomain: "edge.adobedc.net",
        edgeBasePath: "ee",
        datastreamId: "XXXXX", // replace datastreamId
        orgId: "--aepImsOrgId--", // replace ims org Id
        debugEnabled: true,
        idMigrationEnabled: false,
        thirdPartyCookiesEnabled: false,
        prehidingStyle: ".personalization-container { opacity: 0 !important }",
    });

window["alloy"]("sendEvent", {
    conversation: {
        fetchConversationalExperience: true
    }
}).then(result => {
    console.log("Conversation experience fetched", result);
    window["alloy"]("bootstrapConversationalExperience", {
        selector: "#brand-concierge-mount",
        src: "/scripts/brandconciergemain.js",
        stylingConfigurations: window.styleConfiguration,
        stickySession: true // create a sticky session cookie with expiration
    })
});
</script>
```

按一下&#x200B;**認可變更……**。

![Brand Concierge](./images/aem10.png)

按一下&#x200B;**認可變更**。

![Brand Concierge](./images/aem11.png)

您現在已更新在網站上載入程式庫所需的程式碼。

![Brand Concierge](./images/aem12.png)

## 1.4.2.3測試您的設定

您現在可以移至`main--citisignal-aem-accs--XXX.aem.page`或`main--citisignal-aem-accs--XXX.aem.live`，在將XXX取代為GitHub使用者帳戶（在此範例中為`woutervangeluwe`）之後，在您的網站上測試您的變更。

在此範例中，完整URL會變成：
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page`和/或`https://main--citisignal-aem-accs--woutervangeluwe.aem.live`。

可能需要一些時間，才能正確顯示所有資產，因為它們必須先發佈。

您應該會看到此訊息。 按一下&#x200B;**Brand Concierge**。

![Brand Concierge](./images/aem13.png)

之後，您應該會看到此Brand Concierge，您可以在其中輸入提示。

![Brand Concierge](./images/aem14.png)

返回[Brand Concierge](./brandconcierge.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}