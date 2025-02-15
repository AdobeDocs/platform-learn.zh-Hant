---
title: Bootcamp - Customer Journey Analytics - Analysis Workspace的資料準備 — 巴西
description: Bootcamp - Customer Journey Analytics - Analysis Workspace的資料準備 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Workspace Basics, Calculated Metrics
exl-id: d56128af-dd1e-47ea-922f-85418e9da687
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# 4.4 Preparação de dados em Customer Journey Analytics

## 物件

- Entenda a UO do Analysis Workspace no CJA
- Entenda os conceitos de preparação de dados no Analysis Workspace
- 卡魯庫洛斯·德·達多斯魔法師的阿普倫達

## 4.4.1 UI do Analysis Workspace no CJA

O Analysis Workspace移除了todas as limitacoes típicas de um único relatório do Analytics。 Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados， visualizacoes e components (dimensoes， métricas， segmentos e granularidades de tempo) para um projeto. Criação instantanea de avarias e segmentos， criação de cortes para análise， criação de alertas， comparação de segmentos， análise de fluxo e de falhas e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

O Customer Journey Analytics traz essa solução além dos dados da plataforma. 您還可在此點選幾分鐘：

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on&enablevpops)

在Analysis Workspace的祖先上課，建議你：

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on&enablevpops)

### Crie Seu專案

Agora é hora de criar seu primeiro projeto do CJA。 Vá para aba de projetos dentro do CJA. 點按&#x200B;**新建**。

![示範](./images/prmenu.png)

我願意，願意。 選取&#x200B;**空白專案** entao clique em **建立**。

![示範](./images/prmenu1.png)

Voce verá um projeto vazio.

![示範](./images/premptyprojects.png)

Primeiro， certifique-se de selecionar a Visualização de dados correta no canto superior direito da tela. Neste範例， a Visualização de dados a ser selecitoonada é `vangeluwe - Omnichannel Data View`。

![示範](./images/prdv.png)

Em seguida， voce irá salvar seu projeto e dar um nome a ele. Voce pode usar o seguinte comando para salvar：

| 作業系統 | 捷徑 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command + S |

語音快顯：

![示範](./images/prsave.png)

使用este modelo de nomenclatura：

| 名稱 | 說明 |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em seguida，點按&#x200B;**儲存**。

![示範](./images/prsave2.png)

## 4.4.2梅特里卡斯電腦

Embora tenhamos organizado todo os components na Visualização de dados， voce ainda deve adaptar alguns dels para que os usuários de negócios estejam prontos para iniciar suas análises. Além disso， durante qualquer processo de analytics， voce pode criar métricas calculadas para profundar a descoberta de insights.

Como範例， criaremos uma Taxa de converso calculado usando a metric/evento Compras que definimos na Visualização de dados。

## 轉換的分類法

Vamos comecar a abrir o constructor de métricas calculadas. 在Analysis Workspace上建立群組&#x200B;**+** para criar sua primeira Media calculada。

![示範](./images/pradd.png)

O **計算量度產生器** irá aparecer：

![示範](./images/prbuilder.png)

進入&#x200B;**購買** na lista de métricas no menu do lado esquerdo。 Em **量度** clique em **全部顯示**

![示範](./images/calcbuildercr1.png)

Agora arraste e solte a métrica **購買** na definicao da métrica calculada。

![示範](./images/calcbuildercr2.png)

Normalmente， taxa de conversão signifa **轉換/工作階段**。 Entao， vamos fazer o mesmo cálculo na tela de definicao de metric calculada. 進入媒體&#x200B;**工作階段**&#x200B;排程e solte-a no criador de definicao，無事件&#x200B;**購買**。

![示範](./images/calcbuildercr3.png)

觀察運算元自動選取的差異。

![示範](./images/calcbuildercr4.png)

A taxa de conversão é commente representada em porcentagem. Entao， vamos mudar o formato para porcentagem e seleciconar 2 casas decismais.

![示範](./images/calcbuildercr5.png)

最後，變更計算量度的名稱和說明：

| 標題 | 說明 |
| ----------------- |-------------| 
| 轉換率 | 轉換率 |

冰淇淋、冰淇淋、冰淇淋：

![示範](./images/calcbuildercr6.png)

Nao se esqueca de **Salvar** a Métrica電腦。

![示範](./images/pr9.png)

## 4.4.3維度電腦：Filtros (segmentacao) e intervalos de datas

### 篩選：維度計算

Os cálculos nao devem ser apenas para métricas. Antes de iniciar qualquer análise， também é interessante criar algumas **已計算的維度**。 Adobe Analytics上的Isso重要性， essencialmente， **區段**。 無Customer Journey Analytics，esses segmentos sao chamados de **篩選器**。

![示範](./images/prfilters.png)

A criação de filtros ajudará os usuários de negócios a iniciar o analytics com algumas dimensoes calculadas valiosas。 Isso irá automatizar algumas tarefas， além de ajudar na parte de adocao. Abaixo演演算法範例：

1. 米迪亞普洛普利亞，米迪亞帕加，
2. Visitas novas x recorrentes
3. 客戶公司放棄購買

Esses filtros podem ser criados antes ou durante a parte de análise (o que voce fará no próximo exercício)。

### 資料間隔：時間計算的維度

如維度所示。 Alguns já foram criados， mas voce também pode criar suas próprias Dimensoes de tempo personalizadas na fase de preparação de dados.

Essas Dimensoes de tempo calculado ajudarao analistas e usuários de negócios a lembrar datas important e usá-las para filtrar e alterar o tempo de relatório. 佩爾貢塔斯·烏維達斯·提皮卡斯·全都·法澤莫斯·阿納利塞斯：

- 全島黑色星期五不吃香腸？ Entre os dias 21 e 29？
- 全都veiculamos aquela campanha de TV em dezembro？
- De quando a quando fizemos as vendas de verao de 2018？ Quero comparar com 2019。 2019年sabe os dias exatos em的提案？

![示範](./images/timedimensions.png)

Agora voce conclouiu o excício de preparação de dados usando o o Analysis Workspace do CJA.

Próxima etapa： [4.5 Visualizaao usando Customer Journey Analytics](./ex5.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
