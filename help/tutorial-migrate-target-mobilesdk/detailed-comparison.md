---
title: Target擴充功能與決策擴充功能的比較
description: 瞭解Target擴充功能與Decisioning擴充功能之間的差異，包括功能、功能、設定和資料流程。
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: cb08ad8a1ffd687d7748ca02643b11b2243cd1a7
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 2%

---

# Target擴充功能與決策擴充功能的比較

Adobe Journey Optimizer - Decisioning擴充功能與適用於行動應用程式的Adobe Target擴充功能不同。 下表為參考資料，可協助您評估在移轉程式期間可能需要著重的實作領域。

檢閱下列資訊並評估您目前的技術Target擴充功能實作後，您應該就能瞭解下列內容：

- Adobe Journey Optimizer支援哪些Target功能 — Decisioning
- 哪些Adobe Target擴充功能具有Adobe Journey Optimizer — 決策等效功能
- 如何將Target設定套用至Adobe Journey Optimizer — 決策
- 使用Adobe Journey Optimizer - Decisioning擴充功能時資料流動的方式

## 營運差異

| | 目標延伸功能 | Decisioning擴充功能 |
|---|---|---|
| 程式 | 變更Target實作可能會遵循的流程與其他應用程式（例如Analytics）具有不同的步調或QA需求。 | 對決策擴充功能實作的變更應考慮所有下游應用程式，並應相應地調整QA和發佈程式。 |
| 共同作業 | Target專屬的資料可直接在Target呼叫中傳遞。 如果Target報表來源是Adobe Analytics (A4T)，則當Target擴充功能中呼叫適當的追蹤方法來用於Target內容顯示和互動時，特定於Target的資料也可以傳遞到Adobe Analytics。 | 如果Target報表來源為Adobe Analytics (A4T)、已在資料串流中啟用Adobe Analytics，且顯示Target內容並與之互動時，系統可將Decisioning擴充功能呼叫中傳遞的資料轉送至Target和Analytics。 |

## 基本差異

| | 目標延伸功能 | Decisioning擴充功能 |
|---|---|---|
| 相依性 | 僅取決於行動核心SDK | 取決於行動核心和Edge NetworkSDK |
| 程式庫功能 | 僅支援從Adobe Target擷取內容 | 支援從Adobe Target和Offer decisioning擷取內容 |
| 請求 | Target呼叫基本上獨立於其他網路呼叫 | Target網路呼叫會針對其他Edge型解決方案(例如Edge SDK中的傳訊)與網路呼叫一起排入佇列，並依序執行。 |
| Edge Network | 使用Target伺服器值或具有使用者端代碼(clientcode.tt.omtrdc.net)的Adobe Experience CloudEdge Network，兩者都在資料收集UI的[Target組態](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui)中指定 | 在資料收集UI中使用Adobe Experience Platform [Edge Network組態](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui)中指定的Edge網路網域。 |
| 基本術語 | mbox， TargetParameters | 目標引數的DecisionScope， Map (Android)/dictionary (iOS) |
| 預設內容 | 允許在TargetRequest中傳遞使用者端預設內容，如果網路呼叫失敗或導致錯誤，則會傳回此內容。 | 不允許傳遞使用者端預設內容。 如果網路呼叫失敗或導致錯誤，則不會傳回任何內容。 |
| Target引數 | 允許傳遞每個要求的全域TargetParameters和每個mbox的不同TargetParameters | 僅允許傳遞每個要求的全域TargetParameters |



## 功能比較

| 功能 | 目標延伸功能 | 決策擴充功能(透過Edge的Target) |
|---|---|---|
| 預先擷取模式 | 支援 | 支援 |
| 執行模式 | 支援 | 不支援 |
| 自訂引數 | 支援 | 支援* |
| 輪廓參數 | 支援 | 支援* |
| 實體引數 | 支援 | 支援* |
| 目標客群 | 支援 | 支援 |
| Real-Time CDP對象 | 不支援 | 支援 |
| Real-Time CDP屬性 | 不支援 | 支援 |
| 生命週期量度 | 支援 | 透過資料收集規則支援 |
| thirdPartyId (mbox3rdPartyId) | 支援 | 透過資料流中的身分對應和目標第三方ID名稱空間支援 |
| 通知（顯示、按一下） | 支援 | 支援 |
| 回應Token | 支援 | 支援 |
| Analytics for Target (A4T) | 僅限使用者端 | 使用者端和伺服器端 |
| 行動裝置預覽（QA模式） | 支援 | Assurance的有限支援 |

>[!IMPORTANT]
>
> \*在要求中傳送的引數會套用至要求中的所有範圍。 如果您需要為不同的範圍設定不同的引數，則必須提出其他要求。



## 值得注意的圖說文字

