---
title: 取代SDK — 將行動應用程式中的Adobe Target實作移轉至Adobe Journey Optimizer — 決策擴充功能
description: 瞭解從SDK移轉至Adobe Journey Optimizer - Decisioning Mobile擴充功能時，如何取代Adobe Target。
exl-id: f1b77cad-792b-4a80-acff-e1a2f29250e1
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---

# 以最佳化SDK取代SDK

瞭解如何以行動實施中的最佳化SDK取代Adobe Target SDK。 基本取代包含下列步驟：

* 更新您Podfile或`build.gradle`檔案中的相依性
* 更新匯入
* 更新應用程式程式碼

>[!INFO]
>
>在Adobe Experience Platform Mobile SDK生態系統內，擴充功能會由匯入應用程式（名稱可能不同）的SDK實作：
>
> * **目標SDK**&#x200B;實作&#x200B;**Adobe Target擴充功能**
> * **最佳化SDK**&#x200B;實作&#x200B;**Adobe Journey Optimizer - Decisioning擴充功能**

## 更新相依性

+++Android範例

>[!BEGINTABS]

>[!TAB 最佳化SDK]

移轉後的`build.gradle`相依性

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:edgeidentity'
implementation 'com.adobe.marketing.mobile:edge'
implementation 'com.adobe.marketing.mobile:optimize'
```


>[!TAB 目標SDK]

移轉前`build.gradle`個相依性

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:analytics'
implementation 'com.adobe.marketing.mobile:target'
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:identity'
implementation 'com.adobe.marketing.mobile:lifecycle'
implementation 'com.adobe.marketing.mobile:signal'
implementation 'com.adobe.marketing.mobile:userprofile'
```


>[!ENDTABS]

+++

+++ iOS範例

>[!BEGINTABS]


>[!TAB 最佳化SDK]

移轉後的`Podfile`相依性

```Swift
use_frameworks!
target 'YourAppTarget' do
    pod 'AEPCore', '~> 5.0'
    pod 'AEPEdge', '~> 5.0'
    pod 'AEPEdgeIdentity', '~> 5.0'
    pod 'AEPOptimize', '~> 5.0'
end
```

>[!TAB 目標SDK]

移轉前`Podfile`個相依性

```Swift
use_frameworks!
pod 'AEPAnalytics', '~> 5.0'
pod 'AEPTarget', '~> 5.0'
pod 'AEPCore', '~> 5.0'
pod 'AEPIdentity', '~> 5.0'
pod 'AEPSignal', '~>5.0'
pod 'AEPLifecycle', '~>5.0'
pod 'AEPUserProfile', '~> 5.0'
```

>[!ENDTABS]

+++

## 更新匯入和程式碼

+++ Android範例

>[!BEGINTABS]

>[!TAB 最佳化SDK]

移轉後的Java初始化程式碼

```Java
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.edge.identity.Identity;
import com.adobe.marketing.mobile.optimize.Optimize;
import com.adobe.marketing.mobile.AdobeCallback;
 
public class MainApp extends Application {
 
  private final String ENVIRONMENT_FILE_ID = "YOUR_APP_ENVIRONMENT_ID";
 
    @Override
    public void onCreate() {
        super.onCreate();
 
        MobileCore.setApplication(this);
        MobileCore.configureWithAppID(ENVIRONMENT_FILE_ID);
 
        MobileCore.registerExtensions(
            Arrays.asList(Edge.EXTENSION, Identity.EXTENSION, Optimize.EXTENSION),
            o -> Log.d("MainApp", "Adobe Journey Optimizer - Decisioning Mobile SDK was initialized.")
        );
    }
}
```

>[!TAB 目標SDK]

移轉前的Java初始化程式碼

```Java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Analytics;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.Target;
import com.adobe.marketing.mobile.UserProfile;
import java.util.Arrays;
import java.util.List;
...
import android.app.Application;
...
public class MainApp extends Application {
...
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
        ...
        List<Class<? extends Extension>> extensions = Arrays.asList(
            Analytics.EXTENSION,
            Target.EXTENSION,
            Identity.EXTENSION,
            Lifecycle.EXTENSION,
            Signal.EXTENSION,
            UserProfile.EXTENSION
        );
 
 
        MobileCore.registerExtensions(extensions, new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID(<Environment File ID>);
            }
        });
    }
}
```

>[!ENDTABS]

+++

+++ iOS

>[!BEGINTABS]

>[!TAB 最佳化SDK]

移轉後的Swift初始化程式碼

