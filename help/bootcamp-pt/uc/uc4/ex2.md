---
title: Bootcamp -Customer Journey Analytics — 連接Customer Journey Analytics中的Adobe Experience Platform資料集 — 巴西
description: Bootcamp -Customer Journey Analytics — 連接Customer Journey Analytics中的Adobe Experience Platform資料集 — 巴西
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 2%

---

# 4.2收集資料集da Adobe Experience Platform無Customer Journey Analytics

## 奧比蒂沃斯

- Compresenda a UI da conexão de dados
- Traga os dados da Adobe Experience Platform para o CJA
- 了解ID da pessoa e compilação de dados
- Aprenda o conceito de streaming de dados no Customer Journey

## 4.2.1科內桑

阿塞斯 [analytics.adobe.com](https://analytics.adobe.com) 準Customer Journey Analytics。

我是Customer Journey Analytics，老師 **連線**.

![示範](./images/cja2.png)

Aqui você ver todas a diferentes conexsues entre o CJA e a Platforma. Essas conexões têm o mesmo objetivo dos conjuntos de relatórios no Adobe Analytics。 沒有恩坦托，一個coleta dos dados，完全不同。 Todos os dados vêm da da Adobe Experience Platform。

來點來點來。 小組 **建立新連線**.

![示範](./images/cja4.png)

Você verá a UI **建立連線** UI。

![示範](./images/cja5.png)

Agora você pode dar um nomeà conexão.

使用este modelo de nomenclatura: `yourLastName – Omnichannel Data Connection`.

樣本： `vangeluw - Omnichannel Data Connection`

Você também拒絕選擇沙箱或沙箱。 無菜單沙箱，選擇一個沙箱，按順序 `Bootcamp`. 不用做樣本，要沙箱 **布坎普**. E você também deve definir o **每日事件平均數** to **不到100萬**.

![示範](./images/cjasb.png)

Após selectionar seu sandbox, você pode começar a adicionar資料集a esta conexão. 小組 **新增資料集**.

![示範](./images/cjasb1.png)

## 4.2.2選取資料集 — da Adobe Experience Platform

Pesquise o dataset `Demo System - Event Dataset for Website (Global v1.1)`. 小組 **+** para adicionar或資料集a esta conexão。

![示範](./images/cja7.png)

Agora pesquise e marque as caixas de seleção `Demo System - Event Dataset for Voice Assistants (Global v1.1)` 和 `Demo System - Event Dataset for Call Center (Global v1.1)`.

Em seguida，這是一個彈奏。 小組 **下一個**.

![示範](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID da pessoa

奧比蒂沃·阿戈拉·榮塔爾處理資料集。 Para cada資料集選擇，você verá um campo chamado **人員ID**. Cada資料集項目seu próprio campo de ID de pessoa。

![示範](./images/cja11.png)

Como voê pode ver, a maioria detem o ID da pessoa selecionado automaticamente. Isso ocorre porque um identification principal em selecionado em cada esquema na Adobe Experience Platform。 像我一樣，我是你的 `Demo System - Event Schema for Call Center (Global v1.1)`，從Primário está definido como身份 `phoneNumber`.

![示範](./images/cja13.png)

沒有entanto,você ainda pode influciar qual identification ador será usado para compilar data par a sua conexão。 Você pode usar qualquer identification ador configurado no esquema vinculado seu dataset. 團體無功能表暫停suspenso para explorar os ID disponíveis em cada資料集。

![示範](./images/cja14.png)

Conforme mencionado, você可定義ID de pessoa para cada資料集。 Isso permite會參照CJA上的múltiplas origens資料集。 想像一下NPS是否有意義？

O nome do campo ID da pessoa não e importante, desque o valor nos campos ID da pessoa對應。 迪加摩斯 `email` em um資料集e `emailAddress` em outro資料集定義como ID da pessoa。 Se `delaigle@adobe.com` tiver o mesmo valor para o campo ID da pessoa ambos資料集， o CJA poderá compilar os dados。

Atualmente, existem algumas outras limitações, comportamento anônimo para conhecido. 請參考perguntas頻率aqui: [常見問題集](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=zh-Hant).


### Compilando os dados usando o ID da pessoa

Agora que você能夠構思出合併資料集usando或ID da pessoa, vamos escolher `email` COMO ID da pessoa para cada資料集。

![示範](./images/cja15.png)

Acesse cada資料集para autalizar o ID da pessoa。

![示範](./images/cja12a.png)

阿戈拉·普雷恩查·坎波ID達佩索阿·埃斯科倫多 `email` 暫停。

![示範](./images/cja17.png)

Depois de compilar os três資料集， estamos prontos para continuar。

| 資料集 | 人員 ID |
| ----------------- |-------------| 
| 示範系統 — 網站事件資料集（全域v1.1） | 電子郵件 |
| 示範系統 — 語音助理事件資料集（全域v1.1） | 電子郵件 |
| 示範系統 — 客服中心（全域v1.1）的事件資料集 | 電子郵件 |

Você também precisa garantir que, para cada資料集， essa opções estejam habilitadas:

- 重要的todos os novos dados
- Preencher todos os dados存在論

小組 **新增資料集**.

![示範](./images/cja16.png)

小組 **儲存** 我要去練習。 Depois de criar sua **連線**, pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![示範](./images/cja20.png)

埃塔帕： [4.3 Crie uma Visualização de Dados](./ex3.md)

[烏薩里奧河畔雷托爾](./uc4.md)

[托多斯山](./../../overview.md)
