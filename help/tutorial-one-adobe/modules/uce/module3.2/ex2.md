---
title: 使用AJO翻譯服務建立您的行銷活動
description: 使用AJO翻譯服務建立您的行銷活動
kt: 5342
doc-type: tutorial
source-git-commit: 3b3c62499bfed86ab13a657a816424879cab4f42
workflow-type: tm+mt
source-wordcount: '1644'
ht-degree: 1%

---

# 3.2.2建立您的行銷活動

移至[https://experience.adobe.com/](https://experience.adobe.com/)。 按一下&#x200B;**Journey Optimizer**。

![翻譯](./images/ajolp1.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。

![ACOP](./images/ajolp2.png)

## 3.2.2.1建立您的標頭片段

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

## 3.2.2.2建立您的頁尾片段

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

## 3.2.2.3建立Fiber歷程

您現在將建立歷程。 不同於仰賴傳入體驗事件的事件型歷程，此歷程將專注於讀取現有對象，並將透過電子報、一次性促銷活動或特定行銷活動等獨特內容，一次性鎖定整個對象。

在功能表中，前往&#x200B;**歷程**&#x200B;並按一下&#x200B;**建立歷程**。

![Journey Optimizer](./images/campaign1.png)

在歷程建立畫面上，將&#x200B;**名稱**&#x200B;設定為`--aepUserLdap-- - Fiber`。 按一下&#x200B;**儲存**。

![Journey Optimizer](./images/campaign2.png)

在&#x200B;**協調流程**&#x200B;功能表中，將&#x200B;**讀取對象**&#x200B;物件拖放到畫布上。

![Journey Optimizer](./images/campaign2a.png)

按一下&#x200B;**編輯**&#x200B;圖示以選取對象。

![Journey Optimizer](./images/campaign2b.png)

針對&#x200B;**對象**，選取您在上一步建立的對象`--aepUserLdap-- - CitiSignal Eligible for Fiber`。 按一下&#x200B;**儲存**。

![Journey Optimizer](./images/campaign2c.png)

您應該會看到此訊息。 將&#x200B;**名稱空間**&#x200B;設定為&#x200B;**電子郵件**。 按一下&#x200B;**儲存**。

![Journey Optimizer](./images/campaign3.png)

在&#x200B;**動作**&#x200B;底下，將&#x200B;**電子郵件**&#x200B;動作拖放到畫布上。

![Journey Optimizer](./images/campaign4.png)

將&#x200B;**類別**&#x200B;設定為&#x200B;**行銷**，並為&#x200B;**電子郵件**&#x200B;選取&#x200B;**設定**。 按一下&#x200B;**編輯內容**。

![Journey Optimizer](./images/campaign5.png)

您將會看到此訊息。 按一下&#x200B;**主旨列**&#x200B;旁的&#x200B;**編輯**&#x200B;圖示。

![Journey Optimizer](./images/campaign6.png)

將主旨列設為：

```
{{profile.person.name.firstName}}, here's your Fiber offer!
```

按一下&#x200B;**儲存**。

![Journey Optimizer](./images/campaign5a.png)

您應該會看到此訊息。 接著，按一下&#x200B;**編輯電子郵件內文**。

![Journey Optimizer](./images/campaign5b.png)

選擇&#x200B;**從頭開始設計**。

![Journey Optimizer](./images/campaign7.png)

您將會看到此訊息。 在左側選單中，您會找到可用來定義電子郵件結構（列和欄）的結構元件。

將&#x200B;**1:1資料行**&#x200B;拖放至畫布上2次，您應該會看到此結構：

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

As a CitiSignal member, you're part of a dynamic community that's constantly evolving to meet your needs. We're committed to delivering innovative solutions that enhance your digital lifestyle and keep you ahead of the curve.

Stay connected.
```

![Journey Optimizer](./images/campaign12.png)

將&#x200B;**Image**&#x200B;元件拖放至第3和第4列。 按一下第3列的&#x200B;**瀏覽**。

![Journey Optimizer](./images/campaign13.png)

開啟資料夾&#x200B;**citi-signal-images**，按一下以選取影像&#x200B;**Offer_AirPods.jpg**，然後按一下&#x200B;**選取**。

![Journey Optimizer](./images/campaign14.png)

在第4列的影像預留位置上按一下&#x200B;**瀏覽**。

![Journey Optimizer](./images/campaign15.png)

開啟資料夾&#x200B;**citi-signal-images**，按一下以選取影像&#x200B;**Offer_Phone.jpg**，然後按一下&#x200B;**選取**。

![Journey Optimizer](./images/campaign16.png)

將&#x200B;**Text**&#x200B;元件拖放至第3和第4列。

![Journey Optimizer](./images/campaign17.png)

在第3列的元件中選取預設文字&#x200B;**請在此輸入您的文字。**&#x200B;並以下面的文字取代。

```javascript
Get AirPods for free:

Experience seamless connectivity like never before with CitiSignal. Sign up for select premium plans and receive a complimentary pair of Apple AirPods. Stay connected in style with our unbeatable offer.
```

在第4列&#x200B;**的元件中選取預設文字。請在此輸入您的文字。**&#x200B;並以下面的文字取代。

```javascript
We'll pay off your phone:

Make the switch to CitiSignal and say goodbye to phone payments! Switching to CitiSignal has never been more rewarding. Say farewell to hefty phone bills as we help pay off your phone, up to 800$!
```

![Journey Optimizer](./images/campaign18.png)

您的基本電子報電子郵件現已準備就緒。 按一下&#x200B;**儲存**。

按一下左上角主旨列文字旁的&#x200B;**箭頭**，返回行銷活動控制面板。

![Journey Optimizer](./images/campaign19.png)

按一下&#x200B;**檢閱以啟動**。

![Journey Optimizer](./images/campaign20.png)

您可能會收到此錯誤。 如果是這種情況，您可能需要等候最多24小時，直到評估對象為止，然後嘗試再次啟用您的行銷活動。 您也可能需要更新行銷活動的排程，以便稍後執行。

按一下&#x200B;**啟動**。

![Journey Optimizer](./images/campaign21.png)

啟用後，您的行銷活動將排程執行。

![Journey Optimizer](./images/campaign22.png)

您的行銷活動現在已啟用。 您的電子報電子郵件訊息將會依照您在排程中的定義傳送，且您的行銷活動會在傳送最後一封電子郵件後立即停止。

您也應收到您先前建立示範設定檔所用電子郵件地址的電子郵件。

![Journey Optimizer](./images/campaign23.png)

您已完成此練習。

## 後續步驟

移至[3.2.3 ...](./ex3.md)

返回[模組3.2](./ajotranslationsvcs.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}
