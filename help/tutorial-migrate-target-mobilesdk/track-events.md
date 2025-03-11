---
title: 追蹤轉換事件 — 將行動應用程式中的Adobe Target實作移轉至Adobe Journey Optimizer — 決策擴充功能
description: 瞭解如何使用Adobe Journey Optimizer - Decisioning Mobile擴充功能追蹤Adobe Target轉換事件
exl-id: 7b53aab1-0922-4d9f-8bf0-f5cf98ac04c4
source-git-commit: d2da62ed2d36f73af1c8053be5af27feea32cb14
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# 使用Decisioning行動擴充功能追蹤目標轉換事件

大部分的Target活動都是為了在您的應用程式中推動重要的使用者動作，例如購買、註冊、點按等等。 Target實施通常會使用自訂轉換事件來追蹤這些動作，且通常會包含轉換的其他詳細資訊。 您可以使用類似Target SDK的「最佳化SDK」來追蹤Target的轉換事件。 需呼叫特定API才能追蹤轉換事件，如下表所示：

| 活動目標 | 目標延伸功能 | Decisioning擴充功能 |
|---|---|---|
| 追蹤mbox位置（範圍）的檢視轉換事件 | 檢視mbox位置時，呼叫[displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} API | 檢視mbox位置的選件時，請呼叫[顯示的](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} API。 這會將具有事件型別decisioning.propositionDisplay的事件傳送到Experience Edge網路。 **這對於在Target活動中增加訪客是必要的，並且必須在傳遞一般和預設Target選件時完成。** |
| 追蹤mbox位置（範圍）的點選轉換事件 | 按一下mbox位置時，呼叫中的[clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} API | 按一下mbox位置的選件時，請呼叫[taped](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} API。 這會將具有事件型別decisioning.propositionInteract的事件傳送至Experience Edge網路。 |
| 追蹤可能也會包含其他資料的自訂轉換事件，例如Target設定檔引數和訂單詳細資料 | 在[displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank}與[clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} API提供的TargetParameters欄位中傳遞其他資料 | 使用選件中適用於mbox位置的公用方法[generateDisplayInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank}和[generateTapInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} API，分別產生檢視和點按的XDM格式化資料。 然後呼叫Edge SDK [sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#sendevent){target=_blank} API，將此追蹤XDM資料連同任何其他XDM和自由格式資料傳送至Experience Edge網路。 |


接下來，瞭解如何[更新對象和設定檔指令碼](update-audiences.md)，以確保與Decisioning擴充功能相容。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
