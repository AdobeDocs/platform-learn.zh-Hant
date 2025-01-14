---
title: 建立變數資料元素
description: 新增將根據多個規則建置的資料元素，然後將其傳送至Edge Network並轉送至Adobe Analytics
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16759
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# 建立變數資料元素

新增將根據多個規則建置的資料元素，然後將其傳送至Edge Network並轉送至Adobe Analytics。

此資料元素會建立「資料」物件，其將用於將Adobe Analytics變數（prop、eVar、事件等）傳回Adobe Analytics和Adobe Target。 因此，就像在Analytics的AppMeasurement實作中建立「s物件」一樣，我們會建立此型別：變數物件，以跨規則存取和更新，且可用於將prop和eVar填入Analytics。

1. 在資料收集介面中，按一下左側導覽中的&#x200B;**資料元素**。

   您將被帶往資料元素登陸頁面，您將在其中看到所有預先存在的資料元素。 我們需要建立新的資料元素來協助移轉。 按一下&#x200B;**新增資料元素**。

   ![新增資料元素](assets/add-new-data-alement.jpg)

1. 設定您的資料元素。
   1. 隨意命名您的資料元素 — 有助於您記住這正在頁面上建置資料，且這將會是「變數」型別。 在本教學課程中，我們將它稱為&#x200B;**頁面檢視資料變數**。
   1. 從「擴充功能」下拉式清單中選取&#x200B;**Adobe Experience Platform Web SDK**。
   1. 從&#x200B;**資料元素型別**&#x200B;下拉式清單中選取&#x200B;**變數**。
   1. 在右側面板中，選取&#x200B;**資料**&#x200B;選項按鈕。
   1. 檢查&#x200B;**Adobe Analytics**&#x200B;解決方案，以及您要移轉的其他解決方案，例如此熒幕擷圖中顯示的&#x200B;**Adobe Target**。
1. 按一下&#x200B;**儲存**。

   ![設定變數資料元素](assets/configure-variable-data-element.jpg)
