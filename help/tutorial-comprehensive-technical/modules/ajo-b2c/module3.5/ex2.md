---
title: 使用AJO翻譯服務建立您的行銷活動
description: 使用AJO翻譯服務建立您的行銷活動
kt: 5342
doc-type: tutorial
exl-id: 441b3b6a-74e5-4294-9a30-9c44ea4bbf84
source-git-commit: 7438a1289689c5c3fb3deb398aa9898d7ac26cf8
workflow-type: tm+mt
source-wordcount: '1596'
ht-degree: 0%

---

# 3.5.2建立您的行銷活動

移至[https://experience.adobe.com/](https://experience.adobe.com/)。 按一下&#x200B;**Journey Optimizer**。

![翻譯](./images/ajolp1.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。

![ACOP](./images/ajolp2.png)

>[!NOTE]
>
>如果您已在練習[練習3.1.2.1](./../module3.1/ex2.md)和[練習3.1.2.2](./../module3.1/ex2.md)中建立頁首和頁尾片段，請跳到練習3.5.2.3 「建立Fiber促銷活動」。 不要再建立您的頁首與頁尾片段。

## 3.5.2.1建立您的標頭片段

在左側功能表中，按一下&#x200B;**片段**。 片段是Journey Optimizer中的可重複使用元件，可避免重複並方便未來應影響所有訊息的變更，例如電子郵件訊息中頁首或頁尾的變更。

按一下&#x200B;**建立片段**。

![ACOP](./images/fragm1.png)

輸入名稱`--aepUserLdap-- - CitiSignal - Header`並選取&#x200B;**型別：視覺片段**。 按一下&#x200B;**建立**。

![ACOP](./images/fragm2.png)

您將會看到此訊息。 在左側選單中，您會找到可用來定義電子郵件結構（列和欄）的結構元件。

將&#x200B;**1:1欄**&#x200B;從功能表拖放到畫布中。 這將是標誌影像的預留位置。

![Journey Optimizer](./images/fragm3.png)

接下來，您可以使用內容元件來新增這些區塊中的內容。 將&#x200B;**Image**&#x200B;元件拖放到第一列的第一個儲存格。 按一下&#x200B;**瀏覽**。

![Journey Optimizer](./images/fragm4.png)

然後您會看到快顯視窗開啟，顯示您的AEM Assets Media Library。 前往資料夾&#x200B;**citi-signal-images**，按一下以選取影像&#x200B;**CitiSignal-Logo-White.png**，然後按一下&#x200B;**選取**。

>[!NOTE]
>
>如果您在AEM Assets資料庫中看不到Citi Signal影像，您可以在[這裡](../../../assets/ajo/CitiSignal-images.zip)找到它們。 將它們下載到您的案頭，建立資料夾&#x200B;**citi-signal-images**，然後上傳該資料夾中的所有影像。

![Journey Optimizer](./images/fragm5.png)

您將會看到此訊息。 您的影像是白色的，尚未顯示。 您現在應該定義背景顏色，讓影像正確顯示。 按一下&#x200B;**樣式**，然後按一下&#x200B;**背景顏色**&#x200B;方塊。

![Journey Optimizer](./images/fragm6.png)

在快顯視窗中，將&#x200B;**十六進位**&#x200B;色彩代碼變更為&#x200B;**#8821F4**，然後按一下&#x200B;**100%**&#x200B;欄位來變更焦點。 然後您會看到新顏色套用到影像。

![Journey Optimizer](./images/fragm7.png)

影像目前也有些變大。 讓我們將&#x200B;**寬度**&#x200B;切換器滑動至&#x200B;**40%**，以變更寬度。

![Journey Optimizer](./images/fragm8.png)

您的標頭片段現已準備就緒。 按一下&#x200B;**儲存**，然後按一下箭頭，返回上一個畫面。

![Journey Optimizer](./images/fragm9.png)

您的片段必須先發佈，才能使用。 按一下&#x200B;**Publish**。

![Journey Optimizer](./images/fragm10.png)

幾分鐘後，您會看到片段的狀態已變更為&#x200B;**即時**。
接下來，您應該為電子郵件訊息的頁尾建立新的片段。 按一下**建立片段**。

![Journey Optimizer](./images/fragm11.png)

## 3.5.2.2建立您的頁尾片段

按一下&#x200B;**建立片段**。

![Journey Optimizer](./images/fragm11.png)

輸入名稱`--aepUserLdap-- - CitiSignal - Footer`並選取&#x200B;**型別：視覺片段**。 按一下&#x200B;**建立**。

![Journey Optimizer](./images/fragm12.png)

您將會看到此訊息。 在左側選單中，您會找到可用來定義電子郵件結構（列和欄）的結構元件。

將&#x200B;**1:1欄**&#x200B;從功能表拖放到畫布中。 這會是頁尾內容的預留位置。

![Journey Optimizer](./images/fragm13.png)

接下來，您可以使用內容元件來新增這些區塊中的內容。 將&#x200B;**HTML**&#x200B;元件拖放到第一列的第一個儲存格。 按一下元件以選取它，然後按一下&#x200B;**&lt;/>**&#x200B;圖示以編輯HTML原始程式碼。

![Journey Optimizer](./images/fragm14.png)

您將會看到此訊息。

![Journey Optimizer](./images/fragm15.png)

複製以下HTML程式碼片段，並將其貼到Journey Optimizer的&#x200B;**編輯HTML**&#x200B;視窗中。

```html
<!--[if mso]><table cellpadding="0" cellspacing="0" border="0" width="100%"><tr><td style="text-align: center;" ><![endif]-->
<table style="width: auto; display: inline-block;">
  <tbody>
    <tr class="component-social-container">
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.facebook.com" data-component-social-icon-id="facebook">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://x.com" data-component-social-icon-id="twitter">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.instagram.com" data-component-social-icon-id="instagram">
         
        </a>
      </td>
    </tr>
  </tbody>
</table>
<!--[if mso]></td></tr></table><![endif]-->
```

您就會擁有此專案。 在第7、12和17行，您現在需要使用AEM Assets資料庫中的資產插入影像檔案。

![Journey Optimizer](./images/fragm16.png)

請確定游標位於第7行，然後按一下左側功能表中的&#x200B;**Assets**。 按一下&#x200B;**開啟資產選擇器**&#x200B;以選取您的影像。

![Journey Optimizer](./images/fragm17.png)

開啟資料夾&#x200B;**citi-signal-images**，然後按一下以選取影像&#x200B;**Icon_Facebook.png**。 按一下&#x200B;**選取**。

![Journey Optimizer](./images/fragm18.png)

請確定您的游標位於第12行，然後按一下[開啟資產選取器] **以選取您的影像。**

![Journey Optimizer](./images/fragm19.png)

開啟資料夾&#x200B;**citi-signal-images**，然後按一下以選取影像&#x200B;**Icon_X.png**。 按一下&#x200B;**選取**。

![Journey Optimizer](./images/fragm20.png)

請確定您的游標位於第17行，然後按一下[開啟資產選取器] **以選取您的影像。**

![Journey Optimizer](./images/fragm21.png)

開啟資料夾&#x200B;**citi-signal-images**，然後按一下以選取影像&#x200B;**Icon_Instagram.png**。 按一下&#x200B;**選取**。

![Journey Optimizer](./images/fragm22.png)

您將會看到此訊息。 按一下&#x200B;**儲存**。

![Journey Optimizer](./images/fragm23.png)

然後您會回到編輯器中。 您的圖示尚未顯示，因為背景和影像檔案都是白色的。 若要變更背景顏色，請移至&#x200B;**樣式**&#x200B;並按一下&#x200B;**背景顏色**&#x200B;核取方塊。

![Journey Optimizer](./images/fragm24.png)

將&#x200B;**十六進位**&#x200B;色彩代碼變更為&#x200B;**#000000**。

![Journey Optimizer](./images/fragm25.png)

將對齊方式變更為置中。

![Journey Optimizer](./images/fragm26.png)

讓我們將其他部分新增到頁尾。 將&#x200B;**Image**&#x200B;元件拖放至您剛建立的HTML元件上方。 按一下&#x200B;**瀏覽**。

![Journey Optimizer](./images/fragm27.png)

按一下以選取影像檔&#x200B;**`CitiSignal_Footer_Logo.png`**，然後按一下&#x200B;**選取**。

![Journey Optimizer](./images/fragm28.png)

移至&#x200B;**樣式**&#x200B;並按一下&#x200B;**背景顏色**&#x200B;核取方塊，讓我們再次將其變更為黑色。 將&#x200B;**十六進位**&#x200B;色彩代碼變更為&#x200B;**#000000**。

![Journey Optimizer](./images/fragm29.png)

將寬度變更為&#x200B;**20%**，並確認對齊方式已設定為置中。

![Journey Optimizer](./images/fragm30.png)

接著，將&#x200B;**Text**&#x200B;元件拖放到您建立的HTML元件下。 按一下&#x200B;**瀏覽**。

![Journey Optimizer](./images/fragm31.png)

取代預留位置文字，複製並貼上以下文字。

```
1234 N. South Street, Anywhere, US 12345

Unsubscribe

©2024 CitiSignal, Inc and its affiliates. All rights reserved.
```

將&#x200B;**文字對齊方式**&#x200B;設定為置中。

![Journey Optimizer](./images/fragm32.png)

將&#x200B;**字型顏色**&#x200B;變更為白色，**#FFFFFF**。

![Journey Optimizer](./images/fragm33.png)

將&#x200B;**背景顏色**&#x200B;變更為黑色，**#000000**。

![Journey Optimizer](./images/fragm34.png)

在頁尾中選取文字&#x200B;**取消訂閱**，然後按一下功能表列中的&#x200B;**連結**&#x200B;圖示。 將&#x200B;**Type**&#x200B;設定為&#x200B;**外部選擇退出/取消訂閱**，並將URL設定為&#x200B;**https://aepdemo.net/unsubscribe.html** （取消訂閱連結不允許有空白URL）。

![Journey Optimizer](./images/fragm35.png)

您就會擁有此專案。 您的頁尾現已準備就緒。 按一下&#x200B;**儲存**，然後按一下箭頭返回上一頁。

![Journey Optimizer](./images/fragm36.png)

按一下&#x200B;**Publish**&#x200B;發佈您的頁尾，以便用於電子郵件中。

![Journey Optimizer](./images/fragm37.png)

幾分鐘後，您會看到頁尾的狀態已變更為&#x200B;**即時**。

![Journey Optimizer](./images/fragm38.png)

## 3.5.2.3建立Fiber促銷活動

您現在將建立行銷活動。 上一個練習的事件型歷程仰賴傳入體驗事件或對象進入或退出，以觸發1個特定客戶的歷程，而行銷活動則以唯一內容（例如電子報、一次性促銷活動或一般資訊）鎖定整個對象，或定期傳送類似內容（例如例項生日行銷活動和提醒）。

在功能表中，前往&#x200B;**行銷活動**&#x200B;並按一下&#x200B;**建立行銷活動**。

![Journey Optimizer](./images/oc43.png)

選取&#x200B;**排程 — 行銷**&#x200B;並按一下&#x200B;**建立**。

![Journey Optimizer](./images/campaign1.png)

在行銷活動建立畫面上，設定下列專案：

- **名稱**： `--aepUserLdap-- - CitiSignal Fiber`。
- **描述**： Fiber行銷活動
- **身分型別**：變更為電子郵件

![Journey Optimizer](./images/campaign2.png)

向下捲動至&#x200B;**動作**。 針對&#x200B;**動作**，選取&#x200B;**電子郵件**。

![Journey Optimizer](./images/campaign3.png)

然後，選取現有的&#x200B;**電子郵件組態**。 您將在幾分鐘後編輯內容。

![Journey Optimizer](./images/campaign3a.png)

向上捲動至&#x200B;**對象**。 按一下&#x200B;**選取對象**。

![Journey Optimizer](./images/campaign2b.png)

針對&#x200B;**對象**，選取您在[1.3.3中建立的對象，建立名為`--aepUserLdap-- - CitiSignal Eligible for Fiber`的同盟組合](./../../datacollection/module1.3/ex3.md)。 按一下&#x200B;**儲存**。

![Journey Optimizer](./images/campaign2a.png)

向下捲動至&#x200B;**排程**。 針對&#x200B;**排程**，請選擇&#x200B;**在特定日期和時間**，並設定選擇的時間。

![Journey Optimizer](./images/campaign4.png)

您現在可以開始建立電子郵件訊息本身。 向上捲動，然後按一下&#x200B;**編輯內容**。

![Journey Optimizer](./images/campaign5.png)

您將會看到此訊息。 對於&#x200B;**主旨列**，請使用以下專案：

```
{{profile.person.name.firstName}}, here's your Fiber offer!
```

接著，按一下&#x200B;**編輯電子郵件內文**。

![Journey Optimizer](./images/campaign6.png)

選擇&#x200B;**從頭開始設計**。

![Journey Optimizer](./images/campaign7.png)

您將會看到此訊息。 在左側選單中，您會找到可用來定義電子郵件結構（列和欄）的結構元件。

將&#x200B;**1:1資料行**&#x200B;拖放四次，畫布應該會提供下列結構：

![Journey Optimizer](./images/campaign8.png)

在左側功能表中，移至&#x200B;**片段**。 將您先前建立的標頭拖曳至畫布中的第一個元件。 將您先前建立的頁尾拖曳至畫布中的最後一個元件。

![Journey Optimizer](./images/campaign9.png)

按一下左側功能表中的&#x200B;**+**&#x200B;圖示。 移至&#x200B;**內容**，開始將內容新增至畫布。

![Journey Optimizer](./images/campaign10.png)

將&#x200B;**Text**&#x200B;元件拖放到第二列。

![Journey Optimizer](./images/campaign11.png)

選取該元件中的預設文字&#x200B;**請在此輸入您的文字。**&#x200B;並以下面的文字取代。 將對齊方式變更為&#x200B;**置中對齊**。

```javascript
Hi {{profile.person.name.firstName}}

As a CitiSignal customer, you're in pole position to discover our new Fiber offering. Have a look at the below offer and update your contract!

Stay connected.
```

![Journey Optimizer](./images/campaign12.png)

將&#x200B;**Image**&#x200B;元件拖放至第三列。 按一下&#x200B;**瀏覽**。

![Journey Optimizer](./images/campaign13.png)

選取您先前在模組中建立的AEM Assets存放庫。 該存放庫應命名為`--aepUserLdap-- - Citi Signal dev`。 按一下以開啟資料夾`--aepUserLdap-- - Workfront Assets`。

![Journey Optimizer](./images/campaign15a.png)

按一下以選取影像&#x200B;**2048x2048_buynow.png**，然後按一下&#x200B;**選取**。

![Journey Optimizer](./images/campaign14.png)

您的基本電子報電子郵件現已準備就緒。 按一下&#x200B;**儲存**。

![Journey Optimizer](./images/ready.png)

按一下左上角主旨列文字旁的&#x200B;**箭頭**，返回行銷活動控制面板。

![Journey Optimizer](./images/campaign19.png)

按一下&#x200B;**檢閱以啟動**。

![Journey Optimizer](./images/campaign20.png)

您可能會收到此錯誤。 如果是這種情況，您可能需要等候最多24小時，直到評估對象為止，然後嘗試再次啟用您的行銷活動。 您也可能需要更新行銷活動的排程，以便稍後執行。

![Journey Optimizer](./images/campaign21a.png)

按一下&#x200B;**啟動**。

![Journey Optimizer](./images/campaign21.png)

啟動後，您的行銷活動將排程執行。

![Journey Optimizer](./images/campaign22.png)

您已完成此練習。

## 後續步驟

移至[3.5.3新增語言至您的電子郵件](./ex3.md)

返回[模組3.5](./ajotranslationsvcs.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}
