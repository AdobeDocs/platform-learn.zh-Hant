---
title: Bootcamp -Customer Journey Analytics — 建立資料檢視 — 巴西
description: Customer Journey Analytics — 建立資料檢視 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Data Views
exl-id: 8cfd4467-167d-4235-a305-4596e3a7d4fb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 3%

---

# 4.3 Crie uma Visualização de Dados

## 物件

- Entenda a UI de Visualização de Dados
- Compreenda as configuracoes básicas de definicao de visita
- Compreenda a atribuicao e a Persistencia em uma Visualização de

## 4.3.1達多斯的視覺化創作

Agora， com sua conexao concleída， é possível progredir para influenciar a visualização. Uma diferenca entre o Adobe Analytics e o CJA é que o CJA precia de uma visualização de dados para limpar e preparar os dados antes da visualização.

Uma Visualização de Dados é semelhante ao conceito de Virtual Report Suites no Adobe Analytics， onde voce establete as definicoes de visita com reconnecimento de contexto， filtragem e também como os componentes sao chamados.

塞拉·內塞薩里奧、不mínimo、烏馬·維蘇阿里薩索·德·達多斯·波爾·科內克索。 沒有entanto， para alguns casos de uso， é ótimo ter múltiplas Visualizacoes de Dados para mesma conexao， com o objetvo de fornecer insights differentities para equipes distints。 我們非常重視這項技術，我們非常重視這項技術，我們非常重視這項技術。 Alguns範例：

- Métricas de UX apenas para a equipe de UX設計
- 使用os mesmos nomes para KPIs e métricas para oGoogle Analyticse para oCustomer Journey Analytics， para quipe de análise digital fale apenas 1 idioma。
- Visualização de Dados filtrada para mostrar， por exemplo， dados para apenas um mercado， ou uma marca， ou apenas para Dispossitivos móveis.

Na tela de **Connections**&#x200B;標示caixa de seleção da conexao que voce acabou de criar。 按一下&#x200B;**建立資料檢視**。

![示範](./images/exta.png)

Voce será redirecionado para o fluxo de trabalho **建立資料檢視**&#x200B;工作流程。

![示範](./images/0-v2.png)

## 4.3.2達多斯視覺化定義

Agora voce pode configurar as definicoes básicas para sua Visualização de dados.

![示範](./images/0-v2.png)

**連線** que voce criou no excício anterior está selecionada. Sua conexao se chama `yourLastName – Omnichannel Data Connection`。

![示範](./images/ext5.png)

Em seguida， de um nome à sua Visualização de Dados seguindo este modelo de nomenclatura： `yourLastName – Omnichannel Data View`。

Insira o mesmo valor para a descrição： `yourLastName – Omnichannel Data View`。

| 名稱 | 說明 |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![示範](./images/1-v2.png)

Para **時區**，選擇fuso horário **Berlim， Estocolmo， Roma， Berna， Bruxelas， Viena， Amsterda GMT+01:00**。 Este é um cenário realmente interessante， pois algumas empresas operam em diferences países e geografias. Alocar o fuso horário certo para cada país evitará erros típicos de dados， como， por explo， acreditar que a maioria das pessoas compra camisetas a 4h no Peru.

![示範](./images/ext7.png)

Voce também pode modificar a nomenclatura das métricas principais (Pessoa， Sessao e Evento)。 Isso nao é obrigatório， mas alguns clientes gostam de usar Pessoas， Visitas e Acessos em vez de Pessoa， Sessao e Eventos (convencao de nomenclatura padrao do Customer Journey Analytics)

Agora voce device as seguintes configuracoes definidas：

![示範](./images/1-v2.png)

點按&#x200B;**儲存並繼續**。

![示範](./images/12-v2.png)

## 4.3.3達多斯的視覺化元件

Neste excício， voce irá configurar os components necessários para analisar os dados e visualizá-los usando o o Analysis Workspace。 內斯塔·尤說：

- Lado esquerdo： Components disponíveis dos datasets seleconados
- Meio： Components adicionados à Visualização de Dados
- Lado directory：設定元件組態

![示範](./images/2-v2.png)

>[!IMPORTANT]
>
>Se voce nao encontrar uma metrica ou dimensao específica， verifique se to campo `Contains data` foi removido de sua visualização de dados. 野營店，敬請見諒。
>
>![示範](./images/2-v2a.png)

Agora voce precisa arrastar e soltar os components necessários para a análise nos **新增元件**。 這表示沒有功能表沒有選擇性。

Vamos Comecar com o primeiro元件： **名稱(web.webPageDetails.name)**。 請回答元件排列問題。

