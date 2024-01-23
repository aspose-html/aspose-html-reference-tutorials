---
title: 使用 Aspose.HTML for Java 調整 XPS 頁面大小
linktitle: 調整 XPS 頁面大小
second_title: 使用 Aspose.HTML 進行 Java HTML 處理
description: 了解如何使用 Aspose.HTML for Java 調整 XPS 頁面大小。輕鬆控制 XPS 文件的輸出尺寸。
type: docs
weight: 16
url: /zh-hant/java/advanced-usage/adjust-xps-page-size/
---

在本教學中，我們將引導您完成使用 Aspose.HTML for Java 調整 XPS 頁面大小的過程。這個功能強大的程式庫可讓您操作 HTML 文件並將其呈現為各種格式，包括 XPS。當您需要控制 XPS 文件的輸出尺寸時，調整頁面尺寸至關重要。

## 先決條件

在我們開始之前，請確保您具備以下先決條件：

1. Java 開發環境：確保您的系統上安裝了 Java 開發工具包 (JDK)。

2.  Aspose.HTML for Java 程式庫：您需要下載 Aspose.HTML for Java 程式庫並將其包含在您的 Java 專案中。你可以找到圖書館[這裡](https://releases.aspose.com/html/java/).

3. 輸入 HTML 檔案：準備要渲染的 HTML 檔案並調整 XPS 頁面大小。您可以在本教學中使用自己的 HTML 檔案。

## 導入包

首先，您需要匯入必要的套件才能使用 Aspose.HTML for Java。在 Java 類別的開頭包含這些套件：

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## 第1步：設定輸入檔名

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    //……
}
```

在此步驟中，我們使用`FileInputStream`.

## 第 2 步：建立 HTML 文件並設定樣式

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

//……
```

此步驟涉及建立一個`HTMLDocument`並向其添加樣式。

## 第 3 步：建立 XPS 渲染選項

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

在這裡，我們建立 XPS 渲染選項來配置渲染過程。

## 步驟 4：調整頁面大小

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

此步驟涉及設定頁面大小並指定是否將其調整為最寬頁面。

## 第 5 步：渲染輸出

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

在最後一步中，我們使用配置的選項來渲染 XPS 輸出。

## 結論

在本教學中，我們向您展示如何使用 Aspose.HTML for Java 調整 XPS 頁面大小。您可以控制 XPS 文件的輸出尺寸，確保它們符合您的特定要求。透過提供的程式碼和步驟，您可以在 Java 應用程式中輕鬆實現此功能。

如果您有任何疑問或需要進一步協助，請隨時訪問[Aspose.HTML for Java 文檔](https://reference.aspose.com/html/java/)或尋求協助[Aspose論壇](https://forum.aspose.com/).

## 常見問題解答

### Q1：什麼是 Java 版 Aspose.HTML？

A1：Aspose.HTML for Java 是一個 Java 函式庫，可讓開發人員操作 HTML 文件並將其轉換為各種格式，例如 XPS、PDF 和映像。

### Q2：哪裡可以下載 Aspose.HTML for Java？

 A2：您可以從下列位置下載 Aspose.HTML for Java 程式庫：[這個連結](https://releases.aspose.com/html/java/).

### 問題 3：Aspose.HTML for Java 是否有免費試用版？

 A3：是的，您可以從以下位置獲得 Aspose.HTML for Java 的免費試用版：[這裡](https://releases.aspose.com/).

### Q4：如何取得 Aspose.HTML for Java 的臨時授權？

 A4：若要取得 Aspose.HTML for Java 的臨時許可證，請造訪[這一頁](https://purchase.aspose.com/temporary-license/).

### Q5：我可以獲得 Aspose.HTML for Java 的支援嗎？

 A5：是的，您可以向Aspose社群尋求協助和支持[Aspose論壇](https://forum.aspose.com/).