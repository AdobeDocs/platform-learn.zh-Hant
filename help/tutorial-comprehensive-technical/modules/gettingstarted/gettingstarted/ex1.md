---
title: 快速入門 — 安裝Chrome擴充功能以取得Experience League檔案
description: 快速入門 — 安裝Chrome擴充功能以取得Experience League檔案
kt: 5342
doc-type: tutorial
source-git-commit: 8d595675c09a4347c04e900414d94b6c674e20f7
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 0.1安裝適用於Experience League檔案的Chrome擴充功能

## 0.1.1我們為何建立Chrome擴充功能？

此檔案已改成通用檔案，任何人都能使用任何Adobe Experience Platform例項輕鬆重複使用。
透過讓檔案可重複使用，檔案中引入了**環境變數**，這表示您將在檔案中找到以下&#x200B;**索引鍵**。 每個索引鍵都是特定環境的特定變數，Chrome擴充功能會為您變更該變數，因此讓您能夠從教學課程頁面輕鬆復製程式碼和文字，並將其貼到您將作為教學課程一部分使用的各種使用者介面中。

您可在下方找到這類值的範例。 目前，這些值尚無法使用，但當您安裝並啟動Chrome擴充功能時，就會看到這些變數變更為您可複製並重複使用的「一般」文字。

| 名稱 | 索引鍵 |
|:-------------:| :---------------:|
| AEP IMS組織ID | `--aepImsOrgId--` |
| AEP租使用者ID | `--aepTenantId--` |
| AEP沙箱名稱 | `--aepSandboxName--` |
| 學習者設定檔LDAP | `--aepUserLdap--` |

例如，在下方熒幕擷圖中，您可以看到`--aepTenantId--`的參考。

![DSN](./images/mod7before.png)

安裝擴充功能後，相同的文字會自動變更，以反映執行個體特定的值。

![DSN](./images/mod7.png)

擴充功能也可讓您：

- 註冊參加教學課程

## 0.1.2安裝Chrome擴充功能

