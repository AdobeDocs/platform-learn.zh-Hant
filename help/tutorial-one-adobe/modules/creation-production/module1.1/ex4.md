---
title: Firefly自訂模型API
description: 使用Firefly自訂模型API
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 330f4492-d0df-4298-9edc-4174b0065c9a
source-git-commit: a1da1c73cbddacde00211190a1ca3d36f7a2c329
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---

# 1.1.4 Firefly自訂模型API

## 1.1.4.1什麼是Firefly自訂模型？

透過Firefly自訂模型，您可以使用「文字轉換影像」功能產生與品牌一致的影像變化。 透過使用您自己的影像來訓練這些模型，您可以產生可反映您品牌身分識別的內容。
轉換您的風格或主題以探索新概念、視覺化不同的環境、產生創新內容，並根據特定區段量身打造內容。

使用Firefly自訂模型，您可以……

- 建立品牌內創意和概念
- 產生具有一致樣式的字元主題
- 建立一致的品牌樣式以快速擴展行銷活動

為了達成此目的，Firefly自訂模型支援：

- 自訂主題模型
- 自訂樣式模型

### 自訂主題模型

在訓練特定主題（無論是物件或字元）的自訂模型時，目標是識別主題的基本功能，並幫助模型在不同內容與位置中複製它們。

訓練主旨模型時，請尋找具有以下特性的影像：

- 物件一致性：提供和您的主旨具有相同品牌和模型的影像，同時確保主旨在不同影像間看起來不會有很大差異。 避免混合多種顏色，並確保影像間有共同的主題或模式。 不過，您的主旨可能會因場景、姿勢、服裝和背景而異。
- 物件焦點：使用焦點清晰的主旨影像，而不會造成不必要的干擾。 將主題保持在影像中心附近，並確定它至少佔據影像區域的25%。
- 環境前後關聯：提供不同檢視和前後關聯中的主體影像，以各種照明條件顯示。 雖然可以使用白色或透明背景的影像，但最好還是與更複雜的環境混合。
- 避免使用其他物件：避免在背景中使用大型專案或與字元關聯的大型專案。 模型會記憶影像中顯示的任何大型專案，且該專案會出現在產生的影像中，類似於訓練資料集中的相同專案。

### 自訂樣式模型

接受樣式訓練的自訂模型將識別資產的外觀與風格，以在提示時產生類似的影像。

若要訓練有效的樣式模型，請執行下列動作：

- 提供類似的美學：包含顯示各種場景和物件的影像，同時保持相同的外觀和風格。
- 使用各種影像：使用儘可能多的影像，以防止模型過多地聚焦在不需要的物件或主體上。
- 避免任何固定片語：固定圖樣的權重比其他片語大。 例如，如果每個註解都包含「背景為純黑色」或「可愛的卡通樣式」，則模型將取決於這個片語，任何沒有它的測試提示將不會產生想要的結果。

## 1.1.4.2設定您的自訂模型

