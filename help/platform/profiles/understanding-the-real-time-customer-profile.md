---
title: 瞭解即時客戶個人檔案
description: 這部影片說明 Adobe Experience Platform 如何收集和更新即時客戶輪廓，並解說您能如何存取及使用這些輪廓。
feature: Profiles
role: Data Engineer, Data Architect, Developer
level: Beginner
jira: KT-2701
thumbnail: 27251.jpg
exl-id: 6ef5b589-f874-4687-bee3-9650c993f383
source-git-commit: 112e092df6d486d8b9103013bec57d820b8ae6d7
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 13%

---

# 即時客戶輪廓概觀

此影片說明Adobe Experience Platform如何組合和更新即時客戶設定檔，以及您如何存取和使用這些設定檔。 如需詳細資訊，請瀏覽[即時客戶個人檔案檔案](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=zh-Hant)。

>[!VIDEO](https://video.tv.adobe.com/v/27251?learn=on&enablevpops)

## 架構與功能

<!-- CARDS
* overview-diagram.md
* create-merge-policies.md
* union-schemas-overview.md
* create-a-computed-attribute-for-sum-of-purchases.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Overview Diagram of Real-Time Customer Profile">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="overview-diagram.md" title="即時客戶個人檔案的概觀圖表" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/33600?format=jpeg&nocache=1740415066741" alt="即時客戶個人檔案的概觀圖表"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="overview-diagram.md" target="_blank" rel="referrer" title="即時客戶個人檔案的概觀圖表">即時客戶個人檔案的概觀圖表</a>
                    </p>
                    <p class="is-size-6">本影片將逐步解說說明Adobe Experience Platform即時客戶個人檔案功能的概觀圖表。</p>
                </div>
                <a href="overview-diagram.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Create merge policies">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="create-merge-policies.md" title="建立合併原則" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/330433?format=jpeg&nocache=1740415066765" alt="建立合併原則"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="create-merge-policies.md" target="_blank" rel="referrer" title="建立合併原則">建立合併原則</a>
                    </p>
                    <p class="is-size-6">本影片說明如何在Adobe Experience Platform中建立合併原則。 合併原則是Platform用來決定在合併來自不同來源的資料集時將使用哪些資料並排定優先順序的規則，以便建立客戶設定檔。</p>
                </div>
                <a href="create-merge-policies.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Union schemas overview">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="union-schemas-overview.md" title="聯合結構概觀" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/329940?format=jpeg&nocache=1740415066755" alt="聯合結構概觀"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="union-schemas-overview.md" target="_blank" rel="referrer" title="聯合結構概觀">聯集結構概觀</a>
                    </p>
                    <p class="is-size-6">即時客戶個人檔案可在客戶歷程的每個階段大規模實現跨管道個人化。 透過啟用結構和對應的資料集，可以為即時客戶設定檔啟用批次或串流資料。</p>
                </div>
                <a href="union-schemas-overview.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Create a computed attribute for the sum of purchases">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="create-a-computed-attribute-for-sum-of-purchases.md" title="建立購買總和的計算屬性" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3425899?format=jpeg&nocache=1740415066775" alt="建立購買總和的計算屬性"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="create-a-computed-attribute-for-sum-of-purchases.md" target="_blank" rel="referrer" title="建立購買總和的計算屬性">建立購買總和的計算屬性</a>
                    </p>
                    <p class="is-size-6">了解如何使用計算屬性來加總使用者在多個銷售管道中購買的金額。</p>
                </div>
                <a href="create-a-computed-attribute-for-sum-of-purchases.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 擷取和管理設定檔資料

<!-- CARDS
* bring-data-into-the-real-time-customer-profile.md
* delete-profiles.md
* update-a-specific-attribute-with-upsert.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Bring Data into Real-Time Customer Profile">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="bring-data-into-the-real-time-customer-profile.md" title="將資料帶入即時客戶個人檔案" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/27301?format=jpeg&nocache=1740415067018" alt="將資料帶入即時客戶個人檔案"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="bring-data-into-the-real-time-customer-profile.md" target="_blank" rel="referrer" title="將資料帶入即時客戶個人檔案">將資料帶入即時客戶個人檔案</a>
                    </p>
                    <p class="is-size-6">即時客戶個人檔案可在客戶歷程的每個階段大規模實現跨管道個人化。 透過啟用結構和對應的資料集，可以為即時客戶設定檔啟用批次或串流資料。</p>
                </div>
                <a href="bring-data-into-the-real-time-customer-profile.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Delete profiles">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="delete-profiles.md" title="刪除設定檔" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429807/?format=jpeg&nocache=1740415067005" alt="刪除設定檔"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="delete-profiles.md" target="_blank" rel="referrer" title="刪除設定檔">刪除輪廓</a>
                    </p>
                    <p class="is-size-6">瞭解如何使用即時客戶設定檔API從設定檔存放區中刪除資料。 使用設定檔API，您可以從設定檔存放區中移除資料，而不會影響資料湖或身分圖表。 疑難排解身分圖表問題，以及修正只影響少數設定檔的資料擷取中偶爾發生的錯誤時，這項功能會很有用。</p>
                </div>
                <a href="delete-profiles.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">觀看</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Update specific profile attributes using `upsert`">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="update-a-specific-attribute-with-upsert.md" title="使用「upsert」更新特定設定檔屬性" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3416133/?format=jpeg&nocache=1740415067029" alt="使用「upsert」更新特定設定檔屬性"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" title="使用「upsert」更新特定設定檔屬性">使用'upsert'更新特定設定檔屬性</a>
                    </p>
                    <p class="is-size-6">瞭解如何使用Adobe Experience Platform的「更新插入」功能更新設定檔的特定屬性。</p>
                </div>
                <a href="update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">觀看</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 帳戶輪廓

<!-- CARDS
* view-account-profiles.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="View account profiles">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="view-account-profiles.md" title="檢視帳戶設定檔" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/338251?format=jpeg&nocache=1740415067214" alt="檢視帳戶設定檔"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="view-account-profiles.md" target="_blank" rel="referrer" title="檢視帳戶設定檔">檢視帳戶設定檔</a>
                    </p>
                    <p class="is-size-6">瞭解如何在Real-Time CDP B2B edition中檢視帳戶設定檔。</p>
                </div>
                <a href="view-account-profiles.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->