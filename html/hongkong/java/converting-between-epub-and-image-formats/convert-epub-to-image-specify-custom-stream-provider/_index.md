---
date: 2026-03-13
description: 了解如何使用 Aspose.HTML for Java 將 EPUB 轉換為圖像及 JPEG。本分步指南可協助您在 Java 中高效轉換
  EPUB 頁面。
linktitle: Specifying Custom Stream Provider for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: 使用 Aspose.HTML for Java 將 EPUB 轉換為圖片
url: /zh-hant/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

Make sure to keep code block placeholders unchanged.

Now craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML for Java 將 EPUB 轉換為圖像

如果您想在 Java 中 **將 EPUB 轉換為圖像**，Aspose.HTML for Java 是一個功能強大的工具，可簡化此過程。在本步驟指南中，我們將帶您完成所需的全部內容——從安裝庫到從 EPUB 文件生成高品質圖像檔案。完成後，您將了解為何此方法可靠、如何自訂輸出格式，以及如何有效處理產生的圖像串流。

## 快速解答
- **轉換會產生什麼？** 一系列圖像檔案（例如 JPEG、PNG），代表 EPUB 的每一頁。  
- **需要哪個程式庫？** Aspose.HTML for Java。  
- **我需要授權嗎？** 在正式使用時需要臨時或完整授權；亦提供免費試用版。  
- **我可以更改圖像格式嗎？** 可以——調整 `ImageSaveOptions` 為 PNG、GIF 或 **JPEG**（請參閱「convert EPUB to JPEG」）。  
- **此程式碼相容於 Java 8+ 嗎？** 當然相容；可在任何近期的 JDK 上執行。

## 「將 EPUB 轉換為圖像」是什麼？
將 EPUB 轉換為圖像是指將電子書的每一頁渲染為點陣圖。這對於產生預覽圖、建立縮圖，或將 EPUB 內容整合至僅支援圖像資產的平台非常有用。

## 為何在此轉換中使用 Aspose.HTML for Java？
- **高保真渲染** – 保留版面配置、字型與 SVG 圖形。  
- **基於串流的處理** – 使用記憶體串流，避免產生暫存檔。  
- **彈性輸出** – 支援 JPEG、PNG、GIF 等多種格式。  
- **跨平台** – 可在任何支援的 JDK 作業系統上執行。

## 前置條件

- Java Development Kit (JDK)：您應在系統上安裝 Java SE Development Kit (JDK)。可從 [here](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。  
- Aspose.HTML for Java：您需要擁有 Aspose.HTML for Java 程式庫。若尚未取得，可在 [here](https://releases.aspose.com/html/java/) 下載。  
- EPUB 檔案：準備好您想要轉換為圖像的 EPUB 檔案。

## 匯入套件

在您的 Java 專案中，您需要匯入 Aspose.HTML for Java 所需的套件。請確保在程式碼中加入以下內容。

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.image.ImageFormat;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## 步驟說明

以下將 **將 EPUB 轉換為圖像** 的過程分解為多個步驟：

### 步驟 1：開啟 EPUB 檔案

您將使用 `FileInputStream` 開啟現有的 EPUB 檔案以供讀取。

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

### 步驟 2：建立 Memory Stream Provider

接著，建立 `MemoryStreamProvider` 的實例，以協助轉換。

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
```

### 步驟 3：將 EPUB 轉換為圖像

現在是執行實際的 EPUB 轉換為圖像的時候。使用 `Converter.convertEPUB` 方法，並將輸出格式指定為 JPEG。這即是 **convert EPUB to JPEG** 的核心。

```java
Converter.convertEPUB(
    fileInputStream,
    new ImageSaveOptions(ImageFormat.Jpeg),
    streamProvider.getStream()
);
```

### 步驟 4：存取產生的資料

轉換完成後，您可以存取包含產生圖像資料的記憶體串流。遍歷這些串流以處理圖像。

```java
int size = streamProvider.getStream().size();
for (int i = 0; i < size; i++) {
    InputStream inputStream = streamProvider.getStream().get(i);

    // Flush the page to the output file
    try (FileOutputStream fileOutputStream = new FileOutputStream("page_" + (i + 1) + ".jpg")) {
        byte[] buffer = new byte[inputStream.available()];
        inputStream.read(buffer);
        fileOutputStream.write(buffer);
    }
}
```

就這樣！您已成功使用 Aspose.HTML for Java **將 EPUB 轉換為圖像**。

## 如何在 Java 中將 EPUB 頁面轉換為圖像？

如果您需要 **在 Java 中將 EPUB 頁面逐一轉換**，只需如步驟 4 所示，遍歷 `streamProvider.getStream()` 回傳的串流。您亦可過濾集合，只處理特定頁面，這對於建立章節專屬縮圖相當方便。

## 常見陷阱與技巧

- **記憶體使用量** – 轉換大型 EPUB 時，記憶體串流可能佔用大量 RAM。若遇到 `OutOfMemoryError`，請考慮分批處理頁面。  
- **圖像品質** – 調整 `ImageSaveOptions`（例如設定 `Quality` 屬性）以控制 JPEG 壓縮等級。  
- **檔案命名** – 範例使用簡單的命名規則（`page_1.jpg`）。您可以自訂為包含章節標題或時間戳記。  
- **效能提示**：若大量轉換頁面，請重複使用同一個 `ImageSaveOptions` 實例，以減少物件建立的開銷。

## 結論

Aspose.HTML for Java 簡化了將 EPUB 檔案轉換為圖像的流程。依照本指南所列步驟，您可以快速且有效地完成此任務。請務必符合前置條件並匯入所需套件，以確保轉換流程順暢。

## 常見問答

**Q: 如何將輸出改為 PNG 而非 JPEG？**  
A: 在 `ImageSaveOptions` 建構子中將 `ImageFormat.Jpeg` 替換為 `ImageFormat.Png`。

**Q: 是否可以只轉換部分頁面？**  
A: 可以——您可以過濾 `streamProvider.getStream()` 回傳的串流，僅將所需的索引寫入檔案。

**Q: 支援哪些 Java 版本？**  
A: 支援任何 Java SE 8 以上的版本。

**Q: 我可以直接將圖像串流至 Web 回應嗎？**  
A: 當然可以。您可以改寫成將位元組陣列寫入 HTTP 回應的輸出串流，而非寫入 `FileOutputStream`。

**Q: 程式庫會處理嵌入的字型嗎？**  
A: 會，Aspose.HTML 會自動嵌入並渲染 EPUB 中的自訂字型。

**Q: 如何降低非常大型 EPUB 的記憶體消耗？**  
A: 將頁面分成較小批次處理，並在寫入檔案後釋放每個 `InputStream`。

---

**最後更新：** 2026-03-13  
**測試環境：** Aspose.HTML for Java 24.11  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}