移至[https://firefly.adobe.com/](https://firefly.adobe.com/)。 按一下&#x200B;**自訂模型**。

![Firefly自訂模型](./images/ffcm1.png){zoomable="yes"}

您可能會看到此訊息。 如果是，請按一下[同意]****&#x200B;繼續。

![Firefly自訂模型](./images/ffcm2.png){zoomable="yes"}

您應該會看到此訊息。 按一下&#x200B;**訓練模型**。

![Firefly自訂模型](./images/ffcm3.png){zoomable="yes"}

設定下列欄位：

- **名稱**：使用`--aepUserLdap-- - Citi Signal Router Model`
- **訓練模式**：選取&#x200B;**主題（技術預覽）**
- **概念**：輸入`router`
- **儲存至**：開啟下拉式清單，然後按一下&#x200B;**+建立新專案**

![Firefly自訂模型](./images/ffcm4.png){zoomable="yes"}

為新專案命名： `--aepUserLdap-- - Custom Models`。 按一下&#x200B;**建立**。

![Firefly自訂模型](./images/ffcm5.png){zoomable="yes"}

您應該會看到此訊息。 按一下&#x200B;**繼續**。

![Firefly自訂模型](./images/ffcm6.png){zoomable="yes"}

您現在需要提供參考影像，以訓練自訂模型。 按一下&#x200B;**從您的電腦選取影像**。

![Firefly自訂模型](./images/ffcm7.png){zoomable="yes"}

在[這裡](https://tech-insiders.s3.us-west-2.amazonaws.com/CitiSignal_router.zip)下載參考影像。 將下載檔案解壓縮，這會為您提供此資訊。

![Firefly自訂模型](./images/ffcm8.png){zoomable="yes"}

導覽至包含下載影像檔案的資料夾。 全部選取並按一下&#x200B;**開啟**。

![Firefly自訂模型](./images/ffcm9.png){zoomable="yes"}

然後您會看到正在載入影像。

![Firefly自訂模型](./images/ffcm10.png){zoomable="yes"}

幾分鐘後，您的影像就會正確載入。 您可能會看到部分影像發生錯誤，這是因為影像的標題尚未產生或長度不足。 檢閱每個有錯誤的影像，並輸入符合要求的註解及描述影像。

![Firefly自訂模型](./images/ffcm11.png){zoomable="yes"}

一旦所有影像都有符合要求的註解，您仍需要提供範例提示。 輸入任何使用&#39;router&#39;字樣的提示。 完成後，您可以開始訓練您的模型。 按一下&#x200B;**訓練**。

![Firefly自訂模型](./images/ffcm12.png){zoomable="yes"}

您將會看到此訊息。 訓練您的模型可能需要20到30分鐘或更長的時間。

![Firefly自訂模型](./images/ffcm13.png){zoomable="yes"}

20-30分鐘後，您的模型現在已訓練完畢，可以發佈。 按一下&#x200B;**發佈**。

![Firefly自訂模型](./images/ffcm14.png){zoomable="yes"}

再按一下&#x200B;**發佈**。

![Firefly自訂模型](./images/ffcm15.png){zoomable="yes"}

關閉&#x200B;**共用自訂模型**&#x200B;快顯視窗。

![Firefly自訂模型](./images/ffcm16.png){zoomable="yes"}

## 1.1.4.3在UI中使用您的自訂模型

移至[https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train)。 按一下「自訂模型」以開啟。

![Firefly自訂模型](./images/ffcm19.png){zoomable="yes"}

按一下&#x200B;**預覽和測試**。

![Firefly自訂模型](./images/ffcm17.png){zoomable="yes"}

之後，您將會看到在執行之前輸入的範例提示。

![Firefly自訂模型](./images/ffcm18.png){zoomable="yes"}

## 1.1.4.4啟用Firefly Services自訂模型API的自訂模型

您的自訂模型培訓完成後，也可以透過API使用。 在練習1.1.1中，您已設定您的Adobe I/O專案，以透過API與Firefly服務互動。

移至[https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train)。 按一下「自訂模型」以開啟。

![Firefly自訂模型](./images/ffcm19.png){zoomable="yes"}

按一下3個點&#x200B;**...**，然後按一下&#x200B;**共用**。

![Firefly自訂模型](./images/ffcm20.png){zoomable="yes"}

若要存取Firefly自訂模型，該自訂模型必須與Adobe I/O專案的&#x200B;**技術帳戶電子郵件**&#x200B;共用。

若要擷取您的&#x200B;**技術帳戶電子郵件**，請移至[https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)。 按一下以開啟名為`--aepUserLdap-- One Adobe tutorial`的專案。

![Firefly自訂模型](./images/ffcm24.png){zoomable="yes"}

按一下&#x200B;**OAuth伺服器對伺服器**。

![Firefly自訂模型](./images/ffcm25.png){zoomable="yes"}

按一下以複製您的&#x200B;**技術帳戶電子郵件**。

![Firefly自訂模型](./images/ffcm23.png){zoomable="yes"}

貼上您的&#x200B;**技術帳戶電子郵件**&#x200B;並按一下&#x200B;**邀請編輯**。

![Firefly自訂模型](./images/ffcm21.png){zoomable="yes"}

**技術帳戶電子郵件**&#x200B;現在應該能夠存取自訂模型。

![Firefly自訂模型](./images/ffcm22.png){zoomable="yes"}

## 1.1.4.5與Firefly Services自訂模型API互動

在練習1.1.1開始使用Firefly Services時，您將此檔案： [postman-ff.zip](./../../../assets/postman/postman-ff.zip)下載至您的本機案頭，然後將該集合匯入Postman。

開啟Postman並前往資料夾&#x200B;**FF — 自訂模型API**。

![Firefly自訂模型](./images/ffcm30.png){zoomable="yes"}

開啟要求&#x200B;**1。 FF - getCustomModels**&#x200B;並按一下&#x200B;**傳送**。

![Firefly自訂模型](./images/ffcm31.png){zoomable="yes"}

您應該會看到您之前建立的自訂模型（名為`--aepUserLdap-- - Citi Signal Router Model`）做為回應的一部分。 欄位&#x200B;**assetId**&#x200B;是您的自訂模型的唯一識別碼，將在下一個請求中參照。

![Firefly自訂模型](./images/ffcm32.png){zoomable="yes"}

開啟要求&#x200B;**2。 非同步**&#x200B;產生影像。 在此範例中，您將要求根據自訂模型產生2個變數。 請隨時更新此例中為`a white router on a volcano in Africa`的提示。

按一下&#x200B;**傳送**。

![Firefly自訂模型](./images/ffcm33.png){zoomable="yes"}

回應包含欄位&#x200B;**jobId**。 產生這2個影像的工作正在執行，您可以使用下一個請求來檢查狀態。

![Firefly自訂模型](./images/ffcm34.png){zoomable="yes"}

開啟要求&#x200B;**3。 取得CM狀態**&#x200B;並按一下&#x200B;**傳送**。 之後，您應該會看到狀態已設為「執行中」。

![Firefly自訂模型](./images/ffcm35.png){zoomable="yes"}

幾分鐘後，再按一下請求&#x200B;**3的**&#x200B;傳送&#x200B;**。 取得CM狀態**。 之後，您應該會看到狀態變更為&#x200B;**succeeded**，而且輸出中應該會看到兩個影像URL。 按一下以開啟兩個檔案。

![Firefly自訂模型](./images/ffcm36.png){zoomable="yes"}

這是此範例產生的第一個影像。

![Firefly自訂模型](./images/ffcm37.png){zoomable="yes"}

這是此範例產生的第二個影像。

![Firefly自訂模型](./images/ffcm38.png){zoomable="yes"}

您現在已經完成此練習。

## 後續步驟

移至[摘要與優點](./summary.md){target="_blank"}

返回[使用Photoshop API](./ex3.md){target="_blank"}

返回[Adobe Firefly Services概觀](./firefly-services.md){target="_blank"}
