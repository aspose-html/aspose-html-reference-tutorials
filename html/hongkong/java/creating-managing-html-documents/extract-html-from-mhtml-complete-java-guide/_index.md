---
category: general
date: 2026-04-19
description: 使用 Java 快速從 MHTML 中提取 HTML。了解如何將 MHTML 轉換為 HTML、提取郵件正文、將字串寫入檔案以及處理 MHT
  轉換。
draft: false
keywords:
- extract html from mhtml
- convert mhtml to html
- extract email body
- write string to file
- convert mht to html
language: zh-hant
og_description: 在 Java 中從 MHTML 提取 HTML。本指南展示如何將 MHTML 轉換為 HTML、提取電郵正文，並將字串寫入檔案。
og_title: 從 MHTML 提取 HTML – Java 步驟說明
tags:
- Java
- Aspose.HTML
- Email Processing
title: 從 MHTML 中提取 HTML – 完整 Java 指南
url: /zh-hant/java/creating-managing-html-documents/extract-html-from-mhtml-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 MHTML 中提取 HTML – 完整 Java 指南

是否曾需要**從 MHTML 提取 HTML**，卻不知從何開始？也許你收到了一封已封存的電郵（`.mht`），想要取得乾淨的正文以供網頁預覽，或是你正在編寫一個遷移腳本，將舊有的封存檔案轉換為現代的 HTML 頁面。無論哪種情況，問題都是相同的：你手上有一個單一檔案的網頁封存檔，需要將其中的原始 HTML 標記取出。

好消息是？只要幾行 Java 程式碼加上 Aspose.HTML 函式庫，你就能**將 MHTML 轉換為 HTML**、擷取電郵正文，甚至將該字串寫入檔案——全部在 IDE 中完成。在本教學中，我們將逐步說明整個流程，解釋每一步的意義，並示範如何處理常見的邊緣情況，例如資源遺失或非 UTF‑8 編碼。

> **快速回顧：** 完成本指南後，你將能夠**擷取電郵正文**、**將 MHTML 轉換為 HTML**，以及**將字串寫入檔案**，使用一段乾淨且可重用的程式碼片段，適用於任何 `.mht` 或 `.mhtml` 檔案。

## 需求環境

