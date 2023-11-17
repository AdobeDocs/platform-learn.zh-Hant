---
title: 同意
description: 瞭解如何在行動應用程式中實施同意。
feature: Mobile SDK,Consent
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 6%

---

# 同意

瞭解如何在行動應用程式中實施同意。

>[!INFO]
>
> 在2023年11月下旬，此教學課程將由使用新範例行動應用程式的新教學課程取代

Adobe Experience Platform同意行動擴充功能可讓您在使用Adobe Experience Platform Mobile SDK和Edge Network擴充功能時，從行動應用程式收集同意偏好設定。 進一步瞭解 [同意擴充功能](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/)，在檔案中。

## 先決條件

* 成功建立並執行應用程式，且已安裝並設定SDK。

## 學習目標

在本課程中，您將會：

* 提示使用者同意。
* 根據使用者回應更新擴充功能。
* 瞭解如何取得目前的同意狀態。

## 要求同意

如果您從頭開始按照教學課程進行，您會記得設定 **[!UICONTROL 預設同意層級]** 變更為「擱置中」。 為了開始收集資料，您必須獲得使用者的同意。 在本教學課程中，只要在真實世界應用程式中詢問您想要諮詢所在地區的同意最佳實務，即可取得同意。

1. 您只想詢問使用者一次。 管理此資訊的簡單方法就是使用 `UserDefaults`.
1. 導覽至 `Home.swift`。
1. 將下列程式碼新增至 `viewDidLoad()`.

   ```swift
   let defaults = UserDefaults.standard
   let consentKey = "askForConsentYet"
   let hidePopUp = defaults.bool(forKey: consentKey)
   ```

1. 如果使用者之前未看到警報，則顯示警報並根據其回應更新同意。 將下列程式碼新增至 `viewDidLoad()`.

   ```swift
   if(hidePopUp == false){
       //Consent Alert
       let alert = UIAlertController(title: "Allow Data Collection?", message: "Selecting Yes will begin data collection", preferredStyle: .alert)
       alert.addAction(UIAlertAction(title: "Yes", style: .default, handler: { action in
           //Update Consent -> "yes"
           let collectConsent = ["collect": ["val": "y"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       alert.addAction(UIAlertAction(title: "No", style: .cancel, handler: { action in
           //Update Consent -> "no"
           let collectConsent = ["collect": ["val": "n"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       self.present(alert, animated: true)
   }
   ```


## 取得目前的同意狀態

同意行動擴充功能將會根據目前的同意值自動隱藏/擱置/允許追蹤。 您也可以自行存取目前的同意狀態：

1. 導覽至 `Home.swift`。
1. 將下列程式碼新增至 `viewDidLoad()`.

```swift
Consent.getConsents{ consents, error in
    guard error == nil, let consents = consents else { return }
    guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
    guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
    print("Consent getConsents: ",jsonStr)
}
```

在上述範例中，您只是將同意狀態列印到主控台。 在真實情境中，您可以使用它來修改要向使用者顯示哪些功能表或選項。

## 使用保證進行驗證

1. 檢閱 [保證](assurance.md) 課程。
1. 安裝應用程式。
1. 使用保證產生的URL啟動應用程式。
1. 如果您正確新增上述程式碼，系統會提示您提供同意。 選取 **是**.
   ![同意快顯視窗](assets/mobile-consent-validate.png)
1. 您應該會看到 **[!UICONTROL 同意偏好設定已更新]** 保證UI中的事件。
   ![驗證同意](assets/mobile-consent-update.png)

下一步： **[收集生命週期資料](lifecycle-data.md)**

>[!NOTE]
>
>感謝您花時間學習Adobe Experience Platform Mobile SDK。 如果您有疑問、想分享一般意見或有關於未來內容的建議，請分享這些內容 [Experience League社群討論貼文](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)