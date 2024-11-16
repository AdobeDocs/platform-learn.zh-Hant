---
title: Adobe Journey Optimizer — 設定觸發式歷程 — 訂單確認
description: 在本節中，您將設定觸發式歷程 — 訂購確認
kt: 5342
doc-type: tutorial
exl-id: b9d9b357-08d1-4f65-9e0b-46224d035602
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 0%

---

# 3.4.1設定觸發式歷程 — 訂購確認

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。 若要從一個沙箱變更為另一個沙箱，請按一下&#x200B;**PRODUCTION Prod (VA7)**，然後從清單中選取沙箱。 在此範例中，沙箱名為&#x200B;**AEP Enablement FY22**。 然後您就會進入沙箱`--aepSandboxName--`的&#x200B;**首頁**&#x200B;檢視。

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

## 3.4.1.1建立您的活動

在功能表中，移至&#x200B;**組態**&#x200B;並按一下&#x200B;**事件**&#x200B;底下的&#x200B;**管理**。

![Journey Optimizer](./images/oc30.png)

在&#x200B;**事件**&#x200B;畫面上，您會看到類似此的檢視。 按一下&#x200B;**建立事件**。

![Journey Optimizer](./images/oc31.png)

然後您會看到空白的事件設定。

![Journey Optimizer](./images/oc32.png)

首先，請為事件命名如下： `--aepUserLdap--PurchaseEvent`，然後新增如下描述： `Purchase Event`。

![Journey Optimizer](./images/oc34.png)

下一個是&#x200B;**事件型別**&#x200B;選項。 選取&#x200B;**單一**。

![Journey Optimizer](./images/eventidtype1.png)

下一個是&#x200B;**事件ID型別**&#x200B;選擇。 選取&#x200B;**系統產生**

![Journey Optimizer](./images/eventidtype.png)

接下來是「結構描述」選項。 已針對此練習準備結構描述。 請使用結構描述`Demo System - Event Schema for Website (Global v1.1) v.1`。

![Journey Optimizer](./images/oc35.png)

選取結構描述後，您將會在&#x200B;**裝載**&#x200B;區段中看到一些正在選取的欄位。 按一下&#x200B;**編輯/鉛筆**&#x200B;圖示以新增其他欄位至此事件。

![Journey Optimizer](./images/oc36.png)

然後您會看到此快顯視窗。 您現在需要核取其他核取方塊，才能在觸發此事件時存取其他資料。

![Journey Optimizer](./images/oc37.png)

首先，核取行`--aepTenantId--`上的核取方塊。

![Journey Optimizer](./images/oc38.png)

接下來，向下捲動並勾選`productListItems`行上的核取方塊。

![Journey Optimizer](./images/oc39.png)

接下來，向下捲動並勾選`commerce`行上的核取方塊。

![Journey Optimizer](./images/oc391.png)

接著，按一下&#x200B;**確定**。

之後，您會看到其他欄位已新增至事件。 按一下&#x200B;**儲存**。

![Journey Optimizer](./images/oc40.png)

您的新活動會隨即共用，而您現在將在可用活動清單中看到您的活動。

再次按一下您的事件以再次開啟&#x200B;**編輯事件**畫面。
再次將游標暫留在**承載**&#x200B;欄位上，可再次看到3個圖示。 按一下&#x200B;**檢視裝載**&#x200B;圖示。

![Journey Optimizer](./images/oc41.png)

您現在將看到預期裝載的範例。 您的事件具有獨特的協調流程eventID，您可以在該承載中向下捲動直到看到`_experience.campaign.orchestration.eventID`為止。

![Journey Optimizer](./images/oc42.png)

事件ID需要傳送至Adobe Journey Optimizer，才能觸發您將在下一個步驟中建立的歷程。 記下此eventID，因為您會在後續步驟中用到它。
`"eventID": "ef6dd943c94fe1b4763c098ccd1772344662f2a9f614513106cb5ada8be36857"`

按一下&#x200B;**確定**，然後按一下&#x200B;**取消**。

您的事件現在已設定完畢，且可供使用。

