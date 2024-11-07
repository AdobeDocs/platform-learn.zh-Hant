---
title: Microsoft Azure事件中心的區段啟用 — 建立串流區段
description: Microsoft Azure事件中心的區段啟用 — 建立串流區段
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# 2.4.3建立區段

## 2.4.3.1簡介

您將建立一個簡單的區段：

- 當客戶設定檔造訪Luma示範網站的&#x200B;**裝置**&#x200B;頁面時，**對裝置的興趣**。

### 很高興知道

當您符合某個區段的資格（該區段屬於某個目的地的啟用清單的一部分）時，Real-time CDP會觸發對該目的地的啟用。 若是如此，將傳送至該目的地的區段資格承載將包含&#x200B;**您的設定檔符合資格的所有區段**。

此模組的目標是顯示您的客戶設定檔的區段資格已即時傳送至&#x200B;**您的**&#x200B;事件中樞目的地。

### 區段狀態

Adobe Experience Platform中的區段資格一律具有&#x200B;**status** — 屬性，且可為下列其中一項：

- **已實現**：這表示有新的區段資格
- **existing**：這表示有現有的區段資格
- **已退出**：這表示設定檔不再符合區段的資格

## 2.4.3.2建立區段

建立區段在[模組2.3](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)中有詳細說明。

### 建立區段

前往此URL登入Adobe Experience Platform： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

登入後，您會登入Adobe Experience Platform的首頁。

![資料擷取](./../../../modules/datacollection/module1.2/images/home.png)

繼續之前，您必須選取&#x200B;**沙箱**。 要選取的沙箱名為``--aepSandboxName--``。 您可以按一下熒幕上方藍線中的文字&#x200B;**[!UICONTROL Production Prod]**&#x200B;來執行此操作。 選取適當的沙箱後，您會看到畫面變更，現在您已進入專屬沙箱。

![資料擷取](./../../../modules/datacollection/module1.2/images/sb1.png)

移至&#x200B;**區段**。 按一下&#x200B;**+建立區段**&#x200B;按鈕。

![資料擷取](./images/seg.png)

為您的區段命名`--aepUserLdap-- - Interest in Equipment`並新增頁面名稱體驗事件：

按一下&#x200B;**事件**，然後拖放&#x200B;**XDM ExperienceEvent >網頁>網頁詳細資料>名稱**。 輸入&#x200B;**裝置**&#x200B;作為值：

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

拖放&#x200B;**XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**。 輸入`--aepUserLdap--`做為值，將比較引數設定為&#x200B;**包含**，然後按一下&#x200B;**儲存**：

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### PQL定義

您區段的PQL看起來像這樣：

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--aepUserLdap--", false))])
```

下一步： [2.4.4啟動區段](./ex4.md)

[返回模組2.4](./segment-activation-microsoft-azure-eventhub.md)

[返回所有模組](./../../../overview.md)
