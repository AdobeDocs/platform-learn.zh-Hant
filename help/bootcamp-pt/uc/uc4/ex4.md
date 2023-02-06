---
title: Bootcamp -Customer Journey Analytics-Analysis Workspace — 巴西的資料準備
description: Bootcamp -Customer Journey Analytics-Analysis Workspace — 巴西的資料準備
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4準備Customer Journey Analytics

## 奧比蒂沃斯

- 了解UO do Analysis Workspace no CJA
- Entenda os conceitos de preparção de dados no Analysis Workspace
- 阿普倫達，加的卡爾庫洛斯德達多斯

## 4.4.1 UI do Analysis Workspace no CJA

O Analysis Workspace將toda作為limitações típicas de umúnico relatório do Analytics移除。 Ele forence uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes(dimensões, métricas, segmentos e graularidades de tempo)paraum projeto。 Criação instantânea de avarias e segmentos, criação de cortes para análise, criação de alertas, comparção de segmentos, análise de fluxo e falhas e relatórios de curadoria e agendamentto paramportilhar com qualquer pesem seu sengócio.

OCustomer Journey Analyticstraz essa solução além dos dados da platforma。 É altamente recommendável assistir a est vídeo de visão geral de quatro minutos:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

她說，「Analysis Workspace」的意思是：

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### 克里·蘇·普羅耶托

Agora y hora de criar seu primeiro projeto do CJA. CJA中的人。 小組 **新建**.

![示範](./images/prmenu.png)

Em seguida，這是一個彈奏。 選取項 **空白專案** então plicque am **建立**.

![示範](./images/prmenu1.png)

那是我的天。

![示範](./images/premptyprojects.png)

Primeiro, certifique-se de selecionar a Visualização de dados correta no canto super direito da tela. Neste exmelo, Visualização de dados a ser selecionadaé `vangeluwe - Omnichannel Data View`.

![示範](./images/prdv.png)

Em seguida, você irá salvar seu projeto e dar um nome a ele. Você pode usar o seguinte comando para salvar:

| 作業系統 | 短切 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command + S |

Você verá este poup:

![示範](./images/prsave.png)

使用este modelo de nomenclatura:

| 名稱 | 說明 |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

阿姆·西吉達，小團 **儲存**.

![示範](./images/prsave2.png)

## 4.4.2梅特里卡斯計算器

Embora tenhamos organizado todos os components na Visualização de dados, você ainda deve adaptar alguns deles para que os usurios de negócios estejam prontos para iniciar suas análises。 Além disso, durante qualquer processo de analytics, você pode criar métricas calculadas paraprofundar a descoberta de insights.

Como exmo, criaremos uma uma Taxa de conversão calculada usa a métrica/evento Compras que definitos na Visualização de dados。

## 托克桑

我們要做計算師。 小組 **+** 正是梅特里卡計算的Analysis Workspace。

![示範](./images/pradd.png)

O **計算量度產生器** 伊拉·阿帕雷克：

![示範](./images/prbuilder.png)

恩孔特 **購買** 不要菜單，就要點菜。 Em **量度** 團 **全部顯示**

![示範](./images/calcbuildercr1.png)

阿戈拉阿雷斯特與墨西哥 **購買** 那個定義是否是卡爾卡。

![示範](./images/calcbuildercr2.png)

正規，分類 **轉換/工作階段**. Então,Vamos fazer o mesmo cálculo na tela de definição de métrica calculada. 美國 **工作階段** arraste e solte-a no criador de definição, no evento **購買**.

![示範](./images/calcbuildercr3.png)

觀察自動選擇的操作器。

![示範](./images/calcbuildercr4.png)

一個代表波森塔格姆的計程車。 Então, vamos mudar o formato para porcentagem e selecionar 2 casas decimais.

![示範](./images/calcbuildercr5.png)

最後，變更計算量度的名稱和說明：

| 標題 | 說明 |
| ----------------- |-------------| 
| 轉換率 | 轉換率 |

波爾菲姆，或者說，這是一種描述：

![示範](./images/calcbuildercr6.png)

納昂·塞斯克薩 **薩爾瓦爾** 一個墨西哥計算器。

![示範](./images/pr9.png)

## 4.4.3維度計算：Filtros(segmentação)e intervalos de datas

### Filtros:維森斯計算

卡爾庫洛斯·諾·德韋納斯·帕梅特里卡斯。 Antes de iniciar quer análise, também e intersante criar algumas **計算Dimension**. 意義重大， **區段** 不，Adobe Analytics。 沒有Customer Journey Analytics，聖沙馬多斯 **篩選器**.

![示範](./images/prfilters.png)

A criação de filtros ajudará os usuários de negócios a iniciar o analytics com algumas dimensões calculadas valiosas。 Isso irá automatizar algumas tarefas, além de ajudar na parte de adoção. Abaixo estão alguns exemplos:

1. Mídia Própria, Mídia Paga,
2. Visitas novas x recorrentes
3. Clientes com carrinho abandonado

Esses filtros podem ser criados antes ou durante a parte de análise(você fará no próximo mexcrecio)。

### 資料間：天寶計算

如dimensões de tempo são outro tipo de dimensões calculadas。 Alguns já foram criados, mas você também pode criar suas próprias Dimensões de personalizadas na fase de preparção de dados.

Essas Dimensões de tempo calculado ajudarão analistas e uusários de negócios a lembrar data importantes e usá-las para filtrar e alterar e alterar o tempo de relatório. Perguntas e dúvidas típicas quando fazemos análises:

- 庫多有黑色的星期五嗎？ 21 e 29?
- Quando veiculamos aquela campanha de TV em dezembro?
- 2018年的旺達斯·德·維朗？ 查詢比較網2019。 2019年，有人說：

![示範](./images/timedimensions.png)

Agora você總結為準備工作，使Analysis Workspace的CJA。

埃塔帕： [4.5 Visualização usandoCustomer Journey Analytics](./ex5.md)

[烏薩里奧河畔雷托爾](./uc4.md)

[托多斯山](./../../overview.md)
