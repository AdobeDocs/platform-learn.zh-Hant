---
title: Bootcamp - Real-time CDP — 建立區段並採取行動 — 將您的區段傳送至Adobe Target — 巴西
description: Bootcamp - Real-time CDP — 建立區段並採取行動 — 將您的區段傳送至Adobe Target — 巴西
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Segments, Integrations
exl-id: 862afd4c-1b6c-48fe-bc1f-967c065642e0
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# 1.4 Acao：envie seu segmento para o Adobe Target

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer登入，voce irá存取página incial da Adobe Experience Platform。

![資料擷取](./images/home.png)

Antes de continuar， voce precisa seclecionar um **沙箱**. Bootcamp不做沙箱。 É possível fazer isso clicando no texto **[!UICONTROL 生產產品]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙箱] dedicado。

![資料擷取](./images/sb1.png)

## 1.4.1 Active seu segmento para o destino do Adobe Target

O Adobe Target está disponível como um destino do CDP em tempo real. Para configurar sua integracao com o Adobe Target， acesse **目的地** e **目錄**.

小團體 **個人化** 無功能表 **類別**. 我們的目標 **Adobe Target**. 小團體 **啟用區段**.

![於](./images/atdest1.png)

目的地選擇 ``Bootcamp Target`` 小團體 **下一個**.

![於](./images/atdest3.png)

區段選擇區段區段 [1.3臨界值區段](./ex3.md)，com名稱 `yourLastName - Interest in Real-Time CDP`. Em seguida，小團體 **下一個**.

![於](./images/atdest8.png)

小圈子，小圈子 **下一個**.

![於](./images/atdest9.png)

小團體 **完成**.

![於](./images/atdest10.png)

在Adobe Target上建立區段。

![於](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destino do Adobe Target no Real-Time CDP， pode levar até uma hora para que o destino seja ativado. 我們來看看後端espera único devido à definicao da configuração de back-end是什麼樣子。 Depois que o tempo de espera inicial de 1 hora e a configuracao do backend form concluídos， os segmentos de borda recém-adicionados que sao enviados ao destino do Adobe Target estarao disponíveis para segmentacao em tempo real.

## 1.4.2設定sua atividade no Adobe Target

Agora que seu segmento Real-Time CDP está configurado para ser enviado ao Adobe Target， é possível configurar sua atividade de Segmentacao por experiencia no Adobe Target。 Neste exercício， voce irá configurar uma atividade baseada no Visual Experience Composer.

存取Página inicial da Adobe Experience Cloud acessando [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). 小團體 **Target** para abrir.

![RTCDP](./images/excl.png)

初戀Na página **Adobe Target**，voce verá todas as atividades existenes.
小團體 **+建立活動** para criar uma nova atividade.

![RTCDP](./images/exclatov.png)

選擇器 **體驗鎖定**.

![RTCDP](./images/exclatcrxt.png)

選擇器 **視覺** 定義a **活動URL** como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`、mas、antes disso、substitua XX por um numero entre 01 e 60。

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisao de várias experiencias do Adobe Target。 É possível escolher uma página da Web e包含URL存取： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o numero do participante.
>
>Por範例， o參與1 deve使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`， o參與30 deve使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

工作區選擇 **AT Bootcamp**.

小團體 **下一個**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora voce沒有視覺化體驗撰寫器。 Pode levar de 20 a 30 segundos até que o site esteja completamente carregado.

![RTCDP](./images/atform1.png)

聖保羅州圖阿爾門特 **所有訪客**. 小團體nos **3點** Ao lado de **所有訪客** 小團體 **變更對象**.

![RTCDP](./images/atform3.png)

Agora voce está vendo a lista de públicos disponíveis， e o segmento da Adobe Experience Platform que voce criou anteriormente e enviou ao Adobe Target agora faz parte dessa lista. 選取Adobe Experience Platform前方的區段。 小團體 **指派對象**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora faz parte dessa Atividade de segmentacao por experiencia.

![RTCDP](./images/atform4.png)

Antes de alterar a imagem principal， voce deve clicar em **全部允許** 沒有橫幅de Cookie。

段落，段落 **瀏覽**

![RTCDP](./images/cook1.png)

Em seguida，小團體 **全部允許**.

![RTCDP](./images/cook2.png)

Em seguida， retorne para **撰寫**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página inicial do site. Clique na imagem principal padrao no site， clique em **取代內容** 選擇器 **影像**.

![RTCDP](./images/atform5.png)

Pesquise o arquivo de imagem **rtcdp.png**. 選擇群組 **儲存**.

![RTCDP](./images/atform6.png)

Voce verá a nova experiencia com a nova imagem para o seu Público selectionado

![RTCDP](./images/atform7.png)

小團體沒有坦誠的上級esquerdo para renomeá-la。

![RTCDP](./images/exclatvecname.png)

Para o nome，使用：

- `seuSobrenome - RTCDP - XT (VEC)`

小團體 **下一個**.

![RTCDP](./images/atform8.png)

小團體 **下一個**.

![RTCDP](./images/atform8a.png)

那帕吉納 **目標與設定**，存取權 **目標量度**.

![RTCDP](./images/atform9.png)

定義中繼主體元件 **參與** - **網站逗留時間**. 小團體 **儲存並關閉**.

![RTCDP](./images/vec3.png)

西班牙語 **活動概覽**. Voce ainda precisa activar sua Atividade.

![RTCDP](./images/atform10.png)

小團體無坎波 **非使用中** 選擇器 **啟動**.

![RTCDP](./images/atform11.png)

Voce receberá uma confirmacau visual de que sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada網站沒有啟動營。

Se agora voce voltar ao seu site de demonstracao e visitar a página do produto para **Real-Time CDP**、voce se qualificará instantaneamente para o segmento que criou e verá a atividade do Adobe Target exibida na página inicial em tempo real.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisao de várias experiencias do Adobe Target。 É possível escolher uma página da Web e內含URL accessando ao連結： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o numero do participante.
>
>Por範例， o參與者1 deve usar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`， o參與30 deve使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

冰淇淋甜菜： [1.5 Acao：envie seu segmento para o Facebook](./ex5.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
