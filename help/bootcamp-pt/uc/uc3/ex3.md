---
title: Bootcamp — 混合物理和數位 — Journey Optimizer建立歷程並推播 — 巴西通知
description: Bootcamp — 混合物理和數位 — Journey Optimizer建立歷程並推播 — 巴西通知
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 020e9fb8a1d02b93e4e95a4274806c7926c02757
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 2%

---

# 3.3 Crie sua jornada e notificação push

Neste merkeício, você irá configar a jornada e a mensagem que presisa ser acionada quando alguém inser ir uma sinalização（信標）usando o aplicativo móvel。

登錄Adobe Journey Optimizer帳戶a [Adobe Experience Cloud](https://experience.adobe.com). 小組 **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da **首頁** 不，Journey Optimizer。 Primeiro, Verifique se você usando o sandbox correto. 不要沙箱，就要用 `Bootcamp`. Para alternar de um sandbox para outro, plicaem **生產** 選擇沙箱或沙箱。 不要做沙箱 **布坎普**. Você estará na visualização da **首頁**  做seu沙箱 `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1條

沒有菜單，小伙子 **歷程**. 阿姆·西吉達，小團 **建立歷程** 準新約旦河。

![ACOP](./images/createjourney.png)

Você verá muma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

前無鍛鍊，從頭開始 **事件**. 沃凱諾梅烏奧埃文托 `yourLastNameBeaconEntryEvent` e替代 `yourLastName` 別洛·蘇·索佈雷諾姆。 Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

阿戈拉認為，這甚至與我的意思有關。 Você pode fazer isso indo para o lado esquerdo da tela procando pelo seu evento n a lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de jornada. 我們的愛情。 小組 **確定** 薩爾瓦·蘇亞斯·阿爾特拉松伊斯。

![ACOP](./images/journeyevent.png)

科莫·塞貢達·埃塔帕·達·約納達 **推播**. Vá para o lado esquerdo da tela para **動作**，請選取ação **推播** arraste e solte a ação no segundo nó da sua jornada.

![ACOP](./images/journeyactions.png)

不用拉多·迪雷托·達特拉，阿戈拉·沃克斯·德韋·蘇阿·通達桑推。

定義a **類別** co **行銷** e selecione uma supfície push que permite envion notificações push. Nesse caso，淺層推選 **mmeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Crie a sua mensagem

小組 **編輯內容**.

![ACOP](./images/emptymsg.png)

Em seguida，一個被禁慾的女孩：

![ACOP](./images/emailmsglist.png)

快來點通知。

Prichum no campo de texto **標題**.

![Journey Optimizer](./images/msg5.png)

德克斯托，科米斯 **奧拉**. 個人化團體。

![Journey Optimizer](./images/msg6.png)

Agora você precisa trazer o token de personalização para o campo **名字** 她就是個女人 `profile.person.name.firstName`. 無菜單，選擇 **設定檔屬性**，第baixo/navegue para narr o elemento角色 **人員** 納西塔·帕拉·阿瓦努 `profile.person.name.firstName`. 伊科內集團 **+** para adicionar o campoà tela 小組 **儲存**.

![Journey Optimizer](./images/msg7.png)

恩唐，我要回去。 個人化團體 **主體**.

![Journey Optimizer](./images/msg11.png)

埃斯克里瓦 `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

阿姆·西吉達，小團  **內容屬性** 然後 **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

小組 **事件**.

![ACOP](./images/jomsg4.png)

小集團，不是女的，是女的，是女的。 **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

小組 **放置內容**.

![ACOP](./images/jomsg6.png)

小組 **POI互動**.

![ACOP](./images/jomsg7.png)

小組 **POI詳細資料**.

![ACOP](./images/jomsg8.png)

小集團 **+** 圖示無 **POI名稱**.
塞吉達，塞金特·塞拉。 小組 **儲存**.

![ACOP](./images/jomsg9.png)

我的手足足足足夠了。 Cligus na seta no canto super esquerdo para reconnar à sua jornada.

![ACOP](./images/jomsg11.png)

小組 **確定**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para mu ma tela

科莫·特塞拉·埃塔帕·達·約納達  **sendMessageToScreen** 動作。 Vá para o lado esquerdo da tela para **動作**，請選取ação **sendMessageToScreen** arraste e solte ação no terceiro nó da sua jornada. Em seguida，這是一個彈奏。

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá publicar uma mensagem no ponto de extremidade usado pela exibção na loja. 阿桑 **sendMessageToScreen** 埃斯佩拉·克·穆爾蒂普拉斯·瓦里韋斯·塞賈姆·德菲達斯。 Você pode visualizar essas variáveis rolando para baixo até ver **動作參數**.

![ACOP](./images/jomsg16.png)

Agora você precisa definir os valores para cada parâmetro de ação. Siga esta tabela para entender quais valores são equedários e onde.

| 參數 | 值 |
|:-------------:| :---------------:|
| 傳送 | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| 名字 | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| 沙箱 | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style=&quot;table-layout:auto&quot;}

準定義是，瓦洛雷斯，小集團 **編輯**.

![ACOP](./images/jomsg17.png)

Em seguida, selecione **進階模式**.

![ACOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. 小組 **確定**.

![ACOP](./images/jomsg19.png)

Repita負責處理para adicionar valores para cada campo。

>[!IMPORTANT]
>
>聖壇`yourLastNameBeaconEntryEvent`. Lembre-se-de suptiir  `yourLastName` 別洛·蘇·索佈雷諾姆。

最後，塞梅爾漢特·奧塞金特：

![ACOP](./images/jomsg20.png)

角色 **確定**.

![ACOP](./images/jomsg21.png)

您仍需為歷程命名。 您可以按一下 **屬性** 圖示。

![ACOP](./images/journeyname.png)

有水就有水。 使用 `yourLastName - Beacon Entry Journey`. 小組 **確定** 薩爾瓦·蘇亞斯·阿爾特拉松伊斯。

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **發佈**.

![ACOP](./images/publishjourney.png)

小組 **發佈** 諾瓦門特。

![ACOP](./images/publish1.png)

Você verá uma barra de confirmmação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

我的手術很好。

Você termou est exticio。

埃塔帕： [3.4聖若那達](./ex4.md)

[烏薩里奧3](./uc3.md)

[托多斯山](../../overview.md)
