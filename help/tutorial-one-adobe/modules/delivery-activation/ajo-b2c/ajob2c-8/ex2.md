---
title: 建立您的協調行銷活動
description: 建立您的協調行銷活動
kt: 5342
doc-type: tutorial
exl-id: f3ca3230-db30-4e41-91f1-9324b12211a6
source-git-commit: 0328260e8699107bc82103af98caae684319a60d
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 2%

---

# 3.8.2建立您的協調行銷活動

## 3.8.2.1建立您的協調行銷活動

前往&#x200B;**行銷活動**。 按一下&#x200B;**建立行銷活動**。

![AJO OC](./images/ajooc1.png)

選取&#x200B;**協調流程 — 行銷**，然後按一下&#x200B;**確認**。

![AJO OC](./images/ajooc2.png)

輸入行銷活動名稱： `--aepUserLdap-- - CitiSignal Family Account Optimization Campaign`並按一下&#x200B;**儲存**。

![AJO OC](./images/ajooc3.png)

您應該會看到此訊息。 按一下&#x200B;**+**&#x200B;圖示。

![AJO OC](./images/ajooc4.png)

選取&#x200B;**分支**。

![AJO OC](./images/ajooc5.png)

### 建立對象1

按一下&#x200B;**+**&#x200B;圖示，然後選取&#x200B;**建置對象**。

![AJO OC](./images/ajooc6.png)

按一下以開啟&#x200B;**目標維度**&#x200B;的資料夾。

![AJO OC](./images/ajooc7.png)

選取&#x200B;**`--aepUserLdap--_citisignal_recipients`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc8.png)

按一下&#x200B;**建立對象**。

![AJO OC](./images/ajooc9.png)

按一下&#x200B;**新增條件**。

![AJO OC](./images/ajooc10.png)

選取&#x200B;**recipient_type**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc11.png)

在&#x200B;**`account_holder`**&#x200B;值&#x200B;**欄位中輸入**&#x200B;並按一下&#x200B;**計算**。

![AJO OC](./images/ajooc12.png)

您應該會看到&#x200B;**設定檔目標**&#x200B;的數字。 按一下灰色區域中的某處，如圖所示。

![AJO OC](./images/ajooc13.png)

按一下&#x200B;**新增條件**。

![AJO OC](./images/ajooc14.png)

向下鑽研至&#x200B;**`citisignal_accounts`**。

![AJO OC](./images/ajooc15.png)

選取&#x200B;**`account_status`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc16.png)

在&#x200B;**`active`**&#x200B;值&#x200B;**欄位中輸入**。 然後，按一下灰色區域中的某處（如指示）。

![AJO OC](./images/ajooc17.png)

按一下&#x200B;**新增條件**。

![AJO OC](./images/ajooc18.png)

向下鑽研至&#x200B;**`citisignal_mobile_subscriptions`**。

![AJO OC](./images/ajooc19.png)

選取&#x200B;**`subscription_id`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc20.png)

啟用&#x200B;**彙總資料**&#x200B;的切換器。 然後選取下列專案：

- **彙總函式**： **計數**
- **運運算元**： **大於或等於**
- **值**： **1**

按一下「**確認**」。

![AJO OC](./images/ajooc21.png)

您應該會看到此訊息。 按一下「**確認**」。

![AJO OC](./images/ajooc22.png)

### 建立對象2

按一下另一個路徑中下一個節點上的&#x200B;**+**&#x200B;圖示。

![AJO OC](./images/ajooc23.png)

選取&#x200B;**建立對象**。

![AJO OC](./images/ajooc24.png)

按一下以開啟&#x200B;**目標維度**&#x200B;的資料夾。

![AJO OC](./images/ajooc25.png)

選取&#x200B;**`--aepUserLdap--_mobile_subscriptions`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc26.png)

按一下&#x200B;**建立對象**。

![AJO OC](./images/ajooc27.png)

按一下&#x200B;**新增條件**。

![AJO OC](./images/ajooc28.png)

選取&#x200B;**subscription_status**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc29.png)

在&#x200B;**`active`**&#x200B;值&#x200B;**欄位中輸入**。 然後，按一下&#x200B;**新增條件**。

![AJO OC](./images/ajooc30.png)

選取&#x200B;**`is_upgrade_eligible`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc31.png)

將&#x200B;**值**&#x200B;設為&#x200B;**true**

![AJO OC](./images/ajooc32.png)

按一下&#x200B;**計算**，檢視符合此對象資格的設定檔預估值。 然後，按一下&#x200B;**確認**

