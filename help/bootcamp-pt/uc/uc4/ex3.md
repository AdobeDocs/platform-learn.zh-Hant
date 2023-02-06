---
title: Bootcamp -Customer Journey Analytics — 建立資料檢視 — 巴西
description: Customer Journey Analytics — 建立資料檢視 — 巴西
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 072179998d19c32589280defdb257a86d8728fea
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 2%

---

# 4.3 Crie uma Visualização de Dados

## 奧比蒂沃斯

- 了解Visualização de Dados的UI
- Compreenda as configurações básicas de definição de visita
- Compresenda a atribuição e a Persistência em Visualização de

## 4.3.1 Visualização de Dados

Agora, com sua conexão conculída, e possível progredir para influenciar a visualização. Uma diferença e o Adobe Analytics e o CJA e que o CJA precisa de uma visualização de dados para limpar e prear os dados antes da visualização.

Uma Visualização de Dadosé semelhante ao conceito de Virtual Report Suites no Adobe Analytics, onde você secelecte as definições de visita com reconhimento de contextto, filtargm e também como os compontes são chamados。

Será vesuário, no mínimo, uma Visualização de Dados por conexão. 沒有entanto, para alguns casos de uso, eótimo ter múltiplas Visualizações de Dados para mesma conexão, com o bjetivo de fornecer insights diferentes para equidintas。 請參閱você deseja que sua empresa seja orienta dados, deve adaptar a forma co mo os dados são vistos em cada equipe。 演算法執行者：

- Métricas de UX apenas para a equipe de UX設計
- 使用mesmos nomes para KPIs e métricas para oGoogle Analyticse para oCustomer Journey Analytics, para que a equipe de análise digital fale apenas 1 idioma。
- Visualização de Dados filtrada para mostrar, por exemplo, dados para apenas um mercado, ou uma marca, ou apenas para Dispositivos móveis。

娜特拉德 **連線** marque a caixa de seleção da conexão que você acabou de criar. 小組  **建立資料檢視**.

![示範](./images/exta.png)

Você será redirecionado para o fluxo de trabalho **建立資料檢視** 工作流程。

![示範](./images/0-v2.png)

## 4.3.2 Definição de Visualização de Dados

Agora você pode configurar as definições básicas para sua Visualização de dados.

![示範](./images/0-v2.png)

A **連線** 當然，不能再做運動。 沙馬 `yourLastName – Omnichannel Data Connection`.

![示範](./images/ext5.png)

Em seguida, dê um nome a sua Visualização de Dados seguindo este modelo de nomclatura: `yourLastName – Omnichannel Data View`.

Insira o mesmo valor para a descão: `yourLastName – Omnichannel Data View`.

| 名稱 | 說明 |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![示範](./images/1-v2.png)

段 **時區**，選手，時拉里奧 **貝利姆、埃斯托科爾莫、羅馬、貝爾納、布魯塞拉斯、維耶納、阿姆斯特丹GMT+01:00**. Este e um cenário realmente intersente, pois algumas empresas opeam deferentes países e geografias。 Alocar o fuso horário certo para cada país evitará erros típicos de dados, como, por exmelo, acreditar qua maioria das pessoas compra camisetasàs 4h no peru.

![示範](./images/ext7.png)

Você também pode modificar a nomeclatura das métricas principais(Pessoa, Sessão e Evento)。 Isso não e obrigatório, mas alguns clientes gostam de usar Pessoas, Visitas e Acessos em vez de Pessoa, Sessão e Eventos(convenção de nomclatura padrão doCustomer Journey Analytics)。

Agora você ter as seguintes configurações defidas:

![示範](./images/1-v2.png)

小組 **保存並繼續**.

![示範](./images/12-v2.png)

## 4.3.3 Visualização de Dados元件

Neste mextricício, você irá configurar os components equestrios paranalisar os dados e visualizá-los usando o Analysis Workspace。 Nesta IU，哈，Há tês áreas principais:

- 拉多·埃斯凱多：元件Disponíveis dos資料集selectionados
- Meio:Componentes adicionadosà Visualização de Dados
- 拉多·迪雷托：科波嫩特河

![示範](./images/2-v2.png)

>[!IMPORTANT]
>
>Se você não encontrur uma métrica ou dissão secufica, verifique se o campo `Contains data` foi removido de sua visualização de dados。 卡索·孔特拉里奧，獨家的。
>
>![示範](./images/2-v2a.png)

Agora você preisa arrastar e soltar os components equisé rios para a nalise nos **新增元件**. Paraisso, você deve selecionar os components no menuà esquerda e arrastá-los e soltá-los na tela no meio.

