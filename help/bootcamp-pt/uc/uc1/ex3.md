---
title: Bootcamp — 即時客戶設定檔 — 建立區段 — UI — 巴西
description: Bootcamp — 即時客戶設定檔 — 建立區段 — UI — 巴西
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 9b8d93b5-5bed-4600-8602-b438a0893612
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 2%

---

# 1.3 Crie um區段 — UI

Neste excício， voce irá criar um segmento usando o Construtor de Segmentos da Adobe Experience Platform.

## 歷史學

存取[Adobe Experience Platform](https://experience.adobe.com/platform)。 Depois de fazer登入，voce irá acsesar a página inicial da Adobe Experience Platform。

![資料擷取](./images/home.png)

Antes de continuar， voce precisa selectionar um **沙箱**。 不要做沙箱，請選取``Bootcamp``。 É posssível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte superior da tela。 Depois de selecionar o sandbox apropriado， voce verá a tela mudando e agora voce está em seu [!UICONTROL 沙箱]專用沙箱。

![資料擷取](./images/sb1.png)

沒有功能表來查詢，存取&#x200B;**區段**。 Nesta página， voce tem uma visao geral de todos os segmentos exists. Clique no botao + Criar segmento para comecar a criar um novo segmento。

![區段](./images/menuseg.png)

Quando estiver no novo constructor de segmentos， voce irá perceber imediatamente a opcao de menu **屬性** e a referencia do **XDM個人設定檔**。

![區段](./images/segmentationui.png)

XDM是一種語言，可以用作體驗工具，XDM團隊可以用作區段建構者的基礎。 Todos os dados ingeridos na platforma devem ser mapeados em relação XDM e， portanto， todos os dados se tornam parte do mesmo modelo de dados， independentemente da origem desses dados. Isso oferece uma grande vantagem ao criar segmentos， pois a partial dessa interface do usuário do constructor de segmento， é posível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os segmentos criados no Construtor de segmentos podem ser envirados para solutions comos Adobe Target， Adobe Campaign e Adobe Audience Manager para ativacao.

Agora voce precisa criar um segmento de todos os clientes que visualizaram o producto **Real-Time CDP**。

建築工程節段，節段間隔Adicionar um Evento de Experiencia。 Voce pode encontracr todos os Eventos de experiencia clicando no ícone **事件** na barra de menu **欄位**。

![區段](./images/findee.png)

Em seguida， voce verá o nó **XDM ExperienceEvents** do nível superior。 點按&#x200B;**XDM ExperienceEvent**。

![區段](./images/see.png)

存取&#x200B;**產品清單專案**。

![區段](./images/plitems.png)

選取一個&#x200B;**名稱** e arraste e solte o objeto **名稱** do menu à esquerda na tela do construtor de segmentos na secao **活動**。 Em seguida或seguinte será exibido：

![區段](./images/eewebpdtlname.png)

O parametrod de comparação device ser **等於** e，無campo de entrada，insira **即時CDP**。

![區段](./images/pv.png)

Sempre que adicionar um elemento ao construtor de segmentos， voce pode clicar no botao **重新整理預估** para obter uma nova estimativa da populaçao em seu segmento。

![區段](./images/refreshest.png)

Para **評估方法**，選取&#x200B;**Edge**。

![區段](./images/evedge.png)

香檳酒，香檳酒，香檳酒。

Como modelo de nomenclatura，使用：

- `seuSobrenome - Interest in Real-Time CDP`

Em seguida， clique no botao **儲存並關閉** para salvar seu segmento。

![區段](./images/segmentname.png)

Agora voce irá retornar à página de visao geral do segmento， onde verá uma visualização de amostra dos perfis de clientes que se qualificam para o seu segmento.

![區段](./images/savedsegment.png)

Agora voce pode continuar no próximo exercício e usar seu segmento com o Adobe Target.

Próxima etapa： [1.4 Acao： envie seu segmento para o Adobe Target](./ex4.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