>[!NOTE]
>
>即使您將應用程式程式碼移轉至Decisioning擴充功能後，仍能維持Target擴充功能標籤的組態和設定。 這可協助確保尚未將應用程式更新至新版本的客戶能夠繼續使用Target。
>
>如果您使用Analytics for Target整合(A4T)，在將Target實作移轉至Decisioning擴充功能的同時，請務必將Analytics實作與Edge Bridge擴充功能一起移轉。

## Target擴充功能與決策擴充功能的同等專案

許多Target擴充功能都有等同於下表所列之「決策」擴充功能的方法。 如需[函式](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)的詳細資訊，請參閱Adobe Target開發人員指南。

| 目標延伸功能 | Decisioning擴充功能 | 附註 |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | 使用`getPropositions` API時，不會進行遠端呼叫以擷取SDK中未快取的領域。 |
| `displayedLocations` | 選件 — > `displayed()` | 此外，`generateDisplayInteractionXdm`選件方法可用來產生專案顯示的XDM。 隨後，Edge網路SDK的sendEvent API可用於附加其他XDM自由格式資料，並將體驗事件傳送至遠端。 |
| `clickedLocation` | 選件 — > `tapped()` | 此外，`generateTapInteractionXdm`選件方法可用來產生專案點選的XDM。 隨後，Edge網路SDK的sendEvent API可用於附加其他XDM自由格式資料，並將體驗事件傳送至遠端。 |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` | 不適用 | 使用身分識別的`removeIdentity` API做為SDK的Edge Network延伸，以停止將訪客識別碼傳送至Edge網路。 如需詳細資訊，請參閱[removeIdentity API檔案](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity)。 <br><br>注意：行動核心的`resetIdentities` API會清除SDK中所有儲存的身分識別，包括Experience CloudID (ECID)，請謹慎使用！ |
| `getSessionId` | 不適用 | `state:store`回應控制代碼包含工作階段相關資訊。 Edge網路擴充功能可將未過期的狀態存放區專案附加至後續請求，協助您管理該專案。 |
| `setSessionId` | 不適用 | `state:store`回應控制代碼包含工作階段相關資訊。 Edge網路擴充功能可將未過期的狀態存放區專案附加至後續請求，協助您管理該專案。 |
| `getThirdPartyId` | 不適用 | 使用身分識別中的updateIdentities API進行Edge Network擴充功能，以提供第三方ID值。 然後，在資料流中設定第三方ID名稱空間。 如需更多詳細資料，請參閱[Target第三方ID行動檔案](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| `setThirdPartyId` | 不適用 | 使用身分識別中的updateIdentities API進行Edge Network擴充功能，以提供第三方ID值。 然後，在資料流中設定第三方ID名稱空間。 如需更多詳細資料，請參閱[Target第三方ID行動檔案](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| `getTntId` | 不適用 | `locationHint:result`回應控制代碼包含Target位置提示資訊。 我們假設Target邊緣會與Experience Edge位於同一位置。<br> <br>Edge網路擴充功能會使用EdgeNetwork位置提示來決定要傳送請求的Edge網路叢集。 若要跨SDK （混合式應用程式）共用Edge網路位置提示，請使用Edge Network擴充功能中的`getLocationHint`和`setLocationHint` API。 如需詳細資訊，請參閱[ `getLocationHint` API檔案](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)。 |
| `setTntId` | 不適用 | `locationHint:result`回應控制代碼包含Target位置提示資訊。 我們假設Target邊緣會與Experience Edge位於同一位置。<br> <br>Edge網路擴充功能會使用EdgeNetwork位置提示來決定要傳送請求的Edge網路叢集。 若要跨SDK （混合式應用程式）共用Edge網路位置提示，請使用Edge Network擴充功能中的`getLocationHint`和`setLocationHint` API。 如需詳細資訊，請參閱[ `getLocationHint` API檔案](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)。 |

## Target擴充功能設定與決策擴充功能等同專案

Target擴充功能具有[可設定的設定](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui)，這些設定是在資料流](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup)中以決策擴充功能設定的[。

| 目標延伸功能 | Decisioning擴充功能 | 附註 |
| --- | --- | --- | 
| 用戶端代碼 | 不適用 | 邊緣使用IMS組織詳細資料自動設定 |
| 環境ID | 目標環境ID | 在資料流中設定 |
| 目標Workspace屬性 | 屬性Token | 在資料流中設定 |
| 逾時 | 無法設定 | 決策擴充功能的逾時為10秒 |
| 伺服器網域 | Edge Network網域 | 在Adobe Experience PlatformEdge Network擴充功能中設定 |

>[!IMPORTANT]
>
> 即使您將應用程式程式碼移轉至Decisioning擴充功能後，Target擴充功能設定仍會妥善保留。 這可協助確保尚未更新應用程式的使用者能夠繼續使用Target。

## 決策擴充功能系統圖

下圖應可協助您瞭解使用Adobe Journey Optimizer - Decisioning擴充功能的資料流程。

![使用使用者端Mobile SDK的Adobe Target Edge Decisioning](assets/diagram.png)


>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
