---
title: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
description: Bootcamp -Customer Journey Analytics-Customer Journey Analytics101 — 巴西
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 3272d288185415b4604fe48f18c19f8f06e6dce0
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# 4.1Customer Journey Analytics101

## 奧比蒂沃斯

- 對CJA的理解
- Entenda qualé o papel do CJA
- CJA的協定或工作流程：dados aos見解

## 4.1.1是Customer Journey Analytics?

Customer Journey Analytics(CJA)forrence uma介面em que os times de Analytics、 Negócios e Tecnologia conseguem unir todos os dados da companisa analysira a jornada cross-channel(online e offline)do cliente de ponta a ponta。 O CJAé capaz de fornecer contextto e clareza para essa jornada, trazendo uma visão acionável em cima dificuldades no processo de conversão e possibilitando o planejamentto de experincias relatientes e personalizadas nos matos相關。

CJA,Analysis Workspace,Adobe Experience Platform。 A s Adobe Experience Platform e o cérebro da comunicação e da orquestração e, com o CJA, as marcas agora podem contextralizar e visualizar todos es dados, paque as e e de negócios e insights possam aprender com eles, analisando toda a jornada on-line para of-off do cliente。

作為設備，e insights podem converar com o CJA, fazer perguntas e obter respostas em tempo real com a interface do usário de arrastar e soltar, apontar e clicar e fácil de usar do Analysis Workspace。

![示範](./images/cja-adv-analysis1.png)

## 4.1.2主要優勢

Os três principais受益於para os clients são:

- 一種能力的解釋 — 見解 — 以及見解（你的，民主化者，或者aos dados）。
- cliente de ver o cliente em jornada與情境相關(ou seja, os dados podem ser visualizados sequencialmente, abrangend múltiplos canais on-line e)。
- A capaidade de approveitar o poder dos dados sem que haja a a secsidade(ou seja, permite que indvíduos usem dados para desbloquear insights e análises profundas para ativação de marketing)。

## 4.1.3 ## 4.1.3是否Customer Journey Analytics?

O CJA não se destina a suctiir um applicativo de BI atual, comoPower BI, Microstrategy, Locker ou Tableau。 O objetivo des aplicativos de BIé visualizar dados para criar painéis corativos para que to dos em uma organizas as métricas importantes rapidamente. O objetivo do CJA e trazer poder de análise para as as essoas de Marketing e Negócios, tornando-o uma ferramenta de análise obrigatória para esssoas



Tradicionalmente, os aplicativos de BI têm sido incapazes de permitir a verdadeira inteligência do cliente:

- Eles não podem fazer atribuição e não fazem análises de jornada do cliente.
- Os aplicativos de BI precisam saber a pergunta com antecedência
- 作為咨詢機構，聖里瑪塔斯，pela estrutura do banco de dados
- SQL的必要性。
- Os aplicativos de BI não permitem que você pergunte o motio de um acontecimento.
- Os aplicativos de BI não têm conexão direta com os pontos de contato do cliente。

波坦托， usuários de negócios e analistas chegam a becos sem saída quase imediatamente, tornando a análise cara, lenta, inflexível e desconectada dos sistemas de ação.

CJA電話：com voê pode ter uma visão completa da jornada do cliente, usando dados offline e, com as ferramentas certas para reduzir o tempo de insight, tornando os usurios susuários de negócios independentes para enter por que algo aconteceu e como isso。

![示範](./images/cja-use-case.png)

## 4.1.4全面Customer Journey Analytics

Antes de iniciar os próximos extrecios, essencial comprender quais etapas são equiárias para trazer dados da Adobe Experience Platform para o CJA para visualizá los e obter alguns insights profundos. 不是說CJA有什麼不妥。 Vamos verificar:

![示範](./images/cja-work-flow.jpg)

Antes de iniciar as etapas acima, não se esqueça da etapa 0, que e creender os dados que estão disponíveis na Adobe Experience Platform。

**垃圾進去，垃圾出去。** Você deve ter uma ideia clara de quais dados estão disponíveis e como os esquemas na Adobe Experience Platform são configurados. Comprender os dados que estão na Adobe Experience Platform facilará as coisas, não só na parte de conexão de dados, mas também na hora de construir visualizações e fazer análises。

## 4.1.5埃塔帕0:完整的量度資料集da Adobe Experience Platform

Faça登入Adobe Experience Platform會取得URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

登入Depois de fazer，是Página inical da Adobe Experience Platform。

![資料擷取](../uc1/images/home.png)

連續、前輪 **沙箱**. 不要用沙箱做選擇 ``Bootcamp``. Você pode fazer isso clicando noícone **[!UICONTROL 生產]** 沒有上司迪雷托達特拉。 Depois de selecionar o sandbox a propriado, você verá a mudando e agora você está em seu sandbox depidado。

![資料擷取](../uc1/images/sb1.png)

Verifique會在資料集中處理結構描述(Adobe Experience Platform)。

| 資料集 | 方案 |
| ----------------- |-------------| 
| 示範系統 — 網站事件資料集（全域v1.1） | 示範系統 — 網站事件結構（全域v1.1） |
| 示範系統 — 客服中心（全域v1.1）的事件資料集 | 示範系統 — 客服中心（全域v1.1）的事件結構 |
| 示範系統 — 語音助理事件資料集（全域v1.1） | 示範系統 — 語音助理的事件結構（全域v1.1） |

Certifique-se de ter verificado menos:

- 身份：CRMID, phoneNumber, ECID，電子郵件。 Quais認同são os identification ados primários, quais são os identification ados secundários?

Você pode encontrar os identification abrindo um schema e observando o objeto `_experienceplatform.identification.core`. Verifique o schema [示範系統 — 網站事件結構（全域v1.1）](https://experience.adobe.com/platform/schema).

![示範](./images/identity.png)

- 探索objeto de comércio dentro do schema [示範系統 — 網站事件結構（全域v1.1）](https://experience.adobe.com/platform/schema).

![示範](./images/commerce.png)

- 視覺化todos os [資料集](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e verifique os dados

Agora você está ponto para começar a usar a interface do usuário doCustomer Journey Analytics。

埃塔帕： [4.2收集資料集da Adobe Experience Platform無Customer Journey Analytics](./ex2.md)

[烏薩里奧河畔雷托爾](./uc4.md)

[托多斯山](../../overview.md)
