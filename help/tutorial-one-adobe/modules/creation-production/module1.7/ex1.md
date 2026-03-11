---
title: Firefly自訂工作流程快速入門
description: Firefly自訂工作流程快速入門
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 7d9ad7ec-7744-4ba6-9c11-c434e6cdef09
source-git-commit: a3a78b12f8244c8288eb0fffc82ad769776eb118
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 0%

---

# 1.7.1 Firefly自訂工作流程快速入門

[!BADGE Beta]

+++Beta詳細資料
藉由使用Firefly自訂工作流程Beta，您在此確認Beta係依「現況」提供，並無任何保證。 Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援Beta。 建議您謹慎使用，切勿依賴這類Beta及/或隨附資料的正確運作或效能。 Beta視為Adobe的機密資訊。  任何「意見回饋」(有關Beta的資訊，包括但不限於您在使用Beta時遇到的問題或缺陷、建議、改進和建議)會在此指派給Adobe Adobe，包括所有權利、標題，以及對此等意見回饋的興趣。

+++

移至[https://firefly.adobe.com](https://firefly.adobe.com)。 按一下右上角的設定檔圖示，並確認您已選取正確的執行個體（應為`--aepImsOrgName--`）。

移至&#x200B;**生產**。

![Firefly自訂工作流程](./images/ffcw1.png)

您應該會看到此訊息。 按一下&#x200B;**建立工作流程（測試版）**。

![Firefly自訂工作流程](./images/ffcw2.png)

## 1.7.1.1移除背景

為了進一步瞭解Firefly自訂工作流程，您現在將實作基本使用案例，著重於移除特定影像的背景。

將工作流程名稱變更為`vangeluw - remove background`。

![Firefly自訂工作流程](./images/ffcw3.png)

開啟&#x200B;**影像**

![Firefly自訂工作流程](./images/ffcw4.png)

選取「**移除背景**」，然後將此節點拖放到畫布上。

您現在需要將輸入影像節點和輸出影像節點連線到&#x200B;**移除背景**。

![Firefly自訂工作流程](./images/ffcw5.png)

向上捲動並移至&#x200B;**輸入與輸出**。 按一下&#x200B;**輸入影像**&#x200B;節點，然後將其拖曳到畫布上。

![Firefly自訂工作流程](./images/ffcw6.png)

然後您應該擁有此專案。 將&#x200B;**輸入影像**&#x200B;節點連線到&#x200B;**移除背景**&#x200B;節點，方法是將游標停留在&#x200B;**輸入影像**&#x200B;節點上&#x200B;**影像**&#x200B;旁的藍點上，並在&#x200B;**移除背景**&#x200B;節點上的&#x200B;**輸入影像**&#x200B;旁的藍點上繪製一條直線。

![Firefly自訂工作流程](./images/ffcw7.png)

然後您應該擁有此專案。 接著，按一下&#x200B;**輸出影像**&#x200B;節點，並將其拖曳至畫布上。

![Firefly自訂工作流程](./images/ffcw8.png)

然後您應該擁有此專案。 將&#x200B;**移除背景**&#x200B;節點連線到&#x200B;**輸出影像**&#x200B;節點，方法是將游標停留在&#x200B;**移除背景**&#x200B;節點上&#x200B;**輸出影像**&#x200B;旁的藍點上，並在&#x200B;**輸出影像**&#x200B;節點上的&#x200B;**影像**&#x200B;旁的藍點上繪製一條直線。

![Firefly自訂工作流程](./images/ffcw9.png)

然後您應該擁有此專案。

![Firefly自訂工作流程](./images/ffcw10.png)

您的基本工作流程現在已準備好進行測試。 將影像[phone.png](./assets/phone.png)下載到您的案頭。

![Firefly自訂工作流程](./images/ffcw11.png)

返回工作流程。 按一下&#x200B;**輸入影像**&#x200B;節點的&#x200B;**拖放**&#x200B;區域。

![Firefly自訂工作流程](./images/ffcw11a.png)

選取檔案&#x200B;**phone.png**。 按一下&#x200B;**「開啟」**。

![Firefly自訂工作流程](./images/ffcw12.png)

您應該會看到此訊息。 按一下&#x200B;**執行**。

![Firefly自訂工作流程](./images/ffcw13.png)

在1-2分鐘後，您應該會看到此結果。

![Firefly自訂工作流程](./images/ffcw14.png)

## 1.7.1.2移除背景+裁切

您現在應該將&#x200B;**裁切**&#x200B;節點新增至畫布。 在功能表中，移至&#x200B;**影像**&#x200B;並向下捲動以尋找&#x200B;**裁切**。 將其拖曳至畫布上。

![Firefly自訂工作流程](./images/ffcw15.png)

將&#x200B;**裁切**&#x200B;節點放置在&#x200B;**移除背景**&#x200B;節點和&#x200B;**輸出影像**&#x200B;節點之間。

您現在需要移除&#x200B;**移除背景**&#x200B;節點與&#x200B;**輸出影像**&#x200B;節點之間的連線。 您可以連按兩下兩個節點之間的線來達到此目的。

![Firefly自訂工作流程](./images/ffcw16.png)

然後您應該擁有此專案。 將&#x200B;**移除背景**&#x200B;節點連線到&#x200B;**裁切**&#x200B;節點，然後將&#x200B;**裁切**&#x200B;節點連線到&#x200B;**輸出影像**&#x200B;節點。

![Firefly自訂工作流程](./images/ffcw17.png)

核取&#x200B;**自動裁切**&#x200B;的核取方塊，然後按一下&#x200B;**執行**&#x200B;以測試工作流程。

![Firefly自訂工作流程](./images/ffcw18.png)

1-2分鐘後，您應該會看到此畫面，現在會顯示具有不同解析度的影像。

![Firefly自訂工作流程](./images/ffcw19.png)

## 1.7.1.3移除背景+裁切+複合影像

在功能表的&#x200B;**影像**&#x200B;下方，選取&#x200B;**複合影像(2D)**&#x200B;節點，並將其拖曳至畫布上。

![Firefly自訂工作流程](./images/ffcw20.png)

在&#x200B;**複合影像(2D)**&#x200B;節點上，將&#x200B;**裁切的影像**&#x200B;旁的藍色點連線到&#x200B;**輸入影像**&#x200B;旁的藍色點，以新增第二個連線至&#x200B;**裁切**&#x200B;節點。

![Firefly自訂工作流程](./images/ffcw21.png)

在功能表的&#x200B;**輸入和輸出**&#x200B;下，選取&#x200B;**輸入文字**&#x200B;節點，並將其拖曳到畫布上。

將&#x200B;**輸入文字**&#x200B;節點上&#x200B;**文字**&#x200B;旁的綠色點連線到&#x200B;**複合影像(2D)**&#x200B;節點上&#x200B;**提示**&#x200B;旁的綠色點。

![Firefly自訂工作流程](./images/ffcw22.png)

然後您應該擁有此專案。 在&#x200B;**輸入文字**&#x200B;節點中輸入以下提示。

`magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts`

在功能表的&#x200B;**輸入和輸出**&#x200B;下，選取&#x200B;**輸出影像**&#x200B;節點，並將其拖曳到畫布上。

將&#x200B;**複合影像(2D)**&#x200B;節點上&#x200B;**複合影像**&#x200B;旁的藍點連線到&#x200B;**輸出影像**&#x200B;節點上&#x200B;**輸入影像**&#x200B;旁的藍點。

按一下&#x200B;**執行**。

![Firefly自訂工作流程](./images/ffcw23.png)

幾分鐘後，您應該會看到類似這樣的內容，以特定解析度，根據提供的提示在構成中顯示您的原始影像。

![Firefly自訂工作流程](./images/ffcw24.png)

## 1.7.1.4移除背景+裁切+複合影像+產生視訊

在功能表中，移至&#x200B;**視訊**。 選取&#x200B;**產生視訊**&#x200B;節點，並將其拖曳到畫布上。

將&#x200B;**複合影像(2D)**&#x200B;節點的&#x200B;**複合影像**&#x200B;旁的藍點連線到&#x200B;**產生視訊**&#x200B;節點的&#x200B;**輸入影像**&#x200B;旁的藍點。

![Firefly自訂工作流程](./images/ffcw25.png)

在功能表中，移至&#x200B;**輸入和輸出**。 選取&#x200B;**輸入文字**&#x200B;節點，並將其拖曳到畫布上。

將&#x200B;**輸入文字**&#x200B;節點上&#x200B;**文字**&#x200B;旁的綠色點連線到&#x200B;**產生視訊**&#x200B;節點的&#x200B;**提示**&#x200B;旁的綠色點。

在`background hearts fluttering`輸入文字&#x200B;**節點中輸入提示**。

在功能表中，移至&#x200B;**輸入和輸出**。 選取&#x200B;**輸出視訊**&#x200B;節點，並將其拖曳到畫布上。

將&#x200B;**產生視訊**&#x200B;節點的&#x200B;**視訊輸出**&#x200B;旁的紫色點，連線到&#x200B;**輸出視訊**&#x200B;節點上的&#x200B;**視訊**&#x200B;旁的紫色點。

按一下&#x200B;**執行**。

![Firefly自訂工作流程](./images/ffcw26.png)

看完幾個影片後，您應該會看到此畫面，其中會根據提供的影像和提示的組合顯示影片。

![Firefly自訂工作流程](./images/ffcw27.png)

## 1.7.1.5縮放

您現在已針對1個影像完成此作業。 現在，讓我們針對多個影像使用此工作流程。

將這些影像下載到您的案頭：

- [watch.jpg](./assets/watch.jpg)
- [airpods.jpg](./assets/airpods.jpg)

![Firefly自訂工作流程](./images/ffcw28.png)

在工作流程中，返回第一個節點&#x200B;**輸入影像**。 移除目前選取的影像。

![Firefly自訂工作流程](./images/ffcw29.png)

按一下&#x200B;**拖放**&#x200B;區域。

![Firefly自訂工作流程](./images/ffcw30.png)

選取您已下載的3個影像。 按一下&#x200B;**「開啟」**。

![Firefly自訂工作流程](./images/ffcw31.png)

您應該會看到此訊息。 按一下&#x200B;**執行**。

![Firefly自訂工作流程](./images/ffcw32.png)

幾分鐘後，您應該會看到類似的輸出，其中產生3個影像和3個影片。

![Firefly自訂工作流程](./images/ffcw33.png)

## AEM Assets CS中的1.7.1.5存放區

在本練習中，您會將建立為自訂工作流程一部分的資產儲存在AEM Assets CS中。

您應該先在AEM Assets CS環境中建立新資料夾。

若要這麼做，請前往[https://experience.adobe.com](https://experience.adobe.com)。 按一下以開啟&#x200B;**Experience Manager Assets**。

![Firefly自訂工作流程](./images/ffcw50.png)

選取您應命名為`--aepUserLdap-- - CitiSignal AEM + ACCS`的AEM Assets CS環境。

![Firefly自訂工作流程](./images/ffcw51.png)

移至&#x200B;**Assets**&#x200B;並按一下&#x200B;**建立資料夾**。

![Firefly自訂工作流程](./images/ffcw52.png)

輸入名稱： `--aepUserLdap-- - Firefly Custom Workflows`。 按一下&#x200B;**建立**。

![Firefly自訂工作流程](./images/ffcw53.png)

返回您的自訂工作流程，並移至&#x200B;**輸出影像**&#x200B;節點。 按一下&#x200B;**預設**，然後選取&#x200B;**AEM Assets**。

![Firefly自訂工作流程](./images/ffcw57.png)

之後，您應該會看到此快顯視窗。 選取您的AEM Assets CS存放庫，然後選取您剛建立的資料夾，應該命名為： `--aepUserLdap-- - Firefly Custom Workflows`。 按一下&#x200B;**選取**。

![Firefly自訂工作流程](./images/ffcw54.png)

移至&#x200B;**輸出視訊**&#x200B;節點。 按一下&#x200B;**預設**，然後選取&#x200B;**AEM Assets**。

![Firefly自訂工作流程](./images/ffcw55.png)

之後，您應該會看到此快顯視窗。 選取您的AEM Assets CS存放庫，然後選取您剛建立的資料夾，應該命名為： `--aepUserLdap-- - Firefly Custom Workflows`。 按一下&#x200B;**選取**。

![Firefly自訂工作流程](./images/ffcw56.png)

然後您應該擁有此專案。 按一下&#x200B;**執行**。

![Firefly自訂工作流程](./images/ffcw56a.png)

幾分鐘後，您應該會看到建立的資產可在AEM Assets CS的資料夾中使用。

![Firefly自訂工作流程](./images/ffcw58.png)

返回工作流程。 按一下&#x200B;**發佈**。

![Firefly自訂工作流程](./images/ffcw59.png)

您應該會看到此訊息。

![Firefly自訂工作流程](./images/ffcw60.png)

您的工作流程現在已發佈，並且可以在下一個練習中以程式設計方式執行。

## 後續步驟

移至[1.7.2以程式設計方式執行自訂工作流程](./ex2.md){target="_blank"}

返回[Firefly自訂工作流程](./workflowbuilder.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}
