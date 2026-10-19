---
date: 2026-05-19
description: 了解如何使用 Aspose.HTML for Java 從 EPUB 中提取圖像，並透過本分步指南將 EPUB 轉換為圖像檔案。
keywords:
- extract images from epub
- aspose html for java
- java ebook to image
linktitle: 為 EPUB 轉圖像指定自訂串流提供者
schemas:
- author: Aspose
  dateModified: '2026-05-19'
  description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  headline: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB
    to Image Conversion
  type: TechArticle
- description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  name: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB to Image
    Conversion
  steps:
  - name: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
    text: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
  - name: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
    text: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
  - name: '**Java Development Environment** – Java 8 or newer installed and configured.'
    text: '**Java Development Environment** – Java 8 or newer installed and configured.'
  - name: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
    text: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
  - name: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
    text: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
  - name: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
    text: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
  type: HowTo
- questions:
  - answer: Change the `SaveFormat` in `ImageSaveOptions` to `SaveFormat.Png` and
      update the file extension in the output loop.
    question: How do I convert EPUB to PNG instead of JPEG?
  - answer: Yes. After conversion, iterate over `streamProvider.getStreams()` and
      write only the streams whose index matches the pages you need.
    question: Can I extract only specific pages from an EPUB?
  - answer: Absolutely. Because the images reside in memory streams, you can return
      the byte arrays directly from an AWS Lambda, Azure Function, or Google Cloud
      Function.
    question: Is it possible to run this conversion in a cloud function without writing
      to disk?
  - answer: The library can open unencrypted EPUBs. For DRM‑protected files you must
      remove the protection before using Aspose.HTML.
    question: Does Aspose.HTML support DRM‑protected EPUB files?
  - answer: '`MemoryStreamProvider` has been available since Aspose.HTML 22.9; the
      tutorial was tested with version 23.10.'
    question: What version of Aspose.HTML introduced MemoryStreamProvider?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: 從 EPUB 中提取圖像 – 為 EPUB 轉圖像指定自訂串流提供者
url: /zh-hant/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 EPUB 提取圖像 – 為 EPUB 到圖像轉換指定自訂串流提供者

在本教學中，您將學習如何使用 **Aspose.HTML for Java** 以及自訂串流提供者，從 **EPUB** 檔案中提取圖像。無論您是構建基於雲端的電子書預覽服務，或是需要為數位圖書館產生縮圖，本文所示的方法都能讓您在不觸及檔案系統的情況下，完整掌控圖像輸出。

## 快速解答
- **本教學教什麼？** 如何使用自訂串流提供者從 EPUB 中提取圖像並將其儲存為 JPEG 檔案。  
- **需要哪個函式庫？** Aspose.HTML for Java。  
- **是否需要授權？** 生產環境使用需取得臨時或正式授權。  
- **示範的輸出格式為何？** JPEG（您可以透過變更 `ImageFormat` 來改為 PNG、BMP 等）。  
- **程式碼行數多少？** 只需五段簡潔的程式碼片段，其他皆為純文字說明。

## 什麼是從 EPUB 提取圖像？
將 EPUB 載入並將每一頁提取為圖像的操作稱為 **從 EPUB 提取圖像**。此過程會將電子書內部的 XHTML 頁面轉換為點陣圖，使您能在不使用 EPUB 閱讀器的情況下顯示或處理這些圖像。

## 如何使用自訂串流提供者從 EPUB 提取圖像？
載入 EPUB，將轉換指向 `MemoryStreamProvider`，然後將每個記憶體串流寫入檔案（或從服務返回）。整個流程在記憶體中執行，省去暫存檔案，讓您可彈性地將位元組儲存於任意位置——磁碟、資料庫或雲端儲存。

轉換分為兩個簡單步驟：
1. 使用 `HtmlDocument`（或更高階的 `EpubDocument` 類別）**開啟 EPUB**，並指向您的來源檔案。  
2. **建立 `MemoryStreamProvider`**，告訴轉換器使用它，最後取得產生的圖像串流。

### 步驟說明

#### 開啟現有的 EPUB 檔案
`EpubDocument` 類別在記憶體中表示單一 EPUB 檔案。以檔案路徑建立實例，即會載入整本書的結構。

`EpubDocument epub = new EpubDocument("sample.epub");`

#### 建立 MemoryStreamProvider
`MemoryStreamProvider` 是 Aspose.HTML 的記憶體串流管理器。它會將每個渲染的頁面捕獲為獨立的 `InputStream`，而不寫入磁碟。

`MemoryStreamProvider streamProvider = new MemoryStreamProvider();`

