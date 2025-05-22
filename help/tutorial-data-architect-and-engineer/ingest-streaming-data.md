---
title: 擷取串流資料
seo-title: Ingest streaming data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 擷取串流資料
description: 在本課程中，您將使用網頁SDK將資料串流至Experience Platform。
role: Data Engineer
feature: Data Ingestion
jira: KT-4348
thumbnail: 4348-ingest-streaming-data.jpg
exl-id: 09c24673-af8b-40ab-b894-b4d76ea5b112
source-git-commit: e26f2add184031fd95561bd560b24ad73bb73d01
workflow-type: tm+mt
source-wordcount: '3272'
ht-degree: 0%

---

# 擷取串流資料

<!--1hr-->

在本課程中，您將使用Adobe Experience Platform Web SDK串流資料。

在資料收集介面中，我們必須完成兩項主要工作：

* 我們必須在Luma網站上實作Web SDK，以將有關網站訪客活動的資料傳送至Adobe Edge網路。 我們將使用標籤（先前稱為Launch）進行簡單的實作

* 我們必須設定資料串流，告訴Edge網路將資料轉送至何處。 我們會將其設定為將資料傳送至Platform沙箱中的`Luma Web Events`資料集。

**資料工程師**&#x200B;需要在本教學課程之外擷取串流資料。 實作Adobe Experience Platform的Web或行動SDK時，通常會有Web或行動開發人員參與資料層建立和標籤屬性設定。

在開始練習之前，請觀看這兩個短片，以進一步瞭解串流資料擷取和網頁SDK：

>[!VIDEO](https://video.tv.adobe.com/v/28425?learn=on&enablevpops)

>[!VIDEO](https://video.tv.adobe.com/v/34141?learn=on&enablevpops)

>[!NOTE]
>
>雖然本教學課程著重於使用Web SDK從網站串流擷取，但您也可以使用[Adobe Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)、[Apache Kafka Connect](https://github.com/adobe/experience-platform-streaming-connect)和其他機制串流資料。

## 需要的許可權

在[設定許可權](configure-permissions.md)課程中，您已設定完成本課程所需的所有存取控制。

<!--
* Permission items **[!UICONTROL Launch]** > **[!UICONTROL Property Rights]** > **[!UICONTROL Approve]**, **[!UICONTROL Develop]**, **[!UICONTROL Manage Environments]**, **[!UICONTROL Manage Extensions]**, and **[!UICONTROL Publish]**
* Permission item **[!UICONTROL Launch]** > **[!UICONTROL Company Rights]** > **[!UICONTROL Manage Properties]**
* User-role access to the `Luma Tutorial Launch` product profile
* Admin-role access to the `Luma Tutorial Launch` product profile
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Data Ingestion]** > **[!UICONTROL View Sources]** and **[!UICONTROL Manage Sources]**
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Profiles]** > **[!UICONTROL View Profiles]**, **[!UICONTROL Manage Profiles]** and **[!UICONTROL Export Audience Segment]**
* Permission item **[!UICONTROL Platform]** > **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]**
* Permission item **[!UICONTROL Platform]** > **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

<!--## Create a streaming source

