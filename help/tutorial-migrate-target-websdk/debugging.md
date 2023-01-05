---
title: 除錯 |將Target從at.js 2.x移轉至Web SDK
description: 了解如何使用Adobe Target Web SDK對Adobe Experience Platform實作進行除錯。 主題包括除錯選項、瀏覽器擴充功能，以及at.js和Platform Web SDK之間的差異。
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 3%

---

# 使用Platform Web SDK除錯Target

驗證Target活動並偵錯Web SDK，以疑難排解實作、內容傳送或對象資格問題。 移轉指南的本頁說明使用at.js除錯與Platform Web SDK之間的差異。

下表概述測試和偵錯方法的功能與支援。

| 功能或工具 | at.js支援 | 平台網頁SDK支援 |
| --- | --- | --- |
| 活動QA URL | 是 | 是 |
| `mboxDisable` URL 參數 | 是 | 請參閱以下資訊，以 [停用Target功能](#disable-target-functionality) |
| `mboxDebug` URL 參數 | 是 | 使用 `alloy_debug` 類似偵錯資訊的參數 |
| `mboxTrace` URL 參數 | 是 | 使用Experience Platform偵錯工具瀏覽器擴充功能 |
| Adobe Experience Platform Debugger擴充功能 | 是 | 是 |
| `alloy_debug` URL 參數 | 不適用 | 是 |
| Adobe Experience Platform保障 | 不適用 | 是 |

## Adobe Experience Platform Debugger瀏覽器擴充功能

適用於Chrome與Firefox的Adobe Experience Platform Debugger擴充功能會檢查您的網頁，協助您驗證Adobe Experience Cloud實作。

您可以在任何網頁上執行Platform Debugger，且擴充功能可存取公開資料。 若要使用擴充功能存取非公用資料（例如Target追蹤資訊），您必須透過驗證以Experience Cloud **[!UICONTROL 登入]** 連結。

### 取得並安裝Adobe Experience Platform Debugger

Adobe Experience Platform Debugger可在Google Chrome或Mozilla Firefox瀏覽器中安裝。 請依照下列適當連結，在您偏好的瀏覽器上安裝擴充功能：

- [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
- [Firefox](https://addons.mozilla.org/zh-TW/firefox/addon/adobe-experience-platform-dbg/)

安裝Chrome擴充功能或Firefox附加元件後，圖示(![](assets/start-icon.jpg))新增至擴充功能列。 選取此圖示以開啟擴充功能。

如需 [Adobe Experience Platform Debugger擴充功能](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html) 以及如何對所有AdobeWeb應用程式進行調試。

## 使用QA URL預覽Target活動

at.js和Platform Web SDK都可讓您使用Target QA URL預覽Target活動，且兩種實作方法都支援相同的QA功能。

指示at.js或Platform Web SDK將特定Cookie寫入您名為的瀏覽器，以便Target QA URL運作 `at_qa_mode`. 此Cookie可用來強制限定特定活動和體驗。

>[!CAUTION]
>
>Platform Web SDK 2.13.0或更新版本支援Target QA模式功能。 已根據 `xdm.web.webPageDetails.URL` 傳入的值 `sendEvent` 呼叫。 對此值所做的任何修改（例如小寫所有字元）都可能會使Target QA模式無法正常運作。

如需詳細資訊，請參閱專屬指南 [Target活動QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).

## 除錯Target實作

下表概述at.js與Platform Web SDK除錯策略之間的差異：

| at.js功能 | Platform Web SDK的對等方法 |
| --- | --- |
| **Mbox停用**  — 停用Target從擷取和轉譯，以檢查頁面是否在沒有Target互動的情況下中斷<br><br>載入含有URL參數的頁面： `mboxDisable=true` | 沒有直接等同的。 您可以使用瀏覽器的開發人員工具來封鎖所有Platform Web SDK請求。 |
| **Mbox Debug**  — 在瀏覽器主控台中記錄每個at.js動作，以協助疑難排解轉譯問題<br><br>載入含有URL參數的頁面： `mboxDebug=true` | **Alloy Debug**  — 記錄SDK的詳細動作，包括但不限於Target個人化動作。<br><br>載入含有URL參數的頁面： `alloy_debug=true`  <br /><br />或執行 `alloy("setDebug", { "enabled": true });` 在開發人員主控台中 |
| **目標追蹤** - Target UI中產生mbox追蹤代號後，決策程式中可使用包含詳細資訊的追蹤物件 `window.___target_trace` 物件。<br><br>載入含有URL參數的頁面： `mboxTrace=window&authorization={TOKEN}` | 使用Adobe Experience Platform Debugger擴充功能或平台保證。 |

>[!NOTE]
>
>以上所列的所有at.js除錯功能均可搭配Adobe Experience Platform Debugger中的增強功能使用。

### 停用Target功能

Platform Web SDK目前沒有可選擇性抑制Target回應的功能。 不過，您也可以使用瀏覽器的開發人員工具、各種瀏覽器擴充功能或協力廠商應用程式來隱藏Platform Web SDK請求。 例如，若要使用Google Chrome來封鎖Platform Web SDK:

1. 按一下右鍵頁面上的任意位置，然後選取 **Inspect**
1. 選取 **網路** 標籤
1. 依字串篩選 `//ee//` 僅檢視Platform Web SDK呼叫
1. 重新載入頁面
1. 以滑鼠右鍵按一下其中一個篩選的網路請求，然後選取 **封鎖要求網域**
1. 重新載入頁面，並注意網路要求已遭封鎖
1. 完成調試後，按一下右鍵阻止的網路請求並選擇 **解除阻止**，或關閉「開發人員工具」面板

### 檢視除錯記錄

針對at.js使用 `mboxDebug=true` URL參數會顯示每個Target請求、回應以及嘗試將內容轉譯至頁面的詳細資訊。 Platform Web SDK使用的偵錯記錄類似 `alloy_debug=true` URL參數。

| 記錄的資訊 | at.js (`mboxDebug=true`) | 平台Web SDK(`alloy_debug=true`) |
| --- | --- | --- |
| 篩選的記錄前置詞 | `AT:` | `[alloy]` |
| 頁面載入請求詳細資料 | 是 | 是 |
| mbox或範圍請求詳細資料 | 是 | 是 |
| 請求狀態 | 是 | 是 |
| 回應詳細資訊 | 是 | 是 |
| 呈現狀態 | 成功與錯誤 | 僅錯誤 |
| 呈現詳細資訊 | 是 | 是 |

>[!NOTE]
>
>at.js和Platform Web SDK的除錯記錄檔提供類似層級的詳細資料，但值得注意的例外情況是，Web SDK只會通知因選取器無效而發生的轉譯錯誤。 除錯記錄目前無法確認呈現成功。

### 檢視Target追蹤

Target追蹤提供活動資格和訪客的Target設定檔的詳細資訊。 由於Target追蹤包含非公開的資訊，因此檢視這些追蹤需要授權Token，或在Adobe Experience Platform Debugger瀏覽器擴充功能視窗中進行驗證。

| 目標追蹤方法 | at.js | 平台Web SDK |
| --- | --- | --- |
| `mboxTrace` URL 參數 | 是 | 無 |
| Adobe Experience Platform Debugger瀏覽器擴充功能 | 是 | 有 |
| Adobe Experience Platform保障 | 無 | 是 |


若要使用Adobe Experience Platform Debugger檢視Platform Web SDK Target追蹤，請執行下列動作：

1. 導覽至您網站上已使用Platform Web SDK實作Target的頁面
1. 選取圖示(![](assets/start-icon.jpg))
1. 選取 **[!UICONTROL 登入]** 連結
1. 使用Adobe Experience Cloud登入進行驗證
1. 選取 **[!UICONTROL 記錄檔]** 標籤
1. 選取 **[!UICONTROL Edge]** 標籤
1. （可選）為您的偵錯工作階段命名，然後按一下 **[!UICONTROL Connect]** 按鈕
1. 重新載入頁面，記錄檔應填入邊緣網路互動的詳細資訊
1. 著重於說明中以「目標追蹤」開頭的記錄項目，並選取 **[!UICONTROL 檢視]** 查看Target追蹤詳細資訊

![如何使用Adobe Experience Platform Debugger檢視Target追蹤](assets/target-trace-debugger.png)

選取後 **[!UICONTROL 檢視]**，則會出現覆蓋圖，讓您查看與請求相關的下列資訊：

- 相符的活動
- 不相符的活動
- 請求詳細資訊
- 配置檔案快照

請參閱專屬指南，了解 [偵錯Target內容傳送](https://experienceleague.adobe.com/docs/target/using/activities/troubleshoot-activities/content-trouble.html) 以取得Target追蹤的詳細資訊。

### 疑難排解並保證

您可在Adobe Experience Platform Debugger瀏覽器擴充功能和Assurance應用程式（舊稱為Project Griffon）中檢視Target追蹤資訊。 要在Assurance中查看Target跟蹤，請執行以下操作：

1. 開啟Adobe Experience Platform Debugger瀏覽器擴充功能，並依照上述說明連線遠端除錯工作階段
1. 在偵錯記錄上方選取含有您工作階段名稱的連結
1. Platform Assurance會載入並顯示為您的實作所需資料流中設定之所有Adobe應用程式的詳細記錄
1. 篩選記錄檔 `adobe.target`
1. 選擇類型為的日誌條目 `com.adobe.target.trace`
1. 展開裝載的詳細資訊，並在下方檢視資訊 `context > targetTrace`

![如何檢視Target追蹤並保證](assets/target-trace-assurance.png)

## 檢查網路請求和響應

Platform Web SDK的要求裝載和回應 `sendEvent` 呼叫與at.js不同。 以下大綱應可協助您使用瀏覽器的開發人員工具檢查網路呼叫時，了解要求和回應的結構。

### 內容要求裝載

![鎖定平台Web SDK裝載的特定元素](assets/target-payload.png)

- 設定檔、實體和其他非mbox參數會傳遞至 `data.__adobe.target`
- 決策範圍位於 `query.personalization.decisionScopes`
- 下游對應至mbox參數的XDM資料位於 `xdm`

### 內容回應內文

![鎖定Platform Web SDK回應內文的特定元素](assets/target-response.png)

- Platform Web SDK會傳回下方所有Adobe應用程式的動作 `handle` 物件
- 此 `personalization:decisions` 動作表示來自Target或offer decisioning的回應
- 目標命題以陣列形式呈現，每個命題ID都帶有前置詞的唯一命題ID `AT:`
- 決策範圍和活動詳細資訊位於命題陣列中
- 優惠方案詳細資訊位於 `items` 陣列底下 `data`
- 回應Token位於 `items` 陣列底下 `meta`

### 主張事件裝載

![Target主張事件範例](assets/target-proposition-event.png)

- Target特定SDK事件為 `decisioning.propositionDisplay` 對於曝光或 `decisioning.propositionInteract` ，例如
- 主張事件的詳細資訊位於 `xdm._experience.decisioning`
- 顯示或互動事件的主張ID應符合從Target傳回內容的主張ID


恭喜，您已完成本教學課程的結尾！ 祝您將Adobe Target實作移轉至Web SDK!

>[!NOTE]
>
>我們致力協助您成功從at.js移轉至Web SDK。 如果您在移轉過程中遇到障礙，或覺得本指南中遺漏了重要資訊，請在 [此社區討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
