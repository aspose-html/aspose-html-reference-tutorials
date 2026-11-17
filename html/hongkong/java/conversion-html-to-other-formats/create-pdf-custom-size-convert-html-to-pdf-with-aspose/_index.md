---
category: general
date: 2026-03-26
description: 使用 Aspose.HTML for Java 從 HTML 建立自訂尺寸的 PDF。了解如何將 HTML 轉換為 PDF，並在幾個步驟內設定
  PDF 頁面尺寸。
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: zh-hant
og_description: 使用 Aspose 從 HTML 建立自訂尺寸 PDF。本指南將示範如何將 HTML 轉換為 PDF、變更 PDF 頁面尺寸，以及輕鬆設定
  PDF 頁面尺寸。
og_title: 建立自訂尺寸 PDF – 快速指南：將 HTML 轉換為 PDF
tags:
- aspose
- java
- pdf
- html
title: 建立自訂尺寸 PDF – 使用 Aspose 將 HTML 轉換為 PDF
url: /zh-hant/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立自訂尺寸 PDF – 使用 Aspose 將 HTML 轉換為 PDF

有沒有需要從 HTML 檔案 **建立自訂尺寸 PDF**？在本教學中，我們將示範如何 **將 HTML 轉換為 PDF**，並使用 Aspose.HTML for Java 設定 PDF 頁面尺寸。  

如果您正在製作發票、報告或電子書，精確的頁面尺寸相當重要——否則版面會偏移或被截斷。  

我們會一步步說明，從載入原始 HTML、微調邊距，到產生可直接使用的 PDF。沒有模糊的參考，只有完整、可執行的範例，您今天就能直接複製貼上使用。

## 您需要的環境

- **Java 17**（或任何較新的 JDK）。  
- **Aspose.HTML for Java** JAR 檔案 – 您可從 Maven 套件庫或 Aspose 官方網站取得最新版本。  
- 一個簡單的 `input.html` 檔案，放置於您可控制的資料夾中。  
- 您慣用的 IDE 或文字編輯器；我通常使用 IntelliJ IDEA，但 Eclipse 也同樣適用。

具備這些前置條件即可避免在執行過程中遇到「class not found」錯誤。  

現在，讓我們深入探討。

![建立自訂尺寸 PDF 範例](/images/create-pdf-custom-size.png "螢幕截圖顯示使用自訂頁面尺寸與邊距產生的 PDF – create pdf custom size")

## 建立自訂尺寸 PDF – 核心步驟

以下是最終的完整 Java 程式碼。您可以將它複製到名為 `ConvertHtmlToPdfCustomPage.java` 的檔案中，並在加入 Aspose 相依套件後執行。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### 步驟 1 – 將 HTML 轉換為 PDF：載入文件

首先，我們 **載入要轉換成 PDF 的 HTML**。  
`HTMLDocument` 會讀取檔案、解析相對連結，並建立 Aspose 可渲染的 DOM。  

> **為什麼重要：** 若 HTML 內引用了 CSS 或圖片，Aspose 會依檔案路徑相對取得。使用絕對路徑 (`YOUR_DIRECTORY/input.html`) 可避免「找不到檔案」的意外。

### 步驟 2 – 更改 PDF 頁面尺寸：設定選項

這裡我們建立一個 `PdfConversionOptions` 物件。  
- `setPageSize(PageSize.A4)` 告訴 Aspose 使用標準 A4 尺寸（210 × 297 mm）。  
- `setPageOrientation(...)` 若需要橫向則翻轉頁面。  
- `setMargins(new Margin(20, 20, 20, 20))` 為每一側設定 20 點的邊距。  

您可以將 `PageSize.A4` 換成 `PageSize.LETTER`，甚至傳入 `SizeF` 物件自行定義 **自訂尺寸**，例如：

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **小技巧：** 1 點等於 1/72 英吋。若習慣以毫米計算，乘以 2.83465 即可得到點數。

### 步驟 3 – 從 HTML 產生 PDF：執行轉換

`Converter.convertHTML` 承擔主要工作。它接收已載入的 `HTMLDocument`、輸出路徑以及剛才設定的選項。  

若想根據內容動態 **設定 PDF 頁面尺寸**，可在此步驟前先計算所需尺寸，然後調整 `pdfOptions`。

### 步驟 4 – 驗證結果

`System.out.println` 行為可有可無，但在控制台執行程式時能快速提供回饋。執行完畢後，開啟 `custom_page.pdf` – 您應該會看到一個 A4 直向 PDF，四邊均為 20 點的均勻邊距，正如我們所指定的。

## 將 HTML 轉換為 PDF – 常見變化

### 使用串流取代檔案路徑

有時候沒有實體檔案；HTML 可能來自資料庫或 API。此時可將字串包裝成 `ByteArrayInputStream`：

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

第二個參數是用來解析相對資源的基礎 URL。

### 更改頁面方向

若報表較寬，切換為橫向：

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### 微調邊距

邊距接受浮點數值，您可以設定 0.5 pt 以得到極細的邊框：

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### 處理大型 HTML 檔案

面對巨量文件時，建議啟用 **記憶體效能串流**：

```java
pdfOptions.setUseMemoryCache(true);
```

這會指示 Aspose 將中間資料寫入暫存檔，而非全部保留在 RAM 中。

## 設定 PDF 頁面尺寸 – 邊緣情況與陷阱

- **缺少字型：** 若 HTML 使用的自訂字型未安裝於伺服器，PDF 會退回預設字型。可使用 `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);` 內嵌字型。  
- **影像縮放：** 高解析度影像會使 PDF 體積膨脹。使用 `pdfOptions.setImageResolution(150);` 可在保留品質的同時降低解析度。  
- **CSS 相容性：** 並非所有 CSS 屬性皆受支援。建議使用標準布局技術（flexbox 可用，grid 可能有怪異行為）。  
- **路徑權限：** 確保執行程序對 `YOUR_DIRECTORY` 具有寫入權限，否則會拋出 `IOException`。

## 預期輸出

執行程式會產生如下概念圖所示的 PDF：

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- 頁面尺寸：**A4**（210 × 297 mm）。  
- 方向：**Portrait**（直向）。  
- 邊距：每側 **20 pt**。  

使用任何 PDF 閱讀器（Adobe Reader、Chrome 等）開啟檔案即可確認。

## 總結

您現在已掌握如何使用 Aspose.HTML for Java 從 HTML 來源 **建立自訂尺寸 PDF**。本教學涵蓋了完整流程：**將 HTML 轉換為 PDF**、**更改 PDF 頁面尺寸**、**設定 PDF 頁面尺寸**，以及使用自訂邊距 **從 HTML 產生 PDF**。  

歡迎自行實驗——將 `PageSize.LETTER` 換成 Legal 尺寸、調整邊距，或內嵌自己的字型。接下來，您可以探索 **加入浮水印**、**加密 PDF**，或 **批次處理多個 HTML 檔案**。所有這些主題皆建立在我們剛剛討論的核心概念上。  

對特定邊緣情況有疑問嗎？在下方留言，我會協助您排除問題。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}