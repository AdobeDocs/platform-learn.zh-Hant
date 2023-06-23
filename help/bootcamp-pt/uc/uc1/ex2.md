---
title: Bootcamp — 即時客戶設定檔 — 視覺化您自己的即時客戶設定檔 — UI — 巴西
description: Bootcamp — 即時客戶設定檔 — 視覺化您自己的即時客戶設定檔 — UI — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 4eebb080-77fd-4162-aa64-d599f1274c93
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 2%

---

# 1.2以視覺效果呈現使用者端端速度的seu próprio perfil de cliente em tempo real - UI

Neste exercício， voce irá fazer login na Adobe Experience Platform e visualizar seu próprio Perfil de cliente em tempo real na UI.

## 歷史協會

沒有Perfil do cliente em tempo real， todos os dados do perfil sao exibidos juntamente com os dados do evento， além das associacoes de segmentos existes. Os dados mostrados podem vir de qualquer lugar， de aplicativos daAdobe解決方案外部。 Essa é a exibicao mais poderosa da Adobe Experience Platform， o verdadeiro local do sistema de experiencia.

## 1.2.1使用visualizacao do perfil do cliente na Adobe Experience Platform

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer登入，voce irá存取página incial da Adobe Experience Platform。

![資料擷取](./images/home.png)

Antes de continuar， voce precisa seclecionar um **沙箱**. Bootcamp不做沙箱。 É possível fazer isso clicando no texto **[!UICONTROL 生產產品]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙箱] dedicado。

![資料擷取](./images/sb1.png)

無功能表對應查詢、存取 **設定檔** e **瀏覽**.

![客戶設定檔](./images/homemenu.png)

沒有painel Visualizador de perfil沒有seu網站，voce pode包含visao geral da identidade。 Cada已識別está vinculada a um名稱空間。

![客戶設定檔](./images/identities.png)

沒有painel Visualizador de perfil、agora voce pode ver uma identidade semelhante a seguinte：

| 命名空間 | 身分 |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

Com a Adobe Experience Platform， todos os IDs sao igualmente importants. 先前，在ECID時代ID服務重要無上下文到Adobee todos os outros IDestavam vinculados ao ECID em uma relação hierárquica。 Com a Adobe Experience Platform、isso mudou e cada ID pode ser considerado um identificador primário。

一般情況，以識別基本相依的情境。 Se voce perguntar ao seu呼叫中心： **ID服務是否重要？** Eles提供回應： **不許打電話！** Mas se voce perguntar à sua equipe de CRM， eles responderao： **o endereco de email！** Adobe Experience Platform提供essa complexidade e gerencia isso para voce。 Cada aplicativo， seja um aplicativo da Adobe ou nao， se comunicará com a Adobe Experience Platform referindo-se ao ID que consideram principal. 簡化功能。

Para o campo **身分名稱空間**，選取 **ECID** e para o campo **身分值** 在Insira o ECID que voce pode contract no painel Visualizador de perfil do site do Bootcamp。 小團體 **檢視**. 絕對是假的。 小團體否 **設定檔ID** para abrir seu perfil.

![客戶設定檔](./images/popupecid.png)

Agora voce tem uma visao geral de alguns **Attributos de perfil** 重要的是要確保客戶有適當的偏好。

![客戶設定檔](./images/profile.png)

Acesse **事件**，Onde voce pode ver as entradas de cada evento de experiencia vinculado ao seu Perfil。

![客戶設定檔](./images/profileee.png)

快進，存取快進功能表 **區段會籍**. Agora voce verá todos os segmentos que se qualificam para este perfil.

![客戶設定檔](./images/profileseg.png)

Agora vamos criar um novo segmento que permitirá que voce periencia do cliente para um cliente anonimo ou conhecido.

冰淇淋甜菜： [1.3 Crie um區段 — UI](./ex3.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
