---
title: 建立標籤屬性
description: 瞭解如何登入資料收集介面和建立標籤屬性。 本課程屬於「在網站中實作Experience Cloud」教學課程的一部分。
exl-id: f83d374a-a831-4598-b9d3-6f183224b589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 50%

---

# 建立標籤屬性

在本課程中，您將建立您的第一個標籤屬性。

屬性基本上是個容器，當您將標記部署至網站時，在其中裝入擴充功能、規則、資料元素和程式庫。

## 必要條件

若要完成後續幾堂課，您必須擁有開發、核准、Publish、管理擴充功能及管理標籤中環境的許可權。 如果您因無法使用的使用者介面選項而無法完成其中任何步驟，請聯絡 Experience Cloud 管理員以請求存取權限。如需有關標籤使用者許可權的詳細資訊，請參閱[檔案](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html)。

>[!NOTE]
>
>Adobe Experience Platform Launch正在以資料收集技術套裝的形式整合到Adobe Experience Platform中。 此介面已推出幾項術語變更，使用此內容時請務必注意：
>
> * platform launch（使用者端）現在是&#x200B;**[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)**
> * platform launch伺服器端現在是&#x200B;**[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Edge設定現在是&#x200B;**[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**

## 學習目標

在本課程結束時，您將能夠：

* 登入資料收集使用者介面
* 建立新標籤屬性
* 設定標籤屬性

## 前往資料收集介面

**以存取資料彙集**

1. 登入 [Adobe Experience Cloud](https://experiencecloud.adobe.com)

1. 按一下![解決方案切換器圖示](images/launch-solutionSwitcher.png)圖示，開啟應用程式切換器

1. 從功能表選取&#x200B;**[!UICONTROL 啟動/資料彙集]** ![使用圖示開啟解決方案切換器，然後按一下[啟動/資料彙集] ](images/launch-solutionSwitcherActivation.png)

這時您應該會看到 `Tags Properties` 畫面 (如果帳戶中尚未建立任何屬性，此畫面可能呈現空白狀態)：

![屬性畫面](images/launch-propertiesScreen.png)

## 建立屬性

屬性基本上是個容器，當您將標記部署至網站時，在其中裝入擴充功能、規則、資料元素和程式庫。屬性可以是一或多個網域和子網域的任何群組。同樣地，您可以管理及追蹤這些資產。例如，假設您有多個網站是根據同一個範本，且想要追蹤這所有網站上的相同資產。您可以將一個屬性套用到多個網域。如需建立屬性的詳細資訊，請參閱產品說明文件中的[公司和屬性](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html)。

**建立屬性的方式**

1. 按一下&#x200B;**[!UICONTROL 新增屬性]**&#x200B;按鈕：

   ![按一下「新增屬性」](images/launch-addNewProperty.png)。

1. 為屬性命名 (例如 `Luma Tutorial` 或 `Luma Tutorial - Daniel`)
1. 網域請輸入 `enablementadobe.com`，因為這是託管 Luma 演示網站的網域。雖然「網域」欄位是必填欄位，但標籤屬性可用於實施的任何網域。 此欄位的主要用途是在規則產生器中預先填入功能表選項。
1. 展開&#x200B;**[!UICONTROL 進階選項]**&#x200B;區段，並勾選方塊以&#x200B;**[!UICONTROL 依序執行規則元件]**
1. 按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;按鈕

   ![建立新屬性](images/launch-newProperty.png)

「屬性」頁面上應會顯示您的新屬性。請注意，如果您勾選屬性名稱旁的方塊，屬性清單上方會出現&#x200B;**[!UICONTROL 設定]**&#x200B;或&#x200B;**[!UICONTROL 刪除]**&#x200B;屬性的選項。 按一下屬性的名稱 (例如 `Luma Tutorial`) 以開啟 `Overview` 畫面。![按一下屬性名稱以開啟](images/launch-openProperty.png)

[下堂課「新增內嵌程式碼」>](add-embed-code.md)
