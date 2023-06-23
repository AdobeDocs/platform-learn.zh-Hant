---
title: Bootcamp -Customer Journey Analytics — 連線Customer Journey Analytics的Adobe Experience Platform資料集 — 巴西
description: Bootcamp -Customer Journey Analytics — 連線Customer Journey Analytics的Adobe Experience Platform資料集 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 51078fca-f234-4e50-96ba-ee7f5e286869
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# 4.2連線資料集至Adobe Experience Platform無Customer Journey Analytics

## 物件

- 比較UI da conexao de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda a ID da pessoa e a compilacao de dados
- Aprenda o構想了Streaming de dados no Customer Journey

## 4.2.1康菲可

Acesse [analytics.adobe.com](https://analytics.adobe.com) 段落存取或Customer Journey Analytics。

Customer Journey Analytics的日常生活，訪問 **連線**.

![示範](./images/cja2.png)

Aqui voce pode ver todas as diferences conexoes feitas enter o CJA e a Plataforma. Essas conexoes tem o mesmo objetvo dos conjuntos de relatórios no Adobe Analytics. 無內涵，是互補差異的絕佳選擇。 Todos os dados vem de datasets da Adobe Experience Platform。

Vamos criar sua primeira conexao。 小團體 **建立新連線**.

![示範](./images/cja4.png)

驗證UI **建立連線** UI。

![示範](./images/cja5.png)

Agora voce pode dar um nome à sua conexao.

使用este modelo de nomenclatura： `yourLastName – Omnichannel Data Connection`.

範例： `vangeluw - Omnichannel Data Connection`

沙箱與沙箱之間的虛擬選擇器。 無功能表沙箱，選取一個搜尋沙箱，搜尋搜尋沙箱 `Bootcamp`. 巢狀範例， o沙箱使用者檔案o **Bootcamp**. E voce também deve definir o **平均每日事件數** 至 **少於100萬**.

![示範](./images/cjasb.png)

Após seliconar seu sandbox， voce pode comecar a adicionar datasets a esta conexao. 小團體 **新增資料集**.

![示範](./images/cjasb1.png)

## 4.2.2 Adobe Experience Platform中的選取資料集

在資料集上預設 `Demo System - Event Dataset for Website (Global v1.1)`. 小團體 **+** para adicionar o dataset a esta conexao.

![示範](./images/cja7.png)

Agora pesquise e marque as caixas de selecao `Demo System - Event Dataset for Voice Assistants (Global v1.1)` 和 `Demo System - Event Dataset for Call Center (Global v1.1)`.

真好，敬請期待。 小團體 **下一個**.

![示範](./images/cja9.png)

## 4.2.3 ID da pessoa e compilacao de dados

### ID da pessoa

O objetvo agora é juntar搜尋資料集。 Para cada資料集selecionado， voce verá um campo chamado **個人ID**. Cada資料集tem seu próprio campo de ID de pessoa.

![示範](./images/cja11.png)

Comoo voce pode ver，自動建立ID為pessoa seleconado的區段。 身分識別主講人selecionado em cada esquema na Adobe Experience Platform。 Como範例、aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`，確認身分的榮耀 `phoneNumber`.

![示範](./images/cja13.png)

無entando，voce ainda pode influenciar qual identificator será usado para compilar datasets para sua conexao。 Voce pode usar qualquer identificator configurado no esquema vinculado ao seu dataset. 無功能表擱置部分探索作業系統IDdisponíveis em指令資料集。

![示範](./images/cja14.png)

符合mencionado， voce pode definir會區分ID de pessoa para cada資料集。 Isso permite reunir diferentes datasets de múltiplas origins no CJA. 想像一下trader NPS ou dados de pesquisa que seriam muito interessantes e úteis para compreender o contexto o motivo de um acontecimento。

不要campo ID da pessoa nao é important， desde que o valor nos campos ID da pessoa responderda。 Digamos que temos `email` em um資料集e `emailAddress` 超出資料集定義共用ID比索阿。 Se `delaigle@adobe.com` Tiver o mesmo valor para o campo ID da pessoa em ambos os datasets， o CJA poderá compilar os dados.

專案、現有的演演算法超越限制、共通性、匿名性、關聯性。 諮詢為perguntas frequentes aqui： [常見問題集](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=zh-Hant).


### Compilando os dados usando o o ID da pessoa

Agora que voce compreende o conceito de compilar datasets usando o o ID da pessoa， vamos escolher `email` como ID da pessoa para cada資料集。

![示範](./images/cja15.png)

存取Cada資料集paraAutoalizar或ID da個人檔案。

![示範](./images/cja12a.png)

Agora preencha o campo ID da pessoa escolhendo o `email` 清淡的懸念。

![示範](./images/cja17.png)

Depois de compilar os tres datasets， estamos prontos para continuar.

| 資料集 | 人員 ID |
| ----------------- |-------------| 
| 示範系統 — 網站的事件資料集（全域v1.1） | 電子郵件 |
| 示範系統 — 語音助理的事件資料集（全域v1.1） | 電子郵件 |
| 示範系統 — 客服中心的事件資料集（全域v1.1） | 電子郵件 |

Voce também precisa garantir que， para cada dataset， essas opcoes estejam habilitadas：

- Importar todos os novos dados
- Preencher可執行OS Dados存在作業
- Preencher tipo de fonte de dados com 「其他」
- 預覽資料集mesmo nome do資料集的descrição com

小團體 **新增資料集**.

![示範](./images/cja16.png)

小團體 **儲存** 要練習的動作。 Depois de criar sua **連線**，pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![示範](./images/cja20.png)

冰淇淋甜菜： [4.3 Crie uma Visualização de Dados](./ex3.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
