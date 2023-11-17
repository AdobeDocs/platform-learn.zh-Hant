---
title: 安裝Adobe Experience Platform Mobile SDK
description: 瞭解如何在行動應用程式中實施Adobe Experience Platform Mobile SDK。
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 2%

---

# 安裝Adobe Experience Platform Mobile SDK

瞭解如何在行動應用程式中實施Adobe Experience Platform Mobile SDK。

>[!INFO]
>
> 在2023年11月下旬，此教學課程將由使用新範例行動應用程式的新教學課程取代

## 先決條件

* 使用中所述的擴充功能成功建置標籤程式庫 [上一課程](configure-tags.md).
* 來自的開發環境檔案ID [行動安裝指示](configure-tags.md#generate-sdk-install-instructions).
* 已下載，空白 [範例應用程式](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* 使用體驗 [XCode](https://developer.apple.com/xcode/){target="_blank"}.
* 基本 [命令列](https://en.wikipedia.org/wiki/Command-line_interface){target="_blank"} 知識。

## 學習目標

在本課程中，您將會：

* 更新您的CocoaPod檔案。
* 匯入必要的SDK。
* 註冊擴充功能。

>[!NOTE]
>
>在行動應用程式實作中，「擴充功能」和「SDK」這兩個辭彙幾乎可以互換。


## 更新PodFile

>[!NOTE]
>
> 如果您不熟悉CocoaPods，請查閱官方網站 [快速入門手冊](https://guides.cocoapods.org/using/getting-started.html).

安裝通常是簡單的sudo命令：

```console
sudo gem install cocoapods
```

安裝CocoaPods後，請開啟Podfile。

![初始podfile](assets/mobile-install-initial-podfile.png)

更新檔案以包含下列Pod：

```swift
pod 'AEPCore', '~> 3'
pod 'AEPEdge', '~> 1'
pod 'AEPUserProfile', '~> 3'
pod 'AEPAssurance', '~> 3'
pod 'AEPServices', '~> 3'
pod 'AEPEdgeConsent', '~> 1'
pod 'AEPLifecycle', '~>3'
pod 'AEPMessaging', '~>1'
pod 'AEPEdgeIdentity', '~>1'
pod 'AEPSignal', '~>3'
```

>[!NOTE]
>
> `AEPMessaging` 只有在您打算使用Adobe Journey Optimizer實作推送訊息時，才須使用。 請閱讀上的教學課程 [使用Adobe Journey Optimizer實作推送訊息](journey-optimizer-push.md) 以取得詳細資訊。

將變更儲存至您的Podfile後，請導覽至包含您專案的資料夾並執行 `pod install` 命令以安裝您的變更。

![pod install](assets/mobile-install-podfile-install.png)

>[!NOTE]
>
> 如果您收到「在專案目錄中找不到Podfile」。 錯誤，您的終端機位於錯誤的資料夾中。 請瀏覽至包含您更新的Podfile的資料夾，然後再試一次。

如果您想要升級至最新版本，請執行 `pod update` 命令。

>[!INFO]
>
>如果您無法在自己的應用程式中使用CocoaPods，您可以瞭解其他應用程式 [支援的實作](https://github.com/adobe/aepsdk-core-ios#binaries) GitHub專案中的。

## 建置CocoaPods

若要建置CocoaPods，請開啟 `Luma.xcworkspace`，並選取 **產品**，後接 **清除建置資料夾**.

>[!NOTE]
>
> 您可能需要設定 **僅建置使用中架構** 至 **否**. 若要這麼做，請從專案瀏覽器中選取Pods專案，然後選取 **建置設定**，並設定 **建置使用中架構** 至 **否**.

您現在可以建置並執行專案。

![建置設定](assets/mobile-install-build-settings.png)

>[!NOTE]
>
>Luma專案是以Xcode v12.5在M1晶片組上建置，並在iOS模擬器中執行。 如果您使用不同的設定，您可能需要變更組建設定以反映您的架構。
>
>如果您的建置失敗，請嘗試還原 **建置使用中架構** > **偵錯** 將設回 **是**.
>
>在編寫本教學課程時，使用了模擬器設定「iPod touch （第7代）」。

## 匯入擴充功能

在每個 `.swift` 檔案中，新增下列匯入。 首先，將新增至 `AppDelegate.swift`.

```swift
import AEPUserProfile
import AEPAssurance
import AEPEdge
import AEPCore
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPLifecycle
import AEPMessaging //Optional, used for AJO push messaging
import AEPSignal
import AEPServices
```

## 更新AppDelegate

在 `AppDelegate.swift` 檔案，將下列程式碼新增至 `didFinishLaunchingWithOptions`. 以從「 」中的標籤擷取的開發環境檔案ID值取代currentAppId [上一課程](configure-tags.md).

```swift
let currentAppId = "b5cbd1a1220e/bae66382cce8/launch-88492c6dcb6e-development"

let extensions = [Edge.self, Assurance.self, Lifecycle.self, UserProfile.self, Consent.self, AEPEdgeIdentity.Identity.self, Messaging.self]

MobileCore.setLogLevel(.trace)

MobileCore.registerExtensions(extensions, {
    MobileCore.configureWith(appId: currentAppId)
})
```

`Messaging.self` 只有在您打算透過Adobe Journey Optimizer實施推送訊息時（如所述），才需要使用 [此處](journey-optimizer-push.md).

上述程式碼會執行下列動作：

* 註冊必要的副檔名。
* 設定MobileCore和其他擴充功能以使用標籤屬性設定。
* 啟用偵錯記錄。 如需詳細資訊和選項，請參閱 [行動SDK檔案](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).

>[!IMPORTANT]
>在生產應用程式中，您必須根據目前環境(dev/stag/prod)切換AppId。
>

下一步： **[設定保證](assurance.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想要分享一般意見或有關於未來內容的建議，請在此分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)