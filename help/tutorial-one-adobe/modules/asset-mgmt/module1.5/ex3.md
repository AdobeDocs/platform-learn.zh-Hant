---
title: 將ACCS連線至AEM Assets CS
description: 將ACCS連線至AEM Assets CS
kt: 5342
doc-type: tutorial
source-git-commit: ca895385f5c1f318a7c4d0b338dcfa4e91763005
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 0%

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

## 1.5.3.1更新管道設定

移至[https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}。 您應該選取的組織是`--aepImsOrgName--`。

按一下以開啟您的Cloud Manager程式，程式應該稱為`--aepUserLdap-- - CitiSignal AEM+ACCS`。

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

移至[https://github.com/ankumalh/assets-commerce](https://github.com/ankumalh/assets-commerce)。

接著，將檔案&#x200B;**assets-commerce-main.zip**&#x200B;複製到您的案頭並解壓縮。 開啟資料夾&#x200B;**assets-commerce-main**。

![ACCS+AEM Assets](./images/accsaemassets16.png)

將所有檔案從目錄&#x200B;**assets-commerce-main**&#x200B;複製到您程式的Pipeline Repository目錄的空白目錄。

![ACCS+AEM Assets](./images/accsaemassets17.png)

接下來，開啟&#x200B;**Microsoft Visual Studio Code**，並在&#x200B;**Microsoft Visual Studio Code**&#x200B;中開啟包含您程式之管道存放庫的資料夾。

![ACCS+AEM Assets](./images/accsaemassets18.png)

前往左側功能表中的&#x200B;**搜尋**&#x200B;並搜尋`<my-app>`。 您需要以`<my-app>`取代所有出現的`--aepUserLdap--citisignalaemaccs`。

按一下&#x200B;**全部取代**&#x200B;圖示。

![ACCS+AEM Assets](./images/accsaemassets19.png)

按一下&#x200B;**取代**。

![ACCS+AEM Assets](./images/accsaemassets20.png)

新檔案現在已準備好上傳回Git存放庫，該存放庫已連結至您的計畫的管道存放庫。 若要這麼做，請開啟資料夾&#x200B;**AEM Pipeline GitHub**，然後以滑鼠右鍵按一下包含新檔案的資料夾。 選取&#x200B;**資料夾**&#x200B;的新終端機。

![ACCS+AEM Assets](./images/accsaemassets21.png)

您應該會看到此訊息。 貼上命令`git add .`並按&#x200B;**Enter**。

![ACCS+AEM Assets](./images/accsaemassets22.png)

您應該會看到此訊息。 貼上命令`git commit -m "add assets integration"`並按&#x200B;**Enter**。

![ACCS+AEM Assets](./images/accsaemassets23.png)

您應該會看到此訊息。 貼上命令`git push origin main`並按&#x200B;**Enter**。

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

填寫下列變數：

- **AEM Assets方案ID**：您可以從AEM CS作者URL取得方案ID。 在此範例中，計畫識別碼為`166717`。

![ACCS+AEM Assets](./images/accsaemassets50a.png)

- **AEM Assets環境ID**：您可以從AEM CS作者URL取得環境ID。 在此範例中，環境識別碼為`1786231`。

![ACCS+AEM Assets](./images/accsaemassets50b.png)

- **資產選擇器IMS使用者端ID**：設定為`1`
- **同步處理已啟用**：設定為`Yes`
- **視覺效果擁有者**：設定為`AEM Assets`
- **資產比對規則**： `Match by product SKU`
- **依產品SKU屬性名稱比對**： `commerce:skus`

按一下&#x200B;**儲存設定**。

![ACCS+AEM Assets](./images/accsaemassets51.png)

## 1.5.3.3更新config.json

前往設定AEM Sites CS/EDS環境時建立的GitHub存放庫。 該存放庫是在練習[1.1.2中建立的，用來設定您的AEM CS環境](./../../../modules/asset-mgmt/module2.1/ex3.md){target="_blank"}，名稱應該是&#x200B;**citisignal-aem-accs**。

在根目錄中，向下捲動並按一下以開啟檔案&#x200B;**config.json**。 按一下&#x200B;**編輯**&#x200B;圖示以變更檔案。

![ACCS+AEM Assets](./images/accsaemassets101.png)

在第5 `"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/XXX/graphql",`行下方新增下列程式碼片段：

```json
 "commerce-assets-enabled": "true",
```

按一下&#x200B;**認可變更……**。

![ACCS+AEM Assets](./images/accsaemassets102.png)

按一下&#x200B;**認可變更**。

![ACCS+AEM Assets](./images/accsaemassets103.png)

您的變更現在已儲存，很快就會發佈。 可能需要幾分鐘時間，變更才會顯示在店面上。

![ACCS+AEM Assets](./images/accsaemassets104.png)

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

您的影像將可在您的資料夾中使用。

![ACCS+AEM Assets](./images/accsaemassets42.png)

按一下第一個產品影像以開啟。

![ACCS+AEM Assets](./images/accsaemassets43.png)

將產品影像的狀態設定為&#x200B;**已核准**。 AEM Assets CS - ACCS整合僅適用於已核准的影像。

![ACCS+AEM Assets](./images/accsaemassets44.png)

移至&#x200B;**Commerce**&#x200B;標籤，然後按一下&#x200B;**產品SKU**&#x200B;下的&#x200B;**新增**。

![ACCS+AEM Assets](./images/accsaemassets45.png)

從影像檔案名稱取得產品SKU，將值增加到1，並在&#x200B;**使用狀況**&#x200B;下拉式清單中選取所有選項。

![ACCS+AEM Assets](./images/accsaemassets46.png)

然後您應該擁有此專案。 按一下&#x200B;**儲存並關閉**。

![ACCS+AEM Assets](./images/accsaemassets47.png)

重複此動作，核准資產並為您匯入此資料夾的每個影像設定Commerce標籤。 完成後，每個影像都應該有&#x200B;**綠色的拇指向上**，表示資產已核准。

![ACCS+AEM Assets](./images/accsaemassets48.png)

## 1.5.3.5驗證AEM Sites CS/EDS店面上的產品影像



下一步： [摘要與優點](./summary.md){target="_blank"}

返回[Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[返回所有模組](./../../../overview.md){target="_blank"}
