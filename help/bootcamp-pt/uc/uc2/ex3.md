---
title: Bootcamp - Journey Optimizer建立您的歷程和電子郵件訊息 — 巴西
description: Bootcamp - Journey Optimizer建立您的歷程和電子郵件訊息 — 巴西
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: d486d1aa-7b8e-4301-91e6-4c84fba0c72a
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 3%

---

# 2.3 Crie sua jornada e mensagem de電子郵件

Neste exercício， voce irá configurar a jornada que precisa ser acionada quando alguém criar uma conta no site de demonstracao.

Faca登入無Adobe Journey Optimizer存取權a [Adobe Experience Cloud](https://experience.adobe.com). 小團體 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Voce será redirecionado para a visualização da **首頁**  無Journey Optimizer。 Primeiro，驗證是否成功了。 不要做沙箱que deve susado é `Bootcamp`. Para alternar de um sandbox para outtro， clique em **Prod** 選擇沙箱沙箱。 Neste範例， o nome do sandbox é **Bootcamp**. 視覺化雅緻 **首頁** 執行seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1珍珠母

沒有選單，小團 **歷程**. Em seguida，小團體 **建立歷程** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

敬請期待，敬請期待。

![ACOP](./images/journeyempty.png)

前方沒有練習，重新開始 **事件**. 事件旁白 `seuSobrenomeAccountCreationEvent` e替代 `seuSobrenome` 佩洛·塞烏·索布雷諾姆。 Este foi o resultado da criação do Evento：

![ACOP](./images/eventdone.png)

Agora voce deve considerate este evento como o o início desta Jornada. Voce pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

選擇事件，排定所有事件。 蘇亞莊園酒莊塞梅蘭特奧塞甘特：

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada， voce deve adicionar uma etapa curta de **等待**. Vá para o lado esquerdo da tela até a secao **協調流程** para encontract isso. Voce usará atributos de perfil e precisará garantir que eles sejam preenchidos no Perfil do Cliente em tempo real.

![ACOP](./images/journeywait.png)

海島若爾納達島上塞梅蘭特島上的塞梅蘭特。 沒有lado direito da tela voce precisa configurar o tempo de espera。 Defina como 1分鐘。 為了保護你的權益，你不得不去保護你的權益。

![ACOP](./images/journeywait1.png)

小團體 **確定** para salvar suas alteracoes.

Como terceira etapa da jornada， voce deve adicionar uma acao **電子郵件**. Vá para o lado esquerdo da tela para **動作**，選取a acao **電子郵件** e arraste solte a acao no segundo nó da sua jornada. 永不言而喻。

![ACOP](./images/journeyactions.png)

定義 **類別** como **行銷** e selecicone uma **電子郵件表面** que permita o envio de email. Nesse caso， a **電子郵件表面** 電子郵件使用者。 Certifique-se de que as caixas de seleçao **電子郵件的點按次數** e **電子郵件開啟次數** 埃斯特賈姆·馬卡達斯。

![ACOP](./images/journeyactions1.png)

一種月經的早晚餐。 Para isso， clique em **編輯內容**.

![ACOP](./images/journeyactions2.png)

## 2.3.2基本概念

小團體，月經節段摘要 **編輯內容**.

![ACOP](./images/journeyactions2.png)

再說一遍。

![ACOP](./images/journeyactions3.png)

無無營帳的小型企業 **主旨列**.

![Journey Optimizer](./images/msg5.png)

科梅斯，艾瑞亞 **奧拉**

![Journey Optimizer](./images/msg6.png)

愛因達·愛因達·愛因達·愛因達·愛因斯坦·普朗塔。 Em seguida， voce precisa trader o token de personalização para o **名字** 我這才叫阿瑪澤納多 `profile.person.name.firstName`. 沒有功能表à esquerda、role para baixo para contract或elemento **個人** 小團體na seta para visualizar mais campos

![Journey Optimizer](./images/msg7.png)

Agora encontry o elemento **全名** 建立視覺化的mais campos小團體。

![Journey Optimizer](./images/msg8.png)

Por fim， localize o campo **名字** 無辛波羅 **+**  高腳鍋。 Voce verá o token de personalização aparecer no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em seguida、adicione或texto、 **阿格拉德切莫斯小島人！**。小團體 **儲存**.

![Journey Optimizer](./images/msg10.png)

恩濤，請迴音。 小團體 **電子郵件設計工具**  conteúdo do電子郵件的para criar設定。

![Journey Optimizer](./images/msg11.png)

Na próxima tela， será solicitado que voce forneca o conteúdo do email através de 3 métodos diferentes：

- **從頭開始設計**：Comece com uma tela em branco e使用編輯者WYSIWYG para arrastar e soltar a estructura e os componentes de conteúdo para criar visualmente o conteúdo email。
- **自行撰寫程式碼**：Crie seu próprio modelo de email codificando usandoHTML
- **匯入HTML**：匯入um modeloHTML存在、que voce poderá editar。

小團體 **匯入HTML**.

![Journey Optimizer](./images/msg12.png)

Arraste e solte o arquivo **mailtemplatebootcamp.html**，que voce pode baixa [aqui](../../assets/html/mailtemplatebootcamp.html.zip). 小集團匯入。

![Journey Optimizer](./images/msg13.png)

Voce verá este modelo de email padrao：

![Journey Optimizer](./images/msg14.png)

電子郵件的Vamos個人化。 Clique ao lado do texto **奧拉** e， em seguida， clicque no ícone **新增個人化**.

![Journey Optimizer](./images/msg35.png)

Em seguida， voce precisa trader o token de personalização **名字** 我這才叫阿瑪澤納多 `profile.person.name.firstName`. 沒有選單，將元素本地化 **個人**，法瑪·布卡·德塔爾哈達無元素 **全名** 小集團沒有伊科內 **+** 露營地的助理教士 **名字** ao編輯器。

小團體 **儲存**.

![Journey Optimizer](./images/msg36.png)

Agora voce verá como o campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

小團體 **儲存** para salvar sua mensagem.

![Journey Optimizer](./images/msg55.png)

Retorne para o painel de mensagens clicando na seta ao lado do texto da linha de assunto no canto superior esquerdo。

![Journey Optimizer](./images/msg56.png)

Agora voce得出以下結論：criação do seu email de cadastro. Clique na seta no canto superior esquerdo para retornar à sua jornada.

![Journey Optimizer](./images/msg57.png)

小團體 **確定**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3海南公共航空

我們先瞭解一下這個事實。 Voce pode fazer isso clicando no ícone **屬性** 沒有上乘的直立線。

![ACOP](./images/journeyname.png)

Voce pode fazer isso clicando no item clicar no item &quot;Name&quot; e inserindo o seguinte name `yourLastName - Account Creation Journey`. 小團體 **確定** para salvar as mudancas.

![ACOP](./images/journeyname1.png)

Agora voce pode publicar sua jornada clicando em **發佈**.

![ACOP](./images/publishjourney.png)

小團體 **發佈**  novamente。

![ACOP](./images/publish1.png)

西班牙公共事業部關於澳門的資訊。

![ACOP](./images/published.png)

Voce terminou este expercisio。

冰淇淋甜菜： [2.4測驗sua jornada](./ex4.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