1. Log into the [Experience Platform  user interface](https://experience.adobe.com/platform/)
1. Go to **[!UICONTROL Sources]** in the left navigation
1. Filter the list by selecting **[!UICONTROL Streaming]**
1. In the **[!UICONTROL HTTP API]** section, select the **[!UICONTROL Configure]** button
    ![Configure an HTTP API streaming source](assets/websdk-source-confiigureHTTPAPI.png)
1. On the **[!UICONTROL Authentication]** step, enter `Luma Web Events Source` as the **[!UICONTROL Account name]** and select the **[!UICONTROL Connect to source]** button (we don't need to enable authentication since the data will be originating from website visitors)
    ![Configure an HTTP API streaming source](assets/websdk-source-connectSource.png)
1. Once connected, select the **[!UICONTROL Next]** button to proceed to the next step in the workflow
1. On the **[!UICONTROL Select data]** step, choose **[!UICONTROL Existing Dataset]**, select your `Luma Web Events Dataset`, and then select the **[!UICONTROL Next]** button
    ![Select your dataset](assets/websdk-source-selectDataset.png)
1. On the **[!UICONTROL Dataflow detail]** step, select the **[!UICONTROL Next]** button:
    ![Select Next](assets/websdk-source-dataflowName.png)
    <!--What is a good practice for naming the data flow vs the source-->
<!--
1. On the **[!UICONTROL Review]** step, review your source details and select the **[!UICONTROL Finish]** button:
    ![Select Finish](assets/websdk-source-review.png)
-->

## 設定資料串流

首先，我們將設定資料串流。 資料串流會告訴Adobe Edge網路，從網頁SDK呼叫收到資料後，應將資料傳送至何處。 例如，您要將資料傳送至Experience Platform、Adobe Analytics或Adobe Target嗎？ 資料串流在資料收集使用者介面（前身為Launch）中進行管理，對於透過Web SDK進行資料收集至關重要。

若要建立您的[!UICONTROL 資料流]：

1. 登入[Experience Platform資料彙集使用者介面](https://experience.adobe.com/launch/)
   <!--when will the edge config go live?-->

1. 在左側導覽中選取&#x200B;**[!UICONTROL 資料串流]**
1. 選取右上角的&#x200B;**[!UICONTROL 新資料流]**&#x200B;按鈕

   ![在左側導覽中選取資料串流](assets/websdk-edgeConfig-clickNav.png)


1. 針對&#x200B;**[!UICONTROL 易記名稱]**，輸入`Luma Platform Tutorial` （如果貴公司的多個人員正在參加此教學課程，請將您的名稱加入結尾）
1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;按鈕

   ![命名資料串並儲存](assets/websdk-edgeConfig-name.png)

在下一個畫面中，您指定要傳送資料的位置。 若要將資料傳送至Experience Platform：

1. 開啟&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;以公開其他欄位
1. 針對&#x200B;**[!UICONTROL 沙箱]**，請選取`Luma Tutorial`
1. 針對&#x200B;**[!UICONTROL 事件資料集]**，請選取`Luma Web Events Dataset`
1. 如果您使用其他Adobe應用程式，歡迎探索其他區段，瞭解這些其他解決方案的Edge設定需要哪些資訊。 請記住，開發Web SDK不僅是為了將資料串流到Experience Platform，也是為了取代其他Adobe應用程式使用的所有先前JavaScript資料庫。 Edge設定是用來指定您要傳送資料之各應用程式的帳戶詳細資訊。
1. 選取&#x200B;**[!UICONTROL 儲存]**
   ![設定資料流並儲存](assets/websdk-edgeConfig-addEnvironment.png)

Edge設定儲存後，產生的畫面會顯示已建立用於開發、測試和生產的三個環境。 可以新增其他開發環境：
![每個Edge設定都可以有多個環境](assets/websdk-edgeConfig-environments.png)
這三個環境都包含您剛才輸入的平台詳細資料。 不過，這些詳細資料可依環境以不同方式設定。 例如，您可以讓每個環境將資料傳送至不同的Platform沙箱。 在本教學課程中，我們將不會針對資料流執行任何其他自訂。

## 安裝網頁SDK擴充功能

### 新增屬性

首先，我們必須建立標籤屬性（先前稱為標籤屬性）。 屬性是一個容器，內含所有JavaScript、規則，以及從網頁收集詳細資訊並傳送至不同位置所需的其他功能。

若要建立屬性：

1. 前往左側導覽中的&#x200B;**[!UICONTROL 屬性]**
1. 選取&#x200B;**[!UICONTROL 新屬性]**按鈕
   ![新增屬性](assets/websdk-property-addNewProperty.png)
1. 以&#x200B;**[!UICONTROL Name]**&#x200B;的身分，輸入`Luma Platform Tutorial` （如果貴公司的多人參加此教學課程，請在結尾加上您的姓名）
1. 作為&#x200B;**[!UICONTROL 網域]**，請輸入`enablementadobe.com` （稍後說明）
1. 選取&#x200B;**[!UICONTROL 儲存]**
   ![屬性詳細資料](assets/websdk-property-propertyDetails.png)

<!--
After saving the property, you might see an error message like the one below. If so, this is because you don't actually have access to the property you just created. To fix this, we need to go to the Admin Console to give yourself access:
    ![Error after saving the profile](assets/websdk-property-errorCreating.png)

To give yourself access to the property:

1. In a separate browser tab, log into the [Admin Console](https://adminconsole.adobe.com/)
1. Go to **[!UICONTROL Products]** from the top navigation
1. Select **[!UICONTROL Adobe Experience Platform Launch]** on the left navigation
1. Go to your `Luma Tutorial Launch` product profile
1. Go to the **[!UICONTROL Permissions]** tab
1. On the **[!UICONTROL Properties]** row, select **[!UICONTROL Edit]**
    ![Edit the Property Permissions](assets/websdk-adminconsole-editPermissions.png)
1. Select the "+" icon to move your `Luma Platform Tutorial` property to the right-hand side and select the **[!UICONTROL Save]** button to update the permissions
   
    ![Add the new property](assets/websdk-adminconsole-addProperty.png)

Now switch back to your browser tab with the Data Collection interface still open. Reload the page and the `Luma Platform Tutorial` property should display in the list. Select to open the property:

![Luma Platform Tutorial should appear](assets/websdk-property-showsInList.png)
-->

## 新增網頁SDK擴充功能

現在您已擁有屬性，可以使用擴充功能新增Web SDK。 擴充功能是擴充資料收集介面和功能的程式碼套件。 若要新增擴充功能：

1. 開啟您的標籤屬性
1. 前往左側導覽中的&#x200B;**[!UICONTROL 擴充功能]**
1. 前往&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤
1. 有許多擴充功能可供標籤使用。 篩選含有字詞`Web SDK`的目錄
1. 在&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;擴充功能中，選取&#x200B;**[!UICONTROL 安裝]**按鈕
   ![安裝Adobe Experience Platform Web SDK擴充功能](assets/websdk-property-addExtension.png)
1. Web SDK擴充功能有數種設定可供使用，但在本教學課程中，我們只會設定兩種。 將&#x200B;**[!UICONTROL Edge網域]**&#x200B;更新為`data.enablementadobe.com`。 此設定可讓您透過網頁SDK實作設定第一方Cookie （建議使用）。 在本課程的稍後部分，您將會將`enablementadobe.com`網域上的網站對應至您的標籤屬性。 已設定`enablementadobe.com`網域的CNAME，因此`data.enablementadobe.com`將轉送至Adobe伺服器。 當您在自己的網站上實作Web SDK時，必須針對您自己的資料收集目的建立CNAME，例如`data.YOUR_DOMAIN.com`
1. 從&#x200B;**[!UICONTROL 資料流]**&#x200B;下拉式清單中，選取您的`Luma Platform Tutorial`資料流。
1. 您可以檢視其他組態選項（但不要變更它們！），然後選取&#x200B;**[!UICONTROL 儲存]**
   <!--is edge domain required for first party? when will it break?-->
   <!--any other fields that should be highlighted-->
   ![](assets/websdk-property-configureExtension.png)



## 建立規則以傳送資料

現在我們將建立規則以將資料傳送至Platform。 規則是事件、條件和動作的組合，可指示標籤執行某項動作。 若要建立規則：

1. 前往左側導覽中的&#x200B;**[!UICONTROL 規則]**
1. 選取&#x200B;**[!UICONTROL 建立新規則]**按鈕
   ![建立規則](assets/websdk-property-createRule.png)
1. 將規則命名為 `All Pages - Library Loaded`
1. 在&#x200B;**[!UICONTROL 事件]**&#x200B;下，選取&#x200B;**[!UICONTROL 新增]**按鈕
   ![為規則命名並新增事件](assets/websdk-property-nameRule.png)
1. 使用&#x200B;**[!UICONTROL 核心]** **[!UICONTROL 擴充功能]**，並選取&#x200B;**[!UICONTROL 載入的程式庫（頁面頂端）]**&#x200B;作為&#x200B;**[!UICONTROL 事件型別]**。 此設定表示每當頁面上載入Launch程式庫時，就會觸發規則。
1. 選取&#x200B;**[!UICONTROL 保留變更]**以返回主規則畫面
   ![新增程式庫已載入事件](assets/websdk-property-addEvent.png)
1. 保留&#x200B;**[!UICONTROL 條件]**&#x200B;為空白，因為我們希望此規則依據我們提供的名稱在所有頁面上引發
1. 在&#x200B;**[!UICONTROL 動作]**&#x200B;底下，選取&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕
1. 使用&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]** **[!UICONTROL 擴充功能]**&#x200B;並選取&#x200B;**[!UICONTROL 傳送事件]**&#x200B;作為&#x200B;**[!UICONTROL 動作型別]**
1. 在右側，從&#x200B;**[!UICONTROL 型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL web.webpagedetails.pageViews]**。 這是我們`Luma Web Events Schema`中的XDM欄位之一
1. 選取&#x200B;**[!UICONTROL 保留變更]**以返回主規則畫面
   ![新增傳送事件動作](assets/websdk-property-addAction.png)
1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存規則\
   ![儲存規則](assets/websdk-property-saveRule.png)

## 在程式庫中發佈規則

接下來，我們將規則發佈至開發環境，以便驗證它是否有效。

<!--
There are a few quick steps we must take in the **[!UICONTROL Publishing]** section of Launch.


### Create a host

Launch libraries can be hosted on Adobe's Content Delivery Network (CDN) or on your own servers. In this tutorial, we will use Adobe's CDN since it is faster to set up:

1. Go to **[!UICONTROL Hosts]** in the left navigation
1. Select the **[!UICONTROL Create New Host]** button
    ![Create a new host](assets/websdk-property-createHost.png)   
1. For the **[!UICONTROL Name]**, enter `Adobe CDN`
1. For the **[!UICONTROL Type]**, select **[!UICONTROL Managed by Adobe]**
1. Select the **[!UICONTROL Save]** button to complete the setup of the host
    ![Configure the host](assets/websdk-property-hostDetails.png)   

### Create an environment

Environments allow you to have different versions of a library in different publishing environments to accommodate your publishing workflow. For example, the fully tested version of your library can be published to a Production environment, while new changes are being created in a Development environment. You can also use different hosts for each environment. To create an environment:

1. Go to **[!UICONTROL Environments]** in the left navigation
1. Select the **[!UICONTROL Create New Environment]** button
    ![Create a new environment](assets/websdk-property-createEnvironment.png) 
1. Under **[!UICONTROL Development]** select **[!UICONTROL Select]**   
    ![Select the environment type](assets/websdk-property-selectEnvironment.png) 
1. For the **[!UICONTROL Name]**, enter `Development`
1. For the **[!UICONTROL Select Host]** dropdown, select `Adobe CDN`
1. Select the **[!UICONTROL Save]** button to complete the setup of the environment
    ![Configure the environment](assets/websdk-property-configureEnv.png)
1. You will see a modal with URL and other implementation details of this library. These are critical for a real Launch implementation, but we don't need to worry about them for this tutorial. Select the **[!UICONTROL Close]** button to exit the modal.

### Create and publish the library

Now let's bundle the contents of our property&mdash;currently an extension and a rule&mdash;into a library. 
-->

若要建立程式庫：

1. 前往左側導覽中的&#x200B;**[!UICONTROL 發佈流程]**
1. 選取&#x200B;**[!UICONTROL 新增資料庫]**
   ![選取新增資料庫](assets/websdk-property-pubAddNewLib.png)
1. 為&#x200B;**[!UICONTROL 名稱]**&#x200B;輸入`Luma Platform Tutorial`
1. 針對&#x200B;**[!UICONTROL 環境]**，選取`Development`
1. 選取&#x200B;**[!UICONTROL 新增所有變更的資源]**&#x200B;按鈕。 (除了[!UICONTROL Adobe Experience Platform Web SDK]擴充功能和`All Pages - Library Loaded`規則外，您也會看到已新增[!UICONTROL Core]擴充功能，其中包含所有Launch Web屬性所需的基礎JavaScript。)
1. 選取&#x200B;**[!UICONTROL 儲存並建置以供開發]**按鈕
   ![建立並建置程式庫](assets/websdk-property-buildLibrary.png)

程式庫可能需要幾分鐘的時間才能建置，建置完成後，程式庫名稱左側會顯示一個綠色點：
![建置完成](assets/websdk-property-buildComplete.png)

如您在[!UICONTROL 發佈流程]畫面上所見，本教學課程範圍之外的發佈程式還有更多內容。 我們即將在開發環境中使用單一程式庫。

## 驗證請求中的資料

### 新增Adobe Experience Platform Debugger

Experience Platform Debugger是適用於Chrome和Firefox瀏覽器的擴充功能，可協助您檢視在網頁中實作的Adobe技術。 下載您偏好瀏覽器的版本：

* [Firefox擴充功能](https://addons.mozilla.org/zh-TW/firefox/addon/adobe-experience-platform-dbg/)
* [Chrome擴充功能](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

如果您從未使用過Debugger，而且此版本與舊版Adobe Experience Cloud Debugger不同，您可能會想觀看這段五分鐘的概述影片：

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on&enablevpops)

### 開啟Luma網站

在本教學課程中，我們使用公開託管版本的Luma示範網站。 請開啟檔案並將其加入書籤：

1. 在新的瀏覽器標籤中，開啟[Luma網站](https://luma.enablementadobe.com/content/luma/us/en.html)。
1. 將頁面加入書籤，以便在教學課程的其餘部分使用

這個託管網站是我們在初始標籤屬性設定的[!UICONTROL 網域]欄位中使用`enablementadobe.com`的原因，也是我們在[!UICONTROL Adobe Experience Platform Web SDK]擴充功能中使用`data.enablementadobe.com`作為第一方網域的原因。 我有一個計畫！

![Luma首頁](assets/websdk-luma-homepage.png)

### 使用Experience Platform Debugger對應至您的標籤屬性

Experience Platform Debugger有一種很酷的功能，可讓您使用其他標籤屬性來取代現有的標籤屬性。 這對於驗證非常有用，可讓我們略過本教學課程中的許多實作步驟。

1. 請確定您已開啟Luma網站，並選取Experience Platform Debugger擴充功能圖示
1. Debugger將會開啟並顯示硬式編碼實作的部分詳細資料，這些詳細資料與本教學課程無關（您可能需要在開啟Debugger後重新載入Luma網站）
1. 確認Debugger為&quot;**[!UICONTROL 已連線至Luma]**&quot; （如下圖所示），然後選取&quot;**[!UICONTROL 鎖定]**&quot;圖示以將Debugger鎖定至Luma網站。
1. 選取右上方的&#x200B;**[!UICONTROL 登入]**&#x200B;按鈕以進行驗證。
1. 現在前往左側導覽中的&#x200B;**[!UICONTROL 啟動]**
1. 選取設定索引標籤
1. 在顯示&#x200B;**[!UICONTROL 頁面內嵌程式碼]**&#x200B;的右側，開啟&#x200B;**[!UICONTROL 動作]**&#x200B;下拉式清單，然後選取&#x200B;**[!UICONTROL 取代]**
   ![選取動作>取代](assets/websdk-debugger-replaceLibrary.png)
1. 由於您已通過驗證，Debugger將會提取您可用的Launch屬性和環境。 選取您的`Luma Platform Tutorial`屬性
1. 選取您的`Development`環境
1. 選取&#x200B;**[!UICONTROL 套用]**按鈕
   ![選取替代標籤屬性](assets/websdk-debugger-selectProperty.png)
1. Luma網站現在將使用您的標籤屬性&#x200B;_重新載入_。 救命，我已經被黑進去了！ 開玩笑的。
   已取代![標籤屬性](assets/websdk-debugger-propertyReplaced.png)
1. 前往左側導覽中的&#x200B;**[!UICONTROL 摘要]**，檢視[!UICONTROL Launch]屬性的詳細資料
   ![摘要標籤](assets/websdk-debugger-summary.png)
1. 現在前往左側導覽中的&#x200B;**[!UICONTROL AEP Web SDK]**，檢視&#x200B;**[!UICONTROL 網路要求]**
1. 開啟&#x200B;**[!UICONTROL 事件]**&#x200B;列

   ![Adobe Experience Platform Web SDK請求](assets/websdk-debugger-platformNetwork.png)
1. 請注意，我們如何看到在[!UICONTROL 傳送事件]動作中指定的`web.webpagedetails.pageView`事件型別，以及其他遵循`AEP Web SDK ExperienceEvent Mixin`格式的現成變數
   ![事件詳細資料](assets/websdk-debugger-eventDetails.png)
1. 這些型別的要求詳細資訊也會顯示在瀏覽器的網頁開發人員工具&#x200B;**網路**&#x200B;標籤中。 開啟並重新載入頁面。 篩選具有`interact`的呼叫，以找出該呼叫，選取它，然後檢視&#x200B;**標題**&#x200B;索引標籤，**請求承載**區域。
   ![網路標籤](assets/websdk-debugger-networkTab.png)
1. 前往&#x200B;**回應**標籤，並記下ECID值包含在回應中的方式。 複製此值，因為您將在下一個練習中使用它來驗證設定檔資訊。
   ![網路標籤](assets/websdk-debugger-networkTab-response.png)



## 驗證Experience Platform中的資料

您可以檢視到`Luma Web Events Dataset`的資料批次，以驗證資料是否登陸Platform。 (我知道，這稱為串流資料擷取，但現在我的意思是，它會以批次方式到達！ 它會即時串流至設定檔，因此可用於即時細分和啟動，但每15分鐘會批次傳送至資料湖。)

驗證資料：

1. 在Platform使用者介面中，前往左側導覽中的&#x200B;**[!UICONTROL 資料集]**
1. 開啟`Luma Web Events Dataset`並確認批次已到。 請記住，每15分鐘傳送一次，因此您可能需要等待批次顯示。
1. 選取&#x200B;**[!UICONTROL 預覽資料集]**按鈕
   ![開啟資料集](assets/websdk-platform-dataset.png)
1. 在預覽強制回應視窗中，請注意如何選取左側結構描述的不同欄位，以預覽這些特定資料點：
   ![預覽欄位](assets/websdk-platform-datasetPreview.png)

您也可以確認新設定檔是否顯示：

1. 在Platform使用者介面中，前往左側導覽中的&#x200B;**[!UICONTROL 設定檔]**
1. 選取&#x200B;**[!UICONTROL ECID]**&#x200B;名稱空間並搜尋您的ECID值（從回應中複製）。 設定檔會有專屬的ID，獨立於ECID。
1. 選取&#x200B;**[!UICONTROL 設定檔識別碼]**以開啟設定檔
   ![尋找並開啟設定檔](assets/websdk-platform-openProfile.png)
1. 選取&#x200B;**[!UICONTROL 事件]**索引標籤以檢視您檢視的頁面
   ![設定檔事件](assets/websdk-platform-profileEvents.png)\
   <!--![](assets/websdk-platform-confirmProfile.png)-->

## 新增自訂資料至事件

### 建立頁面名稱的資料元素

1. 在資料收集標籤介面中，在`Luma Platform Tutorial`屬性的右上角，開啟&#x200B;**[!UICONTROL 選取工作程式庫]**&#x200B;下拉式清單，然後選取您的`Luma Platform Tutorial`程式庫。 此設定可讓您更輕鬆地向程式庫發佈其他更新。
1. 現在前往左側導覽中的&#x200B;**[!UICONTROL 資料元素]**
1. 選取&#x200B;**[!UICONTROL 建立新資料元素]**&#x200B;按鈕

   ![建立新的資料元素](assets/websdk-property-createNewDataElement.png)
1. 以&#x200B;**[!UICONTROL Name]**&#x200B;的身分，輸入`Page Name`
1. 作為&#x200B;**[!UICONTROL 資料元素型別]**，請選取`JavaScript Variable`
1. 作為&#x200B;**[!UICONTROL JavaScript變數名稱]**，請輸入`digitalData.page.pageInfo.pageName`
1. 若要協助標準化值的格式，請勾選&#x200B;**[!UICONTROL 強制小寫值]**&#x200B;和&#x200B;**[!UICONTROL 清除文字]**&#x200B;的方塊
1. 確定已選取`Luma Platform Tutorial`作為工作程式庫
1. 選取&#x200B;**[!UICONTROL 儲存至資料庫]**
   ![建立頁面名稱的資料元素](assets/websdk-property-dataElement-pageName.png)

### 將頁面名稱對應至XDM物件資料元素

現在，我們將頁面名稱對應至網頁SDK。

>[!IMPORTANT]
>
>為了完成此任務，我們需要確保您的使用者首先有權存取Prod沙箱。 如果您尚無法從其他產品設定檔存取Prod沙箱，請快速開啟您的`Luma Tutorial Platform`設定檔，並新增許可權專案&#x200B;**[!UICONTROL 沙箱]** > **[!UICONTROL Prod]**。 之後，在資料元素頁面上按住SHIFT鍵重新載入，即可清除您的快取
>![新增Prod沙箱](assets/websdk-property-permissionToLoadSchema.png)

在&#x200B;**[!UICONTROL 資料元素]**&#x200B;頁面上：

1. 建立新的資料元素
1. 以&#x200B;**[!UICONTROL Name]**&#x200B;的身分，輸入`XDM Object`
1. 以&#x200B;**[!UICONTROL 延伸模組]**&#x200B;的形式，選取`Adobe Experience Platform Web SDK`
1. 作為&#x200B;**[!UICONTROL 資料元素型別]**，請選取`XDM object`
1. 以&#x200B;**[!UICONTROL 沙箱]**&#x200B;的身分，選取您的`Luma Tutorial`沙箱
1. 作為&#x200B;**[!UICONTROL 結構描述]**，請選取您的`Luma Web Events Schema`
1. 選取`web.webPageDetails.name`欄位
1. 以&#x200B;**[!UICONTROL Value]**&#x200B;的身分，選取圖示以開啟資料元素選取強制回應視窗，然後選擇您的`Page Name`資料元素
1. 選取&#x200B;**[!UICONTROL 儲存至資料庫]**
   ![將頁面名稱對應至XDM物件資料元素](assets/websdk-property-dataElement-createXDMObject.png)

此相同程式用於將網站上的其他自訂資料對應至XDM欄位。

### 新增XDM資料至您的「傳送事件」動作

現在，您已將資料對應至XDM欄位，可以將它包含在您的「傳送事件」動作中：

1. 移至&#x200B;**[!UICONTROL 規則]**&#x200B;畫面
1. 開啟您的`All Pages - Library Loaded`規則
1. 開啟`Adobe Experience Platform Web SDK - Send Event`動作
1. 做為&#x200B;**[!UICONTROL XDM資料]**，請選取圖示以開啟資料元素選取強制回應視窗，然後選擇您的`XDM Object`資料元素
1. 選取&#x200B;**[!UICONTROL 保留變更]**按鈕
   ![將XDM資料新增至您的傳送事件動作](assets/websdk-property-addXDMtoSendEvent.png)
1. 現在，由於您已在最近幾個練習中選取`Luma Platform Tutorial`作為工作程式庫，因此您最近的變更已直接儲存至程式庫。 您可以開啟藍色按鈕上的下拉式清單，並選取&#x200B;**[!UICONTROL 儲存至程式庫並建置]**，而不需透過發佈流程畫面發佈我們的變更
   ![儲存至程式庫並建置](assets/websdk-property-saveAndBuildUpdatedSendEvent.png)

這會開始建立新的標籤程式庫，其中包含您剛才進行的三項變更。

### 驗證XDM資料

如前所述，當您使用Debugger對應至您的標籤屬性時，現在應該能夠重新載入Luma首頁，並看到頁面名稱欄位會填入請求中！
![驗證XDM資料](assets/websdk-debugger-pageName.png)

您也可以透過預覽資料集和設定檔，驗證在Platform中收到的頁面名稱資料。

## 傳送其他身分

您的Web SDK實作現在會傳送以Experience Cloud ID (ECID)作為主要識別碼的事件。 ECID會由Web SDK自動產生，且在每個裝置和瀏覽器中都是唯一的。 根據他們使用的裝置和瀏覽器，單一客戶可以有多個ECID。 那麼，我們如何取得此客戶的統一檢視，並將其線上活動連結至CRM、忠誠度和離線購買資料？ 為此，我們會在工作階段期間收集其他身分，並透過身分拼接決定性地連結其設定檔。

如果您還記得，我在[對應身分](map-identities.md)課程中曾提到我們會使用ECID和CRM ID做為網頁資料的身分。 現在來使用Web SDK收集CRM ID！

### 新增CRM ID的資料元素

首先，我們將CRM ID儲存在資料元素中：

1. 在標籤介面中，新增名稱為`CRM Id`的資料元素
1. 選取&#x200B;**[!UICONTROL JavaScript變數]**，作為&#x200B;**[!UICONTROL 資料元素型別]**
1. 作為&#x200B;**[!UICONTROL JavaScript變數名稱]**，請輸入`digitalData.user.0.profile.0.attributes.username`
1. 選取&#x200B;**[!UICONTROL 儲存至程式庫]**&#x200B;按鈕（`Luma Platform Tutorial`仍應該是您的工作程式庫）
   ![新增CRM ID的資料元素](assets/websdk-property-dataElement-crmId.png)

### 將CRM ID新增至「身分對應」資料元素

現在我們已擷取CRM ID值，我們必須將其與名為[!UICONTROL 身分對應]資料元素的特殊資料元素型別建立關聯：

1. 新增名稱為`Identities`的資料元素
1. 以&#x200B;**[!UICONTROL 延伸模組]**&#x200B;身分，選取&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**
1. 以&#x200B;**[!UICONTROL 資料元素型別]**，請選取&#x200B;**[!UICONTROL 身分對應]**
1. 以&#x200B;**[!UICONTROL 名稱空間]**&#x200B;身分，輸入`Luma CRM Id`，這是我們在先前的課程中建立的[!UICONTROL 名稱空間]

   >[!WARNING]
   >
   >Adobe Experience Platform Web SDK擴充功能2.2版可讓您使用Platform帳戶中的實際值，從預先填入的下拉式清單中選取名稱空間。 很遺憾，此功能尚未「沙箱感知」，因此`Luma CRM Id`值可能未出現在下拉清單中。 這可能會妨礙您完成此練習。 確認後，我們會張貼因應措施。

1. 以&#x200B;**[!UICONTROL ID]**&#x200B;身分，選取圖示以開啟資料元素選取強制回應視窗，然後選擇您的`CRM Id`資料元素
1. 以&#x200B;**[!UICONTROL 已驗證狀態]**，請選取&#x200B;**[!UICONTROL 已驗證]**
1. 檢查&#x200B;**[!UICONTROL 主要]**

   >[!TIP]
   >
   > Adobe建議將代表個人的身分（例如`Luma CRM Id`）傳送為[!UICONTROL 主要]身分。
   >
   > 如果身分對應包含人員識別碼（例如，`Luma CRM Id`），則人員識別碼會變成[!UICONTROL 主要]身分。 否則，`ECID`會成為[!UICONTROL 主要]身分。

1. 選取&#x200B;**[!UICONTROL 儲存至程式庫]**&#x200B;按鈕（`Luma Platform Tutorial`仍應該是您的工作程式庫）
   ![將CRM ID新增至Identity Map資料元素](assets/websdk-property-dataElement-identityMap.png)

>[!NOTE]
>
>您可以使用[!UICONTROL 身分對應]資料型別傳遞多個識別碼。

### 將身分對應資料元素新增至XDM物件

還有一個資料元素我們必須更新，那就是XDM物件資料元素。 更新三個個別的資料元素來傳遞這個身分看起來可能有點奇怪，但此程式旨在針對多個身分進行縮放。 不用擔心，本課程快要結束了！

1. 開啟您的XDM物件資料元素
1. 開啟IdentityMap XDM欄位
1. 作為&#x200B;**[!UICONTROL 資料元素]**，選取圖示以開啟資料元素選取強制回應視窗，並選擇您的`Identities`資料元素
1. 現在，由於您已在最近幾個練習中選取`Luma Platform Tutorial`作為工作程式庫，因此您最近的變更已直接儲存至程式庫。 您可以開啟藍色按鈕上的下拉式清單，並選取&#x200B;**[!UICONTROL 儲存至程式庫並建置]**，而不需透過發佈流程畫面發佈我們的變更
   ![將IdentityMap資料元素新增至XDM物件](assets/websdk-property-dataElement-addIdentitiesToXDMObject.png)


### 驗證身分

若要驗證CRM ID現在是否由網頁SDK傳送：

1. 開啟[Luma網站](https://luma.enablementadobe.com/content/luma/us/en.html)
1. 根據先前的指示，使用Debugger將其對應至您的標籤屬性
1. 選取Luma網站右上角的&#x200B;**登入**&#x200B;連結
1. 使用認證`test@adobe.com`/`test`登入
1. 在驗證之後，請在Debugger中檢查Experience Platform Web SDK呼叫(**[!UICONTROL Adobe Experience Platform Web SDK]** > **[!UICONTROL 網路要求]** > **[!UICONTROL 事件]**&#x200B;的最近要求)，您應該會看到`lumaCrmId`：
   ![在Debugger中驗證身分](assets/websdk-debugger-confirmIdentity.png)
1. 使用ECID名稱空間和值再次查詢使用者設定檔。 在設定檔中，您會看到CRM ID，也會看到「忠誠度ID」和設定檔詳細資料，例如姓名和電話號碼。 所有身分和資料都已拼接到一個即時客戶個人檔案中！
   ![在Platform中驗證身分](assets/websdk-platform-lumaCrmIdProfile.png)


## 其他資源

* [使用 Web SDK 實作 Adobe Experience Cloud](/help/tutorial-web-sdk/overview.md)
* [串流擷取檔案](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=zh-Hant)
* [串流擷取API參考](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)

做得好！那是有關網頁SDK和Launch的大量資訊。 完整式實作涉及的範圍更廣，但這些是協助您開始使用，並在Platform中檢視成果的基礎。

>[!NOTE]
>
>現在您已完成串流擷取課程，您可以從`Luma Tutorial Platform`產品設定檔中移除[!UICONTROL Prod]沙箱


資料工程師，如果您願意的話，可以跳到[執行查詢課程](run-queries.md)。

資料架構師，您可以改用[合併原則](create-merge-policies.md)！
