---
title: Bootcamp -Customer Journey Analytics — 使用Customer Journey Analytics的視覺效果 — 巴西
description: Bootcamp -Customer Journey Analytics — 使用Customer Journey Analytics的視覺效果 — 巴西
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 3272d288185415b4604fe48f18c19f8f06e6dce0
workflow-type: tm+mt
source-wordcount: '1586'
ht-degree: 1%

---

# 4.5 Visualização usando oCustomer Journey Analytics

## 奧比蒂沃斯

- 了解UI do Analysis Workspace
- Conheça alguns會經常發生Analysis Workspace的不同。
- Aprenda analysiras o CJA usando o Analysis Workspace

## Contextto

Neste mextricio, você usará o Analysis Workspace no CJA paranalisar visualizações de productos, funis de produtos, rotatividade等。

我們要說  [4.4準備工作：Analysis Workspace](./ex4.md), então acesse [https://analytics.adobe.com](https://analytics.adobe.com).

![示範](./images/prohome.png)

阿布拉塞烏普羅耶托 `yourLastName - Omnichannel Analysis`.

Com seu projeto aberto e Visualização de dados `yourLastName - Omnichannel Analysis` selecionado, você está pronto para começar a construir suas primeiras visualizações.

![示範](./images/prodataView1.png)

## Quantas visualizações de productemos diariamente?

Em primeiro lugar, precisamos selecionar作為資料。 Acesse o menu suspenso do calendário no lado direito da tela. Clickue nele e selecione o intervalo de datas aplicável.

>[!IMPORTANT]
>
>選擇資料 **本週** 歐 **本月**. 2022年，Os dados disponíveis mais會被吸收。

![示範](./images/pro1.png)
沒有菜單可以叫做Lado Esquerdo(Área de componentes)，以Métricas計數器 **產品檢視**. Selectione-as e arraste e solte na tela, no canto super direito da tabela de forma livre.

![示範](./images/pro2.png)

自動修改維度 **日** 塞拉·阿迪西奧納達·帕拉·克里亞·蘇阿·普里米拉·塔貝拉。 Agora você pode ver sua pergunta respondida imediatamente.

![示範](./images/pro3.png)

Em seguida, botão direito的pricus com do mouse no resuso da métrica.

![示範](./images/pro4.png)

小組 **視覺化** e選擇 **折線圖** como visualização.

![示範](./images/pro5.png)

Você verá as suas visualizações de produto por dia.

![示範](./images/pro6.png)

Você pode alterar o escopo de tempo para o dia clicando em **設定** 視覺效果。

![示範](./images/pro7.png)

無邦托拉多 **折線圖** e **管理資料來源**.

![示範](./images/pro7a.png)

阿姆·西吉達，小團 **鎖定選擇** e選擇 **所選項目** para bloquear esta visualização para que ela sempre exiba uma linha do tempo de Visualizações de produtos。

![示範](./images/pro7b.png)

## 5件產品

Quais são os 5 productos mais vistos?

Lembre-se de salvar o projeto de tempos em tempos.

| 作業系統 | 短切 |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Command + S |

5件產品是肉製品。 沒有菜單，沒有菜單。

![示範](./images/pro8.png)

阿戈拉阿雷斯特 — 索爾特 **產品名稱** 準替代 **日**:

這是結果。

![示範](./images/pro10a.png)

Em seguida, tente didir um dos productos por Nome da marca. 佩斯基斯 **brandName** arraste para baixo do primeiro nome do produto.

![示範](./images/pro13.png)

阿姆·西吉達，烏薩里奧的法薩。 佩斯基斯 **使用者代理** arraste-o para baixo do nome da marca.

![示範](./images/pro15.png)

Em seguida, será exibida a tela abaixo:

![示範](./images/pro15a.png)

Por fim, você pode adicionar mais visualizações. 沒有lado esquerdo, em visualizações, pesquise `Donut`. 佩格 `Donut`, arraste e solte na tela sob visualizção **折線圖** 

![示範](./images/pro18.png)

接下來，在表格中選取前5個 **使用者代理**  的資料列 **Google Pixel XL 32GB黑色智慧手機** > **Citi Signal**. 選取5列時，請保留 **CTRL** 按鈕（在Windows上）或 **命令** 按鈕(在Mac上)。

Em seguida, na Tabela,selecione as primeiras 5 linhas de **使用者代理** 迪塔勒門托，比塞莫斯 **Google Pixel XL 32GB黑色智慧手機** > **Citi Signal**. Ao Selecionar為5行，segure o botão **CTRL** （無Windows）ou o botão **命令** (不是Mac)。

![示範](./images/pro20.png)

Você verá o gráfico de donut alterado:

![示範](./images/pro21.png)

Você pode até adaptar o design para ser mais legível, tornando o gráfico de **折線圖** 歐·德 **環形圖** 歐姆普科門諾，帕拉克塞亞姆塞比多斯，拉多，拉多。

![示範](./images/pro22.png)

無邦托拉多 *環形圖** **管理資料來源**. 阿姆·西吉達，小團 **鎖定選擇** para bloquear essa visualização para que ela sempre exiba uma linha do tempo de Visualizações de produto.

![示範](./images/pro22b.png)

Saiba mais sobre visualizações usando o Analysis Workspace am:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interação do produto, da visualizaçãoà compra

現有的muitas formas de resolver esta questão. Uma delas e usar o Tipo de Interação de Producto e usá-lo em uma tabela de formato livre. 烏特拉福馬 **流失視覺效果**. Vamos usar oúltimo, pois queremos visualizar e analisar ao mesmo tempo.

Feche o painel atual clicando aqui:

![示範](./images/pro23.png)

從頭到尾的阿戈拉·阿迪西奧內 **+新增空白麵板**.

![示範](./images/pro24.png)

視覺化團體 **流失**.

![示範](./images/pro25.png)

前面有運動的，前面有中間的。

![示範](./images/prodatef.png)

Em seguida,você verá:

![示範](./images/prodatefa.png)

Encontre a dimensão **事件類型** nos元件無lado esquerdo:

![示範](./images/pro26.png)

Clickus na seta para abrir a dimensu:

![示範](./images/pro27.png)

Você verá todos os Tipos de eventos disponíveis.

![示範](./images/pro28.png)

選擇一個項目 **commerce.productViews** 阿拉斯特 — 索爾特 — o no campo **新增接觸點** 登特羅達 **流失視覺效果**.

![示範](./images/pro29.png)

Faça o mesmo com **commerce.productListAdds** 和 **commerce.purchases** e solte-os no campo **新增接觸點** 登特羅達  **流失視覺效果**. Sua visualização agora deve semelhante ao seguinte:

![示範](./images/props1.png)

Você pode fazer muitas coisas aqui. 演算法執行者：比較ao longo do tempo，比較cada passo por dispositivo ou comparar por fidelidade。 沒有entanto, se quisermos analisar coisas intersates como porque os clientes não compram depois de adicionar um item a o carrinho, podemos usar a melhor ferramenta do CJA:clicar com o botão direito.

Clickue com o botão direito執行滑鼠無接觸點 **commerce.productListAdds**. 阿姆·西吉達，小團 **在此接觸點劃分流失**.

![示範](./images/pro32.png)

Uma nova tabela de formato livre será criada paranalisar o que, as pessoas fizeram se não compraram.

![示範](./images/pro33.png)

Altere o **事件類型** by **頁面名稱**, na nova tabela de formato livre, par a em quais páginas eles estão indo, em vez da Página de confirmmação de compra.

![示範](./images/pro34.png)

## 比如說，不要有網站監督你的事？

諾瓦門特，我的愛，我的愛。 我們要去做一個，去做那些不合法的人。

Feche o painel atual clicando aqui:

![示範](./images/pro0.png)

從頭到尾的阿戈拉·阿迪西奧內 **+新增空白麵板**.

![示範](./images/pro0a.png)

視覺化團體 **流量**.

![示範](./images/pro35.png)

西吉達，塞拉：

![示範](./images/pro351.png)

前面有運動的，前面有中間的。

![示範](./images/pro0b.png)

Encontre a dimensão **頁面名稱** nos元件無lado esquerdo:

![示範](./images/pro36.png)

Clickus na seta para abrir a dimensu:

![示範](./images/pro37.png)

Você將Vocará作為Páginas的景象。 我要說： **取消服務**.
阿拉斯特·索爾特 **取消服務** na Visualização de fluxo n campo do meio:

![示範](./images/pro38.png)

西吉達，塞拉：

![示範](./images/pro40.png)

Vamos agora analisar se os clientes que visitaram a página C **取消服務** 沒有站點também ligaram para o call center e qual fo i o resultado。

Nas dimensões, retore encontre e Tipo de interção de chamada. 阿拉斯特·索爾特 **呼叫互動類型** para suplity interação á dirita em **流量視覺效果**.

![示範](./images/pro43.png)

Agora você visualiza o ticket de suporte dos clientes que ligaram para a central de atendimento depois de visitar a página **取消服務**.

![示範](./images/pro44.png)

Em seguida, nas dimensões, procure **呼叫感覺**. Arraste e solte para suptiir a primeira interaçãoà direita visualização de fluxo.

![示範](./images/pro46.png)

西吉達，塞拉：

![示範](./images/flow.png)

Como pode ver, executamos uma análise omnichannel usando a visualização de fluxo. Graças a isso, descobrimos que alguns clientes que estavam pensando em cancerar o serviço tiveram uma avaliação positiva depois de ligar para o call center. Talvez tenhamos mudado de ideia com uma promoção?

## Qualé o desempenho dos clientes com um contato de Call center Positivo em relação aos principais KPIs?

Primeiramente, vamos segmentar os dados para obter apenas usuários com chamadas **正面**. 沒有CJA,Segmentos são chamados de Filtros。 Acesse para filtros na área de components(no lado esquerdo)e clium **+**.

![示範](./images/pro58.png)

Dentro do Construtor de filtro, dê um nome ao filtro

| 名稱 | 說明 |
| ----------------- |-------------| 
| 呼叫感覺 — 積極 | 呼叫感覺 — 積極 |

![示範](./images/pro47.png)

Nos元件(Dentro do Construtor de filtro), encontre **呼叫感覺** arraste e solte na Definição do construtor de filtro.

![示範](./images/pro48.png)

阿戈拉·塞萊翁 **正面** 科莫·瓦洛·帕羅·菲爾特羅。

![示範](./images/pro49.png)

Altere o escopo para o nível **人員**.

![示範](./images/pro50.png)

Para finalizar, basta clicar em **儲存**.

![示範](./images/pro51.png)

恩唐，我要回去。 Se ainda não retronou, feche o painel areotor areo。

![示範](./images/pro0c.png)

從頭到尾的阿戈拉·阿迪西奧內 **+新增空白麵板**.

![示範](./images/pro24c.png)

前面有運動的，前面有中間的。

![示範](./images/pro24d.png)

小組 **自由表格**.

![示範](./images/pro52.png)

阿戈拉·阿拉斯特·索爾特·奧爾特·奧卡布·德·克里亞爾。

![示範](./images/pro53.png)

Hora de adicionar algumas métricas. Comece com **產品檢視**. Arraste e solte na tabela de forma livre. 梅特里卡州 **事件**.

![示範](./images/pro54.png)

Faça o mesmo com **人員**, **新增至購物車** e **購買**. Você via acabar com uma tabela co mo a seguinte.

![示範](./images/pro55.png)

Graçasà primeira análise de fluxo, uma nova pergunta surgiu. Então decidimos criar esta tabela e verificar alguns KPIs em segmento para responder a essa pergunta。 Como voê pode ver, o tempo de insighté muito rápido do que usar SQL ou usar outras soluções de BI.

## Requestulação do Analysis Workspace e doCustomer Journey Analytics

O Analysis Workspace會將todas移除為limitações típicas de um relatório do Analytics。 Ele forence uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes(dimensões, métricas, segmentos e graularidades de tempo)paraum projeto。 Você pode criar de forma instantânea filtros e analises, gráficos de coorte, alertas, segmentos, análises de fluxo e relatórios de curadoria e agendamentto para compartilhar com quer pessoa em seu negócio.

埃塔帕： [4.6 De insights a ação](./ex6.md)

[烏薩里奧河畔雷托爾](./uc4.md)

[托多斯山](./../../overview.md)
