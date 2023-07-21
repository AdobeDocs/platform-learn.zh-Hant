---
title: Bootcamp -Customer Journey Analytics — 從見解到行動 — 巴西
description: Bootcamp -Customer Journey Analytics — 從見解到行動 — 巴西
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
source-wordcount: '443'
ht-degree: 0%

---

# 4.6 Dos insights à acao

## 物件

- Entenda como criar um público com base em uma visao coletada無Customer Journey Analytics
- 使用esse público no CDP em tempo real e no Adobe Journey Optimizer

## 4.6.1 Crie uma audiencia e publicque-a

Em seu projeto， voce criou um filtro chamado **通話感覺** e conseguiu visualizar a quantidade de usuários que tiveram suas ligacoes ao call center classificadas como **正面效果**. Agora， voce poderá criar um segmento com essuários e ativacao-los em jornadas ou em canais de comunicacao.

O primeiro passo é： No painel criado no último exercício， selecio one a linha **1. 通話感覺 — 正面**，點選連結com o botao direito de seu mouse e selecione a opcao **從選取專案建立對象**：

![示範](./images/aud1.png)

Em seguida， de um nome para a sua audiencia seguindo o modelo **yourLastName - cia對象通話感覺良好**：

![示範](./images/aud2.png)

注意：要預覽受眾，請點選：

![示範](./images/aud3.png)

完成部分，小團體 **公關**：

![示範](./images/aud4.png)

## 4.6.2使用sua audiencia como parte de um segmento

Voltando para a Adobe Experience Platform， vá em **區段>瀏覽** 我們把視覺化的conseguirá o seu segmento criado no CJA pronto e disponível para ser usado nas as ativacoes e jornadas！

![示範](./images/aud5.png)

Vamos agora usar esse segmento em uma ativacao no Facebook e em uma jornada do cliente！

## 4.6.3使用seu segmento na Real-Time CDP em tempo real

那個Adobe Experience Platform **區段>瀏覽** 請聽眾que voce criou no CJA：

![示範](./images/aud6.png)

小團體無順序區段e、em seguida、clique em **啟用至目的地**：

![示範](./images/aud7.png)

選取目的地小冊子facebook e、em seguida、clique em下一步：

![示範](./images/aud8.png)

Em seguida，小團體em Next novamente：

![示範](./images/aud9.png)

選擇選擇一個opcao **您的對象來源** e defina como **直接來自客戶** 小團體下一步：

![示範](./images/aud10.png)

潘金娜，潘金娜 **檢閱** 小團體完成！

![示範](./images/aud11.png)

Pronto！ 請再來一次Facebook個人化。
Agora，vamos utilizar沒有區段！

## 4.6.4不使用Adobe Journey Optimizer使用seu區段

Na interface da Adobe Experience Platform clique em Journey Optimizer e， em seguida，無選單橫向esquerdo， clique em **歷程** 我們來做個聖誕老人uma jornada clicando em **建立歷程**：

![示範](./images/aud20.png)

![示範](./images/aud21.png)

![示範](./images/aud22.png)

Em seguida，無選單側面問答集， em事件，選擇 **區段資格** 若納達島上發生這樣的事情：

![示範](./images/aud23.png)

Em seguida， em **區段** 小團體 **編輯** para seleciconar um區段：

![示範](./images/aud24.png)

選擇受眾票證，選擇無CJA票證 **儲存**：

![示範](./images/aud25.png)

Pronto！ 已加入協力廠商的daí voce pode criar uma jornada para clientes que se qualificam para esse segmento！

[返回使用者流程4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
