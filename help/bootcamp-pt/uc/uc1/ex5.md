---
title: Bootcamp - Real-time CDP — 建立區段並採取行動 — 將您的區段傳送至DV360 — 巴西
description: Bootcamp - Real-time CDP — 建立區段並採取行動 — 將您的區段傳送至DV360 — 巴西
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: acb32859-6f82-44e0-8948-a045a9fe2afe
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 1%

---

# 1.5 Acao：envie seu segmento para o Facebook

存取[Adobe Experience Platform](https://experience.adobe.com/platform)。 Depois de fazer登入，voce irá acsesar a página inicial da Adobe Experience Platform。

![資料擷取](./images/home.png)

Antes de continuar， voce precisa selectionar um **沙箱**。 不要做沙箱，你可以選擇一個é Bootcamp。 É posssível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte superior da tela。 Depois de selecionar o sandbox apropriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙箱]專用沙箱。

![資料擷取](./images/sb1.png)

沒有功能表à esquerda， vá para **目的地** e， em seguida， vá para **目錄**。 **目的地目錄**&#x200B;的音量。 Em **目的地**，click em **啟用區段** no cartao **Facebook自訂對象**。

![RTCDP](./images/rtcdpgoogleseg.png)

選取&#x200B;**bootcamp-facebook** e群組&#x200B;**下一步**。

![RTCDP](./images/rtcdpcreatedest2.png)

選擇區段可避免前方活動。 點按&#x200B;**下一個**。

![RTCDP](./images/rtcdpcreatedest3.png)

Na página **Mapping**，驗證se a caixa de selecao **套用轉換** está marcada。 點按&#x200B;**下一個**。

![RTCDP](./images/rtcdpcreatedest4a.png)

Na página **區段排程**，請直接從客戶選取&#x200B;**您的對象來源** e defina como **。** 點按&#x200B;**下一個**。

![RTCDP](./images/rtcdpcreatedest4.png)

Por fim， na página **Review**，click em **完成**。

![RTCDP](./images/rtcdpcreatedest5.png)

Seu segmento agora está vinculado aos Públicos Personalizados do Facebook. Sempre que um cliente se qualificar para esse segmento， um senal será enviado ao lado do servicor （伺服器端） do Facebook para incluir esse cliente no Público Personalizado no lado do Facebook。

無Facebook，請向Adobe Experience Platform區段查詢públicos Personalizados：

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora voce pode ver seu público personalizado aparecer no Facebook：

![RTCDP](./images/rtcdpcreatedest5a.png)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
