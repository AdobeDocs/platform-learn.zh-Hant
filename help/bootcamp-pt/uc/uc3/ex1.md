---
title: Bootcamp — 混合實體和數位 — 使用行動應用程式並觸發信標登入 — 巴西
description: Bootcamp — 混合實體和數位 — 使用行動應用程式並觸發信標登入 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Mobile SDK
exl-id: 14bfbebe-6df3-4a0e-875c-b4c0d016f8da
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# 3.1使用applicativo móvel e acione um beacon

## 安裝Applicativo Movel

Antes de instalar o applicativo， é necsário habilitar o **Rastreamento**&#x200B;沒有seu dispostivo iOS。 para isso，存取&#x200B;**Configuracoes** > **Privacidade e seguranca** > **Rastreamento** e驗證opcao **Permitir que os applicativos solicitem o rastreamento**。

![DSN](./../uc3/images/app4.png)

存取App Store da Apple e pesquise `aepmobile-bootcamp`。 Clique em **安裝** ou **下載**。

![DSN](./../uc3/images/app1.png)

Depois que o aplicativo estiver instalado，小團體&#x200B;**Abrir**。

![DSN](./../uc3/images/app2.png)

點按&#x200B;**確定**。

![DSN](./../uc3/images/app9.png)

叢集&#x200B;**許可權**。

![DSN](./../uc3/images/app3.png)

按一下&#x200B;**我同意**。

![DSN](./../uc3/images/app7.png)

Clique em **Permitir enquanto usa o aplicativo**。

![DSN](./../uc3/images/app8.png)

叢集&#x200B;**許可權**。

![DSN](./../uc3/images/app5.png)

Agora voce está no applicativo， na página inicial， pronto(a) para verificar toda a jornada do cliente.

![DSN](./../uc3/images/app12.png)

## 客戶通貨

必須登入才能使用Primeiramente， é é nexsário fazer。 點按&#x200B;**登入**。

![DSN](./images/app13.png)

前方為越界點，因此不存在任何網站。 Agora é necessário reutilizar o endereco de email da contra quoce criou no applicativo para fazer or login.

![示範](./images/pv1.png)

使用無網站點選集&#x200B;**登入**&#x200B;來編輯電子郵件。

![DSN](./images/app14.png)

Voce receberá uma confirmacao de que está conectado e receberá uma notificação push.

![DSN](./images/app15.png)

Retorne para a página inicial do applicativo e os recursos adicionais irao aparecer.

![DSN](./images/app17.png)

Primeiro，存取&#x200B;**產品**。 小團體em qualquer produto，巢狀範例： **咖啡要喝**。

![DSN](./images/app19.png)

Voce verá a página do producto **咖啡可去**&#x200B;無aplicativo。

![DSN](./images/app20.png)

Agora voce irá simular um evento de entrada de sinalização （信標） em uma loja offline. O objetivo da simulacao é personalizar a experiencia do cliente nas telas da loja. 以視覺化方式呈現一個體驗a experiencia na loja， foi criada uma página que mostrará de forma dinamica as information relevantes para o cliente ao entrar na loja。

Antes de continuar， abra esta página da Web em seu電腦： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

塞吉達，一株長吻鯛：

![DSN](./images/screen1.png)

塞吉達先生，歡迎您來訪。 叢集沒有&#x200B;**信標**。

![DSN](./images/app23.png)

Após essa etapa或seguinte será exibido。 Primeiro，選取&#x200B;**Bootcamp Screen Beacon** e clique no botao de **entrada**。 Isso permitirá que voce simule uma entrada de sinalização com beacon.

![DSN](./images/app21.png)

Agora confira a tela da loja. 我們的產品視覺化體驗nesa tela em 5 segundos。

![DSN](./images/screen2.png)

Em seguida， retorne para **產品**。 Clicque em qualquer produto， neste範例： **Beach blanket Tan**。

![DSN](./images/app22.png)

塞吉達先生，歡迎您來訪。 叢集沒有&#x200B;**信標**。

![DSN](./images/app23.png)

Em seguida，選取&#x200B;**Bootcamp Screen Beacon** e clique no botao de **Entrada** novamente。 Isso permitirá que voce simule uma entrada de sinalização （信標）。

![DSN](./images/app21.png)

阿戈拉，確認一下。 我們的產品視覺化體驗nesa tela em 5 segundos。

![DSN](./images/screen3.png)

Agora、vamos verificar também或seu Visualizador de Perfil無網站。 請問在座的各位，請問在座的各位，請問在座的各位，請問在座的各位，請問在Adobe Experience Platform的e位身邊。

![DSN](./images/screen4.png)

Nos próximos exercícios， voce irá configurar e testar sua própria jornada de entrada do beacon.

Próxima etapa： [3.2 Crie seu evento](./ex2.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
