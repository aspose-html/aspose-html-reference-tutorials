---
date: 2026-01-02
description: 學習如何在 Java 中使用 Aspose.HTML 將 EPUB 轉換為 PDF，同時設定自訂 PDF 頁面大小及其他 PDF 儲存選項。
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 自訂 PDF 頁面尺寸：為 EPUB 轉 PDF 指定 PDF 儲存選項
url: /zh-hant/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 自訂 PDF 頁面尺寸：為 EPUB 轉 PDF 指定 PDF 儲存選項

## 簡介

Aspose.HTML for Java 讓 **將 EPUB 轉換為 PDF** 變得輕鬆，並提供完整的輸出控制，包括設定 **自訂 PDF 頁面尺寸**。在本分步指南中，我們將從環境準備到微調 `PdfSaveOptions`，確保產生的 PDF 符合您所需的精確頁面尺寸。無論您是在建構出版工作流程、線上學習平台，或只是需要自動化文件轉換，這裡的技巧都相當實用。

## 快速答覆
- **本教學的主要目的為何？** 將 EPUB 檔案轉換為 PDF，並套用自訂的 PDF 頁面尺寸。  
- **使用哪個函式庫？** Aspose.HTML for Java。  
- **需要授權嗎？** 提供免費試用版；正式環境需購買商業授權。  
- **可以變更背景顏色嗎？** 可以，透過 `PdfSaveOptions` 設定。  
- **支援 Java 8 以上嗎？** 完全支援——任何現代 Java 執行環境皆可使用。

## 什麼是自訂 PDF 頁面尺寸？

自訂 PDF 頁面尺寸允許您為輸出 PDF 的每一頁定義精確的寬度與高度，而不必受限於 A4、Letter 等標準尺寸。這在電子書、傳單或任何需要與特定設計稿匹配的版面配置時特別有用。

## 為什麼使用 Aspose.HTML 進行 EPUB 轉 PDF 轉換？

- **高保真度：** 完整保留複雜版面、字型與影像。  
- **細緻控制：** 透過 `PdfSaveOptions` 調整頁面尺寸、背景、邊距等。  
- **跨平台：** 同一段 Java 程式碼可在 Windows、Linux、macOS 上執行。  
- **效能佳：** 優化的渲染引擎提供快速轉換。

## 先決條件

在開始之前，請確保您已具備：

- **Java 開發環境：** 已安裝並設定 JDK 8 或更新版本。  
- **Aspose.HTML for Java：** 從[官方網站](https://releases.aspose.com/html/java/)下載最新 JAR。  
- **EPUB 檔案：** 準備好要轉換的 `.epub` 文件。  

一切就緒後，讓我們進入實際的轉換步驟。

## 步驟 1：開啟 EPUB 檔案

首先，我們需要使用 `FileInputStream` 開啟 EPUB 檔案。此串流稍後會傳遞給轉換器。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## 步驟 2：定義 PDF 儲存選項

在這裡設定 **自訂 PDF 頁面尺寸** 以及可選的背景顏色。請依需求調整像素值以符合目標尺寸。

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

### 小技巧：
- **像素 vs. 點數：** `Length.fromPixels` 會將螢幕像素轉換為 PDF 點數（1 點 = 1/72 吋）。請選擇能反映最終列印尺寸的數值。

## 步驟 3：將 EPUB 轉換為 PDF

當輸入串流與自訂選項準備完成後，呼叫轉換器。輸出的 PDF 會儲存至您指定的位置。

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## 完整原始碼

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

| 問題 | 原因 | 解決方法 |
|-------|-------|-----|
| **PDF 頁面為空白** | 轉換前輸入串流已關閉 | 保持 `try‑with‑resources` 區塊開啟，直到 `convertEPUB` 完成後才關閉。 |
| **頁面尺寸不正確** | 使用的像素值未對應到預期的列印尺寸 | 先將目標英吋轉換為點數（`1 inch = 72 points`），再使用 `Length.fromPixels` 轉為像素。 |
| **缺少字型** | EPUB 中未嵌入字型 | 確認字型已打包於 EPUB，或在執行主機上安裝應字型。 |

## 常見問題 (FAQs)

### Aspose.HTML for Java 是免費的嗎？
Aspose.HTML for Java 為商業授權的函式庫，但您可從其[官方網站](https://releases.aspose.com/)取得免費試用版。

### 支援哪些 EPUB 格式的轉換？
Aspose.HTML for Java 支援多種 EPUB 格式，確保與大多數 EPUB 文件相容。

### 我可以進一步自訂 PDF 輸出嗎？
可以，您可透過 `PdfSaveOptions` 調整頁面設定、背景顏色以及其他參數，以達到更細緻的客製化。

### 試用版有什麼限制？
試用版可能會有功能或輸出限制，建議查閱官方文件以取得最新資訊。

### 哪裡可以取得 Aspose.HTML for Java 的支援？
您可在 [Aspose.HTML 論壇](https://forum.aspose.com/)上尋求答案與技術支援。

---

**最後更新：** 2026-01-02  
**測試環境：** Aspose.HTML for Java 24.11（撰寫時的最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}