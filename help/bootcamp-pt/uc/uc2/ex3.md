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
source-wordcount: '944'
ht-degree: 0%

---

# 2.3 Crie sua jornada e mensagem de email

Neste exercício， voce irá configurar a jornada que precisa ser acionada quando alguém criar uma conta no site de demonstracao.

Faca登入無Adobe Journey Optimizer存取[Adobe Experience Cloud](https://experience.adobe.com)。 叢集&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

Voce será redirecionado para a visualização da **Home** no Journey Optimizer。 Primeiro，驗證是否使用沙箱驗證。 不要執行開發使用者`Bootcamp`的沙箱。 Para alternar de um sandbox para outtro， clicque em **Prod**&#x200B;選擇一個o sandbox na lista。 巢狀範例，**Bootcamp**&#x200B;中沒有sandbox。 Voce estará na visualização da **Home**&#x200B;執行seu沙箱`Bootcamp`。

![ACOP](./images/acoptriglp.png)

## 2.3.1珍珠母

沒有功能表à esquerda，請點選&#x200B;**歷程**。 Em seguida， cluque em **建立歷程** para criar uma nova jornada。

![ACOP](./images/createjourney.png)

敬請期待。

![ACOP](./images/journeyempty.png)

前方沒有練習，新錄製了&#x200B;**活動**。 Voce nomeou o evento `seuSobrenomeAccountCreationEvent` e替代`seuSobrenome` pelo seu sobrenome。 Este foi o resultado da criação do Evento：

![ACOP](./images/eventdone.png)

Agora voce deve consider este evento como o início desta Jornada. Voce pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

選取seu evento， arraste e solte o evento na tela de Jornada。 蘇亞·喬納達·阿古拉魔法師塞梅蘭特·奧塞甘特：

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada， voce devicionar uma etapa curta de **等待**。 Vá para o lado esquerdo da tela até a secao **協調流程** para encontrrar isso。 Voce usará atributos de perfil e precisará garantir que eles sejam preenchidos no Perfil do Cliente em tempo real.

![ACOP](./images/journeywait.png)

海島若爾納達·阿古拉島上塞梅蘭特·奧·塞甘特。 沒有lado direito da tela voce precisa configurar or tempo de espera。 Defina como 1分鐘。 我決定要遵守巴斯坦節奏，也要遵守規則。

![ACOP](./images/journeywait1.png)

Clique em **Ok** para salvar suas alteracoes。

Como terceira etapa da jornada， voce deve adicionar uma acao **電子郵件**。 Vá para o lado esquerdo da tela para **動作**，選取acao **電子郵件** e arraste solte a acao no segundo nó da sua jornada。 您也可以。

![ACOP](./images/journeyactions.png)

定義&#x200B;**類別**&#x200B;組合&#x200B;**行銷** e選取一個uma **電子郵件表面** que permita o envio de email。 Nesse caso， a **電子郵件表面** a ser seleciconada é Email。 Certifique-se de que as caixas de seleção **按一下電子郵件** e **電子郵件開啟** estejam marcadas。

![ACOP](./images/journeyactions1.png)

一種美式麵包。 para isso，按一下&#x200B;**編輯內容**。

![ACOP](./images/journeyactions2.png)

## 2.3.2編寫範本

Para criar sua mensagem， clique em **編輯內容**。

![ACOP](./images/journeyactions2.png)

再說吧。

![ACOP](./images/journeyactions3.png)

叢集無campo de texto **主旨列**。

![Journey Optimizer](./images/msg5.png)

Na área de texto， comece **Olá**

![Journey Optimizer](./images/msg6.png)

愛因達·愛因達·愛因斯坦·愛因斯坦。 Em seguida， voce precisa trazer o token de personalização para o **名字** qestá armazenado em `profile.person.name.firstName`。 沒有選單à esquerda， role para baixo para encontract o elemento **人員** e clique na seta para visualizar mais campos

![Journey Optimizer](./images/msg7.png)

Agora encontre o elemento **全名** e clique na seta para visualizar mais campos。

![Journey Optimizer](./images/msg8.png)

Por fim， localize o campo **名字** e clique no símbolo **+** ao lado dele。 Voce verá o token de personalização aparecer no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em seguida， adicione o texto， **agradecemos a sua inscrição！**。點按&#x200B;**儲存**。

![Journey Optimizer](./images/msg10.png)

恩陶，請迴音。 Clique em **電子郵件Designer** para criar o conteúdo電子郵件。

![Journey Optimizer](./images/msg11.png)

Na próxima tela， será solicitado que voce forneca o conteúdo e email através de 3 métodos diferentes：

- **從頭開始設計**： Comece com uma tela em branco e use o editor WYSIWYG para arrastar e soltar a estrutura e os componentes de conteúdo para criar visualmente o conteúdo email.
- **自行編碼**： Crie seu próprio modelo de email codificando usandoHTML
- **匯入HTML**：匯入um modeloHTML存在， que voce poderá editar。

點按&#x200B;**匯入HTML**。

![Journey Optimizer](./images/msg12.png)

Arraste e solte o arquivo **mailtemplatebootcamp.html**， que voce pode baixa [aqui](../../assets/html/mailtemplatebootcamp.html.zip)。 小集團匯入。

![Journey Optimizer](./images/msg13.png)

電子郵件播放器的音量：

![Journey Optimizer](./images/msg14.png)

電子郵件的Vamos個人化。 Clique ao lado do texto **Olá** e， em seguida， clique no ícone **新增Personalization**。

![Journey Optimizer](./images/msg35.png)

Em seguida， voce precisa trazer o token de personalização **名字** qestá armazenado em `profile.person.name.firstName`。 沒有功能表，將元件本地化&#x200B;**人員**，faca uma busca detalhada no elemento **全名** e clique no ícone **+** para adicionar o campo **名字** ao編輯器。

點按&#x200B;**儲存**。

![Journey Optimizer](./images/msg36.png)

Agora voce verá como campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

Clique em **儲存** para salvar sua mensagem。

![Journey Optimizer](./images/msg55.png)

Retorne para o painel de mensagens clicando na seta ao lado do texto da linha de assunto no canto superior esquerdo。

![Journey Optimizer](./images/msg56.png)

Agora voce得出以下結論：criação do seu email de cadastro. Clique na seta no canto superior esquerdo para retornar à sua jornada.

![Journey Optimizer](./images/msg57.png)

點按&#x200B;**確定**。

![Journey Optimizer](./images/msg57a.png)

## 2.3.3海南出版社

我記得你剛才說的話。 Voce pode fazer isso clicando no ícone **屬性**&#x200B;沒有上級direito da tela。

![ACOP](./images/journeyname.png)

Voce pode fazer isso clicando no item clicar no item &quot;Name&quot; e inserindo o seguinte name `yourLastName - Account Creation Journey`。 將群組&#x200B;**OK** para salvar as mudancas。

![ACOP](./images/journeyname1.png)

Agora voce pode publicar sua jornada clicando em **Publish**。

![ACOP](./images/publishjourney.png)

Clique em **Publish** novamente。

![ACOP](./images/publish1.png)

我們非常重視您的需求，我們非常重視您的需求。

![ACOP](./images/published.png)

請回答問題。

Próxima etapa： [2.4 Teste sua jornada](./ex4.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
