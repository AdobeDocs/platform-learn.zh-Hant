---
title: Bootcamp — 即時客戶設定檔 — 視覺化您自己的即時客戶設定檔 — UI — 巴西
description: Bootcamp — 即時客戶設定檔 — 視覺化您自己的即時客戶設定檔 — UI — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4eebb080-77fd-4162-aa64-d599f1274c93
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# 1.2以視覺化方式呈現使用者端即時資料的seu próprio perfil - UI

Neste excício， voce irá fazer login na Adobe Experience Platform e visualizar seu próprio Perfil de cliente em tempo real na UI.

## 歷史學

沒有Perfil do cliente em tempo real， todos os dados do perfil sao exibidos juntamente com os dados do evento， além das associacoes de segmentos existents. 作業系統dados mostrados podem vir de qualquer lugar， de aplicativos daAdobe解決方案外部。 Essa é a exibicao mais poderosa da Adobe Experience Platform， o verdadeiro local do sistema de experiencia.

## 1.2.1使用visualizacao do perfil do cliente na Adobe Experience Platform

存取[Adobe Experience Platform](https://experience.adobe.com/platform)。 Depois de fazer登入，voce irá acsesar a página inicial da Adobe Experience Platform。

![資料擷取](./images/home.png)

Antes de continuar， voce precisa selectionar um **沙箱**。 不要做沙箱，你可以選擇一個é Bootcamp。 É posssível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte superior da tela。 Depois de selecionar o sandbox apropriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙箱]專用沙箱。

![資料擷取](./images/sb1.png)

無功能表à esquerda，存取&#x200B;**設定檔** e **瀏覽**。

![客戶設定檔](./images/homemenu.png)

沒有painel Visualizador de perfil沒有網站，voce pode包含了visao geral da identidade。 已識別está vinculada a um名稱空間。

![客戶設定檔](./images/identities.png)

沒有painel Visualizador de perfil， agora voce pode ver uma identidade semelhante a seguinte：

| 命名空間 | 身分 |
|:-------------:| :---------------:|
| Experience CloudID (ECID) | 19428085896177382402834560825640259081 |

在Adobe Experience Platform、todos os IDs sao igualmente important中存取。 前言，在ECID時代o ID服務很重要，沒有情境到daAdobee todos os outtros IDs estavam vinculados ao ECID em uma relação hierárquica。 在Adobe Experience Platform上，isso mudou e cada ID pode ser considerado um identificador primário。

一般化，以識別主上下文依存性。 Seo voce perguntar ao seu呼叫中心： **Qual é o ID mais important？** Eles provavelmente responderao： **o numero de telefone！** Mas se voce à sua equipe de CRM， eles responderao： **o endereco de email！** A Adobe Experience Platform包含essa complexidade e gerencia isso para voce。 Cada aplicativo， seja um aplicativo da Adobe ou nao， se comunicará com a Adobe Experience Platform referindo-se ao ID que consideram principal. 簡化功能。

Para o campo **身分名稱空間**，請選取&#x200B;**ECID** e para o campo **身分值** insira o ECID que voce pode encontrrar no painel Visualizador de perfil do site do Bootcamp。 叢集&#x200B;**檢視**。 絕對是假的。 叢集無&#x200B;**設定檔識別碼** para abrir seu設定檔。

![客戶設定檔](./images/popupecid.png)

Agora voce tem uma visao geral de alguns **Atributos de perfil**&#x200B;重要資料必須能夠證明客戶的身份。

![客戶設定檔](./images/profile.png)

Accesse **Events**， onde voce pode ver as entradas de cada evento de experiencia vinculado ao seu Perfil.

![客戶設定檔](./images/profileee.png)

Por fim，存取opcao de功能表&#x200B;**區段會籍**。 Agora voce verá todos os segmentos que se qualificam para este perfil.

![客戶設定檔](./images/profileseg.png)

Agora vamos criar um novo segmento que permitirá que voce個人化experiencia do cliente para cliente anonimo ou conhecido。

Próxima etapa： [1.3 Crie um segmento - UI](./ex3.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