Vamos começar com o primeiro componente: **名稱(web.webPageDetails.name)**. Pesquise componente e arraste-o e solte-o na tela。

![示範](./images/3-v2.png)

Esse componenteé o nome da página, como você pode derivar da leitura do campo do schema `(web.webPageDetails.name)`.

沒有恩坦托，烏薩 **名稱** como o não e a melhor convenção de nomclatura para usário corporativo, apidamente essa dimensão.

Vamos mudar o nome para **頁面名稱**. 不是成員的團體 **元件設定**.

![示範](./images/3-0-v2.png)

佩西斯特森西亞河 **持久性設定**. Os concetios de eVars e prop não istem no CJA, mas as configurações de Persstência possibilitam um comportamento semelhante.

![示範](./images/3-0-v21.png)

Se você não alterar essas configurações, o CJA irá interpretar a dimensão como um **Prop** （尼韋爾·德·奧科雷恩西亞）。 Além disso, podemos altera a Persistência para torn a dimensouma **eVar** （波斯斯特爾·瓦洛·奧隆戈·達喬納達）。

請參閱você não estiver familiarizado com eVars e Props, [莉婭·瑪斯·索佈雷·伊索·娜·多克塔桑](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html)...

我們去找Nome da Páginacomo Prop。 Dessa形式，vacê não precisa altera r nenhuma **持久性設定**.

| 要搜索的元件名稱 | 新名稱 | 持久性設定 |
| ----------------- |-------------| --------------------| 
| 名稱(web.webPageDetails.name) | 頁面名稱 |  |

Em seguida, escolha a dimensão **phoneNumber** 太陽。 從頭到尾 **電話號碼**.

![示範](./images/3-1-v2.png)

Por fim, alterar as Configurações de persistência, pois o Número do Celular deve persist in nível do usuário.

Para altera a Persstência, are pa baxo no menu a direita e abra a aba **持久性**:

![示範](./images/5-v2.png)

Marque a caixa de seleção para modificar as configurações de persistência. 選取項 **最近** e o escopo **人員（報告窗口）**, pois nos preocupamos apenas com oúltimo número de celular da pessoa. 請參閱cliente não preencher o celular em visitas futuras, você ainda verá esse valor preenchido。

![示範](./images/6-v2.png)

| 要搜索的元件名稱 | 新名稱 | 持久性設定 |
| ----------------- |-------------| --------------------| 
| phoneNumber | 電話號碼 | 最近，人員（報告窗口） |

O próximo componente `web.webPageDetails.pageViews.value`.

沒有菜單是esquerda,pesquise `web.webPageDetails.pageViews.value`. Arraste e solte essa métrica na tela。

變數 **頁面檢視** 在 **元件設定**.

| 要搜索的元件名稱 | 新名稱 | 歸因設定 |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | 頁面檢視 |  |

![示範](./images/7-v2.png)

Para as configurações de atribuição, deixaremos em branco.

Observação:如Analysis Workspace的Possistência nas métricas também podem ser alteradas。 Em alguns casos, você pode optar por configurá-las aqui para evitar que os usuários de negócios tenham que pensar qual e o melhor modelo de persistência。

Em seguida, você terá que configurar várias Dimensões e Métricas, conforme indicado na tabela abaixo.

### 維森斯

| 要搜索的元件名稱 | 新名稱 | 持久性設定 |
| ----------------- |-------------| --------------------| 
| brandName | 品牌名稱 | 最近，工作階段 |
| 冷靜 | 呼叫感覺 |  |
| 呼叫ID | 呼叫互動類型 |  |
| callTopic | 呼叫主題 | 最近，工作階段 |
| ecid | ECID | 最近，人員（報告窗口） |
| 電子郵件 | 電子郵件ID | 最近，人員（報告窗口） |
| 付款類型 | 付款類型 |  |
| 產品添加方法 | 產品添加方法 | 最近，工作階段 |
| 活動類型 | 活動類型 |  |
| 名稱(productListItems.name) | 產品名稱 |  |
| SKU | SKU（工作階段） | 最近，工作階段 |
| 交易 ID | 交易 ID |  |
| URL(web.webPageDetails.URL) | URL |  |
| 使用者代理 | 使用者代理 | 最近，工作階段 |

### 美特里卡

| 要搜索的元件名稱 | 新名稱 | 歸因設定 |
| ----------------- |-------------| --------------------| 
| 數量 | 數量 |  |
| commerce.order.priceTotal | 收入 |  |

Sua configuração deve semelhante ao seguinte:

![示範](./images/11-v2.png)

Não se esqueça de Salvar sua Visualização de Dados。 恩唐小組 **儲存**.

