---
title: Bootcamp - Journey Optimizer建立您的活動 — 巴西
description: Bootcamp - Journey Optimizer建立您的活動 — 巴西
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 1b9d7a35-cddf-4f4a-ad0a-95723b00c278
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 Crie seu evento

Faca登入無Adobe Journey Optimizer存取權a [Adobe Experience Cloud](https://experience.adobe.com). 小團體 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Voce será redirecionado para a visualização da **首頁** 無Journey Optimizer。 Primeiro，驗證是否成功了。 不要做沙箱que deve susado é `Bootcamp`. Para alternar de um sandbox para outtro， clique em Prod e selection o sandbox na lista. Neste範例， o nome do sandbox é **Bootcamp**. 視覺化雅緻 **首頁** 執行seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

沒有選單à esquerda，role para baixo e clique em **設定**. Em seguida， clique no botao **管理** abaixo de **事件**.

![ACOP](./images/acopmenu.png)

Voce verá uma visão geral de todos os eventos disponíveis. 小團體 **建立事件** para comecar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

![ACOP](./images/emptyevent1.png)

Em primeiro lugar， de um nome ao seu evento como， por範例： `seuSobrenomeAccountCreationEvent` e adicione uma descriçao como， por範例： `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em seguida，認證中心 **型別** 定義共鳴 **單一** e， para a selecao de **事件ID型別**，選取 **系統已產生**.

![ACOP](./images/eventidtype.png)

選擇執行結構描述的etapa seguinte。 Um schema foi preparado para esticio練習。 使用結構描述 `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema， voce verá vários campos sendo selecionados na secao **欄位**. Agora voce deve passar o mouse sobre a secao **欄位** e tres ícones快顯視窗exibidos。 小團體no ícone **編輯**.

![ACOP](./images/eventpayload.png)

Voce verá uma janela快顯視窗 **欄位**，onde voce deve selectionar alguns dos campos que precisamos para personalizar o email。 Escoleremos outros attributos de perfil posteriormente， utilizando os dados já existents na Adobe Experience Platform。

![ACOP](./images/eventfields.png)

無物件 `_experienceplatform.demoEnvironment`， pcertifique-se de selectionar os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

無物件 `_experienceplatform.identification.core`，坎波的certifique-se de selecionar **電子郵件**.

![ACOP](./images/eventpayloadbrid.png)

小團體 **確定** 至殘值，例如替代品。

![ACOP](./images/saveok.png)

Em seguida，一種長吻鄂酒莊出品的exibida。 小團體 **儲存**  mais uma vez para salvar suas alteracoes..

![ACOP](./images/eventsave.png)

諸位若想吃點東西，請盡情享受。

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir mais uma vez a tela **編輯事件**. 滑鼠游標逾時 **欄位** para ver os 3 ícones outra vez. 小團體no ícone **檢視裝載**.

![ACOP](./images/viewevent.png)

Agora voce verá um expero da carga útil esperada.
Seu evento tem um eventID de orquestracao único， que voce pode encontracr rolando para baixo nesa carga útil (payload) até visualizar `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que voce construirá em dos próximos exercíos. Lembre-se destine eventID， voce pode precisar dele posteriormente.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

小團體 **確定** e， em seguida， clicque em **取消**.

Agora voce terminou este expercisio.

冰淇淋甜菜： [ 2.3 Crie sua mensagem de email](./ex3.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
