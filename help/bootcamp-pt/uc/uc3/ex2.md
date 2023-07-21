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
source-wordcount: '467'
ht-degree: 0%

---

# 3.2 Crie seu evento

Faca登入無Adobe Journey Optimizer存取權a [Adobe Experience Cloud]. 小團體 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Voce será redirecionado para a **首頁** 無Journey Optimizer。 Primeiro，驗證是否成功了。 不要做沙箱que deve susado é `Bootcamp`. Para alternar de um sandbox para outtro， clique em **Prod** 選擇沙箱沙箱。 Neste範例， o nome do sandbox é **Bootcamp**. 視覺化雅緻 **首頁** 執行seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

沒有選單à esquerda，role para baixo e clique em **設定**. Em seguida， clique no botao **管理** em事件。

![ACOP](./images/acopmenu.png)

Voce verá uma visão geral de todos os eventos disponíveis. 小團體 **建立事件** para comecar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

Em primeiro lugar， de um nome ao seu evento como， por範例： `yourLastNameBeaconEntryEvent` e adicione uma descriçao como， por範例： `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em seguida，認證中心 **型別** 定義共鳴 **單一** e， para a selecao de **事件ID型別**，選取 **系統已產生**.

![ACOP](./images/eventidtype.png)

選擇執行結構描述的etapa seguinte。 Um schema foi preparado para esticio練習。 使用結構描述 `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema， voce verá vários campos sendo selecionados na secao **欄位**. Agora voce deve passar o mouse sobre a secao **欄位** e tres ícones快顯視窗exibidos。 小團體no ícone de **編輯**.

![ACOP](./images/eventpayload.png)

Voce verá uma janela快顯視窗 **欄位**，onde voce deve selecionar alguns dos campos que precisamos para personalizar a jornada。 Escoleremos outros attributos de perfil posteriormente， utilizando os dados já existents na Adobe Experience Platform

![ACOP](./images/eventfields.png)

物件的角色para baixo até `Place context` 我為caixa de seleção品牌代言。 com isso， todo o contexto da localização do cliente será disponibilizado para a jornada. 小團體 **確定** para salvar suas alteracoes.

![ACOP](./images/eventpayloadbr.png)

我們很清楚，我們很清楚。 小團體 **儲存** mais uma vez para salvar suas alteracoes.

![ACOP](./images/eventsave.png)

諸位若想吃點東西，請盡情享受。

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir a tela **編輯事件** mais uma vez. 滑鼠游標逾時 **欄位** para ver os 3 ícones. 小團體no ícone **檢視**.

![ACOP](./images/viewevent.png)

Agora voce verá um expero do payload esperado.
Seu evento tem um eventID de orquestracao único， que voce pode encontracr rolando para baixo nesa carga útil até visualiza `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que voce construirá em dos próximos exercíos. Lembre-se destine eventID， voce pode precisar dele posteriormente.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

小團體 **確定** e， em seguida， clicque em **取消**.

Voce terminou este expercisio。

冰淇淋甜菜： [3.3 Crie sua jornada e notificação push](./ex3.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