- **Java 17+**（程式碼使用 try‑with‑resources 模式，該模式自 Java 7 起可用，但 Java 17 為目前的長期支援版）。
- **Aspose.HTML for Java** JAR 檔放在 classpath 上。你可以從 [Aspose 官方網站](https://products.aspose.com/html/java/) 或透過 Maven 取得：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- 一個你想處理的範例 **`.mht` 或 `.mhtml`** 檔案。示範中我們將其命名為 `email.mht`，並放置於 `YOUR_DIRECTORY`。

就這樣——不需要額外框架，也不需要大型解析器。只要純 Java 加上一個文件齊全的函式庫即可。

## 步驟 1 – 以 Stream 開啟 MHTML 檔案

我們首先將封存的電郵以 `InputStream` 開啟。使用串流可降低記憶體使用量，特別是對於可能包含嵌入式圖片或 CSS 的大型 `.mht` 檔案。

```java
// Step 1: Open the MHTML file as a stream
try (InputStream mhtmlStream = new FileInputStream("YOUR_DIRECTORY/email.mht")) {
    // Subsequent steps go inside this block
}
```

**為什麼使用串流？**  
串流讓 `MhtmlDocument` 能即時讀取資料，即使封存檔案達數兆位元組，也不會觸發 `OutOfMemoryError`。此外，它還提供彈性，日後可從其他來源讀取（例如，來自資料庫的 `ByteArrayInputStream`）。

## 步驟 2 – 從 Stream 載入 MHTML 文件

現在我們將串流交給 Aspose 的 `MhtmlDocument` 類別。此類別會解析 MIME 編碼的封存檔，並建立一個類似 DOM 的嵌入式 HTML 表示。

```java
// Step 2: Load the MHTML document from the stream
MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);
```

**背後運作原理：**  
Aspose 會提取每個 MIME 部分（HTML、圖片、CSS），並在內部重新組合。因此，你之後只要請求 HTML 部分即可，無需擔心嵌入的資源。

## 步驟 3 – 取得主要 HTML 內容

文件載入後，取得原始 HTML 只需一行程式碼。`getHtmlContent()` 方法會以 `String` 回傳正文，保留原始標記。

```java
// Step 3: Retrieve the main HTML content as a string
String htmlContent = mhtmlDoc.getHtmlContent();
```

**取得內容說明：**  
`htmlContent` 包含完整的 HTML 頁面——包括 `<head>` 與 `<body>` 標籤——與電郵儲存時的原始樣子完全相同。如果只需要可見部分，之後可以使用 Jsoup 解析並移除 `<head>`。

## 步驟 4 – 將提取的 HTML 寫入獨立檔案

使用 `java.nio.file` API 將字串寫入磁碟相當簡單。此步驟示範了適用於任何平台的**將字串寫入檔案**模式。

```java
// Step 4: Save the extracted HTML to a separate file
Files.writeString(Path.of("YOUR_DIRECTORY/email_body.html"), htmlContent);
```

**小技巧：**  
如果需要特定字元集，可使用 `Files.writeString(Path, CharSequence, Charset)`。預設為 UTF‑8，適用於大多數現代電郵。

## 步驟 5 – 確認提取結果

簡單的 `System.out.println` 可讓你驗證程式是否順利執行且未拋出例外。在正式環境中，你應改用適當的日誌記錄。

```java
// Step 5: Indicate successful extraction
System.out.println("HTML extracted.");
```

執行程式後，應在主控台看到 `HTML extracted.`，且檔案 `email_body.html` 會出現在 `YOUR_DIRECTORY`。

## 完整、可直接執行的範例

將上述步驟整合起來，以下是一個完整且獨立的 Java 類別。隨意複製貼上至 IDE，然後點擊 **Run** 即可。

```java
import com.aspose.html.MhtmlDocument;
import java.io.FileInputStream;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;

public class MhtmlToHtmlConverter {

    public static void main(String[] args) {
        // Adjust the path to point to your .mht/.mhtml file
        String sourcePath = "YOUR_DIRECTORY/email.mht";
        String targetPath = "YOUR_DIRECTORY/email_body.html";

        // Try-with-resources ensures the stream is closed automatically
        try (InputStream mhtmlStream = new FileInputStream(sourcePath)) {

            // Load the MHTML document
            MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);

            // Extract the HTML content
            String htmlContent = mhtmlDoc.getHtmlContent();

            // Write the HTML string to a new file
            Files.writeString(Path.of(targetPath), htmlContent);

            // Simple confirmation output
            System.out.println("HTML extracted to " + targetPath);
        } catch (Exception e) {
            // In real code you might want to log this instead of printing
            System.err.println("Failed to extract HTML: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### 預期輸出

執行程式會印出類似以下內容：

```
HTML extracted to YOUR_DIRECTORY/email_body.html
```

而 `email_body.html` 會包含原始電郵的完整 HTML 原始碼。用瀏覽器開啟它，你應該會看到與原始封存訊息相同的視覺呈現（不包括未捆綁的外部資源）。

## 處理常見邊緣情況

### 1. 缺少嵌入資源

有時 MHTML 檔會引用未儲存在封存內的外部圖片。在此情況下，`getHtmlContent()` 仍會回傳 `<img src="...">` 標記，但 URL 會指向原始網路位置。若需要完整自包含的 HTML 檔案，你可以：

- 使用 `MhtmlDocument.save(Path, SaveFormat.HTML)` 讓 Aspose 將所有資源提取至資料夾。
- 或使用像 **Jsoup** 之類的函式庫對 HTML 進行後處理，將遠端 URL 替換為 base64 編碼的 data URI。

### 2. 非 UTF‑8 編碼

如果電郵是以其他字元集（例如 `windows-1252`）儲存，回傳的字串可能會出現亂碼。寫入時可強制指定字元集：

```java
Files.writeString(
    Path.of(targetPath),
    htmlContent,
    StandardCharsets.ISO_8859_1
);
```

### 3. 大檔案

對於超過數百 MB 的封存檔，建議直接將 HTML 輸出串流至 `BufferedWriter`，而非先將整個字串載入記憶體。Aspose 亦提供 **`save`** 方法，可直接寫入檔案，省去中間的 `String`。

## 專業技巧與最佳實踐

- **重複使用 `MhtmlDocument` 物件**，如果需要提取多個部分（例如 CSS、圖片）。它只會解析一次封存檔。
- **驗證輸出**，使用 HTML 驗證工具（如 W3C validator 或 `jsoup.isValid()`），若要將 HTML 輸入其他系統時。
- **使用日誌而非印出**，在正式環境中將 `System.out.println` 換成如 SLF4J 等日誌框架，以捕捉時間戳記與嚴重程度。
- **對相依性使用版本控制**。Aspose 會頻繁發布更新；在 `pom.xml` 中固定版本，以避免意外的破壞性變更。

## 結論

我們剛剛完整示範了使用 Java **從 MHTML 提取 HTML** 的實務端到端解決方案。透過以串流開啟封存檔、使用 Aspose.HTML 載入、取得 HTML 字串，並**將字串寫入檔案**，你現在擁有可靠的方法來**將 MHTML 轉換為 HTML**、**提取電郵正文**，甚至**將 MHT 轉換為 HTML**，以供後續處理。

隨意調整此程式碼片段：若封存檔儲存在資料庫中，可將 `FileInputStream` 換成 `ByteArrayInputStream`，或將程式碼整合至處理數十封電郵的批次作業中。核心概念不變——讓專門的函式庫負責繁重工作，然後依需求處理純文字。

**接下來可以探索的步驟**：

- 使用 Jsoup **清理提取的 HTML**（移除追蹤像素、內嵌 CSS 等）。
- 透過遍歷 `.mht` 檔案目錄，實作 **批次轉換** 自動化。
- 結合 **Apache POI**，將清理後的 HTML 嵌入 Word 或 PDF 文件。

對特定邊緣情況有疑問，或想分享你如何擴充此腳本？在下方留下評論吧——祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}