若要安裝該Chrome擴充功能，請開啟Chrome瀏覽器，並移至： [https://chrome.google.com/webstore/detail/platform-learn-configurat/hhnbkfgioecmhimdhooigajdajplinfi/related?hl=en&amp;authuser=0](https://chrome.google.com/webstore/detail/platform-learn-configurat/hhnbkfgioecmhimdhooigajdajplinfi/related?hl=en&amp;authuser=0)。 您將會看到此訊息。

按一下&#x200B;**新增至Chrome**。

![DSN](./images/c2.png)

您將會看到此訊息。 按一下&#x200B;**新增擴充功能**。

![DSN](./images/c3.png)

隨後將安裝擴充功能，而您會看到類似通知。

![DSN](./images/c4.png)

在&#x200B;**擴充功能**&#x200B;功能表中，按一下&#x200B;**拼圖片段**&#x200B;圖示，並將&#x200B;**Platform Learn - Configuration**&#x200B;擴充功能釘選至擴充功能表。

![DSN](./images/c6.png)

## 0.1.2設定Chrome擴充功能

前往[https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/overview.html?lang=en](https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/overview.html?lang=en)，然後按一下擴充功能圖示以開啟。

![DSN](./images/tuthome.png)

然後您會看到此快顯視窗。 按一下&#x200B;**+**&#x200B;圖示。

![DSN](./images/c7.png)

輸入您的名稱和為您的Adobe Experience Platform環境建立的設定ID。 按一下&#x200B;**新建**。

>[!IMPORTANT]
>
>如果您是Adobe員工：您可以找到要在內部Github存放庫上使用的設定ID (https://git.corp.adobe.com/vangeluw/platformenablement)。
>
>若您是Adobe解決方案合作夥伴，請連絡您的解決方案合作夥伴連絡人或傳送電子郵件至&#x200B;**spphelp@adobe.com**。

![DSN](./images/c8.png)

在擴充功能的左側功能表中，您現在會看到含有縮寫的圖示。 按一下它。 然後您會看到&#x200B;**環境變數**&#x200B;和您的特定Adobe Experience Platform執行個體值之間的對應。 按一下&#x200B;**啟動設定**。

![DSN](./images/c9.png)

啟用您的設定後，您會在首字母縮寫旁邊看到綠色圓點。 這表示您的設定ID現在已啟用。 您也會看到其他選單選項出現。

![DSN](./images/c10.png)

您現在有2個選項：

- 如果您是使用現有設定啟用的現有使用者，請移至&#x200B;**0.1.3現有使用者 — 登入**
- 如果您是第一次啟動此教學課程的全新使用者，請移至&#x200B;**0.1.4註冊**&#x200B;並略過&#x200B;**0.1.3現有使用者 — 登入**

## 0.1.3現有使用者 — 登入

>[!IMPORTANT]
>
>練習&#x200B;**0.1.3現有的使用者 — 登入**&#x200B;只有在您是先前已註冊此教學課程的現有使用者時才有效。

如果您是首次設定此Chrome擴充功能的現有使用者，請按一下左側功能表中的紫色圖示。 您將會看到此訊息。

![DSN](./images/chromeret1.png)

視需要填寫值。

>[!IMPORTANT]
>
>**LDAP**&#x200B;是最重要的欄位：您應該使用您第一次註冊教學課程時所使用的LDAP。 這將確保您的進度成功載入。 如果您不確定您的LDAP是什麼，請檢視您的電子郵件地址。 將您電子郵件地址中@-symbol字之前的文字用作LDAP。 如果您的電子郵件地址是&#x200B;**techinsiders@adobe.com**，則您在此輸入的LDAP應該是&#x200B;**vangeluw**)。

![DSN](./images/chromeret2.png)

按一下&#x200B;**「確定」**。

![DSN](./images/chromeret3.png)

30秒至1分鐘後，您的熒幕將會變更，您將返回&#x200B;**首頁**，您將看到以下內容：

![DSN](./images/chromeret4.png)

您的Chrome擴充功能現已設定完畢，您現在可以驗證是否一切正常運作。

## 0.1.4新使用者 — 註冊

>[!IMPORTANT]
>
>練習&#x200B;**0.1.4新使用者 — 註冊**&#x200B;適用於首次開始此教學課程的新使用者。

如果您是第一次註冊本教學課程的新使用者，請按一下功能表中的黃色圖示。 您將會看到此訊息。

![DSN](./images/c11.png)

視需要填寫欄位。 按一下&#x200B;**儲存**。

>[!IMPORTANT]
>
>**LDAP**&#x200B;是最重要的欄位。 如果您不確定您的LDAP是什麼，請檢視您的電子郵件地址。 將您電子郵件地址中@-symbol字之前的文字用作LDAP。 如果您的電子郵件地址是&#x200B;**techinsiders@adobe.com**，則您在此輸入的LDAP應該是&#x200B;**vangeluw**)。

![DSN](./images/chrome1.png)

30秒至1分鐘後，您的熒幕將會變更，您將返回&#x200B;**首頁**，您將看到以下內容：

![DSN](./images/chrome2.png)

您的Chrome擴充功能現已設定完畢，您現在可以驗證是否一切正常運作。

## 0.1.5驗證教學課程內容

作為測試，請移至[此頁面](https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/module4/ex3.html?lang=en)。

您現在應該會看到根據Chrome擴充功能中的設定ID，所有&#x200B;**環境變數**&#x200B;都已取代為其true值。

您現在應該有類似下列的檢視，其中環境變數`--aepTenantId--`已由您的實際租使用者ID取代，在此案例中為&#x200B;**_experienceplatform**。

![DSN](./images/c12.png)

下一步： [0.2使用示範系統設定您的Adobe Experience Platform Data Collection使用者端屬性](./ex2.md)

[返回模組0](./getting-started.md)

[返回所有模組](./../../../overview.md)
