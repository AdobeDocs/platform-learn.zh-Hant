---
title: 將ACCS連線至AEM Assets CS
description: 將ACCS連線至AEM Assets CS
kt: 5342
doc-type: tutorial
exl-id: 2b944efe-3997-46a0-9eb0-61dfda67f5b9
source-git-commit: 7e0214226eaee0586d036d46de39c08046d43893
workflow-type: tm+mt
source-wordcount: '1688'
ht-degree: 1%

---

# 1.5.3將ACCS連線至AEM Assets CS

>[!IMPORTANT]
>
>為了完成此練習，您需要存取運作中的AEM Sites和Assets CS搭配EDS環境。
>
>如果您還沒有這樣的環境，請前往練習[Adobe Experience Manager Cloud Service和Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}。 按照這裡的指示操作，您將可以存取這樣的環境。

>[!IMPORTANT]
>
>如果您先前已使用AEM Sites和AEM CS環境設定Assets CS計畫，可能是您的AEM CS沙箱已休眠。 鑑於讓這樣的沙箱解除休眠需要10-15分鐘，最好現在開始解除休眠過程，這樣以後就不必等待了。

完成先前的練習後，您可能會看到ACCS將產品傳回至您的網站，但產品尚未顯示影像。 在本練習結束時，您應該也會看到傳回的影像。

![ACCS+AEM Sites](./images/accsaemsites11.png)

## 1.5.3.1更新管道設定

