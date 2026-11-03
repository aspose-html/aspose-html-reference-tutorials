---
date: 2026-05-30
description: 了解如何在 Java 中使用 Aspose.HTML 將 EPUB 轉換為 PDF，並設定自訂 PDF 頁面尺寸及其他 PDF 儲存選項。
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: 為 EPUB 轉 PDF 指定 PDF 儲存選項
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: 自訂 PDF 頁面尺寸 - 為 EPUB 轉 PDF 指定 PDF 儲存選項
url: /zh-hant/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 自訂 PDF 頁面尺寸：為 EPUB 轉 PDF 指定 PDF 儲存選項

## 介紹

Aspose.HTML for Java 讓您輕鬆 **convert EPUB to PDF**，並且完全掌控輸出內容，包括設定 **custom PDF page size**。在本步驟指南中，我們將逐步說明您需要的所有操作——從環境準備到調整 `PdfSaveOptions`，使產生的 PDF 符合您所要求的精確頁面尺寸。無論您是構建出版流程、e‑learning 平台，或只是需要自動化文件轉換，這裡的技巧都相當有用。

## 快速解答
- **本教學的主要目的為何？** 將 EPUB 檔案轉換為 PDF，並套用自訂的 PDF 頁面尺寸。  
- **使用哪個函式庫？** Aspose.HTML for Java。  
- **需要授權嗎？** 提供免費試用版；正式環境需購買商業授權。  
- **可以變更背景顏色嗎？** 是的，使用 `PdfSaveOptions`。  
- **支援 Java 8 以上嗎？** 絕對支援——任何現代的 Java 執行環境皆可。  

## 什麼是自訂 PDF 頁面尺寸？

自訂 PDF 頁面尺寸讓您能夠為輸出 PDF 的每一頁定義精確的寬度與高度，而不必依賴 A4 或 Letter 等標準尺寸。  
您可以以點 (1 point = 1/72 inch) 設定尺寸，或從像素轉換，從而對最終版面擁有像素級的精確控制。這對於電子書、傳單，或任何必須符合預先定義格式且不想手動後製的設計都相當理想。

## 為何使用 Aspose.HTML 進行 EPUB 轉 PDF 轉換？

Aspose.HTML 只需兩行程式碼即可將 EPUB 轉換為 PDF，且能保留複雜版面、內嵌字型與高解析度影像。它支援 **50+ 輸入與輸出格式**，可渲染高達 **2,000 頁** 的 PDF 而不必將整個檔案載入記憶體，且可在 Windows、Linux 與 macOS 上執行，結果完全相同。此函式庫亦提供細緻的 PDF 儲存選項，讓您從 Java 調整頁面尺寸、背景顏色、邊距與壓縮設定。

## 前置條件
- **Java 開發環境：** 已安裝並設定 JDK 8 或更新版本。  
- **Aspose.HTML for Java：** 從[網站](https://releases.aspose.com/html/java/)下載最新的 JAR。  
- **EPUB 檔案：** 您想要轉換的 `.epub` 文件。  

現在所有準備就緒，讓我們深入實際的轉換步驟。

## 如何使用自訂頁面尺寸將 EPUB 轉換為 PDF？

`FileInputStream` 是 Java 用來讀取檔案原始位元的類別。  
`PdfSaveOptions` 是 Aspose.HTML 中用來設定 PDF 輸出選項（如頁面尺寸與背景顏色）的類別。  
使用 `FileInputStream` 載入您的 EPUB，設定 `PdfSaveOptions` 以指定精確的頁面尺寸，然後呼叫轉換器。以下的三步工作流程可在一般電子書大小下於一分鐘內完成轉換，且對於更大型的集合只需少量程式碼變更即可擴展。

### 步驟 1：開啟 EPUB 檔案

首先，建立指向來源 `.epub` 的 `FileInputStream`。在轉換完成前保持串流開啟，可避免出現「空白頁」錯誤。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### 步驟 2：定義 PDF 儲存選項

`PdfSaveOptions` 是 Aspose.HTML 的設定類別，用於控制 PDF 輸出設定，如頁面尺寸、背景顏色與邊距。  
`Length.fromPixels` 可將螢幕像素轉換為 PDF 點 (1 point = 1/72 inch)，讓您以熟悉的像素單位指定尺寸。

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

#### 專業提示：
- **像素 vs. 點：** `Length.fromPixels` 將螢幕像素轉換為 PDF 點 (1 point = 1/72 inch)。選擇能反映最終列印尺寸的數值。

### 步驟 3：將 EPUB 轉換為 PDF

在輸入串流與自訂選項準備就緒後，呼叫轉換器。輸出的 PDF 會儲存至您指定的位置，並保留您設定的精確頁面尺寸。

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` 是一個在 PDF 轉換過程中啟用頁面平行處理的方法。

## 完整原始碼

完整且可執行的範例將上述三個步驟合併於單一 Java 類別。請將佔位路徑替換為您自己的檔案位置。

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## 常見問題與解決方案

| 問題 | 原因 | 解決方式 |
|-------|-------|-----|
| **PDF 頁面為空白** | 轉換前輸入串流已關閉 | 在 `convertEPUB` 之後仍保持 `try‑with‑resources` 區塊開啟。 |
| **頁面尺寸不正確** | 使用的像素未對應到所需的列印尺寸 | 先將所需英吋轉換為點 (`1 inch = 72 points`)，再使用 `Length.fromPixels` 轉為像素。 |
| **缺少字型** | 字型未嵌入於 EPUB 中 | 確保字型已打包於 EPUB 內，或在主機上安裝相應字型。 |
| **大型書籍效能下降** | 逐頁順序渲染 | 透過 `PdfSaveOptions.setEnableParallelProcessing(true)` 啟用多執行緒渲染，以加速 500 頁以上 EPUB 的處理。 |

## 常見問與答 (FAQs)

**問：Aspose.HTML for Java 是免費函式庫嗎？**  
A: Aspose.HTML for Java 為商業函式庫，但您可從其[網站](https://releases.aspose.com/)取得免費試用版。

**問：支援哪些 EPUB 格式的轉換？**  
A: Aspose.HTML for Java 支援 EPUB 2.0、EPUB 3.0 與 EPUB 3.1，能處理可重排與固定版面的書籍，並完整支援 CSS。

**問：我可以進一步自訂 PDF 輸出嗎？**  
A: 可以，您可透過 `PdfSaveOptions` 調整頁面設定、背景顏色、壓縮等其他參數，以自訂 PDF 輸出。

**問：Aspose.HTML for Java 試用版有什麼限制嗎？**  
A: 試用版可能在前幾頁加上浮水印，且最大檔案大小限制為 10 MB；購買授權即可移除這些限制。

**問：我可以從哪裡取得 Aspose.HTML for Java 的支援？**  
A: 您可於 [Aspose.HTML 論壇](https://forum.aspose.com/)尋找答案與取得支援。

---

**最後更新：** 2026-05-30  
**測試環境：** Aspose.HTML for Java 24.11（撰寫時的最新版本）  
**作者：** Aspose

## 相關教學

- [使用 Aspose.HTML for Java 調整 PDF 頁面尺寸](/html/java/advanced-usage/adjust-pdf-page-size/)
- [如何使用 Aspose.HTML 以 Java 轉換 EPUB 為 PDF](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [使用 Aspose.HTML for Java 轉換 EPUB 為 PDF 與影像](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}