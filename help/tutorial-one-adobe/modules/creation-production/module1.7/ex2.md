---
title: 以程式設計方式執行您的自訂工作流程
description: 以程式設計方式執行您的自訂工作流程
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: a3a78b12f8244c8288eb0fffc82ad769776eb118
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# 1.7.2以程式設計方式執行自訂工作流程

## 1.7.2.1使用Postman執行您的自訂工作流程

在上一個練習發佈工作流程後，您應該會看到類似這樣的內容。 按一下&#x200B;**複製**&#x200B;按鈕以複製範例承載。

![Firefly自訂工作流程](./images/ffcw61.png)

開啟Postman並使用名稱&#x200B;**Firefly自訂工作流程**&#x200B;建立新的&#x200B;**集合**。 然後，按一下&#x200B;**新增要求**。

![Firefly自訂工作流程](./images/ffcw62.png)

之後，您應該會看到新的空白請求。 在位址列中，貼上您從已發佈工作流程複製的裝載。

Postman將可辨識您貼上的cURL命令，且會從裝載中取得所有資訊，並以正確方式將其新增至請求中。

![Firefly自訂工作流程](./images/ffcw63.png)

您現在應該會看到這些&#x200B;**標題**&#x200B;變數。

![Firefly自訂工作流程](./images/ffcw64.png)

移至&#x200B;**內文**，您應該會看到類似此內容。

![Firefly自訂工作流程](./images/ffcw65.png)

您現在需要在此要求的內文中提供必要指示。 以程式設計方式處理檔案時，需要使用預先簽署的URL。 在本練習中，您可以在下方找到本練習中3個影像的預設URL。 這些預先簽署的URL是使用Microsoft Azure儲存功能建立的。 如果您想深入瞭解如何建立預先簽署的URL，請參閱此處： [使用Microsoft Azure和預先簽署的URL最佳化Firefly程式](./../module1.1/ex2.md)。

在本練習中，您可以使用以下URL，如此您就不需要自行建立新的預先簽署URL。

- **airpods.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D
```

- **watch.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/watch.jpg?sv=2023-01-03&st=2026-03-11T01%3A26%3A54Z&se=2027-03-12T01%3A26%3A00Z&sr=b&sp=r&sig=xCwQ09E%2F%2FT%2B7RLcb31Fum4uUBfsX0xHITKZTz4Ds9Zs%3D
```

