---
title: 使用Web SDK驗證Target實作 |將Target從at.js 2.x移轉至Web SDK
description: 了解如何使用Adobe Experience Platform Web SDK驗證活動及對Adobe Target實作除錯。
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# 驗證Platform Web SDK實作

將Target實作從at.js移轉至Platform Web SDK後，請務必先驗證一切正常運作，再將任何變更發佈至生產網站。 Adobe建議執行下列操作，本頁將詳細說明：

* 執行技術驗證，確保基本實作和Platform Web SDK要求與回應正確無誤
* 確保Target活動已正確傳送和呈現
* 檢查報表是否正常運作
* 重新造訪對象和設定檔指令碼，確保它們與Platform Web SDK相容
* 確保與Adobe或協力廠商應用程式的整合正常運作

每個Target實作都會根據所使用的網站架構和功能而有所不同。 您可以使用下表作為起點，並新增實作特有的任何項目。 此 [「調試」頁](debugging.md) 在本教學課程中，您可使用工具來協助進行此驗證。

## 技術驗證

| 驗證項目 | 附註 |
|---|---|
| 頁面上不再有at.js預先隱藏程式碼片段 | Platform Web SDK不會自動移除具有ID的樣式 `at-body-style`. 將此舊程式碼片段保留在頁面上會導致隱藏內容，直到達到程式碼片段逾時為止。 |
| 頁面上不再有at.js資料庫 | 檢查瀏覽器的開發人員工具主控台中沒有「adobe.target」物件。 同時包含Platform Web SDK和at.js會導致非預期的轉譯行為 |
| 預期的參數位於的XDM和資料物件中 `sendEvent` 請求 |  |
| 如果使用頁面要求填入目錄，Recommendations目錄會如預期更新 |  |
| 設定檔參數已成功傳遞至Target | 在Debugger中檢視邊緣追蹤 |
| 資料流映射器中對應至XDM的參數會正確傳遞至Target | 使用Debugger的Edge Trace功能和/或Assurance進行驗證 |
| 適用中的目標內容傳回 `sendEvent` 回應 | 預期時間 `renderDecisions` 選項設為 `true` 請求或範圍，且用戶符合特定Target活動的資格 |
| A `decisioning.propositionDisplay` 事件在VEC型活動呈現後觸發 | 自動呈現和隨需呈現的活動預期會有個別的事件呼叫 |
| A `decisioning.propositionDisplay` 表單式活動呈現後會引發事件 | 僅適用於特定實施。 需要自訂程式碼才能執行此呼叫。 |
| A `decisioning.propositionDisplay` 事件會在SPA檢視變更上套用選件時觸發 | 僅適用於SPA實施 |
| A `decisioning.propositionDisplay` SPA元件針對指定檢視重新轉譯時，不會觸發事件 | 僅適用於SPA實施 |
| A `decisioning.propsitionInteract` 事件在活動轉換後引發 | 「點擊元素」和自訂轉換是從at.js移轉 `trackEvent` 或 `sendNotifications` 預期會有個別的事件呼叫 |
| 回應Token會在 `sendEvent` response和具有預期值 | 回應Token應可與Web SDK一起正常運作 |
| ECID與Web SDK和at.js的各頁面一致 | 適用於逐頁移轉。 在這些類型的移轉中，重新導向選件不會正常運作 |


## 活動傳送和呈現

| 驗證項目 | 附註 |
|---|---|
| 頁面載入時可正確呈現VEC型活動 | 最好同時驗證自訂程式碼修改和基本修改，例如重新排列元素或取代文字 |
| VEC型活動會在SPA檢視變更時正確呈現 | 僅適用於SPA實施 |
| 表單式活動可正確呈現 | 僅適用於特定實施。 呈現表單式活動需要類似at.js的自訂程式碼。 |
| 使用重新導向的活動可正常運作 | 如果來源和目的地頁面都使用Platform Web SDK，則可支援重新導向。 不支援從at.js頁面重新導向至Platform Web SDK頁面或相反的方式。 |
| 使用遠端選件的活動可正常運作 | 不常見，請檢查Target選件詳細目錄以取得遠端選件 |
| 適當緩解忽隱忽現 | 忽隱忽現處理是選用的，但請確定您有的任何緩解策略皆如預期般運作，以獲得最佳頁面效能和使用者體驗 |
| QA連結如預期般運作 | 如果無法運作，請確認web.webPageDetails.URL完全符合瀏覽器中的URL |
| 所有常用的選件類型皆如預期般呈現 |  |

## 報告

| 驗證項目 | 附註 |
|---|---|
| 訪客歸因於VEC型活動 | 最好驗證報表對於頁面載入修改和SPA檢視修改都如預期般運作 |
| 訪客會歸因於表單式活動 | 視使用的演算方法而定，您的實作可能需要自訂程式碼才能執行 `decisioning.propositionDisplay` 事件 |
| 正確擷取標準轉換目標 | 套用至Target或Analytics作為報表來源 |
| 正確擷取訂單轉換和詳細資料 | 檢查「審核」報告 |
| 已正確擷取點擊追蹤轉換 |  |
| 已正確擷取自訂轉換目標 | 例如，轉換目標是從at.js移轉 `trackEvent` 或 `sendNotifications` 通常與「已檢視的mbox」目標搭配使用 |

## 對象和設定檔指令碼

| 驗證項目 | 附註 |
|---|---|
| 即時活動中使用的對象與Platform Web SDK相容 | 必須更新使用「自訂」（mbox參數）元件的對象，以包含XDM屬性 |
| 所有設定檔指令碼都與Platform Web SDK相容 | 必須更新使用mbox參數的任何設定檔指令碼，以包含XDM屬性 |
| 目標對象的活動傳回 | 最好對您修改的對象執行端對端驗證，以與Platform Web SDK相容 |
| 設定檔指令碼會如預期般評估 | 在Debugger中檢視邊緣追蹤 |

## 與Adobe應用程式整合

| 驗證項目 | 附註 |
|---|---|
| Experience Cloud對象的活動傳回 | 例如，從Adobe Analytics發佈的區段 |
| Experience Platform對象的活動傳回 | 只有在您擁有基於Experience Platform的應用程式（如RTCDP）的許可證時才適用 |
| Audience Manager對象的活動傳回 | 例如，以瀏覽特定頁面為基礎的區段 |
| Target活動資料顯示於Analysis Workspace | 套用至以Adobe Analytics作為報表來源的活動 |

## 與協力廠商應用程式的整合

| 驗證項目 | 附註 |
|---|---|
| 回應Token資料已正確傳遞至協力廠商應用程式 | 整合方法可能會有所不同，但常見的方法是使用Target回應Token，將活動和體驗資訊傳遞至其他分析工具(例如Google Analytics) |
| 來自協力廠商的資訊會以XDM或設定檔資料的形式傳遞 | 所有來自第三方的相關資訊均應傳入 `sendEvent` 對Target的呼叫 |

執行上述驗證步驟後，您可以確信Platform Web SDK實作已準備好投入生產。

接下來，學習如何 [使用Platform Web SDK疑難排解Target實作](debugging.md).

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).