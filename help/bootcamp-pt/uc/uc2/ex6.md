---
title: Bootcamp — 客服中心的Personalization — 巴西
description: Bootcamp — 客服中心的Personalization — 巴西
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 7acf778b-042f-4deb-9406-ddcf63daacda
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# 2.6 Personalizaçao無客服中心

一致同意將酒莊酒莊的酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊的酒莊酒莊酒莊酒莊酒莊酒莊的酒莊酒莊酒莊酒莊酒莊酒莊酒莊，酒莊酒莊的酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊酒莊的精釀佳作。 呼叫中心geralmente é bastante desconectado do restante da jornada do cliente e isso pode， com frequencia， levar a experiencias frustranters do cliente， mas nao precisa ser assim. Vamos mostrar um exemplo de como客服中心的pode ser facilmente conectado à Adobe Experience Platform， em tempo real。

## 客戶通貨

沒有前方的練習，沒有使用過aplicativo móvel， voce comprou um producto clicando no botao **購買**。

![DSN](./images/app20.png)

要保持音量嗎？要保持音量嗎？ 諾瑪門特，語音連字型大小呼叫中心。

Antes de ligar para o呼叫中心，voce precisa saber seu **忠誠度識別碼**。 Voce pode contract seu ID de fidelidade no Visualizador de Perfil do site.

![DSN](./images/cc1.png)

Nesse caso， o **忠誠度識別碼** é **5863105**。 Como parte de nossa implementacao personalizada do recurso de call center no ambiente de demonstracao， voce deve adicionar um prefixo ao seu **忠誠度識別碼**。 o prefixo é **11373**， portanto， o ID de fidelidade a ser usado neste explo é **113735863105**。

Vamos fazer很讚。 使用seu telefone e ligue para o nurmero **+1 (323) 745-1670**。

![DSN](./images/cc2.png)

塞拉索里塔多在站音識別碼de fidelidade， seguido de **#**。 Digite seu ID de fidelidade。

![DSN](./images/cc3.png)

Voce ouvirá **您好，請講**。 在Adobe Experience Platform中隨時可以享受客戶專屬的專屬服務。 voce tem 3 escolhas。 Pressione o número **1**，**訂單狀態**。

![DSN](./images/cc4.png)

Depois de ouvir o status do seu pedido， voce terá a opcao de pressionar **1** para voltar ao menu principal ou pressionar 2。 Pressione **2**。

![DSN](./images/cc5.png)

Em seguida， será solicitado que voce avalie sua experiencia de call center， selececonando um numero entre 1 e 5， sendo 1 baixo e 5 alto. 開胃小吃。

![DSN](./images/cc6.png)

Sua chamada para o call center será encerrada.

存取[Adobe Experience Platform](https://experience.adobe.com/platform)。 Depois de fazer登入，voce irá acsesar a página inicial da Adobe Experience Platform。

![資料擷取](./images/home.png)

Antes de continuar， voce precisa selectionar um **沙箱**。 不要做沙箱，請選取``Bootcamp``。 É posssível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte superior da tela。 [!UICONTROL 沙箱]的專屬專屬專用裝置，您的專屬裝置為[!UICONTROL 沙箱]專用裝置。

![資料擷取](./images/sb1.png)

無功能表à esquerda，存取&#x200B;**設定檔** e **瀏覽**。

![客戶設定檔](./images/homemenu.png)

選取&#x200B;**身分識別名稱空間** **電子郵件** e insira o endereco de email do seu perfil de cliente。 叢集&#x200B;**檢視**。 小集團違反規定。

![DSN](./images/cc7.png)

客戶的新近行為。 存取&#x200B;**個事件**。

![DSN](./images/cc8.png)

Em eventos， voce verá 2 eventos com um eventType de **呼叫中心**。 O primeiro evento é o resultado da sua reposta à pergunta **評定您的通話滿意度** (avalie seu chamada)。

![DSN](./images/cc9.png)

在&#x200B;**訂單狀態**&#x200B;中擔任以下角色： um pouco para baixo e voce verá o evento que foi registrado quando voce selecionou a opcao de verificar。

![DSN](./images/cc10.png)

存取&#x200B;**區段會籍**。 Agora voce verá que 2 segmentos se qualificam em seu perfil， em tempo real， com base nas interacoes que voce teve por meio do call center. Essas associacoes de segmento podem e devem ser usadas para impactar qual comunicação e personalização acontece em qualquer outtro canal.

![DSN](./images/cc11.png)

請回答問題。

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
