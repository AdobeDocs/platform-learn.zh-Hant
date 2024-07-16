---
title: Bootcamp -Customer Journey Analytics — 從深入解析到行動 — 巴西
description: Bootcamp -Customer Journey Analytics — 從深入解析到行動 — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 28b87e21-3168-447e-9a93-a6ae7e969657
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 4.6 Dos insights à acao

## 物件

- Entenda como criar um público com base em uma visao coletada無Customer Journey Analytics
- 使用esse público no CDP em tempo real no Adobe Journey Optimizer

## 4.6.1 Crie uma audiencia e publish-a

Em seu projeto， voce criou um filtro chamado **Call Effects** e conseguiu visualizar a quantidade de usuários que tiveram suas ligacoes ao call center classificadas como **positivas**。 阿戈拉，voce poderá criar um segmento com essuários e ativacao-los em jornadas ou em canais de comunicacao.

O primeiro passo é：沒有painel criado no último excício，請選擇a linha **1。 通話感覺 — 正面**，點按一下com o botao direito de seu mouse選取opcao **從選取專案建立對象**：

![示範](./images/aud1.png)

Em seguida， de um nome para a sua audiencia seguindo o modelo **yourLastName - cia對象來電感覺良好**：

![示範](./images/aud2.png)

注意：要預覽您的受眾，請點選：

![示範](./images/aud3.png)

Para finalizar，叢集&#x200B;**Publicar**：

![示範](./images/aud4.png)

## 4.6.2使用sua audiencia como parte de um segmento

Voltando para a Adobe Experience Platform， vá em **區段>瀏覽**&#x200B;瀏覽會議視覺化或瀏覽區段criado no CJA pronto e disponível para ser usado nas suas ativacoes e jornadas！

![示範](./images/aud5.png)

Vamos agora usar esse segmento em uma ativacao no Facebook e em uma jornada do cliente！

## 4.6.3使用seu segmento na Real-Time CDP em tempo real

Na Adobe Experience Platform， vem **區段>瀏覽** e encontre a audiences que voce criou no CJA：

![示範](./images/aud6.png)

Clique no seu segmento e， em seguida， clique em **啟用至目的地**：

![示範](./images/aud7.png)

選取目的地小獵場 — facebook e、em seguida、clique em下一步：

![示範](./images/aud8.png)

Em seguida， clicue em Next novamente：

![示範](./images/aud9.png)

選取opcao **您的對象來源** e defina como **直接來自客戶** e clique em下一步：

![示範](./images/aud10.png)

Por fim， na página **檢閱** clique em完成！

![示範](./images/aud11.png)

Pronto！ 我們來看看這個Facebook吧。
Agora， vamos utilizar esse segmento no AJO！

## 4.6.4不使用Adobe Journey Optimizer的seu區段

Na interface da Adobe Experience Platform clique em Journey Optimizer e， em seguida，無功能表橫向問答集， clique em **歷程** e comece a criar uma jornada clicando em **建立歷程**：

![示範](./images/aud20.png)

![示範](./images/aud21.png)

![示範](./images/aud22.png)

Em seguida，無功能表橫向排程，em Eventos，選取&#x200B;**區段資格**&#x200B;排列排列或按一下：

![示範](./images/aud23.png)

Em seguida， em **區段** clique em **編輯** para seseleconar um區段：

![示範](./images/aud24.png)

選取一個受眾CJA e clique em **儲存**：

![示範](./images/aud25.png)

Pronto！ 一個特定的daí voce pode criar uma jornada para clientes que se qualificam para esse segmento！

[返回使用者流程4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
