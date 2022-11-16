---
title: 安裝Adobe Experience Platform Mobile SDK
description: 了解如何在行動應用程式中實作Adobe Experience Platform Mobile SDK。
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# 安裝Adobe Experience Platform Mobile SDK

了解如何在行動應用程式中實作Adobe Experience Platform Mobile SDK。

## 先決條件

* 已成功建立標籤程式庫，其擴充功能於 [上一課](configure-tags.md).
* 開發環境檔案ID，來自 [行動安裝指示](configure-tags.md#generate-sdk-install-instructions).
* 已下載，空 [範例應用程式](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;}。
* 體驗 [XCode](https://developer.apple.com/xcode/){target=&quot;_blank&quot;}。
* 基本 [命令列](https://en.wikipedia.org/wiki/Command-line_interface){target=&quot;_blank&quot;}知識。

## 學習目標

在本課程中，您將：

* 更新CocoaPod檔案。
* 匯入必要的SDK。
* 註冊擴充功能。

>[!NOTE]
>
>在行動應用程式實作中，「擴充功能」和「SDK」幾乎可互換。


## 更新PodFile

>[!NOTE]
>
> 如果您不熟悉CocoaPods，請查閱該官員 [快速入門手冊](https://guides.cocoapods.org/using/getting-started.html).

安裝通常是簡單的sudo命令：

```console
sudo gem install cocoapods
```

安裝CocoaPods後，請開啟Podfile。

![初始podfile](assets/mobile-install-initial-podfile.png)

更新檔案以包含下列Pod:

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
> `AEPMessaging` 只有在您計畫使用Adobe Journey Optimizer實作推送訊息時，才為必要。 請閱讀以下教學課程： [使用Adobe Journey Optimizer實作推送訊息](journey-optimizer-push.md) 以取得更多資訊。

將變更儲存至您的Podfile後，導覽至專案所在的資料夾並執行 `pod install` 命令安裝更改。

![pod安裝](assets/mobile-install-podfile-install.png)

>[!NOTE]
>
> 如果您收到「在專案目錄中找不到Podfile」。 錯誤，您的終端位於錯誤的資料夾中。 導覽至含有您更新之Podfile的資料夾，然後再試一次。

如果您想要升級至最新版本，請執行 `pod update` 命令。

>[!INFO]
>
>如果您無法在自己的應用程式中使用CocoaPods，您可以了解其他 [支援的實作](https://github.com/adobe/aepsdk-core-ios#binaries) GitHub專案中。

## 建置CocoaPods

若要建置CocoaPods，請開啟 `Luma.xcworkspace`，然後選取 **產品**，後跟 **清除建置資料夾**.

>[!NOTE]
>
> 您可能需要設定 **僅構建活動體系結構** to **否**. 若要這麼做，請從專案導覽器中選取Pods專案，然後選取 **建置設定**，並設定 **構建活動體系結構** to **否**.

您現在可以建置並執行專案。

![建置設定](assets/mobile-install-build-settings.png)

>[!NOTE]
>
>Luma專案是在M1晶片集上使用Xcode v12.5建置，並在iOS模擬器上執行。 如果您使用不同的設定，則可能需要變更您的組建設定以反映您的架構。
>
>如果您的組建未成功，請嘗試還原 **構建活動體系結構** > **除錯** 設定回 **是**.
>
>編寫本教學課程時，已使用模擬器設定「iPod touch（第7代）」。

## 匯入擴充功能

在 `.swift` 檔案，新增下列匯入。 首先，將新增至 `AppDelegate.swift`.

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

在 `AppDelegate.swift` 檔案中，將下列程式碼新增至 `didFinishLaunchingWithOptions`. 將currentAppId替換為從 [上一課](configure-tags.md).

```swift
let currentAppId = "b5cbd1a1220e/bae66382cce8/launch-88492c6dcb6e-development"

let extensions = [Edge.self, Assurance.self, Lifecycle.self, UserProfile.self, Consent.self, AEPEdgeIdentity.Identity.self, Messaging.self]

MobileCore.setLogLevel(.trace)

MobileCore.registerExtensions(extensions, {
    MobileCore.configureWith(appId: currentAppId)
})
```

`Messaging.self` 只有在您打算依照所述透過Adobe Journey Optimizer實作推送訊息時，才需要 [此處](journey-optimizer-push.md).

上述程式碼會執行下列動作：

* 註冊所需的擴充功能。
* 設定MobileCore和其他擴充功能以使用您的標籤屬性設定。
* 啟用偵錯記錄。 如需更多詳細資訊和選項，請參閱 [行動SDK檔案](https://aep-sdks.gitbook.io/docs/getting-started/enable-debug-logging).

>[!IMPORTANT]
>在生產應用程式中，您必鬚根據目前環境(dev/stag/prod)切換AppId。

下一個： **[設定保證](assurance.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有任何疑問、想要分享一般意見，或對未來內容有任何建議，請就此分享 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)