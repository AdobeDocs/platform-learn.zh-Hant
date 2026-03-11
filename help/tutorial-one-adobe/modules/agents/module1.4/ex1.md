---
title: Brand Concierge快速入門
description: Brand Concierge快速入門
kt: 5342
doc-type: tutorial
exl-id: e05b60b1-62d7-4b70-834d-ef91782ac388
source-git-commit: a57050bf40105a0b0c6d4ce615aa640e878ece12
workflow-type: tm+mt
source-wordcount: '1121'
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

您應該會看到此訊息。 按一下&#x200B;**沙箱選擇**&#x200B;功能表。

![Brand Concierge](./images/bc2.png)

選擇已指派給您的沙箱。 該沙箱應該命名為`--aepUserLdap-- - bc`。

![Brand Concierge](./images/bc3.png)

按一下&#x200B;**開始使用**。

![Brand Concierge](./images/bc4.png)

對於您的Brand Concierge執行個體的名稱，請使用： `--aepUserLdap-- - CitiSignal Brand Concierge`。

在&#x200B;**下輸入下列文字，您希望服務人員做什麼？**。

```javascript
Brand Concierge should help customers find their best device, plan or entertainment deal. Brand Concierge should help users discover internet plans, entertainment deals,  and help find the best available packages. Brand Concierge should also answer questions about devices such as phones and watches.
```

按一下&#x200B;**建立**。

![Brand Concierge](./images/bc5.png)

您應該會看到此訊息。 按一下&#x200B;**開始使用**&#x200B;以新增知識來源。

![Brand Concierge](./images/bc6.png)

選取&#x200B;**網站連結**&#x200B;並按一下&#x200B;**繼續**。

![Brand Concierge](./images/bc7.png)

您應該會看到此訊息。 輸入`CitiSignal website`作為知識來源的名稱。

您現在需要上傳包含網站連結的csv檔案。 下載[CitiSignal網站連結CSV檔案](./assets/citisignal-website-links.csv)到您的案頭。

按一下&#x200B;**瀏覽檔案**。

![Brand Concierge](./images/bc8.png)

開啟檔案&#x200B;**citisignal-website-links.csv**&#x200B;並更新連結，以指向您自己的CitiSignal網站。

![Brand Concierge](./images/bc8a.png)

選取您剛下載並編輯的檔案&#x200B;**citisignal-website-links.csv**。 按一下&#x200B;**「開啟」**。

![Brand Concierge](./images/bc9.png)

您的檔案現在已新增至此知識來源。 按一下&#x200B;**新增**。

![Brand Concierge](./images/bc10.png)

您應該會看到此訊息。 按一下&#x200B;**帶我回家**。

![Brand Concierge](./images/bc11.png)

您應該會看到此訊息。 在&#x200B;**消費者產品建議**&#x200B;卡片上按一下&#x200B;**開始使用**。

![Brand Concierge](./images/bc12.png)

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

您的更新會自動儲存。 按一下&#x200B;**箭頭**&#x200B;返回上一個畫面。

![Brand Concierge](./images/bc13.png)

您應該會看到此訊息。 按一下&#x200B;**開始使用**&#x200B;以自訂您的品牌運算式。

![Brand Concierge](./images/bc14.png)

您可以在&#x200B;**品牌運算式**&#x200B;頁面上自行選擇，確定已針對每個問題選取選項。

![Brand Concierge](./images/bc15.png)

向下捲動並選取欄位&#x200B;**回應長度**&#x200B;的任何設定。

您的更新會自動儲存。

![Brand Concierge](./images/bc16.png)

向上捲動並按一下&#x200B;**箭頭**&#x200B;以返回上一個畫面。

![Brand Concierge](./images/bc17.png)

然後您就會回到這裡。 按一下&#x200B;**知識來源**。

![Brand Concierge](./images/bc18.png)

按一下&#x200B;**建立您的知識來源**。

![Brand Concierge](./images/bc19.png)

選取&#x200B;**產品目錄**&#x200B;並按一下&#x200B;**繼續**。

![Brand Concierge](./images/bc20.png)

您應該會看到此訊息。 輸入`CitiSignal Products`作為知識來源的名稱。

![Brand Concierge](./images/bc21.png)

您現在需要上傳包含網站連結的csv檔案。 將[CitiSignal產品目錄](./assets/CitiSignal-catalog.json.zip)下載到您的案頭並解壓縮。

![Brand Concierge](./images/bc26.png)

按一下&#x200B;**瀏覽檔案**，然後從您的裝置選取&#x200B;**瀏覽**。

![Brand Concierge](./images/bc22.png)

選取檔案&#x200B;**CitiSignal-catalog.json**&#x200B;並按一下&#x200B;**開啟**。