![AJO OC](./images/ajooc33.png)

### 分割

按一下&#x200B;**+**&#x200B;圖示，然後選取&#x200B;**分割**。

![AJO OC](./images/ajooc34.png)

將欄位&#x200B;**標籤**&#x200B;變更為&#x200B;**90/10處理方式vs控制項**。 按一下以開啟物件&#x200B;**子集**。

![AJO OC](./images/ajooc35.png)

為&#x200B;**啟用限制**&#x200B;啟用切換器，並將&#x200B;**限制大小**&#x200B;設定為&#x200B;**10次近**。

![AJO OC](./images/ajooc36.png)

按一下&#x200B;**新增區段**，然後您應該會看到正在新增的&#x200B;**Result**&#x200B;物件。

按一下&#x200B;**儲存**。

![AJO OC](./images/ajooc37.png)

### 儲存客群

按一下&#x200B;**+**&#x200B;圖示，然後選取&#x200B;**儲存對象**。

![AJO OC](./images/ajooc38.png)

將欄位&#x200B;**對象標籤**&#x200B;設定為&#x200B;**`--aepUserLdap-- - Control Group`**。 按一下&#x200B;**新增對象對應**。

![AJO OC](./images/ajooc39.png)

向下展開至&#x200B;**目標維度**。

![AJO OC](./images/ajooc40.png)

選取&#x200B;**`account_id`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc41.png)

將&#x200B;**設定檔對應欄位**&#x200B;設定為&#x200B;**`--aepUserLdap--_citisignal_recipients - account_id`**。

![AJO OC](./images/ajooc41a.png)

### 擴充：網際網路訂閱

按一下&#x200B;**+**&#x200B;圖示。

![AJO OC](./images/ajooc42.png)

選取&#x200B;**擴充**。

![AJO OC](./images/ajooc43.png)

您應該會看到此訊息。 按一下「**新增擴充資料**」。

![AJO OC](./images/ajooc44.png)

向下鑽研至&#x200B;**`Targeting dimension`**。

![AJO OC](./images/ajooc44a.png)

向下鑽研至&#x200B;**`citisignal_accounts`**。

![AJO OC](./images/ajooc45.png)

向下鑽研至&#x200B;**`citisignal_internet_subscriptions`**。

![AJO OC](./images/ajooc45a.png)

選取&#x200B;**`account_id`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc46.png)

您應該會看到此訊息。 按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc47.png)

選取&#x200B;**`subscription_status`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc48.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc49.png)

選取&#x200B;**`connection_type`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc50.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc51.png)

選取&#x200B;**`service_city`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc52.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc53.png)

選取&#x200B;**`avg_bandwidth_usage_gb`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc54.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc55.png)

選取&#x200B;**`data_cap_gb`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc56.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc57.png)

選取&#x200B;**`advertised_speed_mbps`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc58.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc59.png)

選取&#x200B;**`monthly_recurring_charge`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc60.png)

按一下&#x200B;**儲存**。

![AJO OC](./images/ajooc61.png)

向上捲動並將欄位&#x200B;**標籤**&#x200B;變更為`Enrichment: Internet Subscription`。

![AJO OC](./images/ajooc61a.png)

### 擴充：行動裝置訂閱

按一下下一個節點上的&#x200B;**+**&#x200B;圖示，然後選取&#x200B;**擴充**。

![AJO OC](./images/ajooc62.png)

將欄位&#x200B;**標籤**&#x200B;變更為`Enrichment: Mobile Devices Subscription`，然後按一下&#x200B;**新增擴充資料**。

![AJO OC](./images/ajooc63.png)

向下展開至&#x200B;**目標維度**。

![AJO OC](./images/ajooc64.png)

向下鑽研至&#x200B;**`citisignal_accounts`**。

![AJO OC](./images/ajooc65.png)

向下鑽研至&#x200B;**`citisignal_mobile_subscriptions`**。

![AJO OC](./images/ajooc65a.png)

選取&#x200B;**`phone_number`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc66.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc67.png)

向下鑽研至&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc68.png)

選取&#x200B;**`model`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc68a.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc69.png)

向下鑽研至&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc69a.png)

選取&#x200B;**`recommended_device_model`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc70.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc71.png)

向下鑽研至&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc71a.png)

選取&#x200B;**`is_upgrade_eligible`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc72.png)

您現在可以執行測試回合，以測試進度，並檢視行銷活動中可用的資料。

儲存您的變更，然後按一下[開始]。**&#x200B;**