![示範](./images/3-v2.png)

Esse componente é o nome da página， como voce pode derivar da leitura do campo do schema `(web.webPageDetails.name)`。

無內含式，usar **名稱** como nome nao é a melhor convencao de nomenclatura para um usuário corporativo compreender rapidamente essa dimensao。

Vamos mudar o nome para **頁面名稱**。 叢集沒有元件或重新命名區域&#x200B;**元件設定**。

![示範](./images/3-0-v2.png)

作為Configuracoes de persistencia sao **持續性設定**。 Os conceitos de eVars e prop nao exist no CJA， mas as configuracoes de Persistencia possibilitam um comportamento semelhante.

![示範](./images/3-0-v21.png)

Se voce nao alterar essas configuracoes， o CJA irá interpretar a dimensao como um **Prop** (nível de ocorrencia)。 Além disso， podemos alterar a Persistencia para tornar a dimensao uma **eVar** (persistir o valor ao longo da jornada)。

See voce nao estiver familiarizado com eVars e Props， [leia mais sobre isso na documentacao](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html)..

Vamos deixar o Nome da Página como Prop. Dessa forma， voce nao precisa alterar nenhuma **持續性設定**。

| 要搜尋的元件名稱 | 新名稱 | 持續性設定 |
| ----------------- |-------------| --------------------| 
| 名稱(web.webPageDetails.name) | 頁面名稱 |          |

Em seguida， escolha a dimensao **phoneNumber** e solte-a na tela。 O novo nome device ser **電話號碼**。

![示範](./images/3-1-v2.png)

Por fim， vamos alterar as Configuracoes de persistencia， poi o Numero do Celular deve persising no ível do usuário.

Para alterar a Persistencia， role para baixo no menu à direita e abra a aba **持續性**：

![示範](./images/5-v2.png)

將caixa de selecao para modificar標示為configuracoes de persistencia。 選取&#x200B;**最近** e o escopo **人員（報告視窗）**， pois nos preocupamos apenas com o último número de celular da pessoa。 使用客戶的nao preencher或celular em visitas futuras， voce ainda verá esse valor preenchido。

![示範](./images/6-v2.png)

| 要搜尋的元件名稱 | 新名稱 | 持續性設定 |
| ----------------- |-------------| --------------------| 
| phonenumber | 電話號碼 | 最近，人員（報告期間） |

O próximo componente é `web.webPageDetails.pageViews.value`。

沒有功能表à esquerda，請預留`web.webPageDetails.pageViews.value`。 Arraste e solte essa métrica na tela.

在&#x200B;**元件設定**&#x200B;下的&#x200B;**頁面檢視**&#x200B;替代名稱。

| 要搜尋的元件名稱 | 新名稱 | 歸因設定 |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | 頁面檢視 |         |

![示範](./images/7-v2.png)

Para as configuracoes de atribuicao、deixaremos em branco.

Observação： As configuracoes de persistencia nas métricas também podem ser alteradas no Analysis Workspace。 Em alguns casos， voce pode optar por configurá-las aqui para evitar que os usuários de negócios tenham que pensar qual é melhor modelo de persistencia.

我們很清楚，我們很清楚，我們很清楚。

### 尺寸

| 要搜尋的元件名稱 | 新名稱 | 持續性設定 |
| ----------------- |-------------| --------------------| 
| brandName | 品牌名稱 | 最近，工作階段 |
| callfeeling | 通話感覺 |          |
| 呼叫ID | 通話互動型別 |          |
| callTopic | 呼叫主題 | 最近，工作階段 |
| ecid | ECID | 最近，人員（報告期間） |
| 電子郵件 | 電子郵件ID | 最近，人員（報告期間） |
| 付款類型 | 付款類型 |          |
| 產品廣告方式 | 產品廣告方式 | 最近，工作階段 |
| 事件類型 | 事件類型 |         |
| 名稱(productListItems.name) | 產品名稱 |         |
| SKU | SKU （工作階段） | 最近，工作階段 |
| 交易 ID | 交易 ID |         |
| URL (web.webPageDetails.URL) | URL |         |
| 使用者代理 | 使用者代理 | 最近，工作階段 |

### 美trica

| 要搜尋的元件名稱 | 新名稱 | 歸因設定 |
| ----------------- |-------------| --------------------| 
| 數量 | 數量 |          |
| commerce.order.priceTotal | 收入 |         |

Sua configuração deve ser semelhante ao seguinte：

![示範](./images/11-v2.png)

Nao se esqueca de Salvar sua Visualização de Dados. Entao叢集&#x200B;**儲存**。

![示範](./images/12-v2s.png)

