---
title: 建立驗證報表套裝
description: 在Adobe Analytics中建立報表套裝，以便在從舊實作移轉網站時用來驗證Web SDK資料。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16756
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# 建立驗證報表套裝

在Adobe Analytics中建立報表套裝，以便在從舊實作移轉網站時用來驗證Web SDK資料。

根據Analytics實作的規模和複雜性，移轉至網頁SDK可能需要一點時間。 在此期間，您會想要驗證自己的工作，確保資料正確流入Adobe Analytics報表。 最佳實務是建立全新的報表套裝，供您用於此移轉，而非將此資料連同生產資料或甚至任何其他開發資料一起推送至報表套裝。 在下一個課程中，我們將針對開發、測試和生產建立和設定新的「資料串流」。 完成此操作時，我們需要知道設定的報表套裝ID。

## 建立新的報表套裝

1. 開啟Adobe Analytics並導覽至Admin Console中的&#x200B;**報表套裝**&#x200B;設定

   ![Admin Console](assets/aa-admin-console.jpg)。

1. 選取&#x200B;**[!UICONTROL 新增報表套裝]**

   ![新增報表套裝](assets/add-report-suite.jpg)

1. 填寫表單以建立新的報表套裝。 雖然您可以選擇從範本（甚至空白範本）建立新的報表套裝，但選擇「**複製現有報表套裝**」選項，並選擇您要移轉至Web SDK的報表套裝，可能會對您更有幫助。 這可讓您使用與測試新移轉資料相同的名稱和設定，讓您在測試時更輕鬆驗證。 填寫所有必填欄位，並儲存新的移轉開發報表套裝。

   ![新的移轉開發報表套裝](assets/new-websdk-validation-report-suite.jpg)

1. 記下新報表套裝的ID，當您為Web SDK實作設定資料串流時，將在下一個課程中需要此ID。 網站標題也請記得好，因為您可以在Analysis Workspace中使用它，在Analytics專案中選擇移轉開發報表套裝。

>[!TIP]
>
>如需建立報表套裝的影片逐步解說，請參閱[瞭解及建立報表套裝](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/intro-to-analytics/analytics-basics/understanding-and-creating-report-suites){target="_blank"}。

