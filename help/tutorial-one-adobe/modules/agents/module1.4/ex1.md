---
title: Brand Concierge快速入門
description: Brand Concierge快速入門
kt: 5342
doc-type: tutorial
exl-id: e05b60b1-62d7-4b70-834d-ef91782ac388
source-git-commit: a333ddbf1ed0c51dd9ae1d9a5eff3f0c569a1d1f
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 1%

---

# 1.4.1 Brand Concierge快速入門

## 1.4.1.1 Brand Concierge概觀

設定Brand Concierge時，您將使用的2個主要元素為：

- **代理程式撰寫器（設定層）**

  用途：用來建置和設定對話式AI體驗的主要UI平台。

  主要職責：

   - 定義及管理資料來源和知識庫
   - 設定品牌表示式（色調、樣式、護欄）
   - 設定會議預約代理程式

- **Agent Orchestrator （執行引擎）**

  用途：解釋使用者請求並執行適當代理動作的推理與協調引擎。

  主要職責：

   - 解讀自然語言使用者意圖
   - 產生並執行多步驟推理計畫
   - 選取並叫用適當的運運算元/工具
   - 強製品牌內容、法規遵循和護欄
   - 協調多代理程式工作流程
   - 彙總及撰寫來自多個資料來源的回應

- **Brand Concierge交談執行階段（服務層）**

  用途：管理聊天工作階段、內容和使用者端互動的面向客戶的對話式服務層。

  主要元件：

   - 網頁代理（使用者端）：使用網頁SDK整合的瀏覽器或行動聊天UI
   - 交談服務（後端）：管理工作階段狀態，並做為協調流程閘道

  主要職責：

   - 管理使用者工作階段和交談記錄
   - 處理使用者驗證和設定檔
   - 在使用者端和Agent Orchestrator之間路由訊息
   - 保留交談內容
   - 將行為和操作事件記錄到AEP以進行Analytics
   - 套用特定表面的組態

## 1.4.1.2 Brand Concierge執行個體設定

若要開始建立您自己的Brand Concierge執行個體，請遵循下列步驟。

