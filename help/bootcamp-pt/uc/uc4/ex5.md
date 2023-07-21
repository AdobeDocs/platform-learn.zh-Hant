---
title: Bootcamp -Customer Journey Analytics — 使用Customer Journey Analytics的視覺效果 — 巴西
description: Bootcamp -Customer Journey Analytics — 使用Customer Journey Analytics的視覺效果 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Visualizations
exl-id: eb5eac54-22d8-428b-acac-16570f75085e
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1586'
ht-degree: 1%

---

# 4.5Customer Journey Analytics的Visualização usando

## 物件

- Entenda a UI do Analysis Workspace
- Conheca alguns recursos que tornam o Analysis Workspace tao differente.
- Aprenda a analisar no CJA usando o Analysis Workspace

## Contexto

Neste excício、voce usará o Analysis Workspace no CJA para analisar visualizacoes de produtos、funis de produtos、rotatividade等。

Vamos usar o projeto que voce criou em  [4.4 Preparação de dados no Analysis Workspace](./ex4.md)，恩陶訪問 [https://analytics.adobe.com](https://analytics.adobe.com).

![示範](./images/prohome.png)

Abra seu projeto `yourLastName - Omnichannel Analysis`.

Com seu projeto aberto e Visualização de dados `yourLastName - Omnichannel Analysis` selecionado， voce está pronto para comecar a construir suas primeiras visualizacoes.

![示範](./images/prodataView1.png)

## Quantas visualizacoes de productos temo diariamente？

Em primeiro lugar， precisamos selectionar as datas certas para analisar os dados. 享用選單上的吊單do calendário no lado direito da tela。 應用資料間的Clicque nele e selection。

>[!IMPORTANT]
>
>選取資料間隔的共用 **本週** ou **本月**. Os dados disponíveis mais recentes foram reabsorvidos em 19 de setembro de 2022。

![示範](./images/pro1.png)
沒有功能表可以做lado esquerdo (área de componentes)、entry as métricas calculadas **產品檢視**. 選擇 — as e arraste e solte na tela，無上等直立的直立體。

![示範](./images/pro2.png)

自動調整維度 **日** 青紫色青紫色。 Agora voce pode ver sua pergunta respondida immediatamente.

![示範](./images/pro3.png)

Em seguida， clique com o botao direito do mouse no resumo da métrica.

![示範](./images/pro4.png)

小團體 **視覺化** 選擇器 **折線圖** como visualizaçaao.

![示範](./images/pro5.png)

以視覺效果呈現的聲音。

![示範](./images/pro6.png)

Voce pode alterar o escopo de tempo para o dia clicando em **設定** 視覺化可樂。

![示範](./images/pro7.png)

小團無旁托拉多德 **折線圖** e **管理資料來源**.

![示範](./images/pro7a.png)

Em seguida，小團體 **鎖定選取範圍** 選擇器 **選取的專案** para bloquear esta visualização para que ela sempre exiba uma linha do tempo de Visualizacoes de produtos.

![示範](./images/pro7b.png)

## 5種大型製毒機

Quais sao os 5 productos mais vistos？

Lembre-se de salvar o projeto de tempos em tempos。

| 作業系統 | 捷徑 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command + S |

Vamos comecar a encontrar os 5 productos mais vistos. 沒有功能表do lado esquerdo， entry o Nome do produto - Dimensao。

![示範](./images/pro8.png)

Agora arraste e solte **產品名稱** para substituir a dimensao **日**：

敬請期待。

![示範](./images/pro10a.png)

Em seguida， tente dividir um dos produtos por Nome da marca. Pesquise **brandName** 我們排除了生產上要做的事。

![示範](./images/pro13.png)

Em seguida， faca um detalhamento usando o o Agente de usuário. Pesquise **使用者代理** Arraste-o para baixo do nome da marca.

![示範](./images/pro15.png)

Em seguida， será exibida a tela abaixo：

![示範](./images/pro15a.png)

平淡無奇的fim， voce pode adicionar mais visualizacoes. 沒有lado esquerdo， em visualizations， pesquise `Donut`. Pegue `Donut`、arraste solte na tela sob a visualização **折線圖** 

![示範](./images/pro18.png)

接下來，在表格中，選取前5個 **使用者代理**  劃分的列(我們在 **Google Pixel XL 32GB黑色智慧型手機** > **花旗訊號**. 選取5列時，按住 **CTRL** 按鈕（在Windows上）或 **命令** 按鈕(在Mac上)。

Em seguida， na Tabela，選擇primeiras 5 linhas de **使用者代理** 要做些細節工作 **Google Pixel XL 32GB黑色智慧型手機** > **花旗訊號**. 敖選擇其中5號蓮花，0號寶桃 **CTRL** （無Windows）您的博濤 **命令** (無Mac)。

![示範](./images/pro20.png)

其他環圈圖：

![示範](./images/pro21.png)

Voce pode até adaptar o design para ser mais legível， tornando o o gráfico de **折線圖** e o gráfico de **環形圖** um pouco menor para que sejam exibidos lado a lado：

![示範](./images/pro22.png)

小團無旁托拉多德 *環形圖** para **管理資料來源**. Em seguida，小團體 **鎖定選取範圍** para bloquear essa visualização para que ela sempre exiba uma linha do tempo de Visualizacoes de produto。

![示範](./images/pro22b.png)

Saiba mais sobre visualizations usando o o Analysis Workspace em：

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=zh-Hant](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=zh-Hant)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interacao do produto， da visualização à compra

現有的多音符格式解析器esta questão。 Uma delas é usar o Tipo de Interação de Produto e usá-lo em uma tabela de formato livre. Outra forma é usar uma **流失視覺效果**. Vamos usar o último， pois queremos visualizar e analisar ao mesmo tempo.

實際仙人掌蛋糕的糞便：

![示範](./images/pro23.png)

Agora adicione um novo painel em branco clicando em **+新增空白面板**.

![示範](./images/pro24.png)

小團體na visualização de **流失**.

![示範](./images/pro25.png)

前方的Mesmo intervalo de datas do excício。

![示範](./images/prodatef.png)

Em seguida， voce verá：

![示範](./images/prodatefa.png)

輸入維度 **事件型別** nos元件沒有lado esquerdo：

![示範](./images/pro26.png)

維度上的小團體：

![示範](./images/pro27.png)

Voce verá todos os tipos de eventos disponíveis.

![示範](./images/pro28.png)

選取專案或選取專案 **commerce.productViews** e arraste e solte-o no campo **新增接觸點** dentro da **流失視覺效果**.

![示範](./images/pro29.png)

Faca o mesmo com **commerce.productListAdds** 和 **commerce.purchases** e solte-os no campo **新增接觸點** dentro da  **流失視覺效果**. Sua visualização agora deve ser semelhante ao seguinte：

![示範](./images/props1.png)

Voce pode fazer muitas coisas aqui. Alguns範例： comparar ao longo do tempo， comparar cada passo por dispository ou comparar por fidelidade。 沒關係，請見quisermos analisar coisas interessantes como porque os clientes nao compram depois de adicionar um item ao carrinho， podemos usar a melhor ferramenta do CJA： clicar com o botao direito。

Clique com o botao directory do mouse no touchpoint **commerce.productListAdds**. Em seguida，小團體 **在此接觸點劃分流失**.

![示範](./images/pro32.png)

Uma nova tabela de formato livre será criada para analisar o que as pessoas fizeram se nao compraram.

![示範](./images/pro33.png)

替代o **事件型別** 作者： **頁面名稱**，新版tabela de formato livre， para ver em quais páginas eles estao indo， em vez da Página de confirmacao de compra。

![示範](./images/pro34.png)

## 難道沒有場地antes de acsesar a página Cancelar servico嗎？

Novamente， há muitas forma de realizar essa análise. Vamos usar a análise de fluxo para iniciar parte da descoberta.

實際仙人掌蛋糕的糞便：

![示範](./images/pro0.png)

Agora adicione um novo painel em branco clicando em **+新增空白面板**.

![示範](./images/pro0a.png)

視覺化小團體 **流量**.

![示範](./images/pro35.png)

塞吉達島、塞拉埃西比多：

![示範](./images/pro351.png)

前方的Mesmo intervalo de datas do excício。

![示範](./images/pro0b.png)

輸入維度 **頁面名稱** nos元件沒有lado esquerdo：

![示範](./images/pro36.png)

維度上的小團體：

![示範](./images/pro37.png)

聲音以平易近人的方式進入。 帕吉納之名： **取消服務**.
Arraste e solte **取消服務** Na Visualização de fluxo no campo do meio：

![示範](./images/pro38.png)

塞吉達島、塞拉埃西比多：

![示範](./images/pro40.png)

Vamos agora analisar se os clientes que visitaram a página C **取消服務** 沒有網站também ligaram para o call center e qual foi o resultado。

Nas dimensoes， retorne e entre Tipo de interação de chamada. Arraste e solte **通話互動型別** para替代primeira interacao à direita em **流量視覺效果**.

![示範](./images/pro43.png)

Agora voce visualiza o ticket de suporte dos clientes que ligaram para a central de atendimento depois de visitar a página **取消服務**.

![示範](./images/pro44.png)

Em seguida， nas維度，採購 **通話感覺**. Arraste e solte para substituir a primeira interação à direita na visualização de fluxo.

![示範](./images/pro46.png)

塞吉達島、塞拉埃西比多：

![示範](./images/flow.png)

Como pode ver， executamos uma análise omnicchannel usando a visualização de fluxo. Gracas a isso， descobrimos que alguns clientes que estavam pensando em cancelar o servico tiveram uma avaliação positiva depois de ligar para o客服中心。 塔列維斯天生慕達多de ideia com uma promocao？

## Qual é o desempenho dos clientes com contato de Call Center Positivo em relação aos principai KPIs？

Primeiramente， vamos segmentar os dados para obter apenas usuários com chamadas **正面**. 無CJA，無Segmentos sao chamados de Filtros。 Accesse para filtros na área de componentes (no lado esquerdo) e clique em **+**.

![示範](./images/pro58.png)

Dentro do Construtor de filtro， de um nome ao filtro

| 名稱 | 說明 |
| ----------------- |-------------| 
| 通話感覺 — 正面 | 通話感覺 — 正面 |

![示範](./images/pro47.png)

Nos元件(dentro do Construtor de filtro)、entre **通話感覺** Arraste e solte na Definicao do constructor de filtro.

![示範](./images/pro48.png)

Agora選擇器 **正面** 篩選的共同valor para。

![示範](./images/pro49.png)

Altere o escopo para o nivel **個人**.

![示範](./images/pro50.png)

部分完成，部分點按em **儲存**.

![示範](./images/pro51.png)

恩濤，請迴音。 看吧，老兄，去畫前畫吧。

![示範](./images/pro0c.png)

Agora adicione um novo painel em branco clicando em **+新增空白面板**.

![示範](./images/pro24c.png)

前方的Mesmo intervalo de datas do excício。

![示範](./images/pro24d.png)

小團體 **自由表格**.

![示範](./images/pro52.png)

Agora arraste e solte o filtro que voce acabou de criar.

![示範](./images/pro53.png)

天蠍座Hora de adicionar algumas métricas。 Com網站 **產品檢視**. Arraste e solte na tabela de forma livre. Voce também pode excluir a métrica **事件**.

![示範](./images/pro54.png)

Faca o mesmo com **人員**， **加入購物車** e **購買**. Voce vai acabar com uma tabela como a seguinte.

![示範](./images/pro55.png)

Gracas à primeira análise de fluxo， uma nova pergunta surgiu。 Entao decisimos criar esta tabela e verificar alguns KPIem um segmento para responder a essa pergunta。 Como voce pode ver， o tempo de insight é muito mais rápido do que usar SQL ou usar outtras solutions de BI。

## Recapitulaçao do Analysis Workspace e do Customer Journey Analytics

O Analysis Workspace移除todas as limitacoes típicas de um relatório do Analytics。 Ele fornece uma tela robusta e flexível para criar project de analytics personalizados. Arraste e solte qualquer número de tabelas de dados， visualizacoes e componentes (dimensoes， métricas， segmentos e granularidades de tempo) para um projeto. Voce pode criar de forma instantanea filtros e analises， gráficos de coorte， alertas， segmentos， análises de fluxo e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

冰淇淋甜菜： [4.6 De Insights a acao](./ex6.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
