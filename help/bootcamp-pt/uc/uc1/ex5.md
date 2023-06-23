---
title: Bootcamp - Real-time CDP — 建立區段並採取行動 — 將您的區段傳送至DV360 — 巴西
description: Bootcamp - Real-time CDP — 建立區段並採取行動 — 將您的區段傳送至DV360 — 巴西
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: acb32859-6f82-44e0-8948-a045a9fe2afe
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 1%

---

# 1.5 Acao：envie seu segmento para o Facebook

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer登入，voce irá存取página incial da Adobe Experience Platform。

![資料擷取](./images/home.png)

Antes de continuar， voce precisa seclecionar um **沙箱**. Bootcamp不做沙箱。 É possível fazer isso clicando no texto **[!UICONTROL 生產產品]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙箱] dedicado。

![資料擷取](./images/sb1.png)

沒有功能表à esquerda， vá para **目的地** e， em seguida， vá para **目錄**. Voce verá o **目的地目錄**. Em **目的地**，小團體 **啟用區段** 無卡套 **facebook自訂對象**.

![RTCDP](./images/rtcdpgoogleseg.png)

選擇一或 **bootcamp-facebook** 小團體 **下一個**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de segmentos disponíveis， selectiono o segmento que voce criou no expercício anterior. 小團體 **下一個**.

![RTCDP](./images/rtcdpcreatedest3.png)

那帕吉納 **對應**，驗證選擇caixa de seleçao **套用轉換** 馬卡達。 小團體 **下一個**.

![RTCDP](./images/rtcdpcreatedest4a.png)

那帕吉納 **區段排程**，選取a **您的對象來源** e defina como **直接來自客戶**. 小團體 **下一個**.

![RTCDP](./images/rtcdpcreatedest4.png)

潘金娜，潘金娜 **檢閱**，小團體 **完成**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu segmento agora está vinculado aos Públicos Personalizados do Facebook. Sempre que um cliente se qualificar para esse segmento， um sinal será enviado ao lado do servidor （伺服器端） do Facebook para incluir esse cliente no Público Personalizado no lado do Facebook。

無Facebook，voce encontrará seu segmento da Adobe Experience Platform em Públicos Personalizados：

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora voce pode ver seu público personalizado aparecer no Facebook：

![RTCDP](./images/rtcdpcreatedest5a.png)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
