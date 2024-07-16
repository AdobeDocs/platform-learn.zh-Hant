---
title: Bootcamp — 混合實體和數位 — Journey Optimizer建立您的歷程並推播 — Brazilnotification
description: Bootcamp — 混合實體和數位 — Journey Optimizer建立您的歷程並推播 — Brazilnotification
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: a4ef6eaf-6b39-4450-82bf-7db99595a323
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---

# 3.3 Crie sua jornada e notificacao push

Neste exercício， voce irá configurar a jornada e a mensagem que precisa ser acionada quando alguém inserir uma sinalização （信標） usando o o aplicativo móvel.

Faca登入無Adobe Journey Optimizer存取[Adobe Experience Cloud](https://experience.adobe.com)。 叢集&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

Voce será redirecionado para a visualização da **Home** no Journey Optimizer。 Primeiro，驗證是否使用沙箱驗證。 不要執行開發使用者`Bootcamp`的沙箱。 Para alternar de um sandbox para outtro， clicque em **Prod**&#x200B;選擇一個o sandbox na lista。 巢狀範例，**Bootcamp**&#x200B;中沒有sandbox。 Voce estará na visualização da **Home**&#x200B;執行seu沙箱`Bootcamp`。

![ACOP](./images/acoptriglp.png)

## 3.3.1玉米捲紙

沒有功能表à esquerda，請點選&#x200B;**歷程**。 Em seguida， cluque em **建立歷程** para criar uma nova jornada。

![ACOP](./images/createjourney.png)

敬請期待。

![ACOP](./images/journeyempty.png)

前方沒有練習，新錄製了&#x200B;**活動**。 Voce nomeou o evento `yourLastNameBeaconEntryEvent` e替代`yourLastName` pelo seu sobrenome。 Este foi o resultado da criação do Evento：

![ACOP](./images/eventdone.png)

Agora voce deve consider este evento como o início desta Jornada. Voce pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

選取seu evento， arraste e solte o evento na tela de jornada。 海島若爾納達·阿古拉島上塞梅蘭特·奧·塞甘特。 Clique em **Ok** para salvar suas alteracoes。

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada， voce deve adicionar uma acao **推播**。 Vá para o lado esquerdo da tela para **動作**，選取acao **推播** e arraste solte a acao no segundo nó da sua jornada。

![ACOP](./images/journeyactions.png)

沒有拉多的direito da tela， agora voce deve criar sua notificação push.

定義&#x200B;**類別**&#x200B;組合&#x200B;**行銷**&#x200B;選取一個推送表面que永久環境通知推送。 Nesse caso，超級推播使用者selecionada é **mmeewis-app-mobile-bootcamp**。

![ACOP](./images/journeyactions1.png)

## 3.3.2編寫手冊

點按&#x200B;**編輯內容**。

![ACOP](./images/emptymsg.png)

塞吉達，一株長吻鯛：

![ACOP](./images/emailmsglist.png)

Vamos definir o conteúdo da notificação推送。

叢集無campo de texto **標題**。

![Journey Optimizer](./images/msg5.png)

Na área de texto， comece **Olá**。 無個人主義的小團體。

![Journey Optimizer](./images/msg6.png)

Agora voce precisa trazer o token de personalização para o campo **名字** qestá armazenado em `profile.person.name.firstName`。 沒有功能表à esquerda，選取一個&#x200B;**設定檔屬性**，role para baixo/navegue para encontrar o elemento **人員** e clique na seta para avancar um nível até chegar ao campo `profile.person.name.firstName`。 Clique no ícone **+** para adicionar o campo à tela。 點按&#x200B;**儲存**。

![Journey Optimizer](./images/msg7.png)

恩陶，請迴音。 Clique no ícone de personalizaao lado do campo **主體**。

![Journey Optimizer](./images/msg11.png)

Na area de texto， escreva `Bem-vindo(a)`。

![Journey Optimizer](./images/msg12.png)

Em seguida，點選em **內容屬性** e **Journey Orchestration**。

![ACOP](./images/jomsg3.png)

點按&#x200B;**事件**。

![ACOP](./images/jomsg4.png)

群組no nome do sevento，que deve semelhante ao seguinte： **yourLastNameBeaconEntryEvent**。

![ACOP](./images/jomsg5.png)

點按&#x200B;**放置內容**。

![ACOP](./images/jomsg6.png)

點按&#x200B;**POI互動**。

![ACOP](./images/jomsg7.png)

點按&#x200B;**POI詳細資料**。

![ACOP](./images/jomsg8.png)

叢集編號&#x200B;**+**&#x200B;圖示編號&#x200B;**POI名稱**。
再來，再來。 點按**儲存**。

![ACOP](./images/jomsg9.png)

我們一起吃吧。 Clique na seta no canto superior esquerdo para retornar à sua jornada.

![ACOP](./images/jomsg11.png)

點按&#x200B;**確定**。

![ACOP](./images/jomsg14.png)

## 3.3.2環境uma mensagem para uma tela

Como terceira etapa da jornada， voce deve adicionar uma acao **sendMessageToScreen**。 Vá para o lado esquerdo da tela para **動作**，選取acao **sendMessageToScreen** e arraste e solte a acao no terceiro nó da sua jornada。 我願意，願意。

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma acao personalizada que irá publicar uma mensagem no **端點** usado pela exibicao na loja。 Acao **sendMessageToScreen** espera que múltiplas variáveis sejam definidas。 Voce pode visualizar essas variáveis rolando para baixo até ver **動作引數**。

![ACOP](./images/jomsg16.png)

Agora voce precisa definir os valores para cada parametero de acao. Siga esta tabela para entender quais valores sao necessários e onde.

| 參數 | 值 |
|:-------------:| :---------------:|
| 傳遞 | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| 名字 | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| 沙箱 | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style="table-layout:auto"}

Para definir esses valores， clique no ícone **編輯**。

![ACOP](./images/jomsg17.png)

Em seguida，選取&#x200B;**進階模式**。

![ACOP](./images/jomsg18.png)

Em seguida， cole o valor com base na tabela acima. 點按&#x200B;**確定**。

![ACOP](./images/jomsg19.png)

Repita esse processo para adicionar valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID， há uma referencia ao evento`yourLastNameBeaconEntryEvent`。 Lembre-se de substituir `yourLastName` pelo seu sobrenome。

最後的結果是精靈手錶：

![ACOP](./images/jomsg20.png)

角色para cima e clique em **確定**。

![ACOP](./images/jomsg21.png)

您仍需要提供歷程名稱。 若要這麼做，請按一下熒幕右上方的&#x200B;**屬性**&#x200B;圖示。

![ACOP](./images/journeyname.png)

插入至聖名雅姬。 使用`yourLastName - Beacon Entry Journey`。 Clique em **OK** para salvar suas alteracoes。

![ACOP](./images/journeyname1.png)

Agora voce pode publicar sua jornada clicando em **Publish**。

![ACOP](./images/publishjourney.png)

Clique em **Publish** novamente。

![ACOP](./images/publish1.png)

我們非常重視您的需求，我們非常重視您的需求。

![ACOP](./images/published.png)

長尾相依的相依之人。

請回答問題。

Próxima etapa： [3.4 Teste sua jornada](./ex4.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
