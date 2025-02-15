---
title: 將開發人員新增至Adobe Experience Platform應用程式
description: 瞭解如何將開發人員新增到Adobe Experience Platform型應用程式並授予API憑證的許可權
feature: Access Control
role: Admin, Developer
level: Beginner
jira: KT-14689
last-substantial-update: 2023-12-15T00:00:00Z
exl-id: 4bd28867-b664-4a45-8892-91af821cbbcc
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 新增開發人員並授與API憑證的許可權

瞭解如何將開發人員新增到Real-Time Customer Data Platform和Journey Optimizer等Adobe Experience Platform型應用程式。 開發人員是首次在Admin Console中新增。 在Developer Console中建立Platform專案後，他們的API認證會在Platform或Journey Optimizer介面中指派許可權。 如需詳細資訊，請瀏覽[存取控制檔案](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=zh-Hant)。

>[!VIDEO](https://video.tv.adobe.com/v/3426407?learn=on&enablevpops)

>[!ADMIN]
>
>只有系統管理員可以新增開發人員並為API憑證指派許可權。 產品管理員無法完成這些工作。

>[!TIP]
>
>我們建議您也將該開發人員新增為&#x200B;**使用者**，作為Admin Console中的`AEP-Default-All-Users`產品設定檔，然後將他們新增至平台介面中與API認證相同的角色。 如有需要，這可讓他們使用介面。 如需詳細資訊，請參閱[新增使用者](add-users.md)。
