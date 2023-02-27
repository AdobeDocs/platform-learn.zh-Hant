---
title: 設定保證
description: 了解如何在行動應用程式中實作Assurance擴充功能。
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: 7df759ec0ea248ee91ae673e3468ffa3f6cc5be5
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 2%

---

# 保證

了解如何在行動應用程式中設定Adobe Experience Platform Assurance。

Assurance（正式稱為Project Griffon）旨在協助您檢查、校樣、模擬及驗證您收集資料或在行動應用程式中提供體驗的方式。

保證可協助您檢查由Adobe Experience Platform Mobile SDK產生的原始SDK事件。 SDK收集的所有事件都可供檢查。 SDK事件會以清單檢視載入，並依時間排序。 每個事件都有詳細的檢視，可提供更詳細的資訊。 此外，也提供瀏覽SDK設定、資料元素、共用狀態和SDK擴充功能版本的其他檢視。 深入了解 [保證](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance) 在產品檔案中。


## 先決條件

* 已成功建立並執行已安裝並設定SDK的範例應用程式。

## 學習目標

在本課程中，您將：

* 確認您的組織擁有存取權（若您沒有，請求）。
* 設定您的基礎URL。
* 新增必要的iOS特定程式碼。
* 連接到會話。

## 確認存取

完成下列步驟，確認貴組織有權存取「保證」：

1. 瀏覽 [https://experience.adobe.com/#/assurance](https://experience.adobe.com/griffon){target="_blank"}
1. 使用您的Adobe ID憑證登入Experience Cloud。
1. 如果您被帶到 **[!UICONTROL 工作階段]** 螢幕，則您擁有存取權。 如果您被帶入測試版存取頁面，請選取 **[!UICONTROL 註冊]**.

## 實作

除了 [SDK安裝](install-sdks.md) 您在先前的課程中已完成，iOS也需要新增下列項目。 將下列程式碼新增至 `AppDelegate.swift` 檔案:

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey: Any] = [:]) -> Bool {
    Assurance.startSession(url: url)
    return true
}
```

本教學課程提供的範例Luma使用iOS 12.0。如果您要使用iOS 13和更新版本，連同您自己的基於場景的應用程式，請使用 `UISceneDelegate's scene(_:openURLContexts:)` 方法，如下所示：

```swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    // Called when the app in background is opened with a deep link.
    if let deepLinkURL = URLContexts.first?.url {
        Assurance.startSession(url: deepLinkURL)
    }
}
```

如需詳細資訊，請參閱 [此處](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance#implement-aep-assurance-session-start-apis-ios-only){target="_blank"}.

## 設定基礎URL

1. 開啟XCode並選取專案名稱。
1. 導覽至 **資訊** 標籤。
1. 向下捲動至 **URL類型** ，然後選取 **+** 按鈕以新增一個。
1. 設定 **識別碼** 和 **URL配置** 到&quot;lumadeeplink&quot;。
1. 建立並執行應用程式。

![保證url](assets/mobile-assurance-url-type.png)

若要進一步了解iOS中的URL配置，請檢閱 [Apple檔案](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

確保的運作方式是透過瀏覽器或QR碼開啟URL，該URL從開啟應用程式且包含其他參數的基本URL開始。 這些唯一參數用於連接會話。

## 連接到會話

1. 導覽至 [保證UI](https://experience.adobe.com/griffon){target="_blank"}.
1. 選擇 **[!UICONTROL 建立工作階段]**.
1. 提供 **[!UICONTROL 工作階段名稱]** 例如 `Luma App QA` 和 **[!UICONTROL 基本URL]** `lumadeeplink://default`
1. 選取&#x200B;**[!UICONTROL 「下一步」]**。
   ![保證建立會話](assets/mobile-assurance-create-session.png)
1. **[!UICONTROL 掃描QR碼]** 如果你使用的是物理設備。 如果您使用模擬器，則 **[!UICONTROL 複製連結]** 然後在模擬器中使用Safari開啟。
   ![保證品質代碼](assets/mobile-assurance-qr-code.png)
1. 當應用程式載入時，系統會向您顯示強制回應，要求您從上一步輸入PIN碼。
   ![保證輸入PIN](assets/mobile-assurance-enter-pin.png)
1. 如果連線成功，您會在Assurance Web UI中看到事件，並在應用程式中看到浮動的Assurance圖示。
   * 保證表徵圖浮動。
      ![保證模式](assets/mobile-assurance-modal.png)
   * Experience Cloud事件傳入Web UI。
      ![保證事件](assets/mobile-assurance-events.png)

如果您遇到任何挑戰，請查看 [技術](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance){target="_blank"} and [general documentation](https://aep-sdks.gitbook.io/docs/beta/project-griffon){target="_blank"}.

下一個： **[同意](consent.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
