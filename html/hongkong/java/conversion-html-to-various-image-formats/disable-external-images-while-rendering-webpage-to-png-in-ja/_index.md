---
category: general
date: 2026-05-31
description: 在 Java 中使用 Aspose HTML 將網頁渲染為 PNG 時，禁用外部圖像。學習如何在沙盒中安全載入網頁並將 HTML 文件保存為
  PNG。
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: zh-hant
og_description: 在 Java 中渲染網頁為 PNG 時停用外部圖像。本逐步指南示範如何在沙箱中載入網頁並將 HTML 文件儲存為 PNG。
og_title: 在 Java 中渲染網頁為 PNG 時禁用外部圖片
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: 在 Java 中將網頁渲染為 PNG 時禁用外部圖片
url: /zh-hant/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中渲染網頁為 PNG 時停用外部圖片

有沒有需要在 Java 中將網頁渲染成 PNG 時 **停用外部圖片**？也許你正在打造一個必須與公共互聯網隔離的縮圖服務，或是單純想確保在轉換過程中不會洩漏任何第三方圖片。無論哪種情況，你都來對地方了。

在本教學中，我們將一步步說明如何在沙盒中載入網頁、關閉外部圖片抓取，最後將 HTML 文件儲存為 PNG 檔案——全部使用 Aspose.HTML for Java。完成後，你將得到一個可直接執行的範例，以及避免常見陷阱的實用技巧。

## 你將學到

- **如何使用 Aspose.HTML 的 `Converter`** 將 HTML 轉成 Java 圖片。
- 在自訂視口與 DPI 下 **於沙盒中載入網頁** 的完整步驟。
- **停用外部圖片** 同時仍能正確渲染頁面的設定方式。
- 如何 **將 HTML 文件儲存為 PNG**（或其他支援格式）到磁碟。
- 邊緣案例處理、效能建議與除錯技巧。

### 前置條件

- 已安裝 Java 8 或更新版本（程式碼亦相容 JDK 11+）。
- 具備 Maven 或 Gradle 以取得 Aspose.HTML for Java 套件。
- 基本的 Java 語法與例外處理概念。
- 初次載入頁面時需要網路連線（除非你自行提供本機 HTML）。

> **小技巧：** 若你身處公司代理伺服器後，請在執行範例前先設定 JVM 的 `http.proxyHost` 與 `http.proxyPort` 屬性。

---

## 第一步：設定專案並加入 Aspose.HTML

首先，加入 Aspose.HTML 相依性。若使用 Maven，將以下內容放入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle 的寫法則如下：

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

將函式庫加入 classpath 後，即可開始撰寫程式。

---

## 第二步：使用沙盒環境 **停用外部圖片**

解決方案的核心在 `DocumentSandbox`。將 *allowExternalImages* 旗標設為 `false`，即可指示 Aspose.HTML 忽略所有指向沙盒外部的 `<img>` 標籤，這正是 **停用外部圖片** 的機制。

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **為什麼重要：** 若未使用沙盒，渲染器會嘗試下載頁面中每一張圖片，這不僅可能緩慢、可靠性低，甚至會帶來安全風險。將旗標設為 `false` 可保證一次乾淨、獨立的渲染過程。

---

## 第三步：**於沙盒中載入網頁**  

接著把 Aspose.HTML 指向想要擷取的 URL。`HTMLDocument` 建構子接受沙盒實例，會自動套用先前定義的限制。

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

如果頁面大量依賴外部腳本來排版，你可能會看到內容缺失，因為我們同時停用了腳本。此時可將 `allowExternalScripts` 旗標調整為 `true`，同時保持 `allowExternalImages` 為 `false`。

---

## 第四步：**將網頁渲染為 PNG**  

文件載入後，只需一行程式碼即可使用 `Converter.convert` 產生圖像。`ImageSaveOptions` 讓你選擇輸出格式，這裡我們選 PNG。

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

產生的 `sandboxed.png` 只會保留內嵌的 SVG 或 base64 編碼圖形（若有），不會包含任何外部圖片。

---

## 第五步：驗證輸出並除錯常見問題

執行程式後，用任何圖像檢視器開啟 `sandboxed.png`。你應該會看到頁面的版面、文字與 CSS 樣式，但所有 `<img src="http://…">` 會變成空白（通常呈現為白色方塊或直接省略）。

### 常見問題與解決方式

| 症狀 | 可能原因 | 解決方法 |
|---|---|---|
| 空白頁面 | 目標 URL 阻擋了請求（例如 Cloudflare） | 為沙盒的 user‑agent 加上適當的標頭，或使用代理伺服器。 |
| 缺字型 | 字型檔案位於外部主機 | 本機安裝字型或以 `@font-face` 的 data URI 方式嵌入。 |
| 版面移位 | CSS 參考了被阻擋的外部樣式表 | 僅將 `allowExternalScripts` 設為 `true` 以允許 CSS 載入，然後重新執行。 |
| `java.lang.OutOfMemoryError` | 以高 DPI 渲染過大的頁面 | 縮小視口或 DPI，或提升 JVM 堆積大小（`-Xmx2g`）。 |

---

## 第六步：延伸範例 – 儲存為其他格式

相同程式碼也能輸出 JPEG、BMP，甚至 PDF。只要更換 `SaveFormat` 列舉即可：

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

若要輸出 PDF，將 `ImageSaveOptions` 換成 `PdfSaveOptions`，並相應調整檔案副檔名。

---

## 完整可執行範例（直接複製貼上）

以下是 **完整、可直接執行的程式**。建立新的 Java 類別、貼上程式碼、確保 `output` 目錄已存在，然後執行。

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**預期輸出**（主控台）：

```
PNG image saved to: output/sandboxed.png
```

開啟 `sandboxed.png` – 你會看到頁面已 **不含任何外部圖片** 地渲染完成。

---

## 常見問答

**Q：仍能顯示 HTML 內嵌的圖片嗎？**  
A：可以。`data:` URI 或 base64 編碼的圖片被視為文件的一部份，會出現在 PNG 中。

**Q：如果只想保留部份外部圖片，其他的仍要阻擋該怎麼做？**  
A：沙盒目前只能全開或全關。若需要細部控制，請自行下載允許的圖片，轉為 data URI 後再渲染。

**Q：此方法能在無頭伺服器上執行嗎？**  
A：完全可以。Aspose.HTML 為純 Java 函式庫，無需顯示伺服器或瀏覽器引擎。

**Q：與 Selenium 或 Puppeteer 有何不同？**  
A：Selenium 需要驅動真實瀏覽器，重量級且較難沙盒化。Aspose.HTML 直接在記憶體中渲染 HTML，提供可預測的效能與更簡易的安全控制，例如 **停用外部圖片**。

---

## 結語

現在你已掌握 **在 Java 中渲染網頁為 PNG 時停用外部圖片** 的完整流程。透過 `DocumentSandbox`，你可以嚴格控制允許的外部資源，確保安全與可重現性。接下來，你可以嘗試調整視口大小、DPI 設定或輸出格式——每一次微調都能為產生縮圖、預覽或存檔快照開闢新可能。

想挑戰更高階的任務嗎？試著平行處理多筆 URL，或將此邏輯整合到 Spring Boot 微服務，讓它即時回傳 PNG。結合 Aspose.HTML 的彈性與 Java 的併發工具，創造無限可能。

祝開發順利，別忘了在留言區分享你的成功案例！

## 接下來可以學什麼？

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Render HTML to PNG with Aspose – Complete Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}