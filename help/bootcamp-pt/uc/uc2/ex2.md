---
title: Bootcamp - Journey Optimizer建立您的活動 — 巴西
description: Bootcamp - Journey Optimizer建立您的活動 — 巴西
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 1b9d7a35-cddf-4f4a-ad0a-95723b00c278
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 2.2 Crie seu evento

Faca登入無Adobe Journey Optimizer存取[Adobe Experience Cloud](https://experience.adobe.com)。 叢集&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

Voce será redirecionado para a visualização da **Home** no Journey Optimizer。 Primeiro，驗證是否使用沙箱驗證。 不要執行開發使用者`Bootcamp`的沙箱。 Para alternar de um sandbox para outtro， clique em Prod e selection o sandbox na lista. 巢狀範例，**Bootcamp**&#x200B;中沒有sandbox。 Voce estará na visualização da **Home**&#x200B;執行seu沙箱`Bootcamp`。

![ACOP](./images/acoptriglp.png)

沒有功能表à esquerda，角色para baixo e clique em **設定**。 Em seguida， clique no botao **管理** abaixo de **活動**。

![ACOP](./images/acopmenu.png)

總覽vuma visão geral de todos os eventos disponíveis。 點按&#x200B;**建立事件** para comecar a criar seu próprio evento。

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

![ACOP](./images/emptyevent1.png)

Em primeiro lugar， de um nome ao seu evento como， por範例： `seuSobrenomeAccountCreationEvent` e adicione uma descriçao como， por範例： `Account Creation Event`。

![ACOP](./images/eventdescription.png)

Em seguida， certifique-se de que **型別** está definido como **單一** e， para a seleçao de **事件ID型別**，選取&#x200B;**系統產生**。

![ACOP](./images/eventidtype.png)

etapa seguinte é a selecao do schema. Um schema foi preparado para este excício. 使用結構描述`Demo System - Event Schema for Website (Global v1.1) v.1`。

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema， voce verá vários campos sendo selecionados na seção **欄位**。 Agora voce deve passar o mouse sobre a secao **欄位** e tres ícones快顯視窗exibidos。 叢集無ícone **編輯**。

![ACOP](./images/eventpayload.png)

Voce verá uma janela快顯視窗de **欄位**， onde voce deve selectionar alguns dos campos que precisamos para personalizar o email。 Escolheremos outros attributos de perfil posteriormente，利用dados já extentes na Adobe Experience Platform。

![ACOP](./images/eventfields.png)

沒有物件`_experienceplatform.demoEnvironment`，pcertifique-se de selecionar os campos **brandLogo** e **brandName**。

![ACOP](./images/eventpayloadbr.png)

沒有物件`_experienceplatform.identification.core`，憑證是用來選取帳號&#x200B;**電子郵件**。

![ACOP](./images/eventpayloadbrid.png)

將em **Ok**&#x200B;新增至para salvar suas alteracoes。

![ACOP](./images/saveok.png)

Em seguida是西班牙長腳鴨式酒莊出品的exibida。 叢集&#x200B;**儲存** mais uma vez para salvar suas alteracoes..

![ACOP](./images/eventsave.png)

諸位敬請垂涎三尺。

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir mais uma vez a tela **編輯事件**。 透過滑鼠滑鼠&#x200B;**欄位** para ver os 3 ícones outra vez。 叢集無ícone **檢視承載**。

![ACOP](./images/viewevent.png)

Agora voce verá um exemplo da carga útil esperada.
Seu evento tem um eventID de orquestracao único， que voce pode encontrar rolando para baixo nesa carga útil （承載） até visualizar `_experience.campaign.orchestration.eventID`。

![ACOP](./images/payloadeventID.png)

OventID é é é que deve ser enviado à Adobe Experience Platform para acionar a jornada que voce construirá em dos próximos exercícios. Lembre-se destine eventID， voce pode precisar dele posteriormente.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

點按&#x200B;**確定** e， em seguida，點按&#x200B;**取消**。

Agora voce terminou este excício.

Próxima etapa： [ 2.3 Crie sua mensagem de電子郵件](./ex3.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
