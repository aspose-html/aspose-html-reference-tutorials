---
date: 2026-03-18
description: 了解如何使用 Aspose.HTML for Java 將 HTML 轉換為 XPS 並調整 XPS 頁面大小。輕鬆控制輸出尺寸。
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: 使用 Aspose.HTML for Java 將 HTML 轉換為 XPS 並調整 XPS 頁面大小
url: /zh-hant/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將 HTML 轉換為 XPS 並使用 Aspose.HTML for Java 調整 XPS 頁面大小

在本教學中，您將學會 **如何將 HTML 轉換為 XPS**，並使用 Aspose.HTML for Java 微調產生的頁面尺寸。無論是產生列印報表、發票或歸檔文件，控制 XPS 的尺寸都能確保輸出與預期完全一致。我們將一步步說明——從環境設定到產生最終 XPS 檔案——讓您立即在 Java 應用程式中整合此功能。

## 快速解答
- **「將 HTML 轉換為 XPS」是什麼意思？** 它會將 HTML 文件渲染成 XPS 檔案，保留版面配置與樣式。  
- **需要授權嗎？** 開發階段可使用免費試用版；正式上線須購買商業授權。  
- **支援哪個 Java 版本？** Java 8 或以上（建議使用 JDK 11+）。  
- **可以變更頁面大小嗎？** 可以——Aspose.HTML 允許在渲染前指定自訂尺寸。  
- **轉換需要多長時間？** 標準頁面通常在一秒內完成；較大的文件可能需要更久。

## 什麼是將 HTML 轉換為 XPS？
將 HTML 轉換為 XPS 意指將網頁導向的標記檔案產生成 XPS（XML Paper Specification）文件——一種固定版面、適合列印的格式，類似 PDF。當您需要高保真、與裝置無關的文件進行歸檔或列印時，此功能相當實用。

## 為什麼要調整 XPS 頁面大小？
調整頁面大小可讓您自行決定最終文件的實體尺寸（例如 A4、Letter 或自訂標籤）。這樣可以避免不必要的縮放，確保內容完整呈現，並可透過移除多餘的白邊來減少檔案大小。

## 前置作業

在開始之前，請先確保具備以下條件：

1. **Java 開發環境** – 已在系統上安裝 Java Development Kit (JDK)。  
2. **Aspose.HTML for Java 程式庫** – 下載並將 Aspose.HTML for Java 程式庫加入專案中。您可以在此取得程式庫 [here](https://releases.aspose.com/html/java/)。  
3. **輸入的 HTML 檔案** – 準備好要渲染並調整 XPS 頁面大小的 HTML 檔案。本教學可使用您自己的 HTML 檔案。

## 匯入套件

首先匯入所需的類別。這些套件提供文件處理、渲染與頁面設定等功能。

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## 步驟說明

以下提供簡潔的編號步驟，與原始流程保持一致，並加入額外說明以提升可讀性。

### 步驟 1：設定輸入檔案名稱

使用 `FileInputStream` 讀取來源 HTML 檔案。此串流會將原始 HTML 資料傳遞給 Aspose.HTML 引擎。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### 步驟 2：建立 HTML Document 並設定樣式

建立 `HTMLDocument` 實例，代表即將渲染的內容。範例中同時注入一段簡短的 CSS 以示範樣式設定，您可自行替換為自己的標記。

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### 步驟 3：建立 XPS Rendering Options

實例化 `XpsRenderingOptions`，用來保存所有影響 HTML 轉 XPS 的設定。

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### 步驟 4：調整頁面大小  

**如何設定 XPS 頁面大小** – 定義自訂的頁面尺寸（寬 × 高，單位為點），並告訴渲染器是否自動展開至最寬的頁面。將 `adjustToWidestPage` 設為 `false` 即可保留您指定的精確尺寸。

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### 步驟 5：渲染輸出

最後，使用已配置好的選項建立 `XpsDevice`，並渲染 HTML 文件。產生的即是具備自訂頁面尺寸的完整 XPS 檔案。

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## 常見問題與解決方案

| 問題 | 為何會發生 | 解決方式 |
|------|------------|----------|
| **XPS 輸出為空白** | 輸入串流未關閉或 `HTMLDocument` 指向錯誤檔案。 | 確認 `FileInputStream` 正確使用 try‑with‑resources 包裝，且檔案路徑正確。 |
| **頁面大小未套用** | `adjustToWidestPage` 仍為 `true`。 | 如步驟 4 所示，設定 `pageSetup.setAdjustToWidestPage(false);`。 |
| **不支援的 CSS** | Aspose.HTML 只支援部分 CSS。 | 盡量使用基礎的版面、字型與顏色，避免使用進階選擇器或 CSS Grid。 |
| **LicenseException** | 生產環境未使用有效授權。 | 在渲染前套用臨時或正式授權 (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`)。 |

## 常見問答

**Q: 什麼是 Aspose.HTML for Java？**  
A: Aspose.HTML for Java 是一套 Java 程式庫，讓開發者能操作並將 HTML 文件轉換為多種格式，如 XPS、PDF 與影像。

**Q: 從哪裡可以下載 Aspose.HTML for Java？**  
A: 您可從 [this link](https://releases.aspose.com/html/java/) 下載 Aspose.HTML for Java 程式庫。

**Q: 有提供免費試用版嗎？**  
A: 有，您可從 [here](https://releases.aspose.com/) 取得 Aspose.HTML for Java 的免費試用。

**Q: 如何取得 Aspose.HTML for Java 的臨時授權？**  
A: 前往 [this page](https://purchase.aspose.com/temporary-license/) 取得臨時授權。

**Q: 可以取得 Aspose.HTML for Java 的技術支援嗎？**  
A: 可以，您可在 [Aspose Forum](https://forum.aspose.com/) 向社群尋求協助。

**Q: 能在無圖形介面的伺服器上轉換 HTML 為 XPS 嗎？**  
A: 完全可以。Aspose.HTML 可在沒有 GUI 的環境執行，只要確保 Java 執行環境正確設定即可。

**Q: 程式庫支援自訂頁邊距嗎？**  
A: 支援。在將 `PageSetup` 指派給渲染選項前，可使用 `PageSetup.setMarginTop()`、`setMarginBottom()` 等方法設定邊距。

## 結論

我們已完整示範 **將 HTML 轉換為 XPS** 並使用 Aspose.HTML for Java 調整頁面大小的全流程。依照本教學操作，您即可產生符合精確版面需求的列印就緒 XPS 文件。歡迎嘗試不同的頁面尺寸、樣式，甚至加入頁首與頁尾，以配合專案需求。

如有任何疑問或需要進一步協助，請參考 [Aspose.HTML for Java 文件](https://reference.aspose.com/html/java/) 或前往 [Aspose Forum](https://forum.aspose.com/) 交流討論。

---

**最後更新：** 2026-03-18  
**測試環境：** Aspose.HTML for Java 24.11（撰寫時最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}