## 3.4.1.2建立您的歷程

在功能表中，前往&#x200B;**歷程**&#x200B;並按一下&#x200B;**建立歷程**。

![Journey Optimizer](./images/oc43.png)

您將會看到此訊息。 為您的歷程命名。 使用`--aepUserLdap-- - Order Confirmation journey`。 按一下&#x200B;**「確定」**。

![Journey Optimizer](./images/oc45.png)

首先，您需要新增活動作為歷程的起點。 搜尋您的活動`--aepUserLdap--PurchaseEvent`，並將其拖放到畫布上。 按一下&#x200B;**「確定」**。

![Journey Optimizer](./images/oc46.png)

接下來，在&#x200B;**動作**&#x200B;底下，搜尋&#x200B;**電子郵件**&#x200B;動作，並將其新增至畫布上。

![Journey Optimizer](./images/oc47.png)

將&#x200B;**類別**&#x200B;設定為&#x200B;**行銷**，並選取可讓您傳送電子郵件的電子郵件表面。 在此情況下，要選取的電子郵件表面為&#x200B;**電子郵件**。 請確定已同時啟用&#x200B;**電子郵件**&#x200B;點按和&#x200B;**電子郵件開啟**&#x200B;的核取方塊。

![ACOP](./images/journeyactions1.png)

下一步是建立訊息。 若要這麼做，請按一下[編輯內容]。****

![ACOP](./images/journeyactions2.png)

您現在看到這個了。 按一下&#x200B;**主旨列**&#x200B;文字欄位。

![ACOP](./images/journeyactions3.png)

在文字區域開始寫入&#x200B;**感謝您的訂購，**

![Journey Optimizer](./images/oc5.png)

主旨列尚未完成。 接下來，您需要為&#x200B;**名字**&#x200B;欄位（儲存在`profile.person.name.firstName`下）引入個人化權杖。 在左側功能表中，向下捲動以尋找&#x200B;**人員** > **全名** > **名字**&#x200B;欄位，然後按一下&#x200B;**+**&#x200B;圖示以將個人化權杖新增至主旨列。 按一下&#x200B;**儲存**。

![Journey Optimizer](./images/oc6.png)

然後您就會回到這裡。 按一下&#x200B;**電子郵件Designer**&#x200B;以建立電子郵件的內容。

![Journey Optimizer](./images/oc7.png)

在下一個畫面中，按一下&#x200B;**從草稿開始設計**。

![Journey Optimizer](./images/oc8.png)

在左側選單中，您會找到可用來定義電子郵件結構（列和欄）的結構元件。

將&#x200B;**1:1欄**&#x200B;拖放八次，畫布應會提供下列內容：

![Journey Optimizer](./images/oc9.png)

移至&#x200B;**內容元件**。

![Journey Optimizer](./images/oc10.png)

將&#x200B;**Image**&#x200B;元件拖放到第一列。 按一下&#x200B;**瀏覽**。

![Journey Optimizer](./images/oc11.png)

前往資料夾&#x200B;**enablement-assets**，選取檔案&#x200B;**luma-logo.png**，然後按一下&#x200B;**選取**。

![Journey Optimizer](./images/oc12.png)

您現在已回到這裡。 按一下您的影像加以選取，然後使用&#x200B;**大小**&#x200B;滑桿將標誌影像縮小一點。

![Journey Optimizer](./images/oc13.png)

移至&#x200B;**內容元件**，並將&#x200B;**Image**&#x200B;元件拖放到第二列。 選取&#x200B;**影像元件**，但不要按一下[瀏覽]。

![Journey Optimizer](./images/oc15.png)

將此影像URL貼到欄位&#x200B;**Source**： `https://parsefiles.back4app.com/hgJBdVOS2eff03JCn6qXXOxT5jJFzialLAHJixD9/29043bedcde632a9cbe8a02a164189c9_preparing.png`。 此影像在Adobe以外託管。

![Journey Optimizer](./images/oc14.png)

當您將範圍變更為另一個欄位時，將會演算影像，您將看到以下畫面：

