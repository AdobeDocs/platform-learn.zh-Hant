---
title: 刪除Adobe Analytics擴充功能專案
description: 偵錯和驗證完成後，請移除Adobe Analytics擴充功能專案的所有參考，並移除擴充功能本身。
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16766
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# 刪除Adobe Analytics擴充功能專案

偵錯和驗證完成後，請移除Adobe Analytics擴充功能專案的所有參考，並移除擴充功能本身。

## 概觀

在您滿意屬性中的所有內容皆已移轉至Web SDK，且已完成（在開發環境中）偵錯和驗證後，您就可以移除對Adobe Analytics擴充功能的參考了。 移除這些專案的速度，以及執行測試時的測試次數由您決定。 如果您想要更小心地處理參照，請慢慢移除參照，並在每次移除之間測試。 如果您確信一切正常運作且已正確移轉，您可以「撕掉創可貼」並移除所有專案。 當然，我們仍建議在練習結束時進行測試。

## 從規則中移除舊動作

同樣地，我們假設您已測試所有內容，而且運作正常。 此時，您可以逐一進入規則，並移除屬於Adobe Analytics擴充功能的動作。

1. 開啟您的其中一個規則，例如預設頁面載入規則。
1. 完成此規則的移轉後，您可能會執行4個（或更多）動作。

   ![所有4個動作](assets/all-four-actions.jpg)

1. 您可以看到前兩個標籤上有「Adobe Analytics」識別碼。 這些是我們要刪除的動作。
1. 將游標移至第一個變數上方，例如「Adobe Analytics — 設定變數」動作，就會顯示X以允許刪除。 按一下X並看到動作消失。 移除規則中的所有Adobe Analytics動作，此案例中為「設定變數」動作和「傳送信標」動作。
1. 這將只保留Web SDK動作

   ![僅限Web SDK動作](assets/websdk-actions-only.jpg)

1. 儲存至程式庫
1. 建置程式庫並測試您的網站，確保沒有新錯誤，且一切正常運作
1. 對您的其他規則重複此動作，在開發程式庫中建置，並在每次移除之間測試（或視您熟悉的頻率而定）。 您只需在Debugger中測試，或也可檢視移轉報表套裝中的報表（視您的舒適程度而定）。

## 移除擴充功能

現在您已移除Adobe Analytics擴充功能的參照，您可以移除（或停用）擴充功能，以及使用該擴充功能或相依於其的任何其他擴充功能。 我個人喜歡謹慎的方法，因此「停用」是我的選擇，而不是解除安裝（至少在一開始是這樣）。

1. 從UI的左側邊欄選取&#x200B;**擴充功能**。
1. 確定已選取&#x200B;**已安裝**&#x200B;標籤。
1. 選取Adobe Analytics擴充功能。
1. 在右邊欄中，選擇停用擴充功能(或按一下三個點，然後解除安裝（如果願意）)。

   ![停用Analytics擴充功能](assets/disable-analytics-extension.jpg)

1. 對Experience CloudID服務擴充功能執行相同操作，因為您將不再需要該擴充功能。 網頁SDK擴充功能可處理ID，因此您不需要額外的擴充功能。
1. 對與Adobe Analytics擴充功能相關聯的任何其他擴充功能執行相同操作，但必須先完成必要的移轉變更。
1. 建置對開發環境的變更。