- **phone.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/phone.png?sv=2023-01-03&st=2026-03-11T01%3A27%3A20Z&se=2027-03-12T01%3A27%3A00Z&sr=b&sp=r&sig=VVbX88P2sFSHHo9lmgoRhXRIXb42c0nDQhM9Z8nUG%2Bc%3D
```

您還需要在Postman請求中提供提示。 以下是您可以使用的提示。

- **提示1**：

```
magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts
```

- **提示2**：

```
background hearts fluttering
```

以下是裝載範例，但您無法複製並重複使用它，因為&#x200B;**node_id**&#x200B;欄位是工作流程所獨有的，所以這只是為了讓您瞭解裝載看起來是什麼樣子：

```json
{
    "workflow": {
        "workflowId": "e0c63806-cf7c-442d-8884-26d57e9c0518",
        "inputs": [
            [
                {
                    "node_id": "node_1772156869527_d8mjasues_1_u10dlg",
                    "content": [
                        {
                            "presignedUrl": "https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D",
                            "storageType": "Azure"
                        }
                    ]
                },
                {
                    "node_id": "node_1772157264659_oq2csr2nn_5_fh5hek",
                    "content": "magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts"
                },
                {
                    "node_id": "node_1772157397147_qdwxiyktg_8_nm0o2k",
                    "content": "background hearts fluttering"
                }
            ]
        ]
    }
}
```

變更您的裝載後，看起來應該像這樣。 完成後，按一下&#x200B;**傳送**。 然後，使用&#x200B;**CMD + S**&#x200B;或&#x200B;**CTRL + S**&#x200B;來&#x200B;**儲存**&#x200B;您的請求。

![Firefly自訂工作流程](./images/ffcw66.png)

在回應裝載中，您現在可以找到數個連結。 這些連結可以查詢工作流程的&#x200B;**狀態**，一旦狀態為&#x200B;**已完成**，您就可以使用&#x200B;**結果** URL來擷取產生的影像和視訊。

選取&#x200B;**狀態** URL並加以複製。

![Firefly自訂工作流程](./images/ffcw67.png)

按一下您目前使用之請求上的3個點，然後選取&#x200B;**複製**。

![Firefly自訂工作流程](./images/ffcw69.png)

在新要求中，將要求型別變更為&#x200B;**GET**，並以您剛複製的狀態URL取代URL。

![Firefly自訂工作流程](./images/ffcw70.png)

在&#x200B;**內文**&#x200B;下，確定所有內容都已刪除。 然後，按一下&#x200B;**傳送**。 接著，您應會收到類似的回應裝載，當中會顯示狀態。 您可以重新傳送此要求，直到狀態變更為&#x200B;**已完成**。 別忘了使用&#x200B;**CMD + S**&#x200B;或&#x200B;**CTRL + S**&#x200B;來&#x200B;**儲存**&#x200B;您的請求。

![Firefly自訂工作流程](./images/ffcw71.png)

返回第一個&#x200B;**POST**&#x200B;要求。 現在複製&#x200B;**結果** URL。

![Firefly自訂工作流程](./images/ffcw72.png)

在您建立的第二個要求上按一下3個點&#x200B;**...**，然後選取&#x200B;**複製**。

![Firefly自訂工作流程](./images/ffcw73.png)

在新要求中，貼上您複製的&#x200B;**結果** URL，然後按一下&#x200B;**傳送**。 別忘了使用&#x200B;**CMD + S**&#x200B;或&#x200B;**CTRL + S**&#x200B;來&#x200B;**儲存**&#x200B;您的請求。

![Firefly自訂工作流程](./images/ffcw74.png)

向下捲動回應裝載中，您可在這裡找到已建立影像和視訊的參照。 按一下連結以開啟這些檔案。

![Firefly自訂工作流程](./images/ffcw75.png)

以下是產生的影像。

![Firefly自訂工作流程](./images/ffcw76.png)

## 1.7.2.2使用Workfront Fusion執行您的自訂工作流程

移至[https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}。 開啟&#x200B;**Workfront Fusion**。

![WF Fusion](./images/wffusion1.png)

移至&#x200B;**案例**。 如果您還沒有資料夾，請建立資料夾，並針對資料夾名稱使用： `--aepUserLdap--`。 選取您的資料夾，然後選取&#x200B;**建立新情境**。

![WF Fusion](./images/wffusion2.png)

您應該會看到此訊息。

![WF Fusion](./images/wffusion3.png)

在上一個練習發佈工作流程後，您應該會看到類似這樣的內容。 按一下&#x200B;**複製**&#x200B;按鈕以複製範例承載。

![Firefly自訂工作流程](./images/ffcw61.png)

返回Workfront Fusion情境。 使用&#x200B;**CMD + V**&#x200B;或&#x200B;**CTRL + V**&#x200B;將您複製的裝載貼到情境中。 Workfront Fusion將會自動偵測cURL要求，並將建立新的&#x200B;**HTTP — 自動提出要求**&#x200B;模組。

將&#x200B;**clock**&#x200B;圖示拖曳至&#x200B;**HTTP — 提出要求**&#x200B;模組。

![WF Fusion](./images/wffusion5.png)

您應該會看到此訊息。 按一下&#x200B;**HTTP — 提出要求**&#x200B;模組以開啟。

![WF Fusion](./images/wffusion6.png)

之後，您應該會看到&#x200B;**Header**&#x200B;變數已經可用。

![WF Fusion](./images/wffusion7.png)

向下捲動以檢視預設裝載。 按一下所示的&#x200B;**圖示**，美化JSON裝載。

![WF Fusion](./images/wffusion8.png)

返回Postman，前往第一個&#x200B;**POST**&#x200B;請求。 複製裝載。

![WF Fusion](./images/wffusion9.png)

返回Workfront Fusion情境。 以您從Postman複製的裝載取代現有的預設裝載。 按一下所示的&#x200B;**圖示**，美化JSON裝載。

核取&#x200B;**剖析回應**&#x200B;的核取方塊。

按一下&#x200B;**「確定」**。

![WF Fusion](./images/wffusion10.png)

儲存您的變更，然後按一下[執行一次] ****。

![WF Fusion](./images/wffusion11.png)

一旦您的案例執行後，您會看到類似您在Postman中的回應。 有了這些可在Workfront Fusion中使用的資訊，您現在可以建置它來輪詢&#x200B;**狀態** URL，直到狀態完成為止，而且一旦發生此情況，您就可以使用&#x200B;**結果** URL來收集產生的影像和視訊。

![WF Fusion](./images/wffusion12.png)

## 後續步驟

返回[Firefly自訂工作流程](./workflowbuilder.md){target="_blank"}

返回[所有模組](./../../../overview.md){target="_blank"}