## 4.3.4梅特里卡斯電腦

Embora tenhamos organizado todo os components na Visualização de dados， voce ainda deve adaptar alguns dels para que os usuários de negócios estejam prontos para iniciar suas análises.

Se voce se lembra， nao trouxemos specificamente Métricas como Adicionar ao Carrinho， Visualização do product ou Compras para a Visualização de dados. 沒有entanto， temo uma dimensao chamada： **事件型別**。 Entao， vamos derivar esses tipos de interacao criando 3 métricas calculadas.

Vamos comecar com a primeira Métrica： **產品檢視**。

沒有lado esquerdo，請預設&#x200B;**事件型別**&#x200B;以選取維度。 Em seguida， arraste-o e solte-o na tela **包含的元件**。

![示範](./images/calcmetr1.png)

Cluque para selectionar a nova métrica **事件型別**。

![示範](./images/calcmetr2.png)

Agora altere o name e a descrição do componente para os seguintes valores：

| 元件名稱 | 元件說明 |
| ----------------- |-------------| 
| 產品檢視 | 產品檢視 |

![示範](./images/calcmetr3.png)

Agora vamos contar apenas eventos de **產品檢視**。 Para fazer isso， role para baixo em **元件設定** até ver Valores de **包含排除值**。 Certifique-se de habilitar a opcao **設定包含/排除值**。

![示範](./images/calcmetr4.png)

Como queremos contar apenas **產品檢視**，特別是&#x200B;**commerce.productViews** nos critérios。

![示範](./images/calcmetr5.png)

真可愛啊！

Em seguida， repita o mesmo processo para os eventos **加入購物車** e **購買**。

### 新增至購物車

Primeiro， arraste e solte a mesma dimensao **事件型別**。

![示範](./images/calcmetr1.png)

Voce verá um alerta popup de um Campo Duplicado， pois estamos usando a mesma variável. 仍要加入Click em ****：

![示範](./images/calcmetr6.png)

Agora， siga o mesmo processo que fizemos para a métrica Visualizacoes de producto：
- Primeiro altere o nome e a descrição.
- Por fim， adicione **commerce.productListAdds** como critério para contar apenas Add To Cart

| 名稱 | 說明 | 標準 |
| ----------------- |-------------| -------------|
| 新增至購物車 | 新增至購物車 | commerce.productListAdds |

![示範](./images/calcmetr6a.png)

### 購買次數

Primeiro， arraste e solte a mesma dimensao **事件型別** como fizemos para as duas méticas anteriores。

![示範](./images/calcmetr1.png)

Voce verá um alerta popup de um Campo Duplicado， pois estamos usando a mesma variável. 仍要加入Click em ****：

![示範](./images/calcmetr7.png)

Agora， siga o mesmo processo que fizemos para as métricas產品檢視e加入購物車：
- Primeiro altere o nome e a descrição.
- Por fim， adicione **commerce.purchases** como critérios para conbilizar apenas as Compras

| 名稱 | 說明 | 標準 |
| ----------------- |-------------| -------------|
| 購買次數 | 購買次數 | commerce.purchases |

![示範](./images/calcmetr7a.png)

蘇亞組態精靈精靈精靈。 點按&#x200B;**儲存並繼續**。

![示範](./images/calcmetr8.png)

## 4.3.5 Components da Configuração de Dados

Voce device ser redirecionado para esta tela：

![示範](./images/8-v2.png)

Nesta aba， voce pode modificar algumas configuraces important para alterate a forma como os dados sao processados. Vamos Comecar定義&#x200B;**工作階段逾時**&#x200B;共用30分鐘。 Gracas ao registro de data e hora de cada evento de experiencia， voce pode estender o conceito de uma sessão em todos os canais. 您是來訪網站之客中心depois de visitar o site的acontece se um cliente ligar para？ Usando Tempos Limite de Sessao personalizados， voce tem muita flexibilidade para decisir o que é uma sessao e como essa sessao irá mesclar os dados.

![示範](./images/ext8.png)

Nesta aba voce pode modificar outtras coisas como filtrar os dados usando um segmento/filtro. Voce nao precisará fazer isso nest excício.

![示範](./images/10-v2.png)

Quando終端機，叢集&#x200B;**儲存並完成**。

![示範](./images/13-v2.png)

>[!NOTE]
>
>Voce pode voltar a esta Visualização de dados posteriormente e alterar as configuracoes e os components a qualquery momento. 作為變體，afetarao a forma como os dados historicos sao mostrados。

Agora voce pode continuar com a parte de visualização e análise！

Próxima etapa： [4.4 Preparacao de dados emCustomer Journey Analytics](./ex4.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