移至[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。 您應該選取的組織是`--aepImsOrgName--`。

按一下以開啟您的Cloud Manager程式，其名稱應類似以下其中一項：

- `--aepUserLdap-- - CitiSignal AEM+ACCS`
- 對於面對面技術實驗室會議： **技術內部人員 — AEM + ACCS XX** （將XX取代為指派給您的數字）
- 對於引導式隨選研討會：**隨選技術內部人員 — AEM + ACCS XX** （將XX取代為指派給您的數字）

![ACCS+AEM Assets](./images/accsaemassets1.png)

向下捲動一點，然後在&#x200B;**管道**&#x200B;索引標籤上按一下&#x200B;**存取存放庫資訊**。

![ACCS+AEM Assets](./images/accsaemassets2.png)

您應該會看到此訊息。 按一下&#x200B;**產生密碼**。

![ACCS+AEM Assets](./images/accsaemassets3.png)

再按一下&#x200B;**產生密碼**。

![ACCS+AEM Assets](./images/accsaemassets4.png)

之後，您應該會有可用的密碼。 接著，按一下&#x200B;**Git命令列**&#x200B;欄位旁的&#x200B;**複製**&#x200B;圖示。

![ACCS+AEM Assets](./images/accsaemassets5.png)

在電腦上選擇的位置建立新目錄，並將其命名為&#x200B;**AEM管道GitHub**。

![ACCS+AEM Assets](./images/accsaemassets6.png)

在資料夾上按一下滑鼠右鍵，然後選取&#x200B;**資料夾**&#x200B;的新終端機。

![ACCS+AEM Assets](./images/accsaemassets7.png)

您應該會看到此訊息。

![ACCS+AEM Assets](./images/accsaemassets8.png)

在「終端機」視窗中貼上您之前複製的&#x200B;**Git命令列**&#x200B;命令。

![ACCS+AEM Assets](./images/accsaemassets9.png)

您必須輸入使用者名稱。 從Cloud Manager的程式管道&#x200B;**存取存放庫資訊**&#x200B;複製使用者名稱，然後按下&#x200B;**Enter**。

![ACCS+AEM Assets](./images/accsaemassets10.png)

接下來，您必須輸入密碼。 從Cloud Manager的程式管道&#x200B;**Access存放庫資訊**&#x200B;複製密碼並按&#x200B;**Enter**。

![ACCS+AEM Assets](./images/accsaemassets11.png)

這可能需要一分鐘。 完成後，您將擁有連結至計畫管道的Git存放庫的本機副本。

![ACCS+AEM Assets](./images/accsaemassets12.png)

您會在&#x200B;**AEM管道GitHub**&#x200B;目錄中看到新目錄。 開啟該目錄。

![ACCS+AEM Assets](./images/accsaemassets13.png)

選取該目錄中的所有檔案，並刪除所有檔案。

![ACCS+AEM Assets](./images/accsaemassets14.png)

確定目錄是空的。

![ACCS+AEM Assets](./images/accsaemassets15.png)

移至[https://github.com/ankumalh/assets-commerce](https://github.com/ankumalh/assets-commerce)。 按一下&#x200B;**&lt;>代碼**，然後選取&#x200B;**下載ZIP**。 下載檔案，然後將其拖放到您的案頭上。

![ACCS+AEM Assets](./images/accsaemassets15a.png)

接著，將檔案&#x200B;**assets-commerce-main.zip**&#x200B;複製到您的案頭並解壓縮。 開啟資料夾&#x200B;**assets-commerce-main**。

![ACCS+AEM Assets](./images/accsaemassets16.png)

將所有檔案從目錄&#x200B;**assets-commerce-main**&#x200B;複製到您程式的Pipeline Repository目錄的空白目錄。

![ACCS+AEM Assets](./images/accsaemassets17.png)

接下來，開啟&#x200B;**Microsoft Visual Studio Code**，並在&#x200B;**Microsoft Visual Studio Code**&#x200B;中開啟包含您程式之管道存放庫的資料夾。

![ACCS+AEM Assets](./images/accsaemassets18.png)

前往左側功能表中的&#x200B;**搜尋**&#x200B;並搜尋`<my-app>`。 您需要以`<my-app>`取代所有出現的`techinsiderscitisignalaemaccs`。

按一下&#x200B;**全部取代**&#x200B;圖示。

![ACCS+AEM Assets](./images/accsaemassets19.png)

按一下&#x200B;**取代**。

![ACCS+AEM Assets](./images/accsaemassets20.png)

新檔案現在已準備好上傳回Git存放庫，該存放庫已連結至您的計畫的管道存放庫。 若要這麼做，請開啟資料夾&#x200B;**AEM Pipeline GitHub**，然後以滑鼠右鍵按一下包含新檔案的資料夾。 選取&#x200B;**資料夾**&#x200B;的新終端機。

![ACCS+AEM Assets](./images/accsaemassets21.png)

您應該會看到此訊息。 貼上下列命令並按&#x200B;**Enter**。

```
git add .
```

![ACCS+AEM Assets](./images/accsaemassets22.png)

您應該會看到此訊息。 貼上下列命令並按&#x200B;**Enter**。

```
git commit -m "add assets integration"
```

![ACCS+AEM Assets](./images/accsaemassets23.png)

您應該會看到此訊息。 貼上下列命令並按&#x200B;**Enter**。

```
git push origin main
```

![ACCS+AEM Assets](./images/accsaemassets24.png)

您應該會看到此訊息。 您的變更現在已部署到您計畫的管道Git存放庫。

![ACCS+AEM Assets](./images/accsaemassets25.png)

返回Cloud Manager並按一下&#x200B;**關閉**。

![ACCS+AEM Assets](./images/accsaemassets26.png)

在變更管道的Git存放庫後，您需要再次執行&#x200B;**部署至開發**&#x200B;管道。 按一下3個點&#x200B;**...**，然後選取&#x200B;**執行**。

![ACCS+AEM Assets](./images/accsaemassets27.png)

按一下&#x200B;**執行**。 執行管道部署可能需要10到15分鐘。 繼續之前，您需要等到管道部署成功完成。

![ACCS+AEM Assets](./images/accsaemassets28.png)

## 1.5.3.2啟用ACCS中的AEM Assets整合

返回ACCS執行個體。 在左側功能表中，移至&#x200B;**存放區**，然後選取&#x200B;**組態**。

![ACCS+AEM Assets](./images/accsaemassets49.png)

在功能表中向下捲動至&#x200B;**ADOBE SERVICES**，然後開啟&#x200B;**AEM Assets整合**。 您應該會看到此訊息。

![ACCS+AEM Assets](./images/accsaemassets50.png)

從&#x200B;**AEM環境**&#x200B;的下拉式清單中，選取您的環境。

然後，將&#x200B;**視覺化擁有者**&#x200B;設定為`AEM Assets` （視需要停用&#x200B;**使用系統值**&#x200B;核取方塊）。

然後，將&#x200B;**已啟用同步化**&#x200B;設定為`Yes` （視需要停用&#x200B;**使用系統值**&#x200B;核取方塊）。

請確定這些設定的設定如下：

- **資產比對規則**： `Match by product SKU`
- **依產品SKU屬性名稱比對**： `commerce:skus`

按一下&#x200B;**儲存設定**。

![ACCS+AEM Assets](./images/accsaemassets51.png)

您應該會看到此訊息。

![ACCS+AEM Assets](./images/accsaemassets52.png)

## 1.5.3.3更新config.json

前往設定AEM Sites CS/EDS環境時建立的GitHub存放庫。

在根目錄中，向下捲動並按一下以開啟檔案&#x200B;**config.json**。

您應該會在&#x200B;**config.json**&#x200B;檔案（此影像的第17行）中看到以下行，請確定它設定為&#x200B;**true**。

```json
 "commerce-assets-enabled": "true",
```

![ACCS+AEM Assets](./images/accsaemassets101.png)

如果&#x200B;**commerce-assets-enabled**&#x200B;的值設定為&#x200B;**false**，請更新您的檔案並將值設定為&#x200B;**true**。 然後，提交您的變更。

## 1.5.3.4驗證AEM Assets CS中的Commerce欄位

登入您的AEM CS Author環境並移至&#x200B;**Assets**。

![ACCS+AEM Assets](./images/accsaemassets30.png)

移至&#x200B;**檔案**。

![ACCS+AEM Assets](./images/accsaemassets31.png)

開啟&#x200B;**CitiSignal**&#x200B;資料夾。

![ACCS+AEM Assets](./images/accsaemassets32.png)

將游標暫留在任何資產上，然後按一下&#x200B;**資訊**&#x200B;圖示。

![ACCS+AEM Assets](./images/accsaemassets33.png)

您現在應該會看到包含2個新中繼資料屬性的&#x200B;**Commerce**&#x200B;標籤。

![ACCS+AEM Assets](./images/accsaemassets34.png)

您的AEM Assets CS環境現在支援Commerce整合。 您現在可以開始上傳產品影像。

## 1.5.3.4上傳產品Assets並連結至產品

[在此下載產品影像](./images/Product_Images.zip)。 下載後，將檔案匯出至您的案頭。

![ACCS+AEM Assets](./images/accsaemassets35.png)

按一下&#x200B;**建立**，然後選取&#x200B;**資料夾**。

![ACCS+AEM Assets](./images/accsaemassets36.png)

輸入欄位&#x200B;**Title**&#x200B;和&#x200B;**Name**&#x200B;的值&#x200B;**Product_Images**。 按一下&#x200B;**建立**。

![ACCS+AEM Assets](./images/accsaemassets37.png)

按一下以開啟您剛建立的資料夾。

![ACCS+AEM Assets](./images/accsaemassets38.png)

按一下&#x200B;**建立**，然後選取&#x200B;**檔案**。

![ACCS+AEM Assets](./images/accsaemassets39.png)

瀏覽至案頭上的&#x200B;**Product_Images**&#x200B;資料夾，選取所有檔案，然後按一下[開啟]。****

![ACCS+AEM Assets](./images/accsaemassets40.png)

按一下&#x200B;**上傳**。

![ACCS+AEM Assets](./images/accsaemassets41.png)

您的影像將可在您的資料夾中使用。 將滑鼠停留在產品&#x200B;**iPhone-Air-Light-Gold.png**&#x200B;上，然後按一下&#x200B;**屬性**&#x200B;圖示。

![ACCS+AEM Assets](./images/accsaemassets42.png)

向下捲動並將欄位&#x200B;**檢閱狀態**&#x200B;設定為&#x200B;**已核准**。 AEM Assets CS - ACCS整合僅適用於已核准的影像。

![ACCS+AEM Assets](./images/accsaemassets44.png)

向上捲動，移至&#x200B;**Commerce**&#x200B;標籤，然後按一下&#x200B;**產品SKU**&#x200B;下的&#x200B;**新增**。

![ACCS+AEM Assets](./images/accsaemassets45.png)

為此產品新增下列SKU：

| 索引鍵 | 價值 | 使用方式 |
|:-------------:| :---------------:| :---------------:|
| `iPhone-Air-Light-Gold` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Light-Gold-256GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Light-Gold-512GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Light-Gold-1TB` | `1` | `thumbnail, image, swatch_image, small_image` |

然後您應該擁有此專案。 按一下「**儲存並關閉**」。

![ACCS+AEM Assets](./images/accsaemassets46.png)

將滑鼠停留在產品&#x200B;**iPhone-Air-Space-Black.png**&#x200B;上，然後按一下&#x200B;**屬性**&#x200B;圖示。

![ACCS+AEM Assets](./images/accsaemassets47.png)

向下捲動並將欄位&#x200B;**檢閱狀態**&#x200B;設定為&#x200B;**已核准**。 AEM Assets CS - ACCS整合僅適用於已核准的影像。

![ACCS+AEM Assets](./images/accsaemassets48.png)

向上捲動，移至&#x200B;**Commerce**&#x200B;標籤，然後按一下&#x200B;**產品SKU**&#x200B;下的&#x200B;**新增**。

![ACCS+AEM Assets](./images/accsaemassets201.png)

為此產品新增下列SKU：

| 索引鍵 | 價值 | 使用方式 |
|:-------------:| :---------------:| :---------------:|
| `iPhone-Air-Space-Black` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Space-Black-256GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Space-Black-512GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Space-Black-1TB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air` | `1` | `thumbnail, image, swatch_image, small_image` |

然後您應該擁有此專案。 按一下「**儲存並關閉**」。

![ACCS+AEM Assets](./images/accsaemassets202.png)

將滑鼠停留在產品&#x200B;**iPhone-Air-Sky-Blue.png**&#x200B;上，然後按一下&#x200B;**屬性**&#x200B;圖示。

![ACCS+AEM Assets](./images/accsaemassets203.png)

向下捲動並將欄位&#x200B;**檢閱狀態**&#x200B;設定為&#x200B;**已核准**。 AEM Assets CS - ACCS整合僅適用於已核准的影像。

![ACCS+AEM Assets](./images/accsaemassets204.png)

向上捲動，移至&#x200B;**Commerce**&#x200B;標籤，然後按一下&#x200B;**產品SKU**&#x200B;下的&#x200B;**新增**。

![ACCS+AEM Assets](./images/accsaemassets205.png)

為此產品新增下列SKU：

| 索引鍵 | 價值 | 使用方式 |
|:-------------:| :---------------:| :---------------:|
| `iPhone-Air-Sky-Blue` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Sky-Blue-256GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Sky-Blue-512GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Sky-Blue-1TB` | `1` | `thumbnail, image, swatch_image, small_image` |

然後您應該擁有此專案。 按一下「**儲存並關閉**」。

![ACCS+AEM Assets](./images/accsaemassets206.png)

將滑鼠停留在產品&#x200B;**iPhone-Air-Cloud-White.png**&#x200B;上，然後按一下&#x200B;**屬性**&#x200B;圖示。

![ACCS+AEM Assets](./images/accsaemassets207.png)

向下捲動並將欄位&#x200B;**檢閱狀態**&#x200B;設定為&#x200B;**已核准**。 AEM Assets CS - ACCS整合僅適用於已核准的影像。

![ACCS+AEM Assets](./images/accsaemassets208.png)

向上捲動，移至&#x200B;**Commerce**&#x200B;標籤，然後按一下&#x200B;**產品SKU**&#x200B;下的&#x200B;**新增**。

![ACCS+AEM Assets](./images/accsaemassets209.png)

為此產品新增下列SKU：

| 索引鍵 | 價值 | 使用方式 |
|:-------------:| :---------------:| :---------------:|
| `iPhone-Air-Cloud-White` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Cloud-White-256GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Cloud-White-512GB` | `1` | `thumbnail, image, swatch_image, small_image` |
| `iPhone-Air-Cloud-White-1TB` | `1` | `thumbnail, image, swatch_image, small_image` |

然後您應該擁有此專案。 按一下「**儲存並關閉**」。

![ACCS+AEM Assets](./images/accsaemassets210.png)

現在，每個&#x200B;**iPhone Air**&#x200B;影像都應該有&#x200B;**豎起的綠色縮圖**，表示資產已核准。

![ACCS+AEM Assets](./images/accsaemassets250.png)

您現在應該使用下表，對其餘產品重複這些步驟。 別忘了核准每個影像，然後設定。 在&#x200B;**Commerce**&#x200B;標籤中的SKU設定底下。

| 產品名稱 | 索引鍵 | 價值 | 使用方式 |
|:-------------:|:-------------:| :---------------:| :---------------:|
| Apple Watch Ultra 3-Black | `Apple-Watch-Ultra-3-Black` | `1` | `thumbnail, image, swatch_image, small_image` |
| Apple Watch Ultra 3-Natural | `Apple-Watch-Ultra-3-Natural` | `1` | `thumbnail, image, swatch_image, small_image` |
| CitiSignal Fiber Max | `CitiSignal-Fiber-Max` | `1` | `thumbnail, image, swatch_image, small_image` |
| Apple One | `Apple-One` | `1` | `thumbnail, image, swatch_image, small_image` |
| YouTube Premium | `YouTube-Premium` | `1` | `thumbnail, image, swatch_image, small_image` |
| Disney Plus | `Disney` | `1` | `thumbnail, image, swatch_image, small_image` |
| Netflix + HBO Max | `Netflix-HBO-Max` | `1` | `thumbnail, image, swatch_image, small_image` |

之後，應該會核准您的所有影像。

![ACCS+AEM Assets](./images/accsaemassets251.png)

## 1.5.3.5驗證AEM Sites CS/EDS店面上的產品影像

>[!NOTE]
>
>成功部署您上述變更前，最多可能需要15分鐘的時間。 如果影像尚未顯示，請等待15分鐘，然後再試一次。

若要驗證整合是否有效，您需要開啟CitiSignal網站。

您應該會看到此訊息。 移至&#x200B;**電話**。

![ACCS+AEM Assets](./images/accsaemassets150.png)

接著您應該會看到顯示&#x200B;**iPhone Air**&#x200B;的產品影像。 按一下&#x200B;**iPhone Air**。

![ACCS+AEM Assets](./images/accsaemassets151.png)

您應該會看到此訊息。 變更色彩和儲存選項，您會看到影像會根據您所做的選擇動態變更。

![ACCS+AEM Assets](./images/accsaemassets152.png)

以下是將色彩變更為&#x200B;**Light-Gold**&#x200B;以及將儲存大小變更為&#x200B;**256GB**&#x200B;的範例。

![ACCS+AEM Assets](./images/accsaemassets153.png)

返回[Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}
