---
title: Bootcamp - Journey Optimizer Create your event — 巴西
description: Bootcamp - Journey Optimizer Create your event — 巴西
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 Crie seu evento

登錄Adobe Journey Optimizer帳戶a [Adobe Experience Cloud](https://experience.adobe.com). 小組 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da **首頁** 不，Journey Optimizer。 Primeiro, Verifique se você usando o sandbox correto. 不要沙箱，就要用 `Bootcamp`. para alternar de um sandbox para outro, plicke em Prod e selecione o sandbox na lista. 不要做沙箱 **布坎普**. Você estará na visualização da **首頁** 做seu沙箱 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

沒有菜單，角色是 **配置**. Em seguida，小團體 **管理** 阿貝克索德 **事件**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. 小組 **建立事件** 這是一個罪名。

![ACOP](./images/emptyevent.png)

烏馬諾瓦·雅內拉·德·埃文托·瓦齊亞·阿帕雷克。

![ACOP](./images/emptyevent1.png)

Em primeiro lugar, dê um noma o seu evento como, por exampleo: `seuSobrenomeAccountCreationEvent` e adicione uma描述como como, por exemple: `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certifique-se de que **類型** 我就是，科莫 **單一** e，第seleção de **事件ID類型**, selectone **系統生成**.

![ACOP](./images/eventidtype.png)

一個塞萊桑的方案。 我的計畫是準備做練習。 使用結構 `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos sendo selecionados na seção **欄位**. 阿戈拉·沃克·德韋·帕薩 **欄位** Trêsícones彈出窗口serão exibidos。 伊科內集團 **編輯**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop de **欄位**，通過você deve selectionar alguns dos campos que precisamos para personalizar o e-mail。 Escolheremos outs outros atributos de perfil posteromente, uldando os dados já exises na Adobe Experience Platform。

![ACOP](./images/eventfields.png)

無對象 `_experienceplatform.demoEnvironment`, pcertifique se de selectionar os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

無對象 `_experienceplatform.identification.core`, certifique se de selecionar o campo **電子郵件**.

![ACOP](./images/eventpayloadbrid.png)

小組 **確定** 敬薩爾瓦·蘇亞斯·阿爾特拉松斯。

![ACOP](./images/saveok.png)

Em seguida，一個絕育女。 小組 **儲存**  馬伊斯·烏馬·韋斯·薩爾瓦·蘇亞斯·阿爾特拉松伊斯……

![ACOP](./images/eventsave.png)

我要說，我要說，我要說。

![ACOP](./images/eventdone.png)

Miclus no seu evento novamentte para abrir mais uma vez a tela **編輯事件**. 滑鼠的呼吸 **欄位** 第3段，西科內斯·韋斯。 伊科內集團 **檢視裝載**.

![ACOP](./images/viewevent.png)

阿戈拉語中的意思是，我的意思是：
Seu evento tem um eventID de orquestraçãoú nico, que você pode encontror ralando para baixo nessa cargaútil（裝載）até visualizar `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventIDé o que deve ser enviado à Adobe Experience Platform para acionar a jorna dus próximos extreccios. Lembre-se deste eventID, você pode precisar deposerormente。
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

小組 **確定** e, em seguida，小團em **取消**.

阿戈拉辭職了。

埃塔帕： [ 2.3電子郵件](./ex3.md)

[烏薩里奧河畔雷托納爾2](./uc2.md)

[托多斯山](../../overview.md)