![示範](./images/12-v2s.png)

## 4.3.4梅特里卡斯計算器

Embora tenhamos organizado todos os components na Visualização de dados, você ainda deve adaptar alguns deles para que os usurios de negócios estejam prontos para iniciar suas análises。

Se você se lembra, não trouxemos secificamente Métricas como Adicionar ao Carrinho, Visualização do produto ou Compras para a Visualização de dados。 沒有恩坦托，泰莫斯·烏馬： **事件類型**. 恩唐，瓦莫斯·德里瓦爾處理tipos de interação criando 3 métricas calculadas。

Vamos começar網站： **產品檢視**.

不要拉多·埃斯凱多，佩斯奎斯 **事件類型** 選擇維。 Em seguida, arraste-o e solte-o na tela **包含的元件**.

![示範](./images/calcmetr1.png)

新墨西哥族 **事件類型**.

![示範](./images/calcmetr2.png)

Agora altere o nome e a descrição do componente para os seguintes valores:

| 元件名稱 | 元件說明 |
| ----------------- |-------------| 
| 產品檢視 | 產品檢視 |

![示範](./images/calcmetr3.png)

瓦莫斯山 **產品檢視**. Para fazer isso, rale par a bixo em **元件設定** 瓦洛雷斯河 **包含排除值**. 奧普桑河畔瑟蒂菲克 **設定包含/排除值**.

![示範](./images/calcmetr4.png)

Como queremos contar apenas **產品檢視**，特別是 **commerce.productViews** 克里蒂里奧斯號。

![示範](./images/calcmetr5.png)

我是個大腦，還有本能！

Em seguida, repita o mesmo processo para os eventos **新增至購物車** e **購買**.

### 新增至購物車

Primeiro, arraste e solte a mesma dissão **事件類型**.

![示範](./images/calcmetr1.png)

Você verá um alerta pop de um Campo Duplicado, pois estamos usando a mesma variável。 小組 **仍新增**:

![示範](./images/calcmetr6.png)

Agora, siga o mesmo processso que fizemos para a métrica Visualizações de producto:
- Primeiro改變了。
- 波菲姆，阿迪奧內 **commerce.productListAdds** 科莫·克里特里奧·帕拉·阿佩納斯加到購物車

| 名稱 | 描述 | 標準 |
| ----------------- |-------------| -------------|
| 新增至購物車 | 新增至購物車 | commerce.productListAdds |

![示範](./images/calcmetr6a.png)

### 購買

Primeiro, arraste e solte a mesma dissão **事件類型** 我們的手藝很好。

![示範](./images/calcmetr1.png)

Você verá um alerta pop de um Campo Duplicado, pois estamos usando a mesma variável。 小組 **仍新增**:

![示範](./images/calcmetr7.png)

Agora, siga o mesmo processo que fizemos para as métricas產品視圖e添加到購物車：
- Primeiro改變了。
- 波菲姆，阿迪奧內 **commerce.purchases** 科莫·科普拉斯

| 名稱 | 描述 | 標準 |
| ----------------- |-------------| -------------|
| 購買 | 購買 | commerce.purchases |

![示範](./images/calcmetr7a.png)

Sua configuração final deve ser semelhante ao seguinte. 小組 **保存並繼續**.

![示範](./images/calcmetr8.png)

## 4.3.5元件：達配置

Você deve ser redirecionado para esta:

![示範](./images/8-v2.png)

Nesta aba, você pode modificar algumas configurações a importantes para alterar a forma como os dados são processados. Vamos começar defindo o **工作階段逾時** 30分鐘 Graças ao registro de data e hora de cada evento de experiencia, você pode estendo o conceito de uma sessão em todos os canais。 Por exmelo, o cue se um cliente ligar para o call center depois de visitar o site? Usando Tempos Limite de Sessão個人化， você tem muita flexibilidade para decidir o que u ma sessão e como essa sessão irá mesclar dos。

![示範](./images/ext8.png)

Nesta aba você pode modificar outras coisas como filtrar os dados usando um segmento/filtro. Você não precisará fazer isso nest extriccio.

![示範](./images/10-v2.png)

乾多·塔米納，小伙 **保存並完成**.

![示範](./images/13-v2.png)

>[!NOTE]
>
>Você pode voltar a esta Visualização de dados posteormente e alterar as configurações e os components a qualquer monto. 如alterações aftarão a forma como os dados históricos são mostrados.

Agora você pode continuar com a parte de visualização e análise!

埃塔帕： [4.4準備Customer Journey Analytics](./ex4.md)

[烏薩里奧河畔雷托爾](./uc4.md)

[托多斯山](./../../overview.md)
