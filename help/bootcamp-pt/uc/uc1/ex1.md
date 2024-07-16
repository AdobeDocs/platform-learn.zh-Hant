---
title: Bootcamp — 即時客戶設定檔 — 從未知到網站上已知 — 巴西
description: Bootcamp — 即時客戶設定檔 — 從未知到網站上已知 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 853a69d2-5dac-413d-bb40-ef29604a26ae
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 1%

---

# 1.1 Do descanhecido ao conhecido em nosso網站

## Contexto

Adobe Experience Platform desempenha um papel important nesa jornada. 在&#x200B;**體驗記錄系統**&#x200B;上的Plataforma é é cérebro da comunicacao。

Plataforma é um ambiente em que a palavra cliente engloba mais do que clientes conhecidos. Um visitante desconhecido no site também é um cliente do ponto de vista da Plataforma e， como tal， todo o comportamento de um visitante desconhecido também é envado à Plataforma. Gracas a essa abordagem， quando esse visitante eventualmente se torna um cliente conhecido， uma marca também pode visualizar o que aconteceu antes daquele momento. Isso ajuda a partitir de uma perspectiva de otimização de atribuicao e experiencia.

## 客戶通貨

存取[https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net)。 點按&#x200B;**全部允許**。

![DSN](./images/web8.png)

集團沒有ícone do logotipo da Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfil。

![示範](./images/pv1.png)

驗證Painel do Visualizador de perfil e no Perfil do cliente em tempo real com o **Experience Cloud識別碼** como o identificador primário para este cliente que ainda é desconhecido。

![示範](./images/pv2.png)

Voce também pode ver todos os Eventos de Experiencia coletados com base no comportamento do cliente. 沒有動靜，是穆達拉的靈魂。

![示範](./images/pv3.png)

存取opcao de menu **應用程式服務** e clique no product **Real-Time CDP**。

![示範](./images/pv4.png)

凡是細枝末節的作品。 Um Evento de experiencia do tipo **產品檢視** agora foi enviado para a Adobe Experience Platform usando a implementacao do Web SDK que voce revisou no Módulo 1. Abra o painel Visualizador de perfil e verifique seus **體驗活動**。

![示範](./images/pv5.png)

存取opcao de menu **應用程式服務** e clique no product **Adobe Journey Optimizer**。 Mais um Evento de experiencia foi envirado para Adobe Experience Platform.

![示範](./images/pv7.png)

阿布拉或佩內爾視覺化預設。 Agora voce verá 2 Eventos de experiencia do tipo **產品檢視**。 Embora o comportamento seja anonimo， cada clique é rastreado e armazenado na Adobe Experience Platform. Depois que o cliente anonimo se tornar conhecido， poderemos mesclar todo o comportamento anonimo automaticamente ao perfil conhecido.

![示範](./images/pv8.png)

Agora vamos analisar seu perfil de cliente e usar seu comportamento para periencia do cliente no site.

Próxima etapa： [1.2視覺化seu próprio perfil de cliente em tempo real - UI](./ex2.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
