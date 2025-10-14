---
title: 取代SDK — 將行動應用程式中的Adobe Target實作移轉至Offer Decisioning和Target擴充功能
description: 瞭解如何從SDK移轉至Offer Decisioning和Target Mobile擴充功能時取代Adobe Target。
exl-id: f1b77cad-792b-4a80-acff-e1a2f29250e1
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '726'
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
> * **最佳化SDK**&#x200B;實作&#x200B;**Offer Decisioning和Target擴充功能**

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
            o -> Log.d("MainApp", "Offer Decisioning and Target Mobile SDK was initialized.")
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

## API比較

許多Target擴充功能API都有等同的方法使用Offer Decisioning和Target擴充功能，如下表所述。 如需[函式](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/)的詳細資訊，請參閱API參考。

| 目標延伸功能 | Offer Decisioning和Target擴充功能 | 附註 |
| --- | --- | --- | 
| [prefetchContent](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#prefetchcontent){target=_blank} | [updatePropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/#updatepropositionswithcompletionhandlerandtimeout){target=_blank} |  |
| [retrieveLocationContent](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#retrievelocationcontent){target=_blank} | [getPropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/#getpropositionswithtimeout){target=_blank} | 使用`getPropositions` API時，不會進行遠端呼叫以擷取SDK中未快取的領域。 |
| [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#retrievelocationcontent){target=_blank} | [選件 — >已顯示()](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} | 此外，`generateDisplayInteractionXdm`選件方法可用來產生專案顯示的XDM。 隨後，Edge網路SDK的sendEvent API可用於附加其他XDM自由格式資料，並將體驗事件傳送至遠端。 |
| [clickedLocation](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#clickedlocation){target=_blank} | [選件 — >已點選()](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} | 此外，`generateTapInteractionXdm`選件方法可用來產生專案點選的XDM。 隨後，Edge網路SDK的sendEvent API可用於附加其他XDM自由格式資料，並將體驗事件傳送至遠端。 |
| [clearPrefetchCache](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#clickedlocation){target=_blank} | [clearCachedPropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} |  |
| [resetExperience](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#resetexperience){target=_blank} | 不適用 | 使用SDK的Edge Network延伸模組識別碼中的[removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity){target=_blank} API來停止將訪客識別碼傳送至Edge網路。 如需詳細資訊，請參閱[removeIdentity API檔案](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity)。 <br><br>注意：行動核心的`resetIdentities` API清除了SDK中所有儲存的身分識別，包括Experience Cloud ID (ECID)，應謹慎使用！ |
| [getSessionId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#getsessionid){target=_blank} | 不適用 | `state:store`回應控制代碼包含工作階段相關資訊。 Edge網路擴充功能可將未過期的狀態存放區專案附加至後續請求，協助您管理該專案。 |
| [setSessionId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#setsessionid){target=_blank} | 不適用 | `state:store`回應控制代碼包含工作階段相關資訊。 Edge網路擴充功能可將未過期的狀態存放區專案附加至後續請求，協助您管理該專案。 |
| [getThirdPartyId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#getthirdpartyid){target=_blank} | 不適用 | 使用適用於Edge Network擴充功能之身分的updateIdentities API來提供第三方ID值。 然後，在資料流中設定第三方ID名稱空間。 如需更多詳細資料，請參閱[Target第三方ID行動檔案](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| [setThirdPartyId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#setthirdpartyid){target=_blank} | 不適用 | 使用適用於Edge Network擴充功能之身分的updateIdentities API來提供第三方ID值。 然後，在資料流中設定第三方ID名稱空間。 如需更多詳細資料，請參閱[Target第三方ID行動檔案](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id)。 |
| [getTntId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#gettntid){target=_blank} | 不適用 | `locationHint:result`回應控制代碼包含Target位置提示資訊。 我們假設Target邊緣會與Experience Edge位於同一位置。<br> <br>Edge網路擴充功能會使用EdgeNetwork位置提示來決定要傳送請求的Edge網路叢集。 若要跨SDK （混合式應用程式）共用Edge網路位置提示，請使用Edge Network擴充功能中的`getLocationHint`和`setLocationHint` API。 如需詳細資訊，請參閱[&#x200B; `getLocationHint` API檔案](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)。 |
| [setTntId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#gettntid){target=_blank} | 不適用 | [locationHint：result](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#setlocationhint){target=_blank}回應控制代碼包含Target位置提示資訊。 我們假設Target邊緣會與Experience Edge位於同一位置。<br> <br>Edge網路擴充功能會使用EdgeNetwork位置提示來決定要傳送請求的Edge網路叢集。 若要跨SDK （混合式應用程式）共用Edge網路位置提示，請使用Edge Network擴充功能中的`getLocationHint`和`setLocationHint` API。 如需詳細資訊，請參閱[&#x200B; `getLocationHint` API檔案](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint)。 |


接下來，瞭解如何[請求並將活動](retrieve-activities.md)轉譯到頁面。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Offer Decisioning和Target擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625)中張貼以告知我們。
