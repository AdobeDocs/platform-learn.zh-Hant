---
title: Bootcamp - Journey Optimizer建立您的歷程和電子郵件訊息 — 巴西
description: Bootcamp - Journey Optimizer建立您的歷程和電子郵件訊息 — 巴西
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 3%

---

# 2.3電子郵件

Neste merkeício, você irá configar a jornada quando alguém criar conta no site de dedreção.

登錄Adobe Journey Optimizer帳戶a [Adobe Experience Cloud](https://experience.adobe.com). 小組 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da **首頁**  不，Journey Optimizer。 Primeiro, Verifique se você usando o sandbox correto. 不要沙箱，就要用 `Bootcamp`. Para alternar de um sandbox para outro, plicaem **生產** 選擇沙箱或沙箱。 不要做沙箱 **布坎普**. Você estará na visualização da **首頁** 做seu沙箱 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1條

沒有菜單，小伙子 **歷程**. 阿姆·西吉達，小團 **建立歷程** 準新約旦河。

![ACOP](./images/createjourney.png)

Você verá muma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

前無鍛鍊，從頭開始 **事件**. 沃凱諾梅烏奧埃文托 `yourLastNameAccountCreationEvent` e替代 `yourLastName` 別洛·蘇·索佈雷諾姆。 Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

阿戈拉認為，這甚至與我的意思有關。 Você pode fazer isso indo para o lado esquerdo da tela procando pelo seu evento n a lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de Jornada。 蘇阿·約納達·阿戈拉·德韋·塞梅爾漢特·阿奧·塞金特：

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve adicionar uma etapa curta de **等待**. Vá para o lado esquerdo da tela a seção **協調** 準逆差。 Você usará atributos de perfil e preisará garantir que eles sejam preenchidos no Perfil do Cliente em tempo real.

![ACOP](./images/journeywait.png)

我們的愛情。 不要用espera的節奏來表達。 定義一下1分鐘。 Isso dará bastante tempo para que os atributos do perfil estejam disponíveis após o dameseo do evento.

![ACOP](./images/journeywait1.png)

小組 **確定** 薩爾瓦·蘇亞斯·阿爾特拉松伊斯。

科莫·特塞拉·埃塔帕·達·約納達 **電子郵件**. Vá para o lado esquerdo da tela para **動作**，請選取ação **電子郵件** arraste e solte a ação no segundo nó da sua jornada. 阿戈拉·塞金特·塞拉·埃西比多。

![ACOP](./images/journeyactions.png)

設定 **類別** to **行銷** 並選取電子郵件介面，讓您傳送電子郵件。 在此情況下，要選取的電子郵件表面是 **電子郵件**. 確保的複選框 **電子郵件的點按次數** 和 **電子郵件開啟** 都會啟用。

定義a **類別** co **行銷** e selectione uma supície de e-mail是否允許環境電子郵件。 Nesse caso，一封淺薄的電子郵件，一封電子郵件。 Certifique-se de que as caixas de seleção **電子郵件的點按次數** e **電子郵件開啟** 埃斯特賈姆·馬卡達斯。

![ACOP](./images/journeyactions1.png)

我的心裡有點像。 帕拉索，小伙子 **編輯內容**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Crie a sua mensagem

Para criar sua mensagem, plickeem **編輯內容**.

![ACOP](./images/journeyactions2.png)

我是塞金特·塞拉。

![ACOP](./images/journeyactions3.png)

Prichum no campo de texto **主旨行**.

![Journey Optimizer](./images/msg5.png)

德克斯托，科米斯 **奧拉**

![Journey Optimizer](./images/msg6.png)

一個本來就是人。 Em seguida, você presisa trazer o token de personalização para o **名字** 她就是個女人 `profile.person.name.firstName`. 沒有菜單，角色是 **人員** e pricus na seta para ir um nível mais profundo.

![Journey Optimizer](./images/msg7.png)

埃萊門托的阿戈拉 **全名** e pricus na seta para ir um nível mais profundo.

![Journey Optimizer](./images/msg8.png)

波菲姆，當地化到坎波 **名字** e小團體 **+**  奧·拉多·德勒。 Você verá o token de personalização aparecer no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em seguida, adicione o texto, **阿格拉迪克莫斯是個有名的人！** 塞爾瓦小伙。. 小組 **儲存**.

![Journey Optimizer](./images/msg10.png)

恩唐，我要回去。 小組 **電子郵件設計工具**  cariar o contúdo做電子郵件。

![Journey Optimizer](./images/msg11.png)

Na próxima tela, será solicitado que voê forneça o conteúdo do e-mail através de 3 métodos diferentes:

- **從頭設計**:Comece com uma tela em branco e use o editor WYSIWYG pararrastar e soltar a estrutura e os componentes de contúdo par criar visualmente o conteúdo e-mail。
- **自行編碼**:電子郵件編碼文本HTML
- **匯入HTML**:請改進HTML存在論，比如você poderá editar。

小組 **匯入HTML**.

![Journey Optimizer](./images/msg12.png)

阿拉斯特·索爾特·阿基沃 **mailtemplatebootcamp.html**，闕歌 [此處](../../assets/html/mailtemplatebootcamp.html.zip). 重要的小伙。

![Journey Optimizer](./images/msg13.png)

電子郵件的模式：

![Journey Optimizer](./images/msg14.png)

建立個人化電子郵件。 毛拉多德特斯托 **奧拉** e, em seguida, plicke no icone **新增個人化**.

![Journey Optimizer](./images/msg35.png)

Em seguida, você presisa trazer o token de personalização **名字** 她就是個女人 `profile.person.name.firstName`. 沒有菜單，將元素本地化 **人員**《魔法車》 **完整名稱** 埃爾集團 **+** 坎波 **名字** ao編輯de expressão。

小組 **儲存**.

![Journey Optimizer](./images/msg36.png)

Agora você verá como o campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

小組 **儲存** 薩爾瓦·蘇阿·門薩根。

![Journey Optimizer](./images/msg55.png)

Retorne para o painel de mensagens clicando na seta ao lado do texto da linha de assunto no canto super esquerdo.

![Journey Optimizer](./images/msg56.png)

Agora você結論為criação do seu e-mail de cadastro. Cligus na seta no canto super esquerdo para reconnar à sua jornada.

![Journey Optimizer](./images/msg57.png)

小組 **確定**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3共和國

Você ainda precisa dar um nome a sua jornada. Você pode fazer isso clicando noícone **屬性** 沒有上司迪雷托達特拉。

![ACOP](./images/journeyname.png)

Você ainda precisa dar um nome a sua jornada. Você pode fazer isso clicando noícone `yourLastName - Account Creation Journey`. 小組 **確定** 像瑪丹薩一樣。

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **發佈**.

![ACOP](./images/publishjourney.png)

小組 **發佈**  諾瓦門特。

![ACOP](./images/publish1.png)

Você verá uma barra de confirmmação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

Você termou est exticio。

埃塔帕： [2.4聖若那達](./ex4.md)

[烏薩里奧河畔雷托納爾2](./uc2.md)

[托多斯山](../../overview.md)