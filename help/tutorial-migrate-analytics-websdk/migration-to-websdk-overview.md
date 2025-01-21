---
title: 使用標籤將Adobe Analytics移轉至網路SDK
description: 瞭解移轉至Web SDK期間您將採取的步驟，以及在此過程中需要作出的決策。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16755
exl-id: e578b669-42b4-46ae-b6e6-6688e5c5c772
source-git-commit: 7c0a6c769d56b3e56a5667d5aeff47b55ab6dc33
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 0%

---

# 使用標籤將Adobe Analytics移轉至網路SDK

瞭解使用Experience Platform標籤（先前稱為Launch）中的Analytics擴充功能，以及使用Tags中的Web SDK擴充功能，將Adobe Analytics實作移轉至Web SDK的步驟。 使用Tags中的Adobe Analytics擴充功能時，會在幕後使用「AppMeasurement.js」程式碼。 因此，您可以將此視為將AppMeasurement移轉至Web SDK的教學課程，但本教學課程完全以Tags為主，不包含移至JavaScript實作或從中移轉的部分(Tags UI中使用的JavaScript程式碼除外)。 若要移轉JavaScript實作，請參閱[檔案](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)。

## 您能從本教學課程中學到什麼

在我們開始移轉您的Analytics實作步驟之前，請務必確切瞭解您將要做什麼，這會變更/更新Analytics的&#x200B;_實作_。 在本教學課程結束時，當您進入您的報告且一切均相同時，可能會問自己：「現在，我為什麼要那麼做？」 有其他檔案可概述將Web SDK用於您的Analytics實作的好處，但少數檔案如下：

1. 支援第一方裝置識別碼
1. 更優異的效能
1. 隨著您開始使用Adobe Experience Platform應用程式（啟用新使用案例），為您的實施提供未來保障

請洽詢您的Adobe Analytics代表，進一步瞭解Web SDK如何協助您。 在繼續進行此教學課程時，我們將著重於&#x200B;_如何進行_&#x200B;移轉。

>[!IMPORTANT]
>
>請務必注意，您進行此實作移轉的主要原因之一，是準備使用Adobe Experience Platform應用程式，例如Customer Journey Analytics、Real-Time CDP或Journey Optimizer (如上#3所述)。 若為此目的使用您的網站資料，將會包含本教學課程中未包含的其他步驟，但本教學課程無疑是您進一步實施作業的先決條件。 因此，請完成本教學課程，然後您可以繼續執行必要步驟，將此相同的網站資料傳送至Experience Platform。

## 移轉方法

進行此移轉程式有許多種方式，但我們需要在此談談兩種方式：

**方法1：**&#x200B;將您現有的Tags屬性更新為Web SDK，建立新的資料元素，並對屬性中已存在的規則進行變更。

**方法2：**&#x200B;您也可以建立新屬性（複製現有屬性或建立全新屬性），然後使用Web SDK (而非Adobe Analytics擴充功能)設定新屬性。

**在此移轉教學課程中，我們將使用方法1。**&#x200B;如此一來，與屬性關聯的內嵌程式碼已內嵌於開發、測試和生產網站，因此不需要變更任何內嵌程式碼。 如果您決定使用方法2，別忘了從新屬性的&#x200B;**環境**&#x200B;區段中取得每個環境的新內嵌程式碼，並將其置於網站的head區段中。

>[!NOTE]
>
>雖然我們會在移轉期間在Tags中編輯現有的屬性，但還是建議您謹慎操作。 因此，強烈建議您在開始移轉前，先製作目前屬性的副本。 如此一來，您隨時都可以進入復本，檢視變更前的狀態、從中提取程式碼等。
>小心就是好，以防萬一。 請繼續並製作屬性的副本。 我會在這裡等到您回來。

## 將Analytics實作移轉至Web SDK的步驟

當您逐步進行這些步驟時，請務必瞭解幾項注意事項：

1. 首先，您不一定需要所有這些步驟。 例如，有一堂關於移轉自訂程式碼的課程。 如果您的Tags實作不使用自訂程式碼（包括使用外掛程式），則不需要進行本課程。 我們嘗試加入大部分人所需的課程，因此請至少閱讀這些課程，以瞭解在移轉期間是否需要調整您的網站。
1. 此外，我們完全無法建立移轉教學課程，涵蓋所有人正在使用的全部使用案例。 如前一項所述，我們嘗試納入大部分人需要的課程，這將涵蓋大部分的主要使用案例。 不過，本教學課程中無疑會包含未涵蓋的使用案例。 在此情況下，請檢視包含的課程是否可讓您清楚瞭解應如何針對使用案例進行移轉。 您也可以向[Experience League社群中的同業要求資料收集](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/ct-p/adobe-launch-community)。

移轉程式包含下列重要步驟：

1. 建立移轉驗證報表套裝。
1. 建立及設定資料串流。
1. 在標籤(前身為Adobe Launch)中新增及設定網頁SDK擴充功能。
1. 建立新資料元素以透過網頁SDK傳送資料。
1. 移轉預設頁面載入規則以使用Web SDK資料元素和動作。
1. 移轉規則或外掛程式中的自訂程式碼。
1. Publish會變更您的實作。
1. 瞭解如何偵錯和驗證變更，以及驗證您的預設頁面載入規則及與其關聯的變數。 當您進行變更時，這項驗證應該會在整個移轉過程中繼續。
1. 移轉其他頁面載入規則。
1. 移轉自訂連結規則。
1. 完整驗證後，請移除Analytics擴充功能的參考，並移除擴充功能本身。
1. 完成所有變更後，將程式庫推送至測試環境，然後再推送至生產環境。
1. 完成所有工作後，請再次測試。 此為必要操作，因為您已移除對舊版Analytics程式碼的參照，以進行變更，而且您想要確定一切仍正常運作。


### DOUG注意事項 — 測試教學課程後，請在此處放置社群貼文的連結，客戶可在其中詢問關於教學課程和移轉至Web SDK的問題。
