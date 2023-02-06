---
title: Bootcamp — 即時CDP — 建立區段並採取行動 — 將區段傳送至Adobe Target — 巴西
description: Bootcamp — 即時CDP — 建立區段並採取行動 — 將區段傳送至Adobe Target — 巴西
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 020e9fb8a1d02b93e4e95a4274806c7926c02757
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# 1.4阿桑：Adobe Target

阿塞斯 [Adobe Experience Platform](https://experience.adobe.com/platform). 登入Depois de fazer，是Página inical da Adobe Experience Platform。

![資料擷取](./images/home.png)

連續、前輪 **沙箱**. 不要在Bootcamp上沙箱。 É postível fazer isso clicando no texto **[!UICONTROL 生產產品]** 娜琳娜·阿祖爾娜·帕特·蘇佩拉。 在沙箱上自行選擇 [!UICONTROL 沙箱] 愛心。

![資料擷取](./images/sb1.png)

## 1.4.1Adobe Target

O Adobe Target是CDP的真節奏。 Para configurar sua integratção com o Adobe Target, acesse **目的地** e **目錄**.

小組 **個人化** 無菜單 **類別**. Você verá o cartão de destino do **Adobe Target**. 小組 **啟用區段**.

![AT](./images/atdest1.png)

選擇目標 ``Bootcamp Target`` e集團 **下一個**.

![AT](./images/atdest3.png)

Na lista de segmentos disponíveis, selecione o segmento que você criou em [1.3標準區段](./ex3.md),com o nome `yourLastName - Interest in Real-Time CDP`. 阿姆·西吉達，小團 **下一個**.

![AT](./images/atdest8.png)

我是小朋友 **下一個**.

![AT](./images/atdest9.png)

小組 **完成**.

![AT](./images/atdest10.png)

她是Adobe Target。

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destino do Adobe Target no Real-Time CDP, pode levar até uma hora para que o destino seja ativado. Este e um tempo de esperaúnico devidoà definição da configação de back-end. Depois que o tempo de espera inicial de hora e a configuração do back-end forem conclutios, os segmentos de borda recém-adicionados que são enviados do Adobe Target destino do estarão disponíveis para segmentação tem real。

## 1.4.2設定sua atividade baseada em formulário do Adobe Target

Agora que seu segmento Real-Time CDP está configurado para senviado ao Adobe Target, e posível configurar sua atividade de Segmentação por experincia no Adobe Target. 不參加練習，不參加可視化體驗撰寫器。

Adobe Experience Cloud [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). 小組 **目標** 帕拉·阿布里爾。

![RTCDP](./images/excl.png)

在 **Adobe Target** 首頁，您會看到所有現有活動。
按一下 **+建立活動** 來建立新活動。
非官方的 **Adobe Target**,você verá todas atividades existos。
小組 **+建立活動** para criar uma nova atividade。

![RTCDP](./images/exclatov.png)

選取項 **體驗鎖定**.

![RTCDP](./images/exclatcrxt.png)

選取項 **視覺** e定義a **活動URL** co `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`,mas,antes，否則，替代XX por um número entre 01 e 30。

>[!IMPORTANT]
>
>Cada參與者： Capaciação deve usar uma página da Web separada para evitar a colisão de várias experincias do Adobe Target。 É posível escolher uma página da Web將URL訪問： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o número do participante.
>
>Por exmelo, o participant 1用於刪除URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，或參與30使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

選擇工作區 **AT Bootcamp**.

小組 **下一個**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você está no Visual Experience Composer。 Pode levar de 20 a 30 segundos até que o site esteja completate carregado.

![RTCDP](./images/atform1.png)

阿圖爾門特、奧普布利科帕德朗 **所有訪客**. 小集團 **3點** 奧拉多德 **所有訪客** e團 **變更對象**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de públicos disponíveis, e o segmento da Adobe Experience Platform que você criou anteriormente e envio au Adobe Target agora faz parte dessa lista. 請選擇「Segmento que você criou anteriormente na Adobe Experience Platform」。 小組 **指派對象**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora faz parte dessa Atividade de segmentação por experincia.

![RTCDP](./images/atform4.png)

影像主管，歌手 **允許全部** 無橫幅de cookie。

Para isso, vá para **瀏覽**

![RTCDP](./images/cook1.png)

阿姆·西吉達，小團 **允許全部**.

![RTCDP](./images/cook2.png)

Em seguida, Retorne para **撰寫**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página inicial do site. Clique na imagem principal padrão no site, clique em **取代內容** e選擇 **影像**.

![RTCDP](./images/atform5.png)

Pesquise o arquivo de imagem **rtcdp.png**. 選擇e團 **儲存**.

![RTCDP](./images/atform6.png)

Você verá a nova experiencia com a nova imagem para o seu Público selecionado

![RTCDP](./images/atform7.png)

Cligue no título da sua atividade no canto supererdo para renomeá la.

![RTCDP](./images/exclatvecname.png)

段或段，使用：

- `yourLastName - RTCDP - XT (VEC)`

小組 **下一個**.

![RTCDP](./images/atform8.png)

小組 **下一個**.

![RTCDP](./images/atform8a.png)

納帕吉納 **目標與設定**, acesse **目標量度**.

![RTCDP](./images/atform9.png)

定義元首 **參與** - **網站逗留時間**. 小組 **儲存並關閉**.

![RTCDP](./images/vec3.png)

阿戈拉·沃克斯塔娜·帕吉娜 **活動概覽**. Você ainda precisa ativar sua Atividade。

![RTCDP](./images/atform10.png)

小坎波 **非作用中** e選擇 **啟動**.

![RTCDP](./images/atform11.png)

Você receberá uma confirmação visual de sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada no site do bootcamp.

Se agora você voltar ao seu site de dedezção e visitar a página do produto para **Real-Time CDP**, você se qualificará instantenamente para o segmento que criou e verá a atividade do Adobe Target exibida na página nicial tempo real。

>[!IMPORTANT]
>
>Cada參與者： Capaciação deve usar uma página da Web separada para evitar a colisão de várias experincias do Adobe Target。 É postível escolher uma página da Web加入URL acessando ao連結： [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as páginas compartilham a mesma URL base e terminam com o número do participante.
>
>Por exmelo, o participante 1 deve usar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`，或參與30使用URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

埃塔帕： [1.5採取行動：將區段傳送至Facebook](./ex5.md)

[烏薩里奧1號](./uc1.md)

[托多斯山](../../overview.md)
