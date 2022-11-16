---
title: Customer AI — 計分控制面板和區段（預測並採取動作）
description: Customer AI — 計分控制面板和區段（預測並採取動作）
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 57d6c714-5d41-4ac1-8e60-3000da45b76e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# 5.3客戶AI — 計分控制面板和區段（預測並採取動作）

一旦您的Customer AI例項完成模型執行，就能將評估的傾向分數視覺化，以預測客戶在未來30天內進行購買。

![AI](./images/caimodels.png)

>[!NOTE]
>
>只有狀態為 **成功** 可讓您預覽服務的深入分析。

## 5.3.1傾向預測

現在來檢閱Customer AI例項模型產生的預測傾向。 按一下執行個體名稱以檢視控制面板。

![AI](./images/caimodels1.png)

Customer AI控制面板會顯示分數、人口分佈以及模型評估影響因素的摘要。

![AI說明](./images/caidescription.png)

![控制面板摘要](./images/caidashboard.png)

將滑鼠指標暫留在影響因素上，即可檢視資料分送的進一步劃分。

![影響因素](./images/caiinfluencefactors.png)

## 5.3.2業務行動

### 5.3.2.1劃分客戶

Customer AI控制面板可讓您按一下以定義區段。 按一下 **建立區段** 按鈕。

![建立區段](./images/caiinfluencefactors1.png)

您會看到區段定義已自動建立。

![區段規則](./images/caicreatesegment.png)

依照此命名慣例為您的區段命名： `--demoProfileLdap-- - Customer AI High Propensity`. 按一下「**儲存**」。

![區段規則](./images/caicreatesegment1.png)

您現在可以使用此區段來定位，以用於例項Real-time CDP、Journey Orchestration和Adobe Target。

### 5.3.2.2設定檔概述

由於Customer AI傾向分數成為即時客戶設定檔的一部分，因此您可以檢視個別客戶的分數。

在Adobe Experience Platform中，前往 **設定檔** 在左側功能表中，並選取 **瀏覽**.

使用任何識別碼(例如 **電子郵件hbirkenshawa@businessweek.com**，可在您擷取的JSON檔案中使用。 按一下 **設定檔ID** 來開啟設定檔。

![設定檔](./images/profile1.png)

然後您會看到：

![設定檔](./images/profile2.png)

前往 **屬性**，包含來自您Customer AI模型的輸出。

![設定檔](./images/profile3.png)

向下捲動以查看依您的Customer AI模型計算的「傾向分數」。

![設定檔](./images/profile4.png)

下一步： [摘要和優點](./summary.md)

[返回模組5](./intelligent-services.md)

[返回所有模組](./../../overview.md)
