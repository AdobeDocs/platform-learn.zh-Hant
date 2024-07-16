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
source-wordcount: '1569'
ht-degree: 0%

---

# 4.5視覺化砂桑多洛Customer Journey Analytics

## 物件

- Analysis Workspace的Entenda a UI
- Conheca alguns recursos que tornam或Analysis Workspace陶差異。
- Aprenda a analisar no CJA usando o o Analysis Workspace

## Contexto

Neste excício， voce usará o Analysis Workspace no CJA para analisar visualizacoes de produtos， funis de produtos， rotatividade等。

Vamos usar o projeto que voce criou em [4.4 Preparacao de dados no Analysis Workspace](./ex4.md)， entao acesse [https://analytics.adobe.com](https://analytics.adobe.com)。

![示範](./images/prohome.png)

Abra seu專案`yourLastName - Omnichannel Analysis`。

Com seu projeto aberto e Visualização de dados `yourLastName - Omnichannel Analysis` seleconado， voce está pronto para comecar a construir suas primeiras visualizacoes.

![示範](./images/prodataView1.png)

## Quantas visualizacoes de productos temos diarimente？

Em primeiro lugar， precisamos selectionar as datas certas para analisar os dados. 存取選單暫停do calendário no lado direito da tela。 小團體可為應用資料進行篩選。

>[!IMPORTANT]
>
>選取um intervalo de datas como **本週** ou **本月**。 Os dados disponíveis mais recentes foram absorvidos em 19 de setembro de 2022。

![示範](./images/pro1.png)
沒有功能表do lado esquerdo (área de componentes)，以métricas calculadas **產品檢視**&#x200B;輸入。 選擇 — as e arraste e solte na tela，無上級direito da tabela de forma livre。

![示範](./images/pro2.png)

自動調整維度&#x200B;**日** será adicionada para criar sua primeira tabela。 Agora voce pode ver sua pergunta respondida imediatamente.

![示範](./images/pro3.png)

Em seguida， clique com o botao direito do mouse no resumo da métrica.

![示範](./images/pro4.png)

Clique em **視覺化**&#x200B;選取一個&#x200B;**行** como視覺化。

![示範](./images/pro5.png)

以視覺化方式呈現生產資料的聲音。

![示範](./images/pro6.png)

Voce pode alterar o escopo de tempo para o dia clicando em **設定** na visualizacao。

![示範](./images/pro7.png)

Clique no ponto ao lado de **行** e **管理資料Source**。

![示範](./images/pro7a.png)

Em seguida，按一下em **鎖定選取專案** e選取專案&#x200B;**選取的專案** para bloquear esta visualizacao para que ela sempre exiba uma linha do tempo de Visualizacoes de produtos。

![示範](./images/pro7b.png)

## 5種大型海蝰

Quais sao os 5產品大熒幕？

Lembre-se de salvar o projeto de tempos em tempos.

| 作業系統 | 捷徑 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command + S |

Vamos comecar a encontrar os 5 product mais vistos. 沒有選單do lado esquerdo，請進入Nome do product - Dimensao。

![示範](./images/pro8.png)

Agora arraste e solte **產品名稱** para替代維度&#x200B;**日**：

看看結果如何。

![示範](./images/pro10a.png)

Em seguida， tente dividir um dos produtos por Nome da marca. 請預設&#x200B;**brandName** e arraste para baixo do primeiro nome do product。

![示範](./images/pro13.png)

Em seguida， faca um detalhamento usando o o Agente de usuário. 請預設&#x200B;**使用者代理程式** e arraste-o para baixo do nome da marca。

![示範](./images/pro15.png)

塞吉達語，切除tela abaixo：

![示範](./images/pro15a.png)

平底鞋，點綴成桌上型鞋，視覺效果。 沒有lado esquerdo， em visualizacoes， pesquise `Donut`。 Pegue `Donut`， arraste e solte na tela sob a visualização **行** 

![示範](./images/pro18.png)

接下來，在表格中，從我們在&#x200B;**Google Pixel XL 32GB黑色智慧型手機** > **花旗訊號**&#x200B;下進行的劃分中，選取前5個&#x200B;**使用者代理程式**&#x200B;列。 選取5列時，按住&#x200B;**CTRL**&#x200B;按鈕（在Windows上）或&#x200B;**命令**&#x200B;按鈕(在Mac上)。

Em seguida， na Tabela， selecone as primeiras 5 linhas de **使用者代理程式**&#x200B;會詳細解釋fizemos em **Google Pixel XL 32GB黑色智慧型手機** > **花旗訊號**。 Ao selecionar as 5 linhas，選擇o botao **CTRL** （無Windows） ou botao **命令** (無Mac)。

![示範](./images/pro20.png)

雲端甜甜圈：

![示範](./images/pro21.png)

Voce pode até adaptar o design para ser mais legível， tornando o o gráfico de **Line** e o gráfico de **Donut** um pouco menor para que sejam exibidos lado a lado：

![示範](./images/pro22.png)

Clique no ponto ao lado de *Donut** para **管理資料Source**。 Em seguida， clique em **鎖定選擇** para bloquear essa visualização para que ela sempre exiba uma linha do tempo de Visualizacoes de produto。

![示範](./images/pro22b.png)

Saiba mais sobre visualizations usando o Analysis Workspace em：

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interacao do produto， da visualização à compra

Existem muitas forms de resolver esta questão. Uma delas é usar o Tipo de Interação de Produto e usá-lo em uma tabela de formato livre. Outra forma é usar uma **流失視覺效果**。 Vamos usar o último， pois queremos visualizar e analisar ao mesmo tempo.

雕塑雕塑雕塑雕塑：

![示範](./images/pro23.png)

Agora adicione um novo painel em branco clicando em **+新增空白面板**。

![示範](./images/pro24.png)

小團體na visualização de **流失**。

![示範](./images/pro25.png)

在前方選取資料行銷的mesmo intervalo de data。

![示範](./images/prodatef.png)

Em seguida， voce verá：

![示範](./images/prodatefa.png)

輸入維度&#x200B;**事件型別** nos元件無lado esquerdo：

![示範](./images/pro26.png)

維度上的小團體：

![示範](./images/pro27.png)

總之我們總算有了Tipos de eventos disponíveis。

![示範](./images/pro28.png)

選取專案&#x200B;**commerce.productViews** e arraste e solte-o no campo **新增接觸點** dentro da **流失視覺效果**。

![示範](./images/pro29.png)

Faca o mesmo com **commerce.productListAdds**&#x200B;和&#x200B;**commerce.purchases** e solte-os no campo **新增接觸點** dentro da **流失視覺效果**。 Sua visualização agora deve ser semelhante ao seguinte：

![示範](./images/props1.png)

Voce pode fazer muitas coisas aqui. Alguns範例： comparar ao longo do tempo， comparar cada passo por dispositio ou comparar por fidelidade。 無內涵，請參閱quisermos analisar coisas interessantes como porque os clientes nao compram depois de adicionar um item ao carrinho， podemos usar a melhor ferramenta do CJA： clicar com o botao direito。

點按一下com o botao direito do mouse沒有接觸點&#x200B;**commerce.productListAdds**。 Em seguida，點選此接觸點的em **劃分流失**。

![示範](./images/pro32.png)

Uma nova tabela de formato livre será criada para analisar o que as pessoas fizeram se nao compraram.

![示範](./images/pro33.png)

由&#x200B;**Page Name**&#x200B;進行的&#x200B;**活動型別**&#x200B;變更，新版tabela de formato livre， para ver em quais páginas estao indo， em vez da Página de confirmacao de compra。

![示範](./images/pro34.png)

## 沒有網站可以存取帕吉納取消式服務？

Novamente， muitas forms de realizar essa análise. Vamos usar a análise de fluxo para iniciar parte da descoberta.

雕塑雕塑雕塑雕塑：

![示範](./images/pro0.png)

Agora adicione um novo painel em branco clicando em **+新增空白面板**。

![示範](./images/pro0a.png)

Clicque na visualizacao **流量**。

![示範](./images/pro35.png)

塞吉達島，塞吉比多：

![示範](./images/pro351.png)

在前方選取資料行銷的mesmo intervalo de data。

![示範](./images/pro0b.png)

輸入維度&#x200B;**頁面名稱** nos元件無lado esquerdo：

![示範](./images/pro36.png)

維度上的小團體：

![示範](./images/pro37.png)

聲音以平吉納斯視窗結束。 進入密碼名稱： **取消服務**。
Arraste e solte **取消服務** na Visualizaao de fluxo no campo do meio：

![示範](./images/pro38.png)

塞吉達島，塞吉比多：

![示範](./images/pro40.png)

Vamos agora analisar se os clientes que visitaram a página C **取消服務**&#x200B;沒有網站também ligaram para o呼叫中心e qual foi o resultado。

Nas dimensoes， retorne e entry Tipo de interação de chamada. 排程完成&#x200B;**呼叫互動型別** para替代直接的primeira interacao à direita em **流量視覺效果**。

![示範](./images/pro43.png)

Agora voce visualiza o ticket de suporte dos clientes que ligaram para a central de atendimento depois de visitar a página **取消服務**。

![示範](./images/pro44.png)

Em seguida， nas dimensoes，採購&#x200B;**通話感覺**。 以純品來替代品的Arraste e solte para substitures a direita na visualização de fluxo。

![示範](./images/pro46.png)

塞吉達島，塞吉比多：

![示範](./images/flow.png)

Como pode ver， executamos uma análise omnicchannel usando a visualização de fluxo. Gracas a isso， descobrimos que alguns clientes que estavam pensando em cancelar o servico tiveram uma avaliação positiva depois de ligar para o呼叫中心。 Talvez tenhamos mudado de ideia com uma promocao？

## Qual é o desempenho dos clientes com contato de Call center Positivo em relação aos principais KPIs？

Primeiramente， vamos segmentar os dados para obter apenas usuários com chamadas **正面**。 無CJA，無Segmentos sao chamados de Filtros。 Accesse para filtros na área de componentes （無lado esquerdo） e clique em **+**。

![示範](./images/pro58.png)

Dentro do Construtor de filtro， de um name ao filtro

| 名稱 | 說明 |
| ----------------- |-------------| 
| 通話感覺 — 正面 | 通話感覺 — 正面 |

![示範](./images/pro47.png)

Nos元件(dentro do Construtor de filtro)，輸入&#x200B;**Call Feeling** e arraste solte na Definicao do construtor de filtro。

![示範](./images/pro48.png)

Agora選擇器&#x200B;**正面**&#x200B;共用valor para o篩選。

![示範](./images/pro49.png)

**人員**&#x200B;的備用escopo para o nível。

![示範](./images/pro50.png)

Para最終處理，Basta點按em **儲存**。

![示範](./images/pro51.png)

恩陶，請迴音。 看吧，小菜一碟。

![示範](./images/pro0c.png)

Agora adicione um novo painel em branco clicando em **+新增空白面板**。

![示範](./images/pro24c.png)

在前方選取資料行銷的mesmo intervalo de data。

![示範](./images/pro24d.png)

建立&#x200B;**自由格式表格**&#x200B;的群組。

![示範](./images/pro52.png)

以濾色的方式進行排列。

![示範](./images/pro53.png)

魔術師之星屬。 Comece com **產品檢視**。 為現場製作排程。 Voce também pode excluir a métrica **活動**。

![示範](./images/pro54.png)

Faca o mesmo com **人員**，**加入購物車** e **購買**。 Voce vai acabar com uma tabela como a seguinte.

![示範](./images/pro55.png)

Gracas à primeira análise de fluxo， uma nova pergunta surgiu. Entao decisimos criar esta tabela e verificar alguns KPIem um segmento para responder a essa pergunta。 Como voce pode ver， o tempo de insight é muito mais rápido do que usar SQL ou usar outtras solutions de BI。

## Recapitulação do Analysis Workspace e do Customer Journey Analytics

O Analysis Workspace移除了todas as limitacoes típicas de um relatório do Analytics。 Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados， visualizacoes e components (dimensoes， métricas， segmentos e granularidades de tempo) para um projeto. Voce pode criar de forma instantanea filtros e analises， gráficos de coorte， alertas， segmentos， análises de fluxo e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

Próxima etapa： [4.6 De Insights a acao](./ex6.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
