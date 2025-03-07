---
title: 指定 EPUB 到 PDF 的 PDF 儲存選項
linktitle: 指定 EPUB 到 PDF 的 PDF 儲存選項
second_title: 使用 Aspose.HTML 進行 Java HTML 處理
description: 了解如何使用強大的 HTML 操作庫 Aspose.HTML 在 Java 中將 EPUB 轉換為 PDF。
weight: 12
url: /zh-hant/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 指定 EPUB 到 PDF 的 PDF 儲存選項


## 介紹

Aspose.HTML for Java 是處理 HTML 和 EPUB 文件的強大工具。在本逐步指南中，我們將引導您完成使用 Aspose.HTML for Java 將 EPUB 檔案轉換為 PDF 的過程。無論您是經驗豐富的開發人員還是剛剛入門，本教學都將為您提供有效執行此任務所需的知識和技能。

## 先決條件

在我們開始之前，請確保您具備以下先決條件：

- Java 開發環境：您的系統上必須設定 Java 開發環境。

-  Aspose.HTML for Java：下載並安裝 Aspose.HTML for Java 函式庫。您可以在以下位置找到該庫和相關文檔[網站](https://releases.aspose.com/html/java/).

- EPUB 檔案：您需要一個要轉換為 PDF 的 EPUB 檔案。

現在，讓我們深入了解使用 Aspose.HTML for Java 將 EPUB 轉換為 PDF 的逐步指南。

## 第 1 步：開啟 EPUB 文件

首先，開啟現有的 EPUB 檔案進行閱讀。您可以使用`FileInputStream`為了實現這一點。這是此步驟的程式碼：

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    //您後續步驟的代碼將位於此處。
}
```

## 第 2 步：定義 PDF 儲存選項

建立一個實例`PdfSaveOptions`具有自訂頁面大小和背景顏色。您可以根據您的要求配置頁面設定。您可以這樣做：

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

## 步驟 3：將 EPUB 轉換為 PDF

現在，請致電`ConvertEPUB`將 EPUB 檔案轉換為 PDF 的方法。指定輸入流、PDF 儲存選項和輸出位置。其操作方法如下：

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

恭喜！您已使用 Aspose.HTML for Java 成功將 EPUB 檔案轉換為 PDF。現在您可以在指定的輸出位置存取轉換後的 PDF 檔案。

## 完整的原始碼
```java
Specifying PDF Save Options for EPUB to PDF
        //開啟現有的 EPUB 檔案進行閱讀。
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            //使用自訂頁面大小和背景顏色建立 PdfSaveOptions 的實例。
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
            //呼叫ConvertEPUB方法將EPUB轉換為PDF。
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## 結論

在本教程中，我們學習如何使用 Aspose.HTML for Java 將 EPUB 檔案轉換為 PDF 格式。這個多功能函式庫為開發人員提供了強大的文件操作工具。透過遵循本指南中概述的步驟，您可以將 EPUB 到 PDF 轉換無縫整合到您的 Java 應用程式中。

## 常見問題 (FAQ)

### Aspose.HTML for Java 是免費的函式庫嗎？
 Aspose.HTML for Java 是一個商業庫，但您可以從他們的網站獲得免費試用版[網站](https://releases.aspose.com/).

### 支援轉換哪些 EPUB 格式？
Aspose.HTML for Java支援各種EPUB格式的轉換，確保與大多數EPUB文件的兼容性。

### 我可以進一步自訂 PDF 輸出嗎？
是的，您可以透過調整頁面設定、背景顏色和其他設定來自訂 PDF 輸出`PdfSaveOptions`.

### Aspose.HTML for Java 的試用版有任何限制嗎？
試用版可能會有一些限制，因此建議查看文件以了解詳細資訊。

### 在哪裡可以獲得 Aspose.HTML for Java 的支援？
您可以在以下位置找到問題的答案並尋求支持[Aspose.HTML 論壇](https://forum.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
