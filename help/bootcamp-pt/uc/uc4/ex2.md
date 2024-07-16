---
title: Bootcamp -Customer Journey Analytics — 連線Customer Journey Analytics的Adobe Experience Platform資料集 — 巴西
description: Bootcamp -Customer Journey Analytics — 連線Customer Journey Analytics的Adobe Experience Platform資料集 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 51078fca-f234-4e50-96ba-ee7f5e286869
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 4.2連線資料集至Adobe Experience Platform無Customer Journey Analytics

## 物件

- 比較UI da conexao de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda a ID da pessoa e a compilação de dados
- Aprenda o concept de streaming de dados no Customer Journey

## 4.2.1康菲可

存取[analytics.adobe.com](https://analytics.adobe.com) para acessar oCustomer Journey Analytics。

Na página inicial doCustomer Journey Analytics，存取&#x200B;**連線**。

![示範](./images/cja2.png)

Aqui voce pode ver todas as diferences feitas entre o CJA e a Plataforma. Essas conexos tem o mesmo objetvo dos conjuntos de relatórios no Adobe Analytics. 無內涵，是完整差異的絕佳選擇。 在Adobe Experience Platform中dados vem de datasets的功能。

Vamos criar sua primeira conexao。 點按&#x200B;**建立新連線**。

![示範](./images/cja4.png)

驗證UI **建立連線** UI。

![示範](./images/cja5.png)

Agora voce pode dar um nome à sua conexao.

使用este modelo de nomenclatura： `yourLastName – Omnichannel Data Connection`。

範例： `vangeluw - Omnichannel Data Connection`

無論沙箱或沙箱，都可輕鬆選擇。 沒有功能表沙箱，請選取一個seu沙箱，查詢使用者`Bootcamp`。 巢狀範例， o沙箱為&#x200B;**Bootcamp**&#x200B;的使用者。 **每日事件平均數量**&#x200B;到&#x200B;**小於100萬**。

![示範](./images/cjasb.png)

Após selecionar seu sandbox， voce pode comecar a adicionar datasets a esta conexao. 點按&#x200B;**新增資料集**。

![示範](./images/cjasb1.png)

## 4.2.2在Adobe Experience Platform中選取資料集

對資料集`Demo System - Event Dataset for Website (Global v1.1)`進行預設。 在資料集esta conexao中建立em **+**&#x200B;輔助字元。

![示範](./images/cja7.png)

Agora pesquise e marque as caixas de selecao `Demo System - Event Dataset for Voice Assistants (Global v1.1)`和`Demo System - Event Dataset for Call Center (Global v1.1)`。

我願意，願意。 點按&#x200B;**下一個**。

![示範](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID da pessoa

O objetivo agora é juntar資產資料集。 Para cada資料集seleconado， voce verá um campo chamado **人員ID**。 Cada資料集tem seu próprio campo de ID de pessoa。

![示範](./images/cja11.png)

Comoo voce pode ver，一個自動為使用者提供服務的組織。 我身分是主要的Adobe Experience Platform人。 Como範例， aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`， onde voce pode ver que o Identificador Primário está definido como `phoneNumber`。

![示範](./images/cja13.png)

沒有entando，voce ainda pode influenciar qual identificator será usado para compilar datasets para sua conexao。 Voce pode usar qualquer identificator configurado no esquema vinculado ao seu dataset. 無功能表擱置部分探索作業ID分配資料集。

![示範](./images/cja14.png)

Conforme mencionado， voce pode definir會區分ID de pessoa para cada資料集。 Isso permite reunir diferentes datasets de múltiplas origins no CJA。 想像一下trader NPS ou dados de pesquisa que seriam muito interessantes e úteis para compreender o contexto o motivo de um acontecimento。

不要campo ID da pessoa nao é important， desde que o valor nos campos ID da pessoa corresponda。 Digamos que temos `email` em資料集e `emailAddress` em外部資料集definido como ID da pessoa。 請參閱`delaigle@adobe.com` tiver o mesmo valor para o campo ID da pessoa em ambos os datasets， o CJA poderá compilar os dados。

自動，現有的演演算法超出限制，共通到無任何連結。 以常見的perguntas頻率諮詢： [常見問題](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html)。


### Compilando os dados usando o o ID da pessoa

Agora que voce compende o conceito de compilar datasets usando o ID da pessoa， vamos escolher `email` como ID da pessoa para cada dataset.

![示範](./images/cja15.png)

存取快取資料集引數或ID da pessoa。

![示範](./images/cja12a.png)

Agora preencha o campo ID da pessoa escolhendo o `email` na lista suspensa。

![示範](./images/cja17.png)

Depois de compilar os tres datasets， estamos prontos para continuar.

| 資料集 | 人員 ID |
| ----------------- |-------------| 
| 示範系統 — 網站的事件資料集（全域v1.1） | 電子郵件 |
| 示範系統 — 語音助理的事件資料集（全域v1.1） | 電子郵件 |
| 示範系統 — 客服中心的事件資料集（全域v1.1） | 電子郵件 |

Voce também precisa garantir que， para cada dataset， essas ocoes estejam habilitadas：

- Importar todos os novos dados
- Preencher可執行dados存在作業
- Preencher tipo de fonte de dados com 「其他」
- 預覽資料集mesmo nome do資料集的descriçao com

點按&#x200B;**新增資料集**。

![示範](./images/cja16.png)

小團&#x200B;**儲存** e vá para o próximo excício。 Depois de criar sua **連線**， pode levar algumas horas até que seus dados estejam disponíveis no CJA。

![示範](./images/cja20.png)

Próxima etapa： [4.3 Crie uma Visualização de Dados](./ex3.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