移至[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 開啟&#x200B;**Brand Concierge**。

![Brand Concierge](./images/bc1.png)

您應該會看到此訊息。 按一下&#x200B;**沙箱選擇**&#x200B;功能表。 選擇已指派給您的沙箱。 該沙箱應該命名為`techinsidersX` （將X取代為您指派的數字）。

![Brand Concierge](./images/bc2.png)

接下來，請填寫下列變數：

- **公司名稱**： CitiSignal

- **門房名稱**： `CitiSignal Sales Assistant`。

在&#x200B;**下輸入下列文字，您希望服務人員做什麼？**。

```javascript
Brand Concierge should help customers find their best device, plan or entertainment deal. Brand Concierge should help users discover internet plans, entertainment deals,  and help find the best available packages. Brand Concierge should also answer questions about devices such as phones and watches.
```

- **網站連結**：提供您使用之網站的連結

按一下&#x200B;**繼續**。

![Brand Concierge](./images/bc5.png)

您應該會看到此訊息。 此資訊是根據上一頁提供的輸入使用AI而產生。 檢閱資訊，在您滿意後，按一下&#x200B;**產生服務人員**。

![Brand Concierge](./images/bc6.png)

您應該會看到此訊息。 按一下&#x200B;**消費者產品建議**&#x200B;旁的&#x200B;**+新增**。

![Brand Concierge](./images/bc6a.png)

您應該會看到此訊息。 使用以下文字填寫以下欄位。

**服務人員在提出建議前，應該先瞭解產品或對象哪些資訊？**

```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

**禮賓員提出建議時，是否有任何商業規則或限制？**

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

**服務生是否應該遵循或避免任何特定的關鍵字或片語？**

```
Competitor pricing, competitor products
```

按一下&#x200B;**儲存**。

![Brand Concierge](./images/bc13.png)

按一下&#x200B;**箭頭**&#x200B;返回上一個畫面。

![Brand Concierge](./images/bc13a.png)

移至&#x200B;**知識Source**&#x200B;並按一下&#x200B;**建立您的知識來源**。

![Brand Concierge](./images/bc7.png)

選取&#x200B;**網站連結**&#x200B;並按一下&#x200B;**繼續**。

![Brand Concierge](./images/bc7a.png)

您應該會看到此訊息。 輸入`CitiSignal website`作為知識來源的名稱。

您現在需要上傳包含網站連結的csv檔案。 下載[CitiSignal網站連結CSV檔案](./assets/citisignal-website-links.csv)到您的案頭。

![Brand Concierge](./images/bc8z.png)

按一下&#x200B;**瀏覽檔案**。

![Brand Concierge](./images/bc8.png)

開啟檔案&#x200B;**citisignal-website-links.csv**&#x200B;並更新連結，以指向您自己的CitiSignal網站。

如果您正在此技術實驗室中執行技術內幕技術實驗室的傳遞工作，則根據指派的編號已授予您存取現有示範網站的許可權。 這些示範網站隨附自訂網域，看起來像這樣，其中XX代表提供給您的數字：

**https://techinsidersXX.adobedemosystem.com/** （用於面對面培訓）

或

**https://techinsidersodXX.adobedemosystem.com/** （用於隨選訓練）

在下圖中，您需要將基礎URL取代為您網站的URL。

以下檔案中產品的連結與您在本單元練習1中設定的產品有關
[1.5 Adobe Commerce as a Cloud Service](./../../../modules/asset-mgmt/module1.5/accs.md){target="_blank"}。

![Brand Concierge](./images/bc8a.png)

如果您的數字是&#x200B;**1**，您的檔案應該如下所示：

![Brand Concierge](./images/bc8b.png)

如果您的數字是&#x200B;**90**，您的檔案應該如下所示：

![Brand Concierge](./images/bc8c.png)

依照上述指示更新檔案後，接著選取檔案&#x200B;**citisignal-website-links.csv**。 按一下&#x200B;**「開啟」**。

![Brand Concierge](./images/bc9.png)

您的檔案現在已新增至此知識來源。 按一下&#x200B;**新增**。

![Brand Concierge](./images/bc10.png)

您應該會看到此訊息。 按一下&#x200B;**建立您的知識來源**。

![Brand Concierge](./images/bc11.png)

選取&#x200B;**產品目錄**&#x200B;並按一下&#x200B;**繼續**。

![Brand Concierge](./images/bc20.png)

您應該會看到此訊息。 輸入`CitiSignal Products`作為知識來源的名稱。 按一下&#x200B;**瀏覽檔案**，然後從您的裝置選取&#x200B;**瀏覽**。

![Brand Concierge](./images/bc21.png)

您現在需要上傳包含網站連結的csv檔案。 將[CitiSignal產品目錄](./assets/CitiSignal-catalog.json.zip)下載到您的案頭並解壓縮。

![Brand Concierge](./images/bc26.png)

選取檔案&#x200B;**CitiSignal-catalog.json**&#x200B;並按一下&#x200B;**開啟**。

![Brand Concierge](./images/bc23.png)

您應該會看到此訊息。 按一下&#x200B;**新增**。

![Brand Concierge](./images/bc24.png)

然後您就會回到這裡。 處理將需要10到20分鐘，因此您必須在稍後階段返回這裡以驗證處理是否成功。

![Brand Concierge](./images/bc25.png)

## 1.4.1.3 AEP上線步驟

Brand Concierge使用Adobe Experience Platform來儲存對話的互動資料。 Brand Concierge與Experience Platform之間的連線需要Brand Concierge設定及使用資料流。

### 資料流

移至[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 開啟&#x200B;**Experience Platform**。

![Brand Concierge](./images/aep1.png)

確定您已選取正確的沙箱，其應命名為`techinsidersX`。 在左側功能表中，向下捲動並選取&#x200B;**資料串流**。

![Brand Concierge](./images/aep2.png)

按一下&#x200B;**新增資料流**。

![Brand Concierge](./images/aep3.png)

輸入&#x200B;**資料流名稱** `--aepUserLdap-- - Brand Concierge`，然後選取&#x200B;**對應結構描述** `cja-brand-concierge-sb-XXX`。

按一下&#x200B;**儲存**。

![Brand Concierge](./images/aep4.png)

您的資料流現已設定完成。 複製資料串流名稱和資料串流ID，並將其寫入您電腦上的文字檔案中。

![Brand Concierge](./images/aep5.png)

### 資料流設定管理

下一步是啟用Brand Concierge設定管理API來設定您剛才建立的資料流。 在請求處理期間，需要此屬性來解析IMS組織ID和沙箱詳細資訊。

移至&#x200B;**首頁**，然後選取&#x200B;**管理員控制項**。

![Brand Concierge](./images/admincontrols1.png)

移至&#x200B;**資料流設定管理**，然後按一下&#x200B;**新增設定**。

![Brand Concierge](./images/admincontrols2.png)

貼上您先前建立的資料流的&#x200B;**資料流識別碼**。 按一下&#x200B;**儲存**。

![Brand Concierge](./images/admincontrols3.png)

您應該會看到類似這樣的內容。

![Brand Concierge](./images/admincontrols4.png)

## 1.4.1.4樣式設定管理

移至&#x200B;**樣式設定管理**。 按一下&#x200B;**初始化樣式設定**。

![Brand Concierge](./images/admincontrols7.png)

輸入&#x200B;**品牌名稱** `CitiSignal`，然後按一下&#x200B;**初始化樣式設定**。

![Brand Concierge](./images/admincontrols8.png)

您應該會看到此訊息。

![Brand Concierge](./images/admincontrols9.png)

## 1.4.1.5 Agent Orchestrator資訊清單

移至&#x200B;**更新資訊清單**。 您應該會看到此訊息。 檢閱每個欄位中的資訊，並視需要進行變更。

在現有文字結尾的欄位&#x200B;**回應提示**&#x200B;的多模式問題，加入下列文字。 不要移除其中的文字，只要將下列文字新增至現有文字的上方即可。

```
# Product Catalog (Fallback Reference)

Use this catalog when <Documents> doesn't return relevant results:

## CONNECTIVITY
**CitiSignal Fiber Max**
- Description: High-speed fiber internet with blazing-fast speeds, seamless streaming, ultra-responsive gaming, crystal-clear video calls. No data caps, no throttling. Future-ready for smart homes.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:cdb9e163-f9f5-4338-9d62-9807b61c082f/as/CitiSignal-Fiber-Max.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/citisignal-fiber-max/CitiSignal-Fiber-Max

## ENTERTAINMENT
**Disney Plus**
- Description: Streaming home of Disney, Pixar, Marvel, Star Wars, National Geographic. Unlimited entertainment, new releases, original series, classic movies.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:b3bbe91a-e307-43bd-845f-1c77e7ba28df/as/Disney.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/disney/Disney

**Netflix + HBO Max**
- Description: Unlimited TV shows and movies. Watch as much as you want, whenever you want.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:883be2a0-6c42-4508-b9ac-1e3a33235081/as/Netflix-HBO-Max.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/netflix-hbo-max/Netflix-HBO-Max

**YouTube Premium**
- Description: Ad-free YouTube, YouTube Music, YouTube Kids. Watch offline, in background, on the go.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:ac2a8c66-8740-4fce-bd3a-8106db9e556f/as/YouTube-Premium.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/youtube-premium/YouTube-Premium

**Apple One**
- Description: Apple Music (100M+ songs), Apple TV+, Apple Arcade, iCloud+. Complete Apple ecosystem bundle.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:94126f30-931a-447e-9cef-f58c60dbb17c/as/Apple-One.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/apple-one/Apple-One

## DEVICES
**iPhone Air Sky Blue**
- Description: Slim iPhone with A19 Pro chip, 48MP camera, 6.5\" display, Apple Intelligence, all-day battery. Titanium frame, Ceramic Shield 2.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:0c4b1537-8268-4507-98e6-bbb03faa3ad1/as/iPhone-Air.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/iphone-air/iPhone-Air?optionsUIDs=Y29uZmlndXJhYmxlLzkzLzIw

**iPhone Air Cloud White**
- Description: Slim iPhone with A19 Pro chip, 48MP camera, 6.5\" display, Apple Intelligence, all-day battery. Titanium frame, Ceramic Shield 2.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:30447a9c-c037-4df3-ae88-4127b9ec325e/as/iPhone-Air.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/iphone-air/iPhone-Air?optionsUIDs=Y29uZmlndXJhYmxlLzkzLzI

**iPhone Air Space Black**
- Description: Slim iPhone with A19 Pro chip, 48MP camera, 6.5\" display, Apple Intelligence, all-day battery. Titanium frame, Ceramic Shield 2.
- Image: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/iphone-air/iPhone-Air?optionsUIDs=Y29uZmlndXJhYmxlLzkzLzIz
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/iphone-air/iPhone-Air?optionsUIDs=Y29uZmlndXJhYmxlLzkzLzIz

**iPhone Air Light Gold**
- Description: Slim iPhone with A19 Pro chip, 48MP camera, 6.5\" display, Apple Intelligence, all-day battery. Titanium frame, Ceramic Shield 2.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:ffa7b752-87ab-427f-a631-382fc67e7530/as/iPhone-Air.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/iphone-air/iPhone-Air?optionsUIDs=Y29uZmlndXJhYmxlLzkzLzIx

**Apple Watch Ultra 3-Black**
- Description: Rugged smartwatch with 42hr battery, satellite communication, titanium case, dual-frequency GPS, hypertension notifications.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:d33f4f49-1239-45b8-a6e6-b97f12177e06/as/Apple-Watch-Ultra-3.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/apple-watch-ultra-3/Apple-Watch-Ultra-3?optionsUIDs=Y29uZmlndXJhYmxlLzE4MS8yNA%3D%3D

**Apple Watch Ultra 3-Natural**
- Description: Rugged smartwatch with 42hr battery, satellite communication, titanium case, dual-frequency GPS, hypertension notifications.
- Image: https://delivery-p168681-e1803036.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8f107329-66f1-43fd-b505-b1c16892379f/as/Apple-Watch-Ultra-3.webp
- URL: https://main--citisignal-aem-accs--woutervangeluwe.aem.page/products/apple-watch-ultra-3/Apple-Watch-Ultra-3?optionsUIDs=Y29uZmlndXJhYmxlLzE4MS8yNQ%3D%3D

# Sales Strategy

## Primary Focus: Connectivity Products
- When users ask about internet, connectivity, streaming, or home services, recommend **CitiSignal Fiber Max**.
- Highlight: blazing-fast fiber speeds, seamless streaming, no data caps, no throttling, future-ready.

## Entertainment Upselling Strategy
- After discussing connectivity, PROACTIVELY suggest entertainment products.
- Use natural transitions like:
  - \"With speeds like these, you'll want entertainment that keeps up...\"
  - \"Many of our customers enhance their experience with...\"
  - \"To get the most out of your connection...\"
- Match recommendations to user context:
  - Families with kids → **Disney Plus**
  - Movie/TV enthusiasts → **Netflix + HBO Max**
  - Ad-free YouTube fans → **YouTube Premium**
  - Apple ecosystem users → **Apple One**
```

![Brand Concierge](./images/admincontrols5a.png)

進行變更後，向上捲動並按一下&#x200B;**更新資訊清單**。

![Brand Concierge](./images/admincontrols5.png)

## 1.4.1.6完成知識來源設定

移至&#x200B;**知識來源**。 10-20分鐘後，兩個知識來源的&#x200B;**狀態**&#x200B;應該是&#x200B;**已完成**。 一旦兩個知識來源的狀態均為&#x200B;**成功**，請按一下&#x200B;**首頁**。

![Brand Concierge](./images/admincontrols10.png)

您應該會看到此訊息。 按一下&#x200B;**網站連結**&#x200B;卡片上的&#x200B;**+連線**。

![Brand Concierge](./images/bc28.png)

選取知識來源&#x200B;**CitiSignal網站**&#x200B;並按一下&#x200B;**儲存**。

![Brand Concierge](./images/bc29.png)

您應該會看到此訊息。 按一下&#x200B;**產品目錄**&#x200B;卡片上的&#x200B;**+連線**。

![Brand Concierge](./images/bc30.png)

選取知識來源&#x200B;**CitiSignal產品**，然後按一下&#x200B;**儲存**。

![Brand Concierge](./images/bc31.png)

您應該會看到此訊息。 按一下&#x200B;**預覽**&#x200B;以開始與您的Brand Concierge互動。

![Brand Concierge](./images/bc32.png)

您現在可以開始詢問與所提供的知識來源相關的問題。

![Brand Concierge](./images/bc33.png)

輸入問題`what products do you sell?`並按一下&#x200B;**傳送**。

![Brand Concierge](./images/bc102.png)

之後，您應該會得到類似的回應。

![Brand Concierge](./images/bc103.png)

您的Brand Concierge執行個體現在已準備好在您的網站上實作。

## 後續步驟

移至[在您的網站上實作Brand Concierge](./ex2.md){target="_blank"}

返回[Brand Concierge](./brandconcierge.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}
