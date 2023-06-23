---
title: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
description: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 63933d9e-b774-483f-b547-188c77440595
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# 4.1Customer Journey Analytics101

## 物件

- Entenda o que o CJA
- CJA的紙品文案
- Entenda o工作流程do CJA： da conexao de dados aos insights

## 4.1.1 O que oCustomer Journey Analytics？

OCustomer Journey Analytics(CJA) fornece uma介面em que os times de Analytics， Negócios e Tecnologia conseguem unir todos os dados da companhia e analisar a jornada cross-channel （線上e offline）do cliente de ponta a ponta。 O CJA é capaz de forneceer contexto e clareza para essa jornada， trazendo uma visao acionável em cima das dificuldades no processo de converso e posibilitando o o planejamento de experiencias relevantes e personalizadas nos pontos mais relevantes.

O CJA traz o Analysis Workspace conectado à Adobe Experience Platform。 A Adobe Experience Platform é é cérebro da comunicação e da orquestração e， com o CJA， as marcas agora podem contextualizar e visualizar todos esses dados， para que as equipes de negócios e insights posam aprender com eles， analisando toda a jornada online para off-line do cliente.

作為equipes de negócios e insights podem conversar com o CJA， fazer perguntas e obter repostas em tempo real com a interface do usuário de arrastar e soltar， apontar e clicar e fácil de usar do Analysis Workspace。

![示範](./images/cja-adv-analysis1.png)

## 4.1.2 Principais vantagens

Os tres principais benefícios para os clientes sao：

- Capacidade de disponibilizar insights para todos (ou seja， democratizal o acesso aos dados)。
- A capacidade de ver cliente em uma jornada context (ou seja， os dados podem ser visualizados sequencialmente， abrangendo múltiplos canais online e off-line)。
- A capacidade de approveitar o poder dos dados sem que haja a necessidade (ou seja， permite que indivíduos usem dados para descloquear insights e análises profundas para ativacao de marketing)。

## 4.1.3 ## 4.1.3 Por que escolher oCustomer Journey Analytics？

O CJA nao se destina substituir um applicativo de BI atual、comoPower BI、Microstrategy、Locker ou Tableau。 O objetivo desses applicativos de BI é visualizar dados para criar painéis corporativos para que todos em uma organização possam ver métricas importantes rapidamente. O objetivo do CJA é traser poder de análise para as equiees de Marketing e Negócios， tornando-o uma ferramenta de análise obricatória para essas pessoas



Tradicionalmente， os applicativos de BI tem sido incapazes de permitir a verdadeira inteligencia do cliente：

- Eles nao podem fazer atribuicao e nao fazem análises de jornada do cliente.
- Os applicativos de BI precisam saber a pergunta com antecedencia
- 作為顧問聖利米塔達斯銀行
- Habilidades de SQL sao necessárias.
- Os applicativos de BI nao permitem que voce pergunte o motivo de um acontecimento。
- Os applicativos de BI nao tem conexao direta com os pontos de contato do cliente。

Portanto， usuários de negócios e analistas chegam a becos sem saída quase imediatamente， tornando a análise cara， lenta， inflexível e desconectada dos sistemas de acao.

Com o CJA voce pode ter uma visao completa da jornada do cliente， usando dados offline e online， com as ferramentas certas para reduzir o tempo de insight， tornando os usuários de negócios independents para entender por que algo aconteceu e como responder a isso。

![示範](./images/cja-use-case.png)

## 4.1.4 Compreenda o fluxo de trabalho doCustomer Journey Analytics

Antes de iniciar os próximos exercícios， é é essencial compender quais etapas sao necessárias para dados da Adobe Experience Platform para o CJA para visualizá-los e obter alguns insights profunds。 我們很清楚chamamos de fluxo de trabalho do CJA。 Vamos驗證器：

![示範](./images/cja-work-flow.jpg)

Antes de iniciar as etapas acima， nao se esqueca da etapa 0， que é compender os dados que estão disponíveis na Adobe Experience Platform.

**垃圾進，垃圾出。** Voce deve ter uma ideia clara de quais dados estao disponíveis e como os esquemas na Adobe Experience Platform sao configurados。 以coisas、nao só na parte de conexão de dados、mas também na hora de construir visualizacoes e fazer análises為Adobe Experience Platform facilitará的元件。

## 4.1.5 Etapa 0：Adobe Experience Platform資料集的Compender esquemas e資料集

Faca登入Adobe Experience Platform存取URL： [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer登入，voce irá存取página incial da Adobe Experience Platform。

![資料擷取](../uc1/images/home.png)

Antes de continuar， voce precisa seclecionar um **沙箱**. 不要做沙箱，只要選擇一個 ``Bootcamp``. Voce pode fazer isso clicando no ícone **[!UICONTROL Prod]** 沒有上乘的直立線。 Depois de selecionar o sandbox apriado， voce verá a tela mudando e agora voce está em seu sandbox dedicado。

![資料擷取](../uc1/images/sb1.png)

在Adobe Experience Platform中驗證結構描述和資料集。

| 資料集 | 方案 |
| ----------------- |-------------| 
| 示範系統 — 網站的事件資料集（全域v1.1） | 示範系統 — 網站的事件結構（全域v1.1） |
| 示範系統 — 客服中心的事件資料集（全域v1.1） | 示範系統 — 客服中心的事件結構（全域v1.1） |
| 示範系統 — 語音助理的事件資料集（全域v1.1） | 示範系統 — 語音助理的事件結構描述（全域v1.1） |

Certifique-se de ter verificado ao menos：

- 身分： CRMID、電話號碼、ECID、電子郵件。 Quais identidades sao os identificadores primários， quais sao os identificadores secundários？

Voce pode contract os identificadores abrindo um schema e observando o o objeto `_experienceplatform.identification.core`. 結構描述驗證 [示範系統 — 網站的事件結構（全域v1.1）](https://experience.adobe.com/platform/schema).

![示範](./images/identity.png)

- 探索商業實體結構描述的目標 [示範系統 — 網站的事件結構（全域v1.1）](https://experience.adobe.com/platform/schema).

![示範](./images/commerce.png)

- 視覺化待辦事項作業系統 [資料集](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) 驗證作業系統dados

Agora voce está pronto para comecar a usar a interface do usuário doCustomer Journey Analytics。

冰淇淋甜菜： [4.2連線資料集至Adobe Experience Platform無Customer Journey Analytics](./ex2.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](../../overview.md)
