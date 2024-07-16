---
title: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
description: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
exl-id: 63933d9e-b774-483f-b547-188c77440595
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 0%

---

# 4.1Customer Journey Analytics101

## 物件

- 對CJA進行擴充
- CJA檔案
- CJA工作流程的相關資訊：da conexao de dados aos insights

## 4.1.1Customer Journey Analytics？

OCustomer Journey Analytics(CJA) fornece uma介面em que os times de Analytics， Negócios e Tecnologia conseguem unir todos os dados da companhia e analisar a jornada跨管道（線上e離線）do cliente de ponta a ponta。 O CJA é capaz de fornecer contexto e clareza para essa jornada， trazendo uma visao acionável em cima das dificuldades no processo de converso e possibilitando o o planejamento de experiencias releves e personalizadas nos pontos mais relevents.

O CJA traz o Analysis Workspace conectado à Adobe Experience Platform. A Adobe Experience Platform é é cérebro da comunicação e da orquestração e， com o CJA， as marcas agora podem contextualizar e visualizar todos esses dados， para que as equipes de negócios e insights posam aprender com elees， analisando toda a jornada online para off-line do cliente.

作為equipes de negócios e insights podem conversar com o CJA， fazer perguntas e obter repostas em tempo real com a interface do usuário de arrastar e soltar， apontar e clicar e fácil de usar do Analysis Workspace。

![示範](./images/cja-adv-analysis1.png)

## 4.1.2主要利器

Os tres principais benefícios para os clientes sao：

- Capacidade de disponibilizar insights para todos (ou seja， democratizar o acesso aos dados)。
- 一個客戶群的capacidade de ver cliente em uma jornada context (ou seja， os dados podem ser visualizados sequencialmente， abrangendo múltiplos canais online e offline)。
- A capacidade de approveitar o poder dos dados sem que haja a necessidade (ou seja， permite que indivíduos usem dados para debloquear insights e análises profundas para ativacao de marketing)。

## 4.1.3 ## 4.1.3 Por que escolher oCustomer Journey Analytics？

O CJA nao se destina substituir um applicativo de BI autoal， comoPower BI， Microstrategy， Locker ou Tableau. O objetivo desses applicativos de BI é visualizar dados para criar painéis corporativos para que todos em uma organizaçao possam ver métricas importantes rapidamente. O objetivo do CJA é trazer poder de análise para as equipes de Marketing e Negócios， tornando-o uma ferramenta de análise obricatória para essas pessoas



Tradicionalmente， os applicativos de BI tem sido incapazes de permitir a verdadeira inteligencia do cliente：

- Eles nao podem fazer atribuicao e nao fazem análises de jornada do cliente.
- Os applicativos de BI precisam saber a pergunta com antecedencia
- 作為顧問聖有限制組織
- Habilidades de SQL sao necessárias.
- Os applicativo de BI nao permitem que voce pergunte o motivo de um acontecimento.
- Os applicativos de BI nao tem conexao direta com os pontos de contato do cliente。

Portanto， usuários de negócios e analistas chegam a becos sem saída quase imediatamente， tornando a análise cara， lenta， inflexível e desconectada dos sistemas de acao.

com o CJA voce pode ter uma visao completa da jornada do cliente， usando dados offline e online， com as ferramentas certas para reduzir o tempo de insight， tornando os usuários de negócios independents para entender por que algo aconteceu e como responder a isso.

![示範](./images/cja-use-case.png)

## 4.1.4卡波河通貨Customer Journey Analytics

Antes de iniciar os próximos exercícios， é essencial compender quais etapas sao necessárias para trados da Adobe Experience Platform para o CJA para visualizá-los e obter alguns insights profunds. 我們來做個查默斯·德·卡巴略。 Vamos verificar：

![示範](./images/cja-work-flow.jpg)

Antes de iniciar as etapas acima， nao se esqueca da etapa 0， que é compender os dados que estao disponíveis na Adobe Experience Platform.

**記憶體輸入，記憶體輸出。** Voce deve ter uma ideia clara de quais dados estao disponíveis e como os esquemas na Adobe Experience Platform sao configurados。 以coisas， nao só na parte de conexao de dados， mas também na hora de construir visualizacoes e fazer análises為由dados que estão na Adobe Experience Platform facilitará as coisas， nao só na parte de conexao de dados， mas também na hora de construir visualizacoes e fazer análises.

## 4.1.5 Etapa 0：Adobe Experience Platform資料集的Compreender esquemas e資料集

Faca登入Adobe Experience Platform acessando URL： [https://experience.adobe.com/platform](https://experience.adobe.com/platform)。

Depois de fazer登入，voce irá acsesar a página inicial da Adobe Experience Platform。

![資料擷取](../uc1/images/home.png)

Antes de continuar， voce precisa selectionar um **沙箱**。 不要做沙箱，請選取``Bootcamp``。 Voce pode fazer isso clicando no ícone **[!UICONTROL Prod]**&#x200B;沒有上級direito da tela。 Depois de selectionar o sandbox aprioado， voce verá a tela mudando e agora voce esta em seu sandbox dedicado.

![資料擷取](../uc1/images/sb1.png)

在Adobe Experience Platform中驗證資料集結構描述。

| 資料集 | 綱要 |
| ----------------- |-------------| 
| 示範系統 — 網站的事件資料集（全域v1.1） | 示範系統 — 網站的事件結構（全域v1.1） |
| 示範系統 — 客服中心的事件資料集（全域v1.1） | 示範系統 — 客服中心的事件結構（全域v1.1） |
| 示範系統 — 語音助理的事件資料集（全域v1.1） | 示範系統 — 語音助理的事件結構（全域v1.1） |

墨西哥灣仔仔仔仔雞：

- 身分： CRMID、phoneNumber、ECID、電子郵件。 Quais identidades sao os identificadores primários， quais sao os identificadores secundários？

Voce pode encontrrar os identificadores abrindo um schema e observando o o objeto `_experienceplatform.identification.core`。 驗證結構描述[示範系統 — 網站的事件結構描述（全域v1.1）](https://experience.adobe.com/platform/schema)。

![示範](./images/identity.png)

- 探索o objeto de comércio dentro do schema [示範系統 — 網站的事件結構描述（全域v1.1）](https://experience.adobe.com/platform/schema)。

![示範](./images/commerce.png)

- 視覺化待辦事項os [資料集](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e驗證待辦事項os dados

Agora voce está pronto para comecar a usar a interface do usuário doCustomer Journey Analytics。

Próxima etapa： [4.2 Conecte資料集da Adobe Experience Platform無Customer Journey Analytics](./ex2.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](../../overview.md)