![Journey Optimizer](./images/oc16.png)

接著，移至&#x200B;**內容元件**，並將&#x200B;**文字**&#x200B;元件拖放到第三列。

![Journey Optimizer](./images/oc17.png)

選取該元件中的預設文字&#x200B;**請在此輸入您的文字。**&#x200B;並以下列文字取代：

```javascript
You’re one step closer!

Hi 

We've received your order details!

We will also send you a separate email containing your VAT Invoice.

We'll be back in touch with you as soon as we've finished packing your package. Please read carefully the Order Information detailed below.
```

![Journey Optimizer](./images/oc18.png)

將游標放在文字&#x200B;**嗨**&#x200B;旁邊，然後按一下&#x200B;**新增Personalization**。

![Journey Optimizer](./images/oc19.png)

導覽至「**人員**」>「**全名**」>「**名字**」欄位，然後按一下「**+**」圖示，將個人化權杖新增至主旨列。 按一下&#x200B;**儲存**。

![Journey Optimizer](./images/oc20.png)

然後您會看到以下內容：

![Journey Optimizer](./images/oc21.png)

接著，移至&#x200B;**內容元件**，並將&#x200B;**文字**&#x200B;元件拖放到第四列。

![Journey Optimizer](./images/oc22.png)

選取該元件中的預設文字&#x200B;**請在此輸入您的文字。**&#x200B;並以下列文字取代：

`Order Information`

將字型大小變更為&#x200B;**26px**，並將文字置中於此儲存格中。 之後，您將會擁有此專案：

![Journey Optimizer](./images/oc23.png)

接著，移至&#x200B;**內容元件**，並將&#x200B;**HTML**&#x200B;元件拖放至第五列。 按一下HTML元件，然後按一下&#x200B;**顯示原始程式碼**。

![Journey Optimizer](./images/oc24.png)

在&#x200B;**編輯HTML**&#x200B;快顯視窗中，貼上此HTML：

```<table><tbody><tr><td><b>Items purchased</b></td><td></td><td><b>Quantity</b></td><td><b>Subtotal</b></td></tr><tr><td colspan="4" width="500"><hr></td></tr></tbody></table>```

按一下&#x200B;**儲存**。

![Journey Optimizer](./images/oc25.png)

您就會擁有此專案。 按一下[儲存]儲存進度。****

![Journey Optimizer](./images/oc26.png)

移至&#x200B;**內容元件**，並將&#x200B;**HTML**&#x200B;元件拖放至第六列。 按一下HTML元件，然後按一下&#x200B;**顯示原始程式碼**。

![Journey Optimizer](./images/oc57.png)

在&#x200B;**編輯HTML**&#x200B;快顯視窗中，貼上此HTML：

```{{#each xxx as |item|}}<table width="500"><tbody><tr><td><img src="{{item.--aepTenantId--.core.imageURL}}" width="100"></td><td><table><tbody><tr><td><b>{{item.name}}</b><br>{{item.--aepTenantId--.core.subCategory}}<br><b>{{item.priceTotal}}</b><br>&nbsp;<br>Article no: {{item.SKU}}</td></tr></tbody></table></td><td>{{item.quantity}}</td><td><b>{{item.priceTotal}}</b></td></tr></tbody></table>{{/each}}```

之後，您將會擁有此專案：

![Journey Optimizer](./images/oc58.png)

您現在必須以productListItems物件的參考取代&#x200B;**xxx**，此物件是觸發歷程之事件的一部分。

![Journey Optimizer](./images/oc59.png)

首先，請先刪除HTML代碼中的&#x200B;**xxx**。

![Journey Optimizer](./images/oc60.png)

在左側功能表中，按一下&#x200B;**內容屬性**。 此內容會傳遞至歷程中的訊息。

![Journey Optimizer](./images/oc601.png)

您將會看到此訊息。 按一下&#x200B;**Journey Orchestration**&#x200B;旁的箭頭以深入鑽研。

![Journey Optimizer](./images/oc61.png)

按一下&#x200B;**事件**&#x200B;旁的箭頭，以深入探討。