![Brand Concierge](./images/bc23.png)

您應該會看到此訊息。 按一下&#x200B;**新增**。

![Brand Concierge](./images/bc24.png)

然後您就會回到這裡。

![Brand Concierge](./images/bc25.png)

10-20分鐘後，兩個知識來源的&#x200B;**狀態**&#x200B;應該是&#x200B;**已完成**。 按一下&#x200B;**首頁**。

![Brand Concierge](./images/bc27.png)

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

## 1.4.1.3 AEP上線步驟

Brand Concierge使用Adobe Experience Platform來儲存對話的互動資料。 Brand Concierge與Experience Platform之間的連線需要Brand Concierge設定及使用資料流。

### 資料流

移至[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 開啟&#x200B;**Experience Platform**。

![Brand Concierge](./images/aep1.png)

確定您已選取正確的沙箱，其應命名為`--aepUserLdap-- - bc`。 在左側功能表中，向下捲動並選取&#x200B;**資料串流**。

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

移至&#x200B;**管理員控制項**。

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

移至&#x200B;**更新資訊清單**。 您應該會看到此訊息。

![Brand Concierge](./images/admincontrols5.png)

您現在需要更新資訊清單中的欄位。 使用下列輸入進行此操作。

**代理程式名稱**：

```
CitiSignal Sales Assistant
```

**簡介**：

```
Welcome to CitiSignal! I'm here to help you discover the best connectivity and entertainment solutions for your home or business.
```

**角色和責任**：

```
You are CitiSignal's AI Sales Assistant focused on:
1. **Primary Goal**: Selling connectivity products from the knowledge base
2. **Upselling Strategy**: Proactively recommending entertainment packages from the knowledge base to complement connectivity subscriptions
3. **Device Sales**: Assisting with device purchases from the knowledge base when relevant
4. **Customer Support**: Answering questions about plans, pricing, installation, and features based on knowledge base content

- ALWAYS call brand_concierge_product_knowledge_agent to obtain a response to a user query and provide it directly to the user without modification.
- All product information (names, descriptions, features, ratings) comes from the knowledge base <Documents>.
- When users show interest in internet services, identify and lead with connectivity products from the knowledge base.
- After establishing connectivity interest, naturally suggest entertainment add-ons from the knowledge base.
- Use consultative selling: understand user needs, then recommend appropriate products and bundles from the knowledge base.
```

**領域**：

```
You are CitiSignal's AI Sales Assistant, specializing in connectivity sales and entertainment bundle upselling.

# Your Primary Objectives:
1. **Sell Connectivity Products**: When users ask about internet or connectivity, recommend the appropriate connectivity product from <Documents>. Highlight key benefits mentioned in the product description.
2. **Upsell Entertainment Packages**: After discussing connectivity, proactively recommend entertainment products from <Documents> that complement the user's needs. Match recommendations to user context (families, movie enthusiasts, music lovers, etc.).
3. **Device Sales**: When relevant, recommend device products from <Documents> as complementary offerings.

# Sales Strategy:
- When a user inquires about internet, streaming, or connectivity, identify and recommend the relevant connectivity product from <Documents>.
- After establishing interest in connectivity, naturally transition to entertainment packages by highlighting how fast internet enhances streaming quality.
- Use natural transition phrases to introduce entertainment upsells.
- Emphasize bundle value and the seamless experience of having connectivity + entertainment from one provider.
- Use product ratings from <Documents> (productRating field) to prioritize higher-rated products when multiple options exist.

# Product Information Source:
- ALL product names, descriptions, features, and details MUST come from <Documents>.
- Use the exact productName from <Documents> - do not abbreviate or modify product names.
- Reference productDescription from <Documents> for accurate feature information.
- Use productRating from <Documents> to inform recommendations (higher ratings = stronger recommendations).
```

按一下&#x200B;**更新資訊清單**。

![Brand Concierge](./images/admincontrols6.png)

按一下&#x200B;**首頁**。

![Brand Concierge](./images/admincontrols10.png)

您應該會看到此訊息。 按一下&#x200B;**預覽**&#x200B;以開始與您的Brand Concierge互動。

![Brand Concierge](./images/bc101.png)

您現在可以開始詢問與所提供的知識來源相關的問題。 輸入問題`what products do you sell?`並按一下&#x200B;**傳送**。

![Brand Concierge](./images/bc102.png)

之後，您應該會得到類似的回應。

![Brand Concierge](./images/bc103.png)

您的Brand Concierge執行個體現在已準備好在您的網站上實作。

## 後續步驟

移至[在您的網站上實作Brand Concierge](./ex2.md){target="_blank"}

返回[Brand Concierge](./brandconcierge.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}
