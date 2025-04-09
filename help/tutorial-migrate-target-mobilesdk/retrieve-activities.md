---
title: 擷取Target活動 — 將行動應用程式中的Adobe Target實作移轉至Adobe Journey Optimizer - Decisioning擴充功能
description: 瞭解從Adobe Target移轉至Adobe Journey Optimizer - Decisioning Mobile擴充功能時，如何擷取Adobe Target活動。
exl-id: 39569088-a254-4e64-9956-0c6e1a8ed2a5
source-git-commit: 2ebad2014d4c29a50af82328735258958893b42c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 擷取Target活動

Target行動實作使用地區mbox （現在稱為「範圍」），從使用Target表單式體驗撰寫器的活動傳送內容。 您必須更新行動應用程式，以在網路呼叫中包含範圍。

Target傳回的內容（也稱為「選件」）通常由文字或JSON組成，您需要在應用程式中使用此文字或JSON才能呈現最終的客戶體驗。 Target選件通常用於：

* 在您的應用程式中啟用功能標幟
* 提供替代文字或影像

如果您的活動需要在應用程式的Target擴充功能和Decisioning擴充功能版本中執行，請務必徹底測試。 如果您需要針對不同版本的應用程式使用不同選件，請考慮使用介面中的鎖定目標選項，將不同選件傳送至不同版本。

請務必加入錯誤處理功能，以便在錯誤條件下顯示適當的體驗。


## 隨選要求並套用內容

>[!IMPORTANT]
>
>將內容套用至應用程式後，必須引發`displayed` API，讓Target知道訪客已看到活動中指定的替代或預設內容。 如需詳細資訊，請參閱[追蹤目標轉換事件](track-events.md)頁面。


+++ Android範例

>[!BEGINTABS]

>[!TAB 最佳化SDK]

```Java
// Mboxes for Target activities
final DecisionScope decisionScope1 = DecisionScope("myTargetMbox1");
final DecisionScope decisionScope2 = new DecisionScope("myTargetMbox2");
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope1);
decisionScopes.add(decisionScope2);
 
// Prefetch the Target mboxes
Optimize.updatePropositions(decisionScopes,
                            new HashMap<String, Object>() {
                                {
                                    put("xdmKey", "xdmValue");
                                }
                            },
                            new HashMap<String, Object>() {
                                {
                                    put("dataKey", "dataValue");
                                }
                            },
                            new AdobeCallbackWithOptimizeError<Map<DecisionScope, OptimizeProposition>>() {
                                @Override
                                public void fail(AEPOptimizeError optimizeError) {
                                    // Log in case of error
                                    Log.d("Target Prefetch error", optimizeError.title);
                                }
 
                                @Override
                                public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                    // Retrieve cached propositions if prefetch succeeds
                                    Optimize.getPropositions(scopes, new AdobeCallbackWithError<Map<DecisionScope, OptimizeProposition>>() {
                                        @Override
                                      public void fail(final AdobeError adobeError) {
                                              // handle error
                                        }
 
                                        @Override
                                        public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                              if (propositionsMap != null && !propositionsMap.isEmpty()) {
                                                // get the propositions for the given decision scopes
                                                if (propositionsMap.contains(decisionScope1)) {
                                                      final OptimizeProposition proposition1 = propsMap.get(decisionScope1)
                                                      // read proposition1 offers and display them
                                                }
                                                if (propositionsMap.contains(decisionScope2)) {
                                                      final OptimizeProposition proposition2 = propsMap.get(decisionScope2)
                                                      // read proposition2 offers and display them
                                                }
                                              }
                                        }
                                      });
                                }
                            });
```

>[!ENDTABS]

+++

+++ iOS範例

>[!BEGINTABS]

>[!TAB 最佳化SDK]

```Swift
// Mboxes for Target activities
let decisionScope1 = DecisionScope(name: "myTargetMbox1")
let decisionScope2 = DecisionScope(name: "myTargetMbox2")
 
// Prefetch the Target mboxes
Optimize.updatePropositions(for: [decisionScope1, decisionScope2]
                            withXdm: ["xdmKey": "xdmValue"]
                            andData: ["dataKey": "dataValue"]) { data, error in
            if let error = error as? AEPOptimizeError {
                // handle error
                return
            }
            // Retrieve cached propositions if prefetch succeeds
            Optimize.getPropositions(for: [decisionScope1, decisionScope2]) { propositionsDict, error in
                if let error = error {
                    // handle error
                    return
                }
 
                if let propositionsDict = propositionsDict {
                    // get the propositions for the given decision scopes
 
                    if let proposition1 = propositionsDict[decisionScope1] {
                        // read proposition1 offers and display them
                    }
 
                    if let proposition2 = propositionsDict[decisionScope2] {
                        // read proposition2 offers and display them
                    }
                }
            }
        }
```

>[!ENDTABS]

+++



接下來，瞭解如何使用Decisioning擴充功能[傳遞Target引數](send-parameters.md)。

>[!NOTE]
>
>我們致力協助您成功將行動Target從Target擴充功能移轉至Decisioning擴充功能。 如果您在移轉時遇到問題，或覺得本指南中缺少重要資訊，請在[此社群討論](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625)中張貼以告知我們。