![Journey Optimizer](./images/oc62.png)

按一下`--aepUserLdap--PurchaseEvent`旁的箭頭以深入鑽研。

![Journey Optimizer](./images/oc63.png)

按一下&#x200B;**productListItems**&#x200B;旁的箭頭，以深入鑽研。

![Journey Optimizer](./images/oc64.png)

按一下&#x200B;**名稱**&#x200B;旁的&#x200B;**+**&#x200B;圖示以將其新增至畫布。 您就會擁有此專案。 您現在必須選取&#x200B;**.name** （如下列熒幕擷圖所示），然後您應該移除&#x200B;**.name**。

![Journey Optimizer](./images/oc65.png)

您就會擁有此專案。 按一下&#x200B;**儲存**。

![Journey Optimizer](./images/oc66.png)

您現在會回到電子郵件Designer。 按一下[儲存]儲存進度。****

![Journey Optimizer](./images/oc67.png)

接著，前往&#x200B;**內容元件**，並將&#x200B;**HTML**&#x200B;元件拖放至第七列。 按一下HTML元件，然後按一下&#x200B;**顯示原始程式碼**。

![Journey Optimizer](./images/oc68.png)

在&#x200B;**編輯HTML**&#x200B;快顯視窗中，貼上此HTML：

```<table><tbody><tr><td><b>Subtotal</b><br>Delivery charge (included)</td><td align="right"><b>xxx</b><br><b>5</b></td></tr><tr><td colspan="2" width="500"><hr></td></tr><tr><td><b>Total including VAT</b></td><td align="right"><b>xxx</b></td></tr></tbody></table>```

此HTML程式碼中有2個&#x200B;**xxx**&#x200B;的參考。 您現在必須藉由對productListItems物件的參考來取代每個&#x200B;**xxx**，此物件是觸發歷程的事件的一部分。

![Journey Optimizer](./images/oc69.png)

首先，刪除HTML代碼中的前&#x200B;**xxx**。

![Journey Optimizer](./images/oc71.png)

在左側功能表中，按一下&#x200B;**內容屬性**。

![Journey Optimizer](./images/oc711.png)

按一下&#x200B;**Journey Orchestration**&#x200B;旁的箭頭以深入鑽研。

![Journey Optimizer](./images/oc72.png)

按一下&#x200B;**事件**&#x200B;旁的箭頭，以深入探討。

![Journey Optimizer](./images/oc722.png)

按一下`--aepUserLdap--PurchaseEvent`旁的箭頭以深入鑽研。

![Journey Optimizer](./images/oc73.png)

按一下&#x200B;**Commerce**&#x200B;旁的箭頭以深入探討。

![Journey Optimizer](./images/oc733.png)

按一下&#x200B;**順序**&#x200B;旁的箭頭以深入鑽研。

![Journey Optimizer](./images/oc74.png)

按一下&#x200B;**總價**&#x200B;旁的&#x200B;**+**&#x200B;圖示，將其新增至畫布。

![Journey Optimizer](./images/oc75.png)

您就會擁有此專案。 現在刪除您HTML代碼中的第二個&#x200B;**xxx**。

![Journey Optimizer](./images/oc76.png)

再按一下&#x200B;**總價**&#x200B;旁的&#x200B;**+**&#x200B;圖示以將其新增至畫布。

![Journey Optimizer](./images/oc77.png)

您也可以將&#x200B;**Order**&#x200B;物件內的&#x200B;**Currency**欄位新增至畫布，如這裡所示。
完成時，按一下[儲存]儲存變更。****

![Journey Optimizer](./images/oc771.png)

接著，您會回到電子郵件Designer。 再按一下&#x200B;**儲存**。

![Journey Optimizer](./images/oc78.png)

按一下左上角主旨列文字旁的&#x200B;**箭頭**，返回訊息儀表板。

![Journey Optimizer](./images/oc79.png)

按一下左上角的箭頭，返回您的歷程。

![Journey Optimizer](./images/oc79a.png)

按一下&#x200B;**確定**&#x200B;以關閉您的電子郵件動作。

