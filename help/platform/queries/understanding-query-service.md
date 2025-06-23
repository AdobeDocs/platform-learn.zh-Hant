---
title: 查詢服務與資料Distiller概觀
description: Adobe Experience Platform Query Service可讓使用者利用SQL探索、驗證及轉換儲存在Data Lake中的客戶體驗資料，並透過Data Distiller附加元件提供增強功能，例如資料輸出和排程。 此影片提供核心功能概觀，可協助使用者瞭解如何跨各種平台應用程式利用查詢服務。
feature: Queries
role: Data Engineer, Developer
level: Beginner
jira: KT-3139
thumbnail: 29795.jpg
exl-id: 988bc316-9eec-4dca-8049-95c2d613379d
source-git-commit: 8092c5f120a51b35f068261b70131ef303b4c51d
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 13%

---

# 查詢服務與資料Distiller概觀

Adobe Experience Platform Query Service可讓使用者利用SQL探索、驗證及轉換儲存在Data Lake中的客戶體驗資料，並透過Data Distiller附加元件提供增強功能，例如資料輸出和排程。 此影片提供核心功能概觀，可協助使用者瞭解如何跨各種平台應用程式利用查詢服務。 如需詳細資訊，請瀏覽[查詢服務檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/query/home)。

>[!VIDEO](https://video.tv.adobe.com/v/29795?learn=on&enablevpops)

## 基本用法

<!-- CARDS
* query-service-ui.md
* query-service-api.md
* adobe-defined-functions.md
* run-queries.md
* understanding-data-usage-patterns-with-query-service.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Query Service UI">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="query-service-ui.md" title="查詢服務UI" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333403?format=jpeg&nocache=1740415310696" alt="查詢服務UI"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="query-service-ui.md" target="_blank" rel="referrer" title="查詢服務UI">查詢服務UI</a>
                    </p>
                    <p class="is-size-6">了解如何在 Adobe Experience Platform 查詢服務中撰寫和執行查詢、檢視先前執行的查詢，以及存取由您 IMS 組織內其他使用者儲存的查詢。</p>
                </div>
                <a href="query-service-ui.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Query Service API">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="query-service-api.md" title="查詢服務API" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333700?format=jpeg&nocache=1740415310716" alt="查詢服務API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="query-service-api.md" target="_blank" rel="referrer" title="查詢服務API">查詢服務API</a>
                    </p>
                    <p class="is-size-6">瞭解如何使用Adobe Experience Platform查詢服務API來撰寫和執行查詢、建立排程查詢及建立查詢範本。</p>
                </div>
                <a href="query-service-api.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Adobe Defined Functions">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="adobe-defined-functions.md" title="Adobe定義的函式" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333701?format=jpeg&nocache=1740415310668" alt="Adobe定義的函式"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="adobe-defined-functions.md" target="_blank" rel="referrer" title="Adobe定義的函式">Adobe定義的函式</a>
                    </p>
                    <p class="is-size-6">瞭解如何在Adobe Experience Platform查詢服務中使用Adobe定義的函式，以對Experience Event資料執行常見的業務相關工作。</p>
                </div>
                <a href="adobe-defined-functions.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Run Queries with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="run-queries.md" title="使用查詢服務執行查詢" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29796?format=jpeg&nocache=1740415310683" alt="使用查詢服務執行查詢"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="run-queries.md" target="_blank" rel="referrer" title="使用查詢服務執行查詢">使用查詢服務執行查詢</a>
                    </p>
                    <p class="is-size-6">此影片說明如何在Adobe Experience Platform介面和PSQL使用者端中執行查詢。 此外，在XDM物件中使用個別屬性、使用Adobe定義的函式，以及使用CREATE TABLE AS SELECT (CTAS)進行示範。</p>
                </div>
                <a href="run-queries.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Understanding Data Usage Patterns with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="understanding-data-usage-patterns-with-query-service.md" title="瞭解透過查詢服務的資料使用模式" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29811?format=jpeg&nocache=1740415310706" alt="瞭解透過查詢服務的資料使用模式"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" title="瞭解透過查詢服務的資料使用模式">瞭解查詢服務的資料使用模式</a>
                    </p>
                    <p class="is-size-6">此影片分享在查詢編輯器介面、PSQL使用者端、商業智慧(BI)解決方案和HTTP API中執行查詢的秘訣和最佳實務。</p>
                </div>
                <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 資料驗證和探索

<!-- CARDS
* explore-data.md
* validate-data-in-the-datalake.md
* 
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Explore data">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="explore-data.md" title="探索資料" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333415?format=jpeg&nocache=1740415312087" alt="探索資料"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="explore-data.md" target="_blank" rel="referrer" title="探索資料">探索資料</a>
                    </p>
                    <p class="is-size-6">了解如何使用 SQL 函式驗證所擷取的資料、預覽資料，以及探索資料的統計和分析屬性。</p>
                </div>
                <a href="explore-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Validate data in the datalake with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="validate-data-in-the-datalake.md" title="使用查詢服務驗證Datalake中的資料" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3445688?format=jpeg&nocache=1740415312076&captions=chi_hant" alt="使用查詢服務驗證Datalake中的資料"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="validate-data-in-the-datalake.md" target="_blank" rel="referrer" title="使用查詢服務驗證Datalake中的資料">使用查詢服務驗證datalake中的資料</a>
                    </p>
                    <p class="is-size-6">瞭解如何使用Adobe Experience Platform的查詢服務驗證資料是否已成功擷取到Datalake。</p>
                </div>
                <a href="validate-data-in-the-datalake.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 使用Data Distiller進行資料轉換

<!-- CARDS
* 
* prepare-data.md
* 
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Prepare data">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="prepare-data.md" title="準備資料" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333699?format=jpeg&nocache=1740415313086" alt="準備資料"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="prepare-data.md" target="_blank" rel="referrer" title="準備資料">準備資料</a>
                    </p>
                    <p class="is-size-6">瞭解如何清除、準備和結合多個資料集的資料，並使用CTAS (Create Table AS)和Spark SQL函式建立新資料集，以利製作報表和控制面板。</p>
                </div>
                <a href="prepare-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 使用案例

<!-- CARDS
* understanding-data-usage-patterns-with-query-service.md
* psql-client-tableau.md
* analyze-and-visualize.md
* recharge-your-customer-data.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Understanding Data Usage Patterns with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="understanding-data-usage-patterns-with-query-service.md" title="瞭解透過查詢服務的資料使用模式" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29811?format=jpeg&nocache=1740415313190" alt="瞭解透過查詢服務的資料使用模式"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" title="瞭解透過查詢服務的資料使用模式">瞭解查詢服務的資料使用模式</a>
                    </p>
                    <p class="is-size-6">此影片分享在查詢編輯器介面、PSQL使用者端、商業智慧(BI)解決方案和HTTP API中執行查詢的秘訣和最佳實務。</p>
                </div>
                <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Connect Tableau to Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="psql-client-tableau.md" title="將Tableau連線至查詢服務" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333702?format=jpeg&nocache=1740415313229" alt="將Tableau連線至查詢服務"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="psql-client-tableau.md" target="_blank" rel="referrer" title="將Tableau連線至查詢服務">將 Tableau 連接至查詢服務</a>
                    </p>
                    <p class="is-size-6">瞭解如何從各種支援PostgreSQL通訊協定的案頭使用者端應用程式連線到查詢服務，以及如何使用PostgreSQL工具和驅動程式來連線及寫入查詢。</p>
                </div>
                <a href="psql-client-tableau.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Analyze and visualize omni-channel insights in Tableau using Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="analyze-and-visualize.md" title="在Tableau中使用查詢服務來分析及視覺化全通路見解" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/342115?format=jpeg&nocache=1740415313204" alt="在Tableau中使用查詢服務來分析及視覺化全通路見解"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="analyze-and-visualize.md" target="_blank" rel="referrer" title="在Tableau中使用查詢服務來分析及視覺化全通路見解">在 Tableau 中使用查詢服務來分析及視覺化全通路見解</a>
                    </p>
                    <p class="is-size-6">了解如何在流失分析範例中搭配使用 Adobe Experience Platform 的查詢服務與外部資料視覺化工具。</p>
                </div>
                <a href="analyze-and-visualize.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Recharge your customer data to deliver electrifying experiences">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="recharge-your-customer-data.md" title="為您的客戶資料重新充電，提供絕佳的體驗" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3454957?format=jpeg&nocache=1740415313218&captions=chi_hant" alt="為您的客戶資料重新充電，提供絕佳的體驗"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="recharge-your-customer-data.md" target="_blank" rel="referrer" title="為您的客戶資料重新充電，提供絕佳的體驗">為您的客戶資料重新充電，以提供令人振奮的體驗</a>
                    </p>
                    <p class="is-size-6">瞭解如何減輕低品質資料的影響、縮短實現價值的時間，並透過在許多使用案例中使用相同的資料來倍增ROI。</p>
                </div>
                <a href="recharge-your-customer-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">進一步瞭解</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->