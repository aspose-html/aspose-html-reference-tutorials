---
title: 使用 Aspose.HTML for Java 調整 PDF 頁面大小
linktitle: 調整 PDF 頁面大小
second_title: 使用 Aspose.HTML 進行 Java HTML 處理
description: 了解如何使用 Aspose.HTML for Java 調整 PDF 頁面大小。輕鬆從 HTML 創建高品質的 PDF。有效控制頁面尺寸。
type: docs
weight: 15
url: /zh-hant/java/advanced-usage/adjust-pdf-page-size/
---

在當今的數位時代，從 HTML 內容產生高品質 PDF 的需求不斷增加。 Aspose.HTML for Java 是一個功能強大的 Java 程式庫，可讓您輕鬆地將 HTML 文件轉換為 PDF 格式。在本教程中，我們將重點介紹使用 Aspose.HTML for Java 將 HTML 轉換為 PDF 時調整頁面大小。

## 先決條件

在開始之前，請確保您具備以下先決條件：

- Java 開發環境：確保您的系統上安裝了 Java 開發工具包 (JDK)。
-  Aspose.HTML for Java：您需要從網站下載並安裝Aspose.HTML for Java[這裡](https://releases.aspose.com/html/java/).
- HTML 文件：您應該有一個可供轉換的 HTML 文件。如果沒有，請建立一個或使用現有的 HTML 檔案。

## 導入包

首先，您需要匯入必要的套件才能使用 Aspose.HTML for Java。以下程式碼片段示範如何執行此操作：

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

現在您已經具備了先決條件並導入了必要的包，讓我們將調整 PDF 頁面大小的過程分解為多個步驟：

## 第 1 步：讀取 HTML 內容

首先，您需要閱讀要轉換為 PDF 的 HTML 內容。在此範例中，我們將從名為「FirstFile.html」的檔案中讀取 HTML。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## 第 2 步：編寫 HTML 內容

接下來，您將 HTML 內容寫入名為「FirstFileOut.html」的檔案。

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    //在此處新增自訂 HTML 樣式或內容
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## 第 3 步：將 HTML 渲染為 PDF

現在，您將把 HTML 內容呈現為 PDF 檔案。我們將介紹兩種場景：一種是頁面大小未根據內容寬度進行調整，另一種是進行調整。

### 頁面尺寸未調整

在這種情況下，頁面大小設定為固定的寬度和高度，如果超過這些尺寸，可能會裁切內容。

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

//從 HTML 檔案建立 HTMLDocument 實例
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

//設定 PDF 渲染選項
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//渲染輸出
pdf_renderer.render(device, html_document);
```

### 根據內容寬度調整頁面大小

在這種情況下，頁面大小會根據內容寬度進行調整。

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//渲染輸出
pdf_renderer.render(device, html_document);
```

## 結論

在本教學中，我們探討如何使用 Aspose.HTML for Java 將 HTML 轉換為 PDF 時調整 PDF 頁面大小。您已經了解了先決條件，匯入了所需的套件，並按照逐步指南完成了此任務。使用 Aspose.HTML for Java，您可以輕鬆控制生成的 PDF 的頁面大小，確保您的內容按預期顯示。

請隨意嘗試不同的頁面大小和設置，以滿足您的特定要求。如果您遇到任何問題或有其他疑問，請隨時尋求協助[Aspose.HTML for Java 文檔](https://reference.aspose.com/html/java/)或者[Aspose 支援論壇](https://forum.aspose.com/).

## 常見問題解答

### Q1：什麼是 Java 版 Aspose.HTML？

A1：Aspose.HTML for Java 是一個 Java 函式庫，可讓您處理 HTML 文件、操作、轉換並將其呈現為各種格式，包括 PDF。

### Q2: 使用 Aspose.HTML for Java 將 HTML 轉換為 PDF 時如何調整 PDF 頁面大小？

 A2：您可以使用`PageSetup`類別並設定`AdjustToWidestPage`財產給`true`或“假”，取決於您的要求。

### 問題 3：在將 HTML 內容轉換為 PDF 之前，我可以自訂其樣式嗎？

A3：是的，您可以透過在將 HTML 內容轉換為 PDF 之前新增 CSS 和 HTML 元素來自訂樣式，如教學課程所示。

### Q4：在哪裡可以找到 Aspose.HTML for Java 的文檔？

 A4：可以參考文檔[這裡](https://reference.aspose.com/html/java/)獲取全面的資訊和範例。

### Q5：Aspose.HTML for Java 有免費試用版嗎？

 A5：是的，您可以存取 Aspose.HTML for Java 的免費試用版：[這個連結](https://releases.aspose.com/).