![Journey Optimizer](./images/oc79b.png)

按一下&#x200B;**Publish**&#x200B;以發佈您的歷程。

![Journey Optimizer](./images/oc511.png)

再按一下&#x200B;**Publish**。

![Journey Optimizer](./images/oc512.png)

您的歷程現已發佈。

![Journey Optimizer](./images/oc513.png)

## 3.4.1.5更新您的Adobe Experience Platform資料收集使用者端屬性

移至[Adobe Experience Platform資料彙集](https://experience.adobe.com/launch/)並選取&#x200B;**標籤**。

這是您之前看到的Adobe Experience Platform資料收集屬性頁面。

![屬性頁面](./../../../modules/datacollection/module1.1/images/launch1.png)

在模組0中，示範系統為您建立了兩個使用者端屬性：一個用於網站，另一個用於行動應用程式。 在&#x200B;**[!UICONTROL 搜尋]**&#x200B;方塊中搜尋`--aepUserLdap--`以尋找它們。 按一下以開啟&#x200B;**Web**&#x200B;屬性。

![搜尋方塊](./../../../modules/datacollection/module1.1/images/property6.png)

移至&#x200B;**資料元素**。 搜尋並開啟資料元素&#x200B;**XDM — 購買**。

![Journey Optimizer](./images/oc91.png)

您將會看到此訊息。 導覽至&#x200B;**_experience.campaign.orchestration.eventID**&#x200B;欄位，並在這裡填寫您的eventID。 此處要填寫的eventID是您在練習10.1.2中建立的eventID。按一下&#x200B;**儲存**&#x200B;或&#x200B;**儲存至資料庫**。

![Journey Optimizer](./images/oc92.png)

將變更儲存在使用者端屬性中，然後更新開發程式庫以發佈變更。

![Journey Optimizer](./images/oc93.png)

您的變更現在已部署並可進行測試。

## 3.4.1.6使用示範網站測試您的訂單確認電子郵件

讓我們在示範網站上購買產品，以測試更新的歷程。

移至[https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects)。 使用Adobe ID登入後，您會看到此訊息。 按一下您的網站專案以開啟。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

然後您會看到示範網站已開啟。 選取URL並將其複製到剪貼簿。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

開啟新的無痕瀏覽器視窗。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

貼上您在上一步中複製的示範網站URL。 接著，系統會要求您使用Adobe ID登入。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

選取您的帳戶型別並完成登入程式。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

接著，您會在無痕瀏覽器視窗中看到您的網站已載入。 對於每個示範，您都需要使用全新的無痕瀏覽器視窗來載入您的示範網站URL。

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

按一下畫面左上角的Adobe標誌圖示，開啟設定檔檢視器。

![示範](./../../../modules/datacollection/module1.2/images/pv1.png)

請檢視「設定檔檢視器」面板和即時客戶設定檔，並將&#x200B;**Experience CloudID**&#x200B;設為此目前未知客戶的主要識別碼。

![示範](./../../../modules/datacollection/module1.2/images/pv2.png)

前往「註冊/登入」頁面。 按一下&#x200B;**建立帳戶**。

![示範](./../../../modules/datacollection/module1.2/images/pv9.png)

填寫您的詳細資料，然後按一下&#x200B;**註冊**，之後您將會被重新導向到上一頁。

![示範](./../../../modules/datacollection/module1.2/images/pv10.png)

新增任何產品至購物車，然後前往&#x200B;**購物車**&#x200B;頁面。 按一下&#x200B;**繼續結帳**。

![Journey Optimizer](./images/cart1.png)

接下來，驗證簽出頁面上的欄位，然後按一下&#x200B;**簽出**。

![Journey Optimizer](./images/cart2.png)

您將在數秒內收到訂單確認電子郵件。

![Journey Optimizer](./images/oc98.png)

您已完成此練習。

下一步： [3.4.2設定批次式Newsletter歷程](./ex2.md)

[返回模組3.4](./journeyoptimizer.md)

[返回所有模組](../../../overview.md)
