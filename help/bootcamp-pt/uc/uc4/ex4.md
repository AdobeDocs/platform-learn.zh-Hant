---
title: Bootcamp -Customer Journey Analytics — 在Analysis Workspace準備資料 — 巴西
description: Bootcamp -Customer Journey Analytics — 在Analysis Workspace準備資料 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: d56128af-dd1e-47ea-922f-85418e9da687
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4 Preparacao de dados emCustomer Journey Analytics

## 物件

- Entenda a UO do Analysis Workspace no CJA
- Entenda os conceitos de preparação de dados no Analysis Workspace
- Aprenda a fazer cálculos de dados

## 4.4.1 UI do Analysis Workspace無CJA

O Analysis Workspace移除todas as limitacoes típicas de um único relatório do Analytics。 Ele fornece uma tela robusta e flexível para criar project de analytics personalizados. Arraste e solte qualquer número de tabelas de dados， visualizacoes e componentes (dimensoes， métricas， segmentos e granularidades de tempo) para um projeto. Criação instantanea de avarias e segmentos， criação de cortes para análise， criação de alertas， comparação de segmentos， análise de fluxo e de falhas e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

OCustomer Journey Analyticstraz essa solução além dos dados da plataforma。 在此，我們建議您assistir a este vídeo de visao geral de quatro minutos：

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

在Analysis Workspace的祖先上，建議祖先：

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### Crie Seu專案

Agora é hora de criar seu primeiro projeto do CJA. Vá para a aba de projetos dentro do CJA. 小團體 **新建**.

![示範](./images/prmenu.png)

真好，敬請期待。 選擇器 **空白專案** entao clique em **建立**.

![示範](./images/prmenu1.png)

Voce verá um projeto vazio.

![示範](./images/premptyprojects.png)

Primeiro， certifique-se de selececonar a Visualização de dados correta no canto superior direito da tela. Neste範例，一個Visualização de dados a ser selectionada é `vangeluwe - Omnichannel Data View`.

![示範](./images/prdv.png)

Em seguida， voce irá salvar seu projeto e dar um nome a ele. Voce pode usar o seguinte comando para salvar：

| 作業系統 | 捷徑 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command + S |

Voce verá este快顯：

![示範](./images/prsave.png)

使用este modelo de nomenclatura：

| 名稱 | 說明 |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em seguida，小團體 **儲存**.

![示範](./images/prsave2.png)

## 4.4.2梅特里卡斯電腦

Embora tenhamos organizado todos os componentes na Visualização de dados， voce ainda deve adaptar alguns dels para que os usuários de negócios estejam prontos para iniciar suas análises. Além disso， durante qualquer processo de analytics， voce pode criar métricas calculadas para proprofundar a descoberta de insights.

Como範例，criaremos uma Taxa de converso calculada usando a metric/evento Compras que definimos na Visualização de dados。

## 轉換分類法

Vamos comecar a abrir o constructor de métricas calculadas. 小團體 **+** 在Analysis Workspace上計算過的初級美術。

![示範](./images/pradd.png)

O **計算量度產生器** 伊拉·阿帕雷克：

![示範](./images/prbuilder.png)

參與 **購買** métricas na lista de métricas no menu do lado esquerdo. Em **量度** 小團體 **全部顯示**

![示範](./images/calcbuildercr1.png)

Agora arraste e solte a metric **購買** 一個美體計算器。

![示範](./images/calcbuildercr2.png)

Normalmente， taxa de conversão significa **轉換/工作階段**. Entao， vamos fazer o mesmo cálculo na tela de definicao de métrica calculada. 進入媒體 **工作階段** e arraste e solte-a no criador de definicao，no evento **購買**.

![示範](./images/calcbuildercr3.png)

觀察運算元自動選取。

![示範](./images/calcbuildercr4.png)

Taxa de conversão é commente representada em porcentagem. Entao， vamos mudar o formato para porcentagem e selecesionar 2 casas decismais.

![示範](./images/calcbuildercr5.png)

最後，變更計算量度的名稱和說明：

| 標題 | 說明 |
| ----------------- |-------------| 
| 轉換率 | 轉換率 |

朋友們，請改名，以美食為主題：

![示範](./images/calcbuildercr6.png)

Nao se esqueca de **Salvar** 一個美體電腦。

![示範](./images/pr9.png)

## 4.4.3維度電腦：Filtros (segmentacao) e intervalos de datas

### 篩選：維度計算

Os cálculos nao devem ser apenas para métricas. Antes de iniciar qualquer análise， também é interessante criar algumas **計算Dimension**. 這是重要的，重要的， **區段** 無Adobe Analytics。 無Customer Journey Analytics，esses segmentos sao chamados de **篩選器**.

![示範](./images/prfilters.png)

A criação de filtros ajudará os usuários de negócios a iniciar o analytics com algumas dimensoes calculadas valiosas. Isso irá automatizar algumas tarefas， além de ajudar na parte de adocao. Abaixo演演算法範例：

1. 米迪亞普洛普利亞，帕加，
2. Visitas novas x recorrentes
3. 使用者端com carrinho abandonado

Esses filtros podem ser criados antes ou durante a parte de análise (o que voce fará no próximo exercício)。

### 資料間隔：時間計算的維度

如同維度de tempo sao outro tipo de dimensoes calculadas。 Alguns já foram criados， mas voce também pode criar suas próprias Dimensoes de tempo personalizadas na fase de preparação de dados.

Essas Dimensoes de tempo calculado ajudarao analistas e usuários de negócios a lembrar datas important e usá-las para filtrar e alterar o tempo de relatório. 佩爾貢塔斯·烏維達斯·蒂皮卡斯·坎多·法澤莫斯·阿納利塞斯：

- 全島在黑色星期五可以吃到嗎？ Entre os dias 21 e 29？
- Quando veiculamos aquela campanha de TV em dezembro？
- De quando a quando fizemos as vendas de verao de 2018？ Quero comparar com 2019. 2019年Voce sabe os dias exatos em？

![示範](./images/timedimensions.png)

Agora voce concluiu o excício de preparação de dados usando o o Analysis Workspace do CJA.

冰淇淋甜菜： [4.5 Visualização usandoCustomer Journey Analytics](./ex5.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
