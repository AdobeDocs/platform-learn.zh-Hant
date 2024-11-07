---
title: Customer AI — 評分控制面板和細分（預測並採取行動）
description: Customer AI — 評分控制面板和細分（預測並採取行動）
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# 2.2.3 Customer AI — 評分儀表板和細分（預測和採取行動）

一旦您的Customer AI執行個體完成模型執行，您將能夠視覺化經過評估的傾向分數，以預測客戶在未來30天內執行購買。

![AI](./images/caimodels.png)

>[!NOTE]
>
>只有狀態為&#x200B;**成功**&#x200B;的Customer AI執行個體可讓您預覽服務的深入分析。

## 2.2.3.1傾向性預測

現在，讓我們檢閱Customer AI執行個體模型產生的預測傾向。 按一下例證名稱即可檢視控制面板。

![AI](./images/caimodels1.png)

Customer AI儀表板會顯示分數、母體分佈和模型要評估之影響因素的摘要。

![AI描述](./images/caidescription.png)

![儀表板摘要](./images/caidashboard.png)

暫留在影響因素上，以檢視資料分佈的進一步劃分。

![影響因素](./images/caiinfluencefactors.png)

## 2.2.3.2業務動作

### 2.2.3.2.1劃分客戶

Customer AI儀表板允許按一下即可定義區段。 按一下傾向卡上的&#x200B;**建立區段**&#x200B;按鈕。

![建立區段](./images/caiinfluencefactors1.png)

您會看到區段定義已自動建立。

![區段規則](./images/caicreatesegment.png)

依照此命名慣例，為您的區段命名： `--aepUserLdap-- - Customer AI High Propensity`。 按一下&#x200B;**儲存**。

![區段規則](./images/caicreatesegment1.png)

您現在可以使用此區段來使用進行目標定位，例如Real-time CDP、Journey Orchestration和Adobe Target。

### 2.2.3.2.2設定檔概述

由於Customer AI傾向分數會成為即時客戶個人檔案的一部分，因此您可以檢視個別客戶的分數。

在Adobe Experience Platform中，前往左側功能表中的&#x200B;**設定檔**，然後選取&#x200B;**瀏覽**。

使用任何識別碼搜尋設定檔，例如您擷取的JSON檔案中可用的執行個體&#x200B;**EMAIL hbirkenshawa@businessweek.com**。 按一下&#x200B;**設定檔識別碼**&#x200B;以開啟設定檔。

![輪廓](./images/profile1.png)

然後您會看到以下內容：

![輪廓](./images/profile2.png)

移至&#x200B;**屬性**，其中包含您的Customer AI模型的輸出。

![輪廓](./images/profile3.png)

向下捲動以檢視您的Customer AI模型所計算的傾向分數。

![輪廓](./images/profile4.png)

下一步： [摘要與優點](./summary.md)

[返回模組2.2](./intelligent-services.md)

[返回所有模組](./../../../overview.md)