![AJO OC](./images/ajooctest1.png)

一段時間後，您應該會看到此訊息。 按一下&#x200B;**預覽結果**。

![AJO OC](./images/ajooctest2.png)

之後，您應該會看到類似以下內容。 按一下 **關閉**。

![AJO OC](./images/ajooctest3.png)

返回節點&#x200B;**擴充：行動裝置訂閱**。

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc73.png)

選取&#x200B;**`account_id`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc74.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc75.png)

選取&#x200B;**`subscription_id`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc76.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc77.png)

選取&#x200B;**`renewal_eligibility_date`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc78.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc79.png)

選取&#x200B;**`line_user_recipient_id`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc80.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc81.png)

選取&#x200B;**`current_device_id`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc82.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc86.png)

選取&#x200B;**`contract_start_date`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc87.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc89.png)

向下鑽研至&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc90.png)

選取&#x200B;**`manufacturer`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc91.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc92.png)

向下鑽研至&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc93.png)

選取&#x200B;**`device_age_months`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc94.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc95.png)

向下鑽研至&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc96.png)

選取&#x200B;**`trade_in_value`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc97.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc98.png)

向下鑽研至&#x200B;**`citisignal_equipment_subscriptions`**。

![AJO OC](./images/ajooc99.png)

選取&#x200B;**`monthly_payment`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc100.png)

### 擴充：行動裝置訂閱

然後您應該擁有此專案。 按一下&#x200B;**「儲存」**。然後，按一下&#x200B;**+**&#x200B;圖示以新增節點，並選取&#x200B;**擴充**。

![AJO OC](./images/ajooc101.png)

您應該會看到此訊息。 按一下「**新增擴充資料**」。

![AJO OC](./images/ajooc102.png)

向下展開至&#x200B;**目標維度**。

![AJO OC](./images/ajooc103.png)

向下鑽研至&#x200B;**`citisignal_offer_eligibility`**。

![AJO OC](./images/ajooc104.png)

向下鑽研至&#x200B;**`citisignal_offers`**。

![AJO OC](./images/ajooc105.png)

選取&#x200B;**`offer_name`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc106.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc107.png)

向下鑽研至&#x200B;**`citisignal_offers`**。

![AJO OC](./images/ajooc108.png)

選取&#x200B;**`offer_code`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc109.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc110.png)

向下鑽研至&#x200B;**`citisignal_offers`**。

![AJO OC](./images/ajooc111.png)

選取&#x200B;**`offer_description`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc112.png)

按一下&#x200B;**新增屬性**。

![AJO OC](./images/ajooc110.png)

向下鑽研至&#x200B;**`citisignal_offers`**。

![AJO OC](./images/ajooc113.png)

選取&#x200B;**`offer_description`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc114.png)

開啟&#x200B;**啟用排序**。

![AJO OC](./images/ajooc115.png)

向下鑽研至&#x200B;**`citisignal_offers`**。

![AJO OC](./images/ajooc116.png)

選取&#x200B;**`offer_priority`**&#x200B;並按一下&#x200B;**確認**。

![AJO OC](./images/ajooc117.png)

您現在可以測試行銷活動。 按一下「**開始**」。

![AJO OC](./images/ajooc118.png)

一段時間後，您應該會看到這個訊息。 按一下&#x200B;**結果**，然後選取&#x200B;**預覽結果**。

![AJO OC](./images/ajooc120.png)

之後，您應該會看到類似以下內容。

![AJO OC](./images/ajooc121.png)

### 電子郵件活動

按一下&#x200B;**+**&#x200B;圖示，然後選取&#x200B;**電子郵件**。

![AJO OC](./images/ajooc122.png)

按一下&#x200B;**編輯電子郵件**。

![AJO OC](./images/ajooc123.png)

移至&#x200B;**動作**。

![AJO OC](./images/ajooc124.png)

選取您之前建立的&#x200B;**電子郵件通道設定**，然後按一下&#x200B;**編輯內容**。

![AJO OC](./images/ajooc125.png)

針對&#x200B;**主旨列**，貼上以下內容：

`{{target.--aepUserLdap--_citisignal_recipients.first_name}}, Your CitiSignal Family Account Summary`

按一下&#x200B;**編輯電子郵件內文**。

![AJO OC](./images/ajooc126.png)

## 後續步驟

返回[Adobe Journey Optimizer：協調的行銷活動](./ajocampaigns.md){target="_blank"}

返回[所有模組](./../../../../overview.md){target="_blank"}
