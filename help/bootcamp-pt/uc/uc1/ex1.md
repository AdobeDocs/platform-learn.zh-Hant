---
title: Bootcamp — 即時客戶設定檔 — 從未知到網站上已知 — 巴西
description: Bootcamp — 即時客戶設定檔 — 從未知到網站上已知 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 853a69d2-5dac-413d-bb40-ef29604a26ae
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# 1.1 Do desconhecido ao conhecido em nosso網站

## Contexto

Adobe Experience Platform desempenha um papel important nesa jornada. A plataforma é é cérebro da comunicação， o **體驗記錄系統**.

Plataforma é um ambiente em que a palavra cliente engloba mais do que clientes conhecidos. Um visitante desconhecido no site também é um cliente do ponto de vista da Plataforma e， como tal， todo o comportamento de um visitante desconhecido também é enviado à Plataforma. Gracas a essa abordagem， quando esse visitante eventualmente se torna um cliente conhecido， uma marca também pode visualizar o que aconteceu antes daquele momento. Isso ajuda a partir de uma perspectiva de otimização de atribuicao e experiencia.

## Fluxo da jornada do cliente

Acesse [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). 小團體 **全部允許**.

![DSN](./images/web8.png)

無任何小團體no ícone do logotipo da Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfil.

![示範](./images/pv1.png)

驗證o painel do Visualizador de perfil e no Perfil do cliente em tempo real com o **EXPERIENCE CLOUDID** 身分已達最高點primário para este cliente que ainda é desconhecido。

![示範](./images/pv2.png)

Voce também pode ver todos os Eventos de Experiencia coletados com base no comportamento do cliente. 一個沒有動機的狀態，mas isso mudará em breve。

![示範](./images/pv3.png)

存取opcao de功能表 **應用程式服務** 小集團沒有產品 **Real-Time CDP**.

![示範](./images/pv4.png)

凡是細枝末節的作品，都值得一閱。 Um Evento de experiencia do tipo **產品檢視** Agora foi envirado para a Adobe Experience Platform usando a implementacao do Web SDK que voce revisou no Módulo 1. Abra o painel Visualizador de perfil e verificue seus **體驗事件**.

![示範](./images/pv5.png)

存取opcao de功能表 **應用程式服務** 小集團沒有產品 **Adobe Journey Optimizer**. Mais um Evento de experiencia foi environado para Adobe Experience Platform.

![示範](./images/pv7.png)

Abra o painel Visualizador de perfil. Agora voce verá 2 Eventos de experiencia do tipo **產品檢視**. Embora o comportamento seja anonimo、cada clique é rastreado e armazenado na Adobe Experience Platform。 Depois que o cliente anonimo se tornar conhecido， poderemos messclar todo o comportamento anonimo automaticamente ao perfil conhecido.

![示範](./images/pv8.png)

Agora vamos analisar seu perfil de cliente e usar seu comportamento para periencia do cliente no site.

冰淇淋甜菜： [1.2以視覺效果呈現使用者端端速度的seu próprio perfil de cliente em tempo real - UI](./ex2.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
