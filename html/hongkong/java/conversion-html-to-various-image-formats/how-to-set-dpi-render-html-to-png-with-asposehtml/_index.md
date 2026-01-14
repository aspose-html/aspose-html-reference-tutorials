---
category: general
date: 2026-01-14
description: 將 URL 轉換為 PNG 時如何設定 DPI。學習使用 Aspose.HTML 在 Java 中將 HTML 渲染為 PNG、設定視口大小，並將
  HTML 儲存為 PNG。
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: zh-hant
og_description: 將 URL 轉換為 PNG 時如何設定 DPI。一步一步的指南，說明如何將 HTML 渲染為 PNG、控制視口大小，以及使用 Aspose.HTML
  將 HTML 儲存為 PNG。
og_title: 如何設定 DPI – 使用 AsposeHTML 將 HTML 渲染為 PNG
tags:
- AsposeHTML
- Java
- image rendering
title: 如何設定 DPI – 使用 AsposeHTML 將 HTML 渲染為 PNG
url: /zh-hant/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何設定 DPI – 使用 AsposeHTML 將 HTML 渲染為 PNG

有沒有想過 **如何設定 DPI** 以產生類似螢幕截圖的網頁圖像？也許你需要 300 DPI 的 PNG 以供列印，或是低解析度的縮圖供手機應用程式使用。無論哪種情況，關鍵在於告訴渲染引擎你想要的邏輯 DPI，然後讓它自行處理。  

在本教學中，我們將使用實際的 URL，將其渲染為 PNG 檔案，**設定視口大小**，調整 DPI，最後 **將 HTML 儲存為 PNG**——全部使用 Aspose.HTML for Java。無需外部瀏覽器，無需繁雜的命令列工具——只要乾淨的 Java 程式碼，隨時可放入任何 Maven 或 Gradle 專案中。

> **專業提示：** 如果你只需要快速產生縮圖，可以保持 DPI 為 96 DPI（大多數螢幕的預設值）。若是列印用的素材，則建議提升至 300 DPI 或更高。

![設定 DPI 範例](https://example.com/images/how-to-set-dpi.png "設定 DPI 範例")

## 您需要的環境

- **Java 17**（或任何較新的 JDK）。  
- **Aspose.HTML for Java** 24.10 或更新版本。您可以從 Maven Central 取得：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- 需要網際網路連線以下載目標頁面（範例使用 `https://example.com/sample.html`）。  
- 需要對輸出資料夾具有寫入權限。

就是這樣——不需要 Selenium，也不需要無頭 Chrome。Aspose.HTML 於程式內部完成渲染，意味著您仍在 JVM 內部執行，避免了啟動瀏覽器的額外開銷。

## 步驟 1 – 從 URL 載入 HTML 文件

首先，我們建立指向欲擷取頁面的 `HTMLDocument` 實例。建構子會自動下載 HTML、解析並準備 DOM。

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*為什麼這很重要：* 直接載入文件即可省去額外的 HTTP 客戶端。Aspose.HTML 會遵守重新導向、Cookie，甚至在 URL 中嵌入的基本驗證。

## 步驟 2 – 建立具備目標 DPI 與視口的 Sandbox

**Sandbox** 是 Aspose.HTML 模擬瀏覽器環境的方式。在此我們讓它假裝是一個 1280 × 720 的螢幕，且最重要的是設定 **裝置 DPI**。變更 DPI 會改變渲染圖像的像素密度，而不會改變邏輯尺寸。

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*為什麼可能需要調整這些值：*  
- **視口大小** 會影響 CSS 媒體查詢 (`@media (max-width: …)`) 的行為。  
- **裝置 DPI** 會影響列印時圖像的實體尺寸。96 DPI 圖像在螢幕上看起來不錯；300 DPI 圖像在紙張上則保持清晰。  

如果需要正方形縮圖，只需將 `setViewportSize(500, 500)` 改為相同的寬高，並保持較低的 DPI。

## 步驟 3 – 選擇 PNG 作為輸出格式

Aspose.HTML 支援多種點陣圖格式（PNG、JPEG、BMP、GIF）。PNG 為無損格式，非常適合需要完整保留每個像素的螢幕截圖。

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

如果在意檔案大小，也可以調整壓縮等級（`pngOptions.setCompressionLevel(9)`）。

## 步驟 4 – 渲染並儲存圖像

現在我們指示文件 **儲存** 為圖像。`save` 方法接受檔案路徑以及先前設定好的選項。

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

程式執行完畢後，您會在 `YOUR_DIRECTORY/sandboxed.png` 找到 PNG 檔案。開啟它——如果您將 DPI 設為 300，圖像的中繼資料會顯示該 DPI，儘管像素尺寸仍為 1280 × 720。

## 步驟 5 – 驗證 DPI（可選但實用）

如果想再次 DPI 是否真的套用，可使用輕量級函式庫 **metadata‑extractor** 讀取 PNG 中繼資料：

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

您應該會在主控台看到 `300`（或您設定的數值）被印出。此步驟對渲染不是必須的，但作為快速的正確性檢查相當有用，尤其在產出列印工作流程的資產時。

## 常見問題與邊緣情況

### 「如果頁面使用 JavaScript 載入內容？」

Aspose.HTML 會執行 **受限的 JavaScript 子集**。對於大多數靜態網站，它可直接運作。若頁面大量依賴客戶端框架（React、Angular、Vue），可能需要先行預渲染頁面或改用無頭瀏覽器。然而，一旦 DOM 準備好，設定 DPI 的方式相同。

### 「我可以渲染 PDF 而非 PNG 嗎？」

當然可以。將 `ImageSaveOptions` 換成 `PdfSaveOptions`，並將輸出副檔名改為 `.pdf`。DPI 設定仍會影響任何嵌入圖像的點陣化外觀。

### 「高解析度螢幕（Retina）截圖該怎麼做？」

只要將視口尺寸加倍，同時保持 DPI 為 96 DPI，或保持視口不變並將 DPI 提升至 192。產生的 PNG 會有兩倍的像素，呈現出清晰的 Retina 效果。

### 「我需要清理資源嗎？」

`HTMLDocument` 實作了 `AutoCloseable`。在正式應用中，請將其包在 try‑with‑resources 區塊中：

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

## 完整可執行範例（直接複製貼上）

以下是完整、可直接執行的程式。請將 `YOUR_DIRECTORY` 替換為您機器上的實際資料夾路徑。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

執行此類別，即可取得符合您所指定 **如何設定 DPI** 設定的 PNG。

## 結論

我們已說明在 **將 HTML 渲染為 PNG** 時 **如何設定 DPI**，涵蓋了 **設定視口大小** 的步驟，並示範了如何使用 Aspose.HTML for Java **將 HTML 儲存為 PNG**。主要重點如下：

- 使用 **sandbox** 來控制 DPI 與視口。  
- 為無損輸出選擇適當的 **ImageSaveOptions**。  
- 如需確保列印品質，請驗證 DPI 中繼資料。

從此您可以嘗試不同的 DPI 值、較大的視口，甚至批次處理多個 URL。想將整個網站轉換為 PNG 縮圖？只需對 URL 陣列迴圈，重複使用相同的 sandbox 設定即可。

祝渲染順利，願您的螢幕截圖永遠保持像素完美！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}