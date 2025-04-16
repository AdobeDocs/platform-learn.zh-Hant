---
title: Frame.io和Workfront Fusion
description: Frame.io和Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 37de6ceb-833e-4e75-9201-88bddd38a817
source-git-commit: d47b6da364fc6ffdb0c541197edc8a9d2fd34e42
workflow-type: tm+mt
source-wordcount: '2674'
ht-degree: 0%

---

# 1.2.5 Frame.io和Workfront Fusion

在上一個練習中，您設定了案例`--aepUserLdap-- - Firefly + Photoshop`並設定了傳入webhook以觸發案例，以及在案例成功完成時設定webhook回應。 然後您使用Postman來觸發該情境。 Postman是絕佳的測試工具，但在實際商業案例中，商業使用者不會使用Postman來觸發案例。 相反地，他們會使用另一個應用程式，並期望其他應用程式在Workfront Fusion中啟動情境。 在本練習中，您將會使用Frame.io做的事情正是如此。

>[!NOTE]
>
>為了成功完成此練習，您必須是您Frame.io帳戶中的管理員使用者。 以下練習是針對Frame.io V3建立的，並將在稍後階段針對Frame.io V4更新。

## 1.2.5.1正在存取Frame.io

移至[https://app.frame.io/projects](https://app.frame.io/projects)。

按一下&#x200B;**+圖示**，在Frame.io中建立您自己的專案。

![框架IO](./images/frame1.png)

輸入名稱`--aepUserLdap--`並按一下&#x200B;**建立專案**。

![框架IO](./images/frame2.png)

然後，您將在左側選單中看到您的專案。
在先前的練習中，您將[citisignal-fiber.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"}下載到您的案頭。 選取該檔案，然後將其拖放到剛建立的專案資料夾中。

![框架IO](./images/frame3.png)

## 1.2.5.2 Workfront Fusion和Frame.io

在上一個練習中，您建立了案例`--aepUserLdap-- - Firefly + Photoshop`，該案例以自訂webhook開始，以webhook回應結束。 接著，我們使用Postman測試了Webhook的使用情況，但很顯然，這種情況的要點是由外部應用程式呼叫。 如前所述，Frame.io將是該練習，但在Frame.io和`--aepUserLdap-- - Firefly + Photoshop`之間需要另一個Workfront Fusion案例。 您現在將設定該案例。

移至[https://experience.adobe.com/](https://experience.adobe.com/)。 開啟&#x200B;**Workfront Fusion**。

![WF Fusion](./images/wffusion1.png)

在左側功能表中，移至&#x200B;**案例**&#x200B;並選取您的資料夾`--aepUserLdap--`。 按一下&#x200B;**建立新情境**。

![框架IO](./images/frame4.png)

使用名稱`--aepUserLdap-- - Frame IO Custom Action`。

![框架IO](./images/frame5.png)

按一下畫布上的&#x200B;**問號物件**。 在搜尋方塊中輸入文字`webhook`，然後按一下&#x200B;**Webhooks**。

![框架IO](./images/frame6.png)

按一下&#x200B;**自訂webhook**。

![框架IO](./images/frame7.png)

按一下&#x200B;**[新增**]以建立新的webhook url。

![框架IO](./images/frame8.png)

對於&#x200B;**Webhook名稱**，請使用`--aepUserLdap-- - Frame IO Custom Action Webhook`。 按一下&#x200B;**儲存**。

![框架IO](./images/frame9.png)

您應該會看到此訊息。 將此熒幕保持開啟且未觸控，因為您會在下一個步驟中需要它。 您必須按一下&#x200B;**將地址複製到剪貼簿**，在下一個步驟中複製webhook URL。

![框架IO](./images/frame10.png)

移至[https://developer.frame.io/](https://developer.frame.io/)。 按一下&#x200B;**開發人員工具**，然後選擇&#x200B;**自訂動作**。

![框架IO](./images/frame11.png)

按一下&#x200B;**建立自訂動作**。

![框架IO](./images/frame12.png)

輸入下列值：

- **名稱**：使用`--aepUserLdap-- - Frame IO Custom Action Fusion`
- **描述**：使用`--aepUserLdap-- - Frame IO Custom Action Fusion`
- **事件**：使用`fusion.tutorial`。
- **URL**：輸入您剛才在Workfront Fusion中建立的webhook的URL
- **團隊**：選取適當的Frame.io團隊，在此案例中為&#x200B;**一個Adobe教學課程**。

按一下&#x200B;**提交**。

![框架IO](./images/frame15.png)

您應該會看到此訊息。

![框架IO](./images/frame14.png)

返回[https://app.frame.io/projects](https://app.frame.io/projects)。 重新整理頁面。

![框架IO](./images/frame16.png)

重新整理頁面後，按一下資產&#x200B;**citisignal-fiber.psd**&#x200B;上的3個點&#x200B;**...**。 之後，您應該會看到先前建立的自訂動作出現在顯示的功能表中。 按一下自訂動作`--aepUserLdap-- - Frame IO Custom Action Fusion`。

![框架IO](./images/frame17.png)

您應該會看到類似的&#x200B;**成功！**&#x200B;快顯視窗。 此快顯視窗是Frame.io與Workfront Fusion之間通訊的結果。

![框架IO](./images/frame18.png)

將畫面變更回Workfront Fusion。 您現在應該會看到&#x200B;**已成功判定**&#x200B;出現在自訂Webhook物件上。 按一下&#x200B;**「確定」**。

![框架IO](./images/frame19.png)

按一下&#x200B;**執行一次**&#x200B;以啟用測試模式，然後再次測試與Frame.io的通訊。

![框架IO](./images/frame20.png)

返回Frame.io，然後再次按一下自訂動作`--aepUserLdap-- - Frame IO Custom Action Fusion`。

![框架IO](./images/frame21.png)

將畫面切換回Workfront Fusion。 您現在應該會看到綠色核取記號，以及顯示&#x200B;**1**&#x200B;的泡泡。 按一下泡泡圖示以檢視詳細資訊。

![框架IO](./images/frame22.png)

泡泡圖的詳細檢視畫面會顯示從Frame.io收到的資料。 您應該會看到各種ID。例如，欄位&#x200B;**resource.id**&#x200B;會顯示資產&#x200B;**citisignal-fiber.psd**&#x200B;之Frame.io中的唯一ID。

![框架IO](./images/frame23.png)

現在，Frame.io與Workfront Fusion之間的通訊已建立，您可以繼續設定。

## 1.2.5.3提供對Frame.io的自訂表單回應

在Frame.io中叫用自訂動作時，Frame.io預期會收到來自Workfront Fusion的回應。 如果您回想一下您在上一個練習中建立的情境，則需要多個變數來更新標準Photoshop PSD檔案。 這些變數會在您使用的裝載中定義：

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

因此，為了成功執行案例`--aepUserLdap-- - Firefly + Photoshop`，需要&#x200B;**prompt**、**cta**、**button**&#x200B;和&#x200B;**psdTemplate**&#x200B;等欄位。

前3個欄位(**prompt**、**cta**、**button**)需要使用者輸入，當使用者叫用自訂動作時，需要在Frame.io中收集這些輸入。 因此，在Workfront Fusion中首先需要做的就是檢查這些變數是否可用，如果不可用，Workfront Fusion應回傳給Frame.io，要求輸入這些變數。 要達到此目的，請在Frame.io中使用表單。

返回Workfront Fusion並開啟您的案例`--aepUserLdap-- - Frame IO Custom Action`。 將游標暫留在&#x200B;**自訂webhook**&#x200B;物件上，然後按一下&#x200B;**+**&#x200B;圖示以新增另一個模組。

![框架IO](./images/frame24.png)

搜尋`Flow Control`並按一下&#x200B;**流量控制**。

![框架IO](./images/frame25.png)

按一下以選取&#x200B;**路由器**。

![框架IO](./images/frame26.png)

您應該會看到此訊息。

![框架IO](./images/frame27.png)

按一下&#x200B;**？**&#x200B;物件，然後按一下以選取&#x200B;**Webhooks**。

![框架IO](./images/frame28.png)

選取&#x200B;**Webhook回應**。

![框架IO](./images/frame29.png)

您應該會看到此訊息。

![框架IO](./images/frame30.png)

複製下列JSON程式碼並將其貼到欄位&#x200B;**內文**。


```json
{
  "title": "What do you want Firefly to generate?",
  "description": "Enter your Firefly prompt.",
  "fields": [
    {
      "type": "text",
      "label": "Prompt",
      "name": "Prompt",
      "value": ""
    },
    {
      "type": "text",
      "label": "CTA Text",
      "name": "CTA Text",
      "value": ""
    },
    {
      "type": "text",
      "label": "Button Text",
      "name": "Button Text",
      "value": ""
    }
  ]
}
```

按一下圖示以清理和美化JSON程式碼。 然後，按一下&#x200B;**確定**。

![框架IO](./images/frame31.png)

按一下[儲存]儲存變更。****

![框架IO](./images/frame32.png)

接下來，您需要設定篩選器，以確保此情境路徑僅在沒有提示可用時執行。 按一下&#x200B;**扳手**&#x200B;圖示，然後選取&#x200B;**設定篩選器**。

![框架IO](./images/frame33.png)

設定下列欄位：

- **標籤**：使用`Prompt isn't available`。
- **條件**：使用`{{1.data.Prompt}}`。
- **基本運運算元**：選取&#x200B;**不存在**。

>[!NOTE]
>
>可以使用下列語法手動指定Workfront Fusion中的變數： `{{1.data.Prompt}}`。 變數中的數字會參考情境中的模組。 在此範例中，您可以看到情境中的第一個模組稱為&#x200B;**Webhooks**，其序號為&#x200B;**1**。 這表示變數`{{1.data.Prompt}}`將會從序號為1的模組存取欄位&#x200B;**data.Prompt**。 序號有時可能不同，因此在複製/貼上這類變數時請務必注意，並務必確認所使用的序號是否正確。

按一下&#x200B;**「確定」**。

![框架IO](./images/frame34.png)

您應該會看到此訊息。 先按一下&#x200B;**儲存**&#x200B;圖示，然後按一下&#x200B;**執行一次**&#x200B;以測試您的情境。

![框架IO](./images/frame35.png)

您應該會看到此訊息。

![框架IO](./images/frame36.png)

返回Frame.io，然後再次按一下資產&#x200B;**citisignal-fiber.psd**&#x200B;上的自訂動作`--aepUserLdap-- - Frame IO Custom Action Fusion`。

![框架IO](./images/frame37.png)

您現在應該會在Frame.io中看到提示。 尚未填寫欄位且尚未提交表單。 系統會根據您剛設定的Workfront Fusion回應顯示此提示。

![框架IO](./images/frame38.png)

切換回Workfront Fusion，然後按一下&#x200B;**Webhook回應**&#x200B;模組上的泡泡。 您會在&#x200B;**OUTPUT**&#x200B;下看到包含表單之JSON裝載的主體。 再按一下&#x200B;**執行一次**。

![框架IO](./images/frame40.png)

您應該會再次看到此專案。

![框架IO](./images/frame41.png)

返回Frame.io並按指示填寫欄位。 按一下&#x200B;**提交**。

![框架IO](./images/frame39.png)

您應該會看到&#x200B;**成功！**&#x200B;快顯視窗。

![框架IO](./images/frame42.png)

切換回Workfront Fusion，然後按一下&#x200B;**自訂webhook**&#x200B;模組上的泡泡。 在作業1的&#x200B;**輸出**&#x200B;下，您現在可以看到新的&#x200B;**資料**&#x200B;物件，其中包含&#x200B;**按鈕文字**、**CTA文字**&#x200B;和&#x200B;**提示字元**&#x200B;等欄位。 有了這些可在您的情境中使用的使用者輸入變數，您就有足夠的空間繼續您的設定。

![框架IO](./images/frame43.png)

## 1.2.5.4從Frame.io擷取檔案位置

如前所述，此情境需要&#x200B;**prompt**、**cta**、**button**&#x200B;和&#x200B;**psdTemplate**&#x200B;等欄位才能運作。 前3個欄位現在已可供使用，但仍遺失要使用的&#x200B;**psdTemplate**。 **psdTemplate**&#x200B;現在會參考Frame.io位置，因為檔案&#x200B;**citisignal-fiber.psd**&#x200B;是在Frame.io中託管。 為了擷取該檔案的位置，您需要在Workfront Fusion中設定和使用Frame.io連線。

返回Workfront Fusion並開啟您的案例`--aepUserLdap-- - Frame IO Custom Action`。 將游標暫留在&#x200B;**上？**&#x200B;模組，按一下&#x200B;**+**&#x200B;圖示以新增另一個模組並搜尋`frame`。 按一下&#x200B;**Frame.io**。

![框架IO](./images/frame44.png)

按一下&#x200B;**Frame.io （舊版）**。

![框架IO](./images/frame45.png)

按一下&#x200B;**取得資產**。

![框架IO](./images/frame46.png)

若要使用Frame.io連線，您必須先進行設定。 按一下&#x200B;**[新增**]即可執行這個動作。

![框架IO](./images/frame47.png)

開啟&#x200B;**連線型別**&#x200B;下拉式清單。

![框架IO](./images/frame48.png)

選取&#x200B;**Frame.io API Key**&#x200B;並輸入名稱`--aepUserLdap-- - Frame.io Token`。

![框架IO](./images/frame49.png)

若要取得API Token，請移至[https://developer.frame.io/](https://developer.frame.io/)。 按一下&#x200B;**開發人員工具**，然後選擇&#x200B;**代號**。

![框架IO](./images/frame50.png)

按一下&#x200B;**建立Token**。

![框架IO](./images/frame51.png)

使用&#x200B;**描述** `--aepUserLdap-- - Frame.io Token`並按一下&#x200B;**選取所有領域**。

![框架IO](./images/frame52.png)

向下捲動並按一下&#x200B;**提交**。

![框架IO](./images/frame53.png)

您的權杖現已建立。 按一下「複製&#x200B;****」，將其複製到剪貼簿。

![框架IO](./images/frame54.png)

返回Workfront Fusion中的案例。 將權杖貼到欄位&#x200B;**您的Frame.io API金鑰**&#x200B;中。 按一下&#x200B;**確定**。 您的連線現在將由Workfront Fusion測試。

![框架IO](./images/frame55.png)

如果連線測試成功，就會自動顯示在&#x200B;**連線**&#x200B;下。 您現在已成功連線，而且您必須完成設定，才能從Frame.io取得所有資產詳細資訊，包括檔案位置。 若要這麼做，您必須提供&#x200B;**資產識別碼**。

![框架IO](./images/frame56.png)

**資產ID**&#x200B;由Frame.io共用至Workfront Fusion，做為初始&#x200B;**自訂webhook**&#x200B;通訊的一部分，可以在&#x200B;**resource.id**&#x200B;欄位下找到。 選取&#x200B;**resource.id**&#x200B;並按一下&#x200B;**確定**。

![框架IO](./images/frame57.png)

您現在應該會看到此訊息。 儲存您的變更，然後按一下&#x200B;**執行一次**&#x200B;以測試您的情境。

![框架IO](./images/frame58.png)

返回Frame.io，然後再次按一下資產&#x200B;**citisignal-fiber.psd**&#x200B;上的自訂動作`--aepUserLdap-- - Frame IO Custom Action Fusion`。

![框架IO](./images/frame37.png)

您現在應該會在Frame.io中看到提示。 尚未填寫欄位且尚未提交表單。 系統會根據您剛設定的Workfront Fusion回應顯示此提示。

![框架IO](./images/frame38.png)

切換回Workfront Fusion。 再按一下&#x200B;**執行一次**。

![框架IO](./images/frame59.png)

返回Frame.io並按指示填寫欄位。 按一下&#x200B;**提交**。

![框架IO](./images/frame39.png)

切換回Workfront Fusion，然後按一下&#x200B;**Frame.io — 取得資產**&#x200B;模組。

![框架IO](./images/frame60.png)

您現在可以看到許多有關特定資產&#x200B;**citisignal-fiber.psd**&#x200B;的中繼資料。

![框架IO](./images/frame61.png)

此使用案例所需的特定資訊是檔案&#x200B;**citisignal-fiber.psd**&#x200B;的位置URL，您可以向下捲動至&#x200B;**Original**&#x200B;欄位來找到該檔案。

![框架IO](./images/frame62.png)

您現在有此情境運作所需的所有欄位（**prompt**、**cta**、**button**&#x200B;和&#x200B;**psdTemplate**）可供使用。

## 1.2.5.5叫用Workfront情境

在上一個練習中，您已設定情境`--aepUserLdap-- - Firefly + Photoshop`。 您現在需要對該情境進行微幅變更。

在另一個索引標籤中開啟案例`--aepUserLdap-- - Firefly + Photoshop`，然後按一下第一個&#x200B;**Adobe Photoshop — 套用PSD編輯**&#x200B;模組。 您現在應該會看到輸入檔案已設定為使用Microsoft Azure中的動態位置。 基於此使用案例，輸入檔案不再儲存在Microsoft Azure中，而是使用Frame.io儲存，因此您需要變更這些設定。

![框架IO](./images/frame63.png)

將&#x200B;**儲存體**&#x200B;變更為&#x200B;**外部**，並變更&#x200B;**檔案位置**&#x200B;以僅使用從傳入&#x200B;**自訂webhook**&#x200B;模組取得的&#x200B;**psdTemplate**&#x200B;變數。 按一下[確定]****，然後按一下[儲存]****&#x200B;儲存您的變更。

![框架IO](./images/frame64.png)

按一下&#x200B;**自訂webhook**&#x200B;模組，然後按一下&#x200B;**將地址複製到剪貼簿**。 您需要複製URL，因為您需要在其他案例中使用它。

![框架IO](./images/frame65.png)

返回您的案例`--aepUserLdap-- - Frame IO Custom Action`。 將游標暫留在&#x200B;**Frame.io — 取得資產**&#x200B;模組，然後按一下&#x200B;**+**&#x200B;圖示。

![框架IO](./images/frame66.png)

輸入`http`，然後按一下&#x200B;**HTTP**。

![框架IO](./images/frame67.png)

選取&#x200B;**提出要求**。

![框架IO](./images/frame68.png)

在欄位&#x200B;**URL**&#x200B;中貼上自訂webhook的URL。 將&#x200B;**方法**&#x200B;設定為POST**。

![框架IO](./images/frame69.png)

將&#x200B;**主體型別**&#x200B;設定為&#x200B;**原始**，並將&#x200B;**內容型別**&#x200B;設定為&#x200B;**JSON (application/json)**。
將下列JSON裝載貼到欄位**要求內容**&#x200B;中，並啟用&#x200B;**剖析回應**&#x200B;的核取方塊。

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

您現在已設定靜態裝載，但需要使用先前收集的變數將其變成動態。

![框架IO](./images/frame70.png)

針對欄位&#x200B;**psdTemplate**，將靜態變數&#x200B;**citisignal-fiber.psd**&#x200B;取代為變數&#x200B;**Original**。

![框架IO](./images/frame71.png)

對於欄位&#x200B;**prompt**、**cta**&#x200B;和&#x200B;**button**，請以Frame.io傳入的webhook要求插入情境中的動態變數來取代靜態變數，這些欄位是&#x200B;**data.Prompt**、**data.CTA Text**&#x200B;和&#x200B;**data.Button Text**。

按一下&#x200B;**「確定」**。

![框架IO](./images/frame72.png)

按一下[儲存]儲存變更。****

![框架IO](./images/frame73.png)

## 1.2.5.6在Frame.io中儲存新資產

叫用另一個Workfront Fusion案例後，即可使用新的Photoshop PSD範本。 該PSD檔案需要儲存回Frame.io，這是此情境中的最後一個步驟。

將游標暫留在&#x200B;**HTTP上 — 提出要求**&#x200B;模組並按一下&#x200B;**+**&#x200B;圖示。

![框架IO](./images/frame74.png)

選取&#x200B;**Frame.io （舊版）**。

![框架IO](./images/frame75.png)

選取&#x200B;**建立資產**。

![框架IO](./images/frame76.png)

系統將會自動選取您的Frame.io連線。

![框架IO](./images/frame77.png)

選取下列選項：

- **團隊識別碼**：選取適當的團隊識別碼，在此案例中為`One Adobe Tutorial`。
- **專案識別碼**：使用`--aepUserLdap--`。
- **資料夾識別碼**：使用`root`。
- **型別**：使用`File`。

![框架IO](./images/frame78.png)

針對欄位&#x200B;**Name**，您可以使用變數，例如&#x200B;**timestamp** （或將其變更為對您更有意義的內容）。 您可以在&#x200B;**日期與時間**&#x200B;標籤下找到預先定義的變數&#x200B;**timestamp**。

![框架IO](./images/frame79.png)

對於欄位&#x200B;**Source URL**，請使用以下JSON程式碼。

```json
{{6.data.newPsdTemplate}}
```

>[!NOTE]
>
>可以使用下列語法手動指定Workfront Fusion中的變數： `{{6.data.newPsdTemplate}}`。 變數中的數字會參考情境中的模組。 在此範例中，您可以看到情境中的第六個模組稱為&#x200B;**HTTP — 提出要求**，其序號為&#x200B;**6**。 這表示變數`{{6.data.newPsdTemplate}}`將會從序號為6的模組存取欄位&#x200B;**data.newPsdTemplate**。 序號有時可能不同，因此在複製/貼上這類變數時請務必注意，並務必確認所使用的序號是否正確。

按一下&#x200B;**「確定」**。

![框架IO](./images/frame80.png)

按一下[儲存]儲存變更。****

![框架IO](./images/frame81.png)

最後，您需要設定篩選器，以確保此情境路徑僅在提示可用時執行。 按一下&#x200B;**扳手**&#x200B;圖示，然後選取&#x200B;**設定篩選器**。

![框架IO](./images/frame82.png)

設定下列欄位：

- **標籤**：使用`Prompt is available`。
- **條件**：使用`{{1.data.Prompt}}`。
- **基本運運算元**：選取&#x200B;**存在**。

>[!NOTE]
>
>可以使用下列語法手動指定Workfront Fusion中的變數： `{{1.data.Prompt}}`。 變數中的數字會參考情境中的模組。 在此範例中，您可以看到情境中的第一個模組稱為&#x200B;**Webhooks**，其序號為&#x200B;**1**。 這表示變數`{{1.data.Prompt}}`將會從序號為1的模組存取欄位&#x200B;**data.Prompt**。 序號有時可能不同，因此在複製/貼上這類變數時請務必注意，並務必確認所使用的序號是否正確。

按一下&#x200B;**「確定」**。

![框架IO](./images/frame83.png)

按一下[儲存]儲存變更。****

![框架IO](./images/frame84.png)

## 1.2.5.7測試您的端對端使用案例

在您的情境`--aepUserLdap-- - Frame IO Custom Action`中按一下&#x200B;**執行一次**。

![框架IO](./images/frame85.png)

返回Frame.io，然後再次按一下資產&#x200B;**citisignal-fiber.psd**&#x200B;上的自訂動作`--aepUserLdap-- - Frame IO Custom Action Fusion`。

![框架IO](./images/frame37.png)

您現在應該會在Frame.io中看到提示。 尚未填寫欄位且尚未提交表單。 系統會根據您剛設定的Workfront Fusion回應顯示此提示。

![框架IO](./images/frame38.png)

切換回Workfront Fusion。 在您的情境`--aepUserLdap-- - Frame IO Custom Action`中按一下&#x200B;**執行一次**。

![框架IO](./images/frame86.png)

在Workfront Fusion中，開啟案例`--aepUserLdap-- - Firefly + Photoshop`，然後按一下該案例中的&#x200B;**執行一次**。

![框架IO](./images/frame87.png)

返回Frame.io並按指示填寫欄位。 按一下&#x200B;**提交**。

![框架IO](./images/frame39.png)

1-2分鐘後，您應該會在Frame.io中看到自動顯示的新資產。 按兩下新資產以將其開啟。

![框架IO](./images/frame88.png)

現在，您可以清楚看到所有使用者輸入變數均已自動套用。

![框架IO](./images/frame89.png)

您現在已成功完成此練習。

## 後續步驟

移至[1.2.6 Frame.io to Fusion to AEM Assets](./ex6.md){target="_blank"}

返回[使用Workfront Fusion進行Creative工作流程自動化](./automation.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}

