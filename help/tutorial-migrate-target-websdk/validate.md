---
title: 使用Web SDK驗證Target實作 | 將Target從at.js 2.x移轉至Web SDK
description: 瞭解如何使用Adobe Experience Platform Web SDK驗證活動及偵錯Adobe Target實作。
exl-id: 09b4ebeb-fae9-470d-8ea9-f6e3c7d7da5e
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# 驗證平台Web SDK實作

將Target實作從at.js移轉至Platform Web SDK後，請務必先驗證一切都正常運作，然後再將任何變更發佈至生產網站。 Adobe建議進行下列事項，本頁將詳細介紹這些事項：

* 執行技術驗證，以確保基本實作和Platform Web SDK請求與回應看起來正確無誤
* 確保Target活動已正確傳送和呈現
* 檢查報表是否正常運作
* 重新造訪對象和個人資料指令碼，以確保它們與Platform Web SDK相容
* 確保與Adobe或協力廠商應用程式的整合可正常運作

每個Target實作會因使用的網站架構和功能而異。 您可使用下清單格作為起點，並新增實作專用的任何專案。 本教學課程的[偵錯頁面](debugging.md)顯示您可以用來協助進行此驗證的工具。

## 技術驗證

| 驗證專案 | 附註 |
|---|---|
| 頁面上不再有at.js預先隱藏的程式碼片段 | Platform Web SDK不會自動移除識別碼為`at-body-style`的樣式。 將此舊程式碼片段留在頁面上會導致隱藏內容，直到達到程式碼片段逾時為止。 |
| 頁面上不再有at.js資料庫 | 檢查瀏覽器的開發人員工具主控台中是否沒有「adobe.target」物件。 同時包含Platform Web SDK和at.js會導致非預期的轉譯行為 |
| 預期引數位於`sendEvent`請求的XDM和資料物件中 | |
| 如果使用頁面請求填入目錄，Recommendations目錄會如預期更新 | |
| 設定檔引數已成功傳遞至Target | 在Debugger中檢視Edge追蹤 |
| 資料流對應程式中對應至XDM的引數會正確傳遞至Target | 使用Debugger的Edge追蹤功能和/或Assurance進行驗證 |
| 目標內容在適用的`sendEvent`回應中傳回 | 當`renderDecisions`選項設為`true`或請求範圍時，預期會發生此情況，且使用者符合特定Target活動的資格 |
| VEC型活動轉譯之後，`decisioning.propositionDisplay`事件會引發 | 自動及隨選呈現的活動應具有個別的事件呼叫 |
| 表單式活動轉譯之後，`decisioning.propositionDisplay`事件會引發 | 僅適用於特定實施。 需要自訂程式碼才能執行此呼叫。 |
| 將選件套用至SPA檢視變更時，會引發`decisioning.propositionDisplay`事件 | 僅適用於SPA實作 |
| 當SPA元件重新呈現指定檢視時，`decisioning.propositionDisplay`事件不會引發 | 僅適用於SPA實作 |
| 在活動轉換之後會引發`decisioning.propsitionInteract`事件 | 從at.js `trackEvent`或`sendNotifications`移轉的「已點選元素」和自訂轉換應具有個別的事件呼叫 |
| 回應Token在`sendEvent`回應中傳回，並具有預期值 | 回應Token應可透過Web SDK正常運作 |
| 使用Web SDK和at.js的網頁間ECID是一致的 | 適用於逐頁移轉。 重新導向選件不適用於這些型別的移轉 |


## 活動傳送和呈現

| 驗證專案 | 附註 |
|---|---|
| VEC型活動在頁面載入時正確轉譯 | 最好驗證自訂程式碼修改和基本修改，例如重新排列元素或取代文字 |
| 在SPA檢視變更上正確轉譯VEC型活動 | 僅適用於SPA實作 |
| 表單式活動可正確轉譯 | 僅適用於特定實施。 呈現表單式活動需要類似於at.js的自訂程式碼。 |
| 使用重新導向的活動可正常運作 | 如果來源頁面和目的地頁面都使用Platform Web SDK，則支援重新導向。 不支援從at.js頁面或相反方向將Target重新導向至Platform Web SDK頁面。 |
| 使用遠端選件的活動可正常運作 | 不常見的情況，請檢查遠端選件的Target選件詳細目錄 |
| 已適當緩解忽隱忽現情形 | 處理忽隱忽現問題是選用的，但請確保您制定的任何緩解策略都能如預期般運作，以獲得最佳頁面效能和使用者體驗 |
| QA連結如預期般運作 | 如果無法運作，請確認web.webPageDetails.URL與瀏覽器中的URL完全相符 |
| 您所有常用的選件型別都會如預期般轉譯 |  |

## 報告

| 驗證專案 | 附註 |
|---|---|
| 訪客會歸因於VEC型活動 | 最好驗證報告是否如預期般對頁面載入修改和SPA檢視修改運作 |
| 訪客會歸因於表單式活動 | 根據所使用的演算方法，您的實作可能需要自訂程式碼才能執行`decisioning.propositionDisplay`事件 |
| 正確擷取標準轉換目標 | 套用至Target或Analytics作為報表來源 |
| 正確擷取訂單轉換和詳細資訊 | 檢查稽核報告 |
| 正確擷取點選追蹤轉換 |  |
| 正確擷取自訂轉換目標 | 例如，從at.js `trackEvent`或`sendNotifications`移轉的轉換目標常用於「已檢視mbox」目標 |

## 對象和個人資料指令碼

| 驗證專案 | 附註 |
|---|---|
| 即時活動中使用的對象與Platform Web SDK相容 | 必須更新使用「自訂」（mbox引數）元件的對象，以包含XDM屬性 |
| 所有設定檔指令碼都與Platform Web SDK相容 | 必須更新任何使用mbox引數的設定檔指令碼，以包含XDM屬性 |
| 針對Target對象傳回的活動 | 建議您最好對您修改的對象執行端對端驗證，使其與Platform Web SDK相容 |
| 個人資料指令碼會如預期般評估 | 在Debugger中檢視Edge追蹤 |

## 與Adobe應用程式整合

| 驗證專案 | 附註 |
|---|---|
| 活動會為Experience Cloud對象傳回 | 例如，從Adobe Analytics發佈的區段 |
| 活動會為Experience Platform對象傳回 | 僅適用於擁有RTCDP等Experience Platform型應用程式授權的情況 |
| 活動會為Audience Manager對象傳回 | 例如，以造訪特定頁面為基礎的區段 |
| Target活動資料會顯示在Analysis Workspace中 | 套用至使用Adobe Analytics作為報表來源的活動 |

## 與協力廠商應用程式整合

| 驗證專案 | 附註 |
|---|---|
| 回應Token資料已正確傳遞至協力廠商應用程式 | 整合方法可能有所不同，但常見的方法為使用Target回應Token將活動和體驗資訊傳遞至Google Analytics等其他分析工具 |
| 來自協力廠商的資訊會以XDM或設定檔資料形式傳遞 | 所有來自協力廠商的相關資訊都應該在`sendEvent`個Target呼叫中傳遞 |

執行上述驗證步驟後，您可以放心，Platform Web SDK實作已準備好投入生產。

接下來，瞭解如何[使用Platform Web SDK](debugging.md)對Target實作進行疑難排解。

>[!NOTE]
>
>我們致力協助您成功將Target從at.js移轉至Web SDK。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