```Swift
import AEPCore
import AEPEdge
import AEPEdgeIdentity
import AEPOptimize
 
@UIApplicationMain
final class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?
 
  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]? = nil) -> Bool {
 
      // register the extensions
      MobileCore.registerExtensions([Edge.self, AEPEdgeIdentity.Identity.self, Optimize.self]) {
        MobileCore.configureWith(appId: <YOUR_ENVIRONMENT_FILE_ID>) // Replace <YOUR_ENVIRONMENT_FILE_ID> with a String containing your own ID.
      }
 
      return true
  }
}
```

>[!TAB 目標SDK]

移轉前的Swift初始化程式碼

```Swift
import AEPCore
import AEPAnalytics
import AEPTarget
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPServices
import AEPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.setLogLevel(.debug)
        let appState = application.applicationState
        ...
        let extensions = [
            Analytics.self,
            Target.self,
            Identity.self,
            Lifecycle.self,
            Signal.self,
            UserProfile.self
        ]
        MobileCore.registerExtensions(extensions, {
        MobileCore.configureWith(<Environment File ID>)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
            }
        })
        ...
        return true
    }
}
```

>[!ENDTABS]

+++

## 函式比較

許多Target擴充功能都有等同於下表所列之「決策」擴充功能的方法。 如需[函式](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)的詳細資訊，請參閱Adobe Target開發人員指南。

| 目標延伸功能 | Decisioning擴充功能 | 附註 |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | 使用`getPropositions` API時，不會進行遠端呼叫以擷取SDK中未快取的領域。 |
| `displayedLocations` | 選件 — > `displayed()` | 此外，`generateDisplayInteractionXdm`選件方法可用來產生專案顯示的XDM。 隨後，Edge網路SDK的sendEvent API可用於附加其他XDM自由格式資料，並將體驗事件傳送至遠端。 |
| `clickedLocation` | 選件 — > `tapped()` | 此外，`generateTapInteractionXdm`選件方法可用來產生專案點選的XDM。 隨後，Edge網路SDK的sendEvent API可用於附加其他XDM自由格式資料，並將體驗事件傳送至遠端。 |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` | 不適用 | 使用適用於SDK的Edge Network擴充功能之身分識別的`removeIdentity` API來停止將訪客識別碼傳送至Edge網路。 如需詳細資訊，請參閱[removeIdentity API檔案](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity)。 <br><br>注意：行動核心的`resetIdentities` API清除了SDK中所有儲存的身分識別，包括Experience Cloud ID (ECID)，應謹慎使用！ |
| `getSessionId` | 不適用 | `state:store`回應控制代碼包含工作階段相關資訊。 Edge網路擴充功能可將未過期的狀態存放區專案附加至後續請求，協助您管理該專案。 |
| `setSessionId` | 不適用 | `state:store`回應控制代碼包含工作階段相關資訊。 Edge網路擴充功能可將未過期的狀態存放區專案附加至後續請求，協助您管理該專案。 |
| `getThirdPartyId` | 不適用 | 使用適用於Edge Network擴充功能之身分的updateIdentities API來提供第三方ID值。 然後，在資料流中設定第三方ID名稱空間。 如需更多詳細資料，請參閱[Target第三方ID行動檔案](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| `setThirdPartyId` | 不適用 | 使用適用於Edge Network擴充功能之身分的updateIdentities API來提供第三方ID值。 然後，在資料流中設定第三方ID名稱空間。 如需更多詳細資料，請參閱[Target第三方ID行動檔案](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| `getTntId` | 不適用 | `locationHint:result`回應控制代碼包含Target位置提示資訊。 我們假設Target邊緣會與Experience Edge位於同一位置。<br> <br>Edge網路擴充功能會使用EdgeNetwork位置提示來決定要傳送請求的Edge網路叢集。 若要跨SDK （混合式應用程式）共用Edge網路位置提示，請使用Edge Network擴充功能中的`getLocationHint`和`setLocationHint` API。 如需詳細資訊，請參閱[ `getLocationHint` API檔案](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)。 |
| `setTntId` | 不適用 | `locationHint:result`回應控制代碼包含Target位置提示資訊。 我們假設Target邊緣會與Experience Edge位於同一位置。<br> <br>Edge網路擴充功能會使用EdgeNetwork位置提示來決定要傳送請求的Edge網路叢集。 若要跨SDK （混合式應用程式）共用Edge網路位置提示，請使用Edge Network擴充功能中的`getLocationHint`和`setLocationHint` API。 如需詳細資訊，請參閱[ `getLocationHint` API檔案](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)。 |


接下來，瞭解如何[請求並將活動](retrieve-activities.md)轉譯到頁面。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463)中張貼以告知我們。
