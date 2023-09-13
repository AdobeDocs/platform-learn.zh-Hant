---
title: 建立沙箱
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: 建立沙箱
description: 在本課程中，您將建立一個開發環境沙箱，並用於教學課程的其餘部分。
role: Data Architect, Data Engineer
feature: Sandboxes
jira: KT-4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: fdb6a49caa29d98d73524fd0887d25641ef67780
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# 建立沙箱

<!--25min-->

在本課程中，您將建立一個開發環境沙箱，並用於教學課程的其餘部分。

沙箱提供隔離的環境，您可以在其中試用功能而無須將資源和資料與您的生產環境混用在一起。 如需詳細資訊，請參閱 [沙箱檔案](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=zh-Hant).

**資料架構師** 和 **資料工程師** 將需要在本教學課程之外建立沙箱。

在開始練習之前，請觀看此短片，以進一步瞭解沙箱：
>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

## 需要的許可權

在 [設定許可權](configure-permissions.md) 課程，您已設定完成本課程所需的所有存取控制項。

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## 建立沙箱

讓我們建立沙箱：

1. 登入 [Adobe Experience Platform](https://experience.adobe.com/platform) 介面
1. 前往 **[!UICONTROL 沙箱]** 在左側導覽列中
1. 選取 **[!UICONTROL 建立沙箱]** 在右上方
   ![選取「建立沙箱」](assets/sandbox-createSandbox.png)

1. 選取 **[!UICONTROL 開發]** 作為 **[!UICONTROL 型別]**
1. 為您的沙箱命名 `luma-tutorial` （考慮將您的名稱新增至結尾）
1. 為教學課程加上標題 `Luma Tutorial` （考慮將您的名稱新增至結尾）
1. 選取 **[!UICONTROL 建立]** 按鈕
   ![建立您的沙箱](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >雖然您可以使用任何任意值作為沙箱名稱和標題，但建議您遵循建議的值，因為在本教學課程中，我們將會參考這些標籤。 如果您的組織有多人完成本教學課程，請考慮在沙箱標題和名稱的結尾新增您的名稱，例如luma-tutorial-ignatiusjreilly。

建立沙箱大約需要30秒，在此期間「[!UICONTROL 建立]「狀態會顯示。 沙箱完全建立後，會顯示為&quot;[!UICONTROL 作用中]「：
![作用中狀態](assets/sandbox-active.png)

等到您的沙箱是&quot;[!UICONTROL 作用中]」，然後再繼續進行下一個練習。

## 將新沙箱新增到角色

沙箱一旦作用中，您就必須將其納入您的角色中才能使用。 若要將其新增至您的角色（需要系統管理員或產品管理員許可權）：

1. 前往 [!UICONTROL 許可權] 畫面
1. 開啟 `Luma Tutorial Platform` 角色
1. 選擇性 _移除_ 此 `Prod` 角色中的沙箱
1. 新增 `Luma Tutorial` 沙箱
1. 選取 **[!UICONTROL 儲存]**
1. 在 [!UICONTROL 沙箱] 列，選取 **[!UICONTROL 編輯]**

   ![新增Luma教學課程](assets/sandbox-addLumaTutorial.png)

1. 重新載入（或按住Shift鍵重新載入）頁面，而您現在應位於 `Luma Tutorial` 沙箱，或它應該出現在您的沙箱下拉式清單中
1. 切換至 `Luma Tutorial` 沙箱（如果尚未存在）

   ![確認沙箱](assets/sandbox-confirmDropdown.png)

太好了，您已建立沙箱並準備好 [設定開發人員控制檯和Postman](set-up-developer-console-and-postman.md)！
