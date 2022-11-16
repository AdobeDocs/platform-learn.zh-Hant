---
title: Foundation — 即時客戶個人檔案
description: Foundation — 即時客戶個人檔案
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 050e5d99-544d-4a86-a7f6-9f103381dca5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# 3.基礎 — 即時客戶個人檔案

**作者： [沃特·范·蓋盧韋](https://www.linkedin.com/in/woutervangeluwe/)**

在本模組中，我們將深入探討Adobe Experience Platform的即時客戶個人檔案和身分功能。 您將了解如何定義受眾、Identity Service的角色和Experience CloudID，以及如何定義區段產生器查詢以定義您自己的區段。

## 學習目標

- 了解如何透過Adobe Experience Platform的UI將客戶的即時客戶個人檔案視覺化
- 了解如何使用Adobe Experience Platform的區段產生器建立區段
- 了解如何使用Adobe Experience Platform API建立區段，並將區段結果儲存至資料集
- 了解在離線環境中存取完整客戶設定檔（包括即時行為）的影響

## 先決條件

- 存取 [Adobe Experience Platform](https://experience.adobe.com/platform)
- 存取 [https://public.aepdemo.net](https://public.aepdemo.net)
- **下載這些資產**:
   - [Postman集合](./../../assets/postman/postman_profile.zip)

>[!IMPORTANT]
>
>本教學課程的建立是為了便於使用特定研討會格式。 它使用您可能沒有存取權的特定系統和帳戶。 即使沒有訪問權，我們仍然認為，通過閱讀這些非常詳細的內容，您仍可以學到很多。 如果您是其中一個研討會的參與者，並需要您的訪問認證，請聯繫您的Adobe代表，他將向您提供所需資訊。

## 架構概述

請查看下列架構，其中會強調本模組中將討論和使用的元件。

![架構概述](../../assets/images/architecturem3.png)

## 要使用的沙箱

對於此模組，請使用此沙箱： `--aepSandboxId--`.

>[!NOTE]
>
>別忘了安裝、設定和使用Chrome擴充功能，如 [0.1 — 安裝Experience League檔案的Chrome擴充功能](../module0/ex1.md)

## 練習

[3.1訪問網站](./ex1.md)

在本練習中，您將按照指令碼並瀏覽網站。

[3.2將您自己的即時客戶設定檔視覺化 — UI](./ex2.md)

在本練習中，您將登入Adobe Experience Platform，並在UI中檢視您自己的即時客戶個人檔案。

[3.3將您自己的即時客戶個人檔案視覺化 — API](./ex3.md)

在本練習中，您將使用Postman和Adobe I/O，透過Adobe Experience Platform的API來檢視您自己的即時客戶設定檔。

[3.4建立區段 — UI](./ex4.md)

在本練習中，您會使用Adobe Experience Platform的區段產生器來建立區段。

[3.5建立區段 — API](./ex5.md)

在本練習中，您將使用Postman和Adobe I/O，透過Adobe Experience Platform的API來建立區段，並將該區段的結果儲存為資料集。

[3.6在客服中心查看您的即時客戶個人檔案實際運作情況](./ex6.md)

在本練習中，您會模擬接聽客戶來電的客服中心員工。 為了真正影響此客戶的體驗，您需要即時存取所有可用資訊。

[摘要和優點](./summary.md)

本模組的摘要，以及優點的概述。

>[!NOTE]
>
>謝謝你花時間去學習關於Adobe Experience Platform的一切。 如果您有疑問，想要分享對未來內容有建議的一般性反饋，請直接聯繫Wouter Van Geluwe，方法是發送電子郵件至 **vangeluw@adobe.com**.

[返回所有模組](../../overview.md)
