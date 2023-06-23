---
title: Bootcamp — 混合實體和數位 — 使用行動應用程式並觸發信標登入 — 巴西
description: Bootcamp — 混合實體和數位 — 使用行動應用程式並觸發信標登入 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 14bfbebe-6df3-4a0e-875c-b4c0d016f8da
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 3.1使用applicativo móvel e acione um beacon

## 安裝應用程式Mov

應用程式安裝安裝，必需 **Rastreamento** 沒有seu dispositivo iOS。 段落，存取 **設定** > **Privacidade e securanca** > **Rastreamento** 驗證opcao **允許應用程式需求或需求**.

![DSN](./../uc3/images/app4.png)

存取App Store da Apple e pesquise `aepmobile-bootcamp`. 小團體 **安裝** ou **下載**.

![DSN](./../uc3/images/app1.png)

應用程式追蹤系統安裝，小團體 **Abrir**.

![DSN](./../uc3/images/app2.png)

小團體 **確定**.

![DSN](./../uc3/images/app9.png)

小團體 **許可權**.

![DSN](./../uc3/images/app3.png)

按一下 **我同意**.

![DSN](./../uc3/images/app7.png)

小團體 **美國應用程式許可權**.

![DSN](./../uc3/images/app8.png)

小團體 **許可權**.

![DSN](./../uc3/images/app5.png)

Agora voce está no applicativo， na página inicial， pronto(a) para verificar toda a jornada do cliente.

![DSN](./../uc3/images/app12.png)

## Fluxo da jornada do cliente

需要登入的首要條件。 小團體 **登入**.

![DSN](./images/app13.png)

位於前方的越野小越野小越野中，因此不存在任何網站。 Agora é necessário reutilizar o endereco de email da contact quue voce crious no applicativo para fazer or login.

![示範](./images/pv1.png)

Digite o endereco de email que voce沒有網站que em **登入**.

![DSN](./images/app14.png)

Voce receberá uma confirmacao de que está conectado e receberá uma notificação push.

![DSN](./images/app15.png)

Retorne para a página inicial do applicativo e os recursos adicionais irao aparecer.

![DSN](./images/app17.png)

Primeiro， accesse **產品**. 小團體em qualquer產品，巢狀範例： **咖啡待用**.

![DSN](./images/app19.png)

Voce verá a página do produto **咖啡待用** 無應用程式。

![DSN](./images/app20.png)

Agora voce irá simular um evento de entrada de sinalização (beacon) em uma loja offline. O objetivo da simulacao é personalizar a experiencia do cliente nas telas da loja. Para visualizar a experiencia na loja， foi criada uma página que mostrará de forma dinamica as information relevantes para o cliente ao entrar na loja.

Antes de continuar， abra esta página da Web em seu computador： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Em seguida，一種長吻蝮：

![DSN](./images/screen1.png)

Em seguida， retorne para a página inicial. 小集團無任何內涵 **beacon**.

![DSN](./images/app23.png)

Após essa etapa， o seguinte será exibido. Primeiro，選取 **Bootcamp畫面信標** e clique no botao de **entrada**. Isso permitirá que voce simule uma entrada de sinalização com beacon.

![DSN](./images/app21.png)

Agora confira a tela da loja. Voce verá o último produto visualizado aparecer nesa tela em 5 segundos.

![DSN](./images/screen2.png)

Em seguida， retorne para **產品**. 小團體em qualquer產品，巢狀範例： **沙灘毯棕褐色**.

![DSN](./images/app22.png)

Em seguida， retorne para a página inicial. 小集團無任何內涵 **beacon**.

![DSN](./images/app23.png)

Em seguida，選擇 **Bootcamp畫面信標** e clique no botao de **Entrada** novamente。 Isso permitirá que voce simule uma entrada de sinalização （信標）。

![DSN](./images/app21.png)

Agora，確認a tela da loja novamente。 Voce verá o último produto visualizado aparecer nesa tela em 5 segundos.

![DSN](./images/screen3.png)

Agora、vamos verificar também或seu Visualizador de Perfil無網站。 Voce verá muitos eventos que foram adicionados， para mostrar que alquer interacao com um cliente é coletada e armazenada na Adobe Experience Platform.

![DSN](./images/screen4.png)

Nos próximos exercícios， voce irá configurar e testar sua própria jornada de entrada do beacon.

冰淇淋甜菜： [3.2 Crie seu evento](./ex2.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