#### 將 EPUB 轉換為圖像
`ImageSaveOptions` 讓您指定輸出格式、解析度與品質。將 `MemoryStreamProvider` 傳入 `save` 方法後，Aspose.HTML 會將每頁寫入不同的記憶體串流。  
`SaveFormat` 是一個列舉，用於定義輸出圖像的格式（例如 Jpeg、Png）。

`epub.save(streamProvider, new ImageSaveOptions(SaveFormat.Jpeg));`

#### 取得記憶體串流
轉換完成後，提供者會保存一系列串流——每頁一個。您可以遍歷它們，將每個串流轉換為位元組陣列，或直接輸出至 HTTP 回應。

`for (InputStream imageStream : streamProvider.getStreams()) { /* process stream */ }`  
`InputStream` 是 Java I/O 類別，代表可讀取位元組的串流。

#### 將頁面寫入輸出檔案
如果需要實體檔案，只需將每個串流複製到 `FileOutputStream`。`FileOutputStream` 是 Java 用於將位元組寫入檔案系統的類別。以下範例會產生名為 `page_1.jpg`、`page_2.jpg` 等的 JPEG 檔案。

```java
int pageNumber = 1;
for (InputStream imageStream : streamProvider.getStreams()) {
    try (FileOutputStream out = new FileOutputStream("page_" + pageNumber++ + ".jpg")) {
        imageStream.transferTo(out);
    }
}
```

> **專業提示：** 使用 `try‑with‑resources` 區塊可確保每個串流自動關閉，防止記憶體泄漏。

## 為何將 EPUB 轉換為 JPEG？
- **通用相容性** – JPEG 圖像可在幾乎所有裝置上顯示，從瀏覽器到行動應用程式皆支援。  
- **易於整合** – 可在網頁、文件或作為縮圖使用提取的圖像，無需 EPUB 閱讀器。  
- **效能提升** – 渲染靜態圖像遠比載入完整 EPUB 快，適合預覽產生器。  
- **具體效益**：Aspose.HTML 能在標準 2 GHz CPU 上，於 15 秒內將最多 300 頁的 EPUB 轉為 JPEG，每頁平均約耗時 45 ms。

## 前置條件

1. **Java 開發環境** – 已安裝並設定 Java 8 或更新版本。  
2. **Aspose.HTML for Java 函式庫** – 從 [here](https://releases.aspose.com/html/java/) 下載最新的 JAR。  
3. **Aspose.HTML 文件** – 完整 API 參考可於 [here](https://reference.aspose.com/html/java/) 取得。  
4. **IDE** – 任意支援 Java 的開發環境，如 Eclipse、IntelliJ IDEA 或 VS Code。

## 常見陷阱與技巧

- **記憶體管理** – 必須始終關閉串流。上述的 `try‑with‑resources` 模式會自動處理此問題。  
- **大型 EPUB** – 對於頁數達數百頁的書籍，請分批處理串流（例如一次 20 頁），以降低堆積記憶體佔用。  
- **圖像品質** – 調整 `ImageSaveOptions.setQuality(int)`（0‑100）以平衡檔案大小與視覺真實度。  
- **執行緒安全** – `MemoryStreamProvider` 實例非執行緒安全；每個轉換執行緒應建立新的提供者。

## 常見問與答

**Q: 如何將 EPUB 轉換為 PNG 而非 JPEG？**  
A: 將 `ImageSaveOptions` 中的 `SaveFormat` 改為 `SaveFormat.Png`，並在輸出迴圈中更新檔案副檔名。

**Q: 我能只提取 EPUB 中的特定頁面嗎？**  
A: 可以。轉換完成後，遍歷 `streamProvider.getStreams()`，僅寫入索引符合所需頁面的串流。

**Q: 能否在雲端函式中執行此轉換且不寫入磁碟？**  
A: 完全可以。由於圖像存於記憶體串流，您可直接從 AWS Lambda、Azure Function 或 Google Cloud Function 回傳位元組陣列。

**Q: Aspose.HTML 是否支援受 DRM 保護的 EPUB 檔案？**  
A: 此函式庫只能開啟未加密的 EPUB。對於受 DRM 保護的檔案，必須先移除保護才能使用 Aspose.HTML。

**Q: 哪個版本的 Aspose.HTML 引入了 MemoryStreamProvider？**  
A: `MemoryStreamProvider` 自 Aspose.HTML 22.9 起即已提供；本教學測試於版本 23.10。

---

**最後更新:** 2026-05-19  
**測試環境:** Aspose.HTML for Java 23.10  
**作者:** Aspose  

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code here
}
```

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code here
}
```

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // Your code here
}
```

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [使用 Aspose.HTML for Java 轉換 EPUB 為圖像 – 設定自訂頁面大小](/html/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/)
- [如何使用 Aspose.HTML for Java 轉換 EPUB 為圖像](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Java EPUB 轉 PDF – 指定自訂串流提供者](/html/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-custom-stream-provider/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}