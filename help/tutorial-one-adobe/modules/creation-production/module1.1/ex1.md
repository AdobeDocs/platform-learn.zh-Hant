---
title: Firefly服務快速入門
description: 瞭解如何使用Postman和Adobe I/O來查詢Adobe Firefly Services API
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 1.1.1 Firefly服務快速入門

瞭解如何使用Postman和Adobe I/O來查詢Adobe Firefly Services API。

## 1.1.1.1必要條件

在繼續此練習之前，您必須先完成[您的Adobe I/O專案](./../../../modules/getting-started/gettingstarted/ex6.md)的設定，而且您還需要設定應用程式以與API互動，例如[Postman](./../../../modules/getting-started/gettingstarted/ex7.md)或[PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md)。

## 1.1.1.2 Adobe I/O - access_token

在&#x200B;**Adobe IO - OAuth**&#x200B;集合中，選取名為&#x200B;**POST - Get Access Token**&#x200B;的要求，並選取&#x200B;**傳送**。 回應應包含新的&#x200B;**accestoken**。

![Postman](./images/ioauthresp.png){zoomable="yes"}

## 1.1.1.3 Firefly Services API，文字2影像

現在您已具備有效且新的access_token，接下來可以將第一個要求傳送至Firefly Services API。

從&#x200B;**FF - Firefly服務技術內部人士**&#x200B;集合中選取名為&#x200B;**POST - Firefly - T2I V3**&#x200B;的請求。

![Firefly](./images/ff1.png){zoomable="yes"}

從回應中複製影像URL，然後在您的網頁瀏覽器中開啟以檢視影像。

![Firefly](./images/ff2.png){zoomable="yes"}

您應該會看到描繪`horses in a field`的美麗影像。

![Firefly](./images/ff3.png){zoomable="yes"}

在繼續進行下一個練習之前，請隨時嘗試使用API請求。

## 後續步驟

移至[使用Microsoft Azure和預先簽署的URL最佳化您的Firefly程式](./ex2.md){target="_blank"}

返回[Adobe Firefly服務總覽](./firefly-services.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}
