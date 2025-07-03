---
title: Offer Decisioning — 設定優惠和決定ID
description: Offer Decisioning — 設定優惠和決定ID
kt: 5342
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 13%

---

# 3.7.2設定優惠方案與決定

## 3.7.2.1建立您的個人化優惠

在本練習中，您將建立四個&#x200B;**個人化優惠方案**。 以下是建立這些優惠方案時要考慮的詳細資料：

| 名稱 | 日期範圍 | 電子郵件的影像連結 | 網頁的影像連結 | 文字 | 優先順序 | 適用性 | 語言 | 上限頻率 | 影像名稱 |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|:-------:|:-------:|
| `--aepUserLdap-- - AirPods Max` | 今天 — 1個月後 | https://bit.ly/4a9RJ5d | 從Assets資料庫選擇 | `{{ profile.person.name.firstName }}, 10% discount on AirPods Max` | 25 | 全部 — 女性客戶 | 英文 (美國) | 3 | Apple AirPods Max- Female.jpg |
| `--aepUserLdap-- - Galaxy S24` | 今天 — 1個月後 | https://bit.ly/3W8yuDv | 從Assets資料庫選擇 | `{{ profile.person.name.firstName }}, 5% discount on Galaxy S24` | 15 | 全部 — 女性客戶 | 英文 (美國) | 3 | Galaxy S24 - Female.jpg |
| `--aepUserLdap-- - Apple Watch` | 今天 — 1個月後 | https://bit.ly/4fGwfxX | https://bit.ly/4fGwfxX | `{{ profile.person.name.firstName }}, 10% discount on Apple Watch` | 25 | 全部 — 男性客戶 | 英文 (美國) | 3 | Apple Watch - Male.jpg |
| `--aepUserLdap-- - Galaxy Watch 7` | 今天 — 1個月後 | https://bit.ly/4gTrkeo | 從Assets資料庫選擇 | `{{ profile.person.name.firstName }}, 5% discount on Galaxy Watch 7` | 15 | 全部 — 男性客戶 | 英文 (美國) | 3 | Galaxy Watch7 - Male.jpg |

{style="table-layout:auto"}

前往[Adobe Experience Cloud](https://experience.adobe.com)登入Adobe Journey Optimizer。 按一下&#x200B;**Journey Optimizer**。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

您將被重新導向到Journey Optimizer中的&#x200B;**首頁**&#x200B;檢視。 首先，確定您使用正確的沙箱。 要使用的沙箱稱為`--aepSandboxName--`。 然後您就會進入沙箱&#x200B;**的**&#x200B;首頁`--aepSandboxName--`檢視。

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 後續步驟

移至Experience Decisioning的[3.7.3網頁SDK設定](./ex3.md){target="_blank"}

返回[體驗決策](ajo-decisioning.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
