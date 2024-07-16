---
title: Bootcamp — 混合實體和數位 — Journey Optimizer建立您的活動 — 巴西
description: Bootcamp — 混合實體和數位 — Journey Optimizer建立您的活動 — 巴西
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 2133b560-09d8-419d-bb99-05d0f3df52cc
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# 3.2 Crie seu evento

Faca登入無Adobe Journey Optimizer存取[Adobe Experience Cloud]。 叢集&#x200B;**Journey Optimizer**。

![ACOP](./images/acophome.png)

Voce será redirecionado para a **Home** no Journey Optimizer。 Primeiro，驗證是否使用沙箱驗證。 不要執行開發使用者`Bootcamp`的沙箱。 Para alternar de um sandbox para outtro， clicque em **Prod**&#x200B;選擇一個o sandbox na lista。 巢狀範例，**Bootcamp**&#x200B;中沒有sandbox。 Voce estará na visualização da **Home**&#x200B;執行seu沙箱`Bootcamp`。

![ACOP](./images/acoptriglp.png)

沒有功能表à esquerda，角色para baixo e clique em **設定**。 Em seguida， clique no botao **管理** em事件。

![ACOP](./images/acopmenu.png)

總覽vuma visão geral de todos os eventos disponíveis。 點按&#x200B;**建立事件** para comecar a criar seu próprio evento。

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

Em primeiro lugar， de um nome ao seu evento como， por範例： `yourLastNameBeaconEntryEvent` e adicione uma descriçao como， por範例： `Beacon Entry Event`。

![ACOP](./images/eventdescription.png)

Em seguida， certifique-se de que **型別** está definido como **單一** e， para a seleçao de **事件ID型別**，選取&#x200B;**系統產生**。

![ACOP](./images/eventidtype.png)

etapa seguinte é a selecao do schema. Um schema foi preparado para este excício. 使用結構描述`Demo System - Event Schema for Mobile App (Global v1.1) v.1`。

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema， voce verá vários campos sendo selecionados na seção **欄位**。 Agora voce deve passar o mouse sobre a secao **欄位** e tres ícones快顯視窗exibidos。 叢集無ícone de **編輯**。

![ACOP](./images/eventpayload.png)

Voce verá uma janela快顯視窗&#x200B;**欄位**， onde voce deve selectionar alguns dos campos que precisamos para personalizar a jornada。 Escolheremos outros attributos de perfil posteriormente，利用dados já existents na Adobe Experience Platform

![ACOP](./images/eventfields.png)

角色para baixo até ver o objeto `Place context` e marque a caixa de seleção。 com isso， todo o contexto da localização do cliente será disponibilizado para a jornada. Clique em **Ok** para salvar suas alteracoes。

![ACOP](./images/eventpayloadbr.png)

我願意，願意。 Clique em **儲存** mais uma vez para salvar suas alteracoes。

![ACOP](./images/eventsave.png)

諸位敬請垂涎三尺。

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir a tela **編輯事件** mais uma vez。 透過滑鼠sobre **欄位** para ver os 3 ícones。 叢集無ícone **檢視**。

![ACOP](./images/viewevent.png)

Agora voce verá um範例執行裝載專屬。
Seu evento tem um eventID de orquestracao único， que voce pode encontrar rolando para baixo nesa carga útil até visualiza `_experience.campaign.orchestration.eventID`。

![ACOP](./images/payloadeventID.png)

OventID é é é que deve ser enviado à Adobe Experience Platform para acionar a jornada que voce construirá em dos próximos exercícios. Lembre-se destine eventID， voce pode precisar dele posteriormente.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

叢集em **確定** e，em seguida，叢集em **取消**。

請回答問題。

Próxima etapa： [3.3 Crie sua jornada e notificacao push](./ex3.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
