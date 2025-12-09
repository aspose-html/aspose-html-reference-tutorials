---
date: 2025-11-29
description: 學習如何使用 Aspose.HTML for Java 將 HTML 轉換為 XPS 並調整 XPS 頁面大小，輕鬆掌控輸出尺寸。
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

在本教學中，您將了解 **如何將 HTML 轉換為 XPS**，並使用 Aspose.HTML for Java 微調產生的頁面大小。無論是產生可列印的報表、發票或歸檔文件，控制 XPS 的尺寸都能確保輸出如您所預期。我們將一步步說明——從環境設定到最終渲染 XPS 檔案——讓您立即在 Java 應用程式中整合此功能。

## 快速回答
- **「將 HTML 轉換為 XPS」是什麼意思？** 它會將 HTML 文件渲染成 XPS 檔案，保留版面配置與樣式。  
- **需要授權嗎？** 開發階段可使用免費試用版；正式上線需購買商業授權。  
- **支援哪個 Java 版本？** Java 8 或以上（建議使用 JDK 11+）。  
- **可以變更頁面大小嗎？** 可以——Aspose.HTML 允許在渲染前指定自訂尺寸。  
- **轉換需要多長時間？** 標準頁面通常在一秒內完成；較大的文件可能需要更久。

## 什麼是將 HTML 轉換為 XPS？
將 HTML 轉換為 XPS 意指將以網頁為導向的標記檔案產生為 XPS（XML Paper Specification）文件——一種固定版面、適合列印的格式，類似 PDF。當您需要高保真、裝置無關的文件以供歸檔或列印時，這項功能相當實用。

## 為什麼要調整 XPS 頁面大小？
調整頁面大小可讓您掌控最終文件的實體尺寸（例如 A4、Letter、或自訂標籤）。這能避免不必要的縮放，確保內容完整呈現，並可透過去除多餘的白邊來減少檔案大小。

## 前置條件

在開始之前，請確保已具備以下條件：

1. **Java 開發環境** – 已在系統上安裝 Java Development Kit (JDK)。  
2. **Aspose.HTML for Java 程式庫** – 下載並將 Aspose.HTML for Java 程式庫加入專案中。您可以在[此處](https://releases.aspose.com/html/java/)取得。  
3. **輸入 HTML 檔案** – 準備好要渲染並調整 XPS 頁面大小的 HTML 檔案。您可以使用自己的 HTML 檔案進行本教學。

## 匯入套件

首先，匯入所需的類別。這些套件提供文件處理、渲染與頁面設定功能。

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## 第一步：設定輸入檔案名稱

使用 `FileInputStream` 讀取來源 HTML 檔案。此串流會將原始 HTML 傳入 Aspose.HTML 引擎。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## 第二步：建立 HTML Document 並設定樣式

建立 `HTMLDocument` 實例以代表要渲染的內容。此範例同時注入一段簡短的 CSS 以示範樣式——您可以自行替換為自己的標記。

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

## 第三步：建立 XPS Rendering Options

實例化 `XpsRenderingOptions`，以保存所有影響 HTML 轉換為 XPS 的設定。

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## 第四步：調整頁面大小

定義自訂的頁面大小（寬 × 高，單位為點），並告訴渲染器是否自動展開至最寬的頁面。將 `adjustToWidestPage` 設為 `false` 可保留您指定的精確尺寸。

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## 第五步：渲染輸出

最後，使用已配置好的選項建立 `XpsDevice`，並渲染 HTML 文件。結果是一個具備自訂頁面尺寸的完整 XPS 檔案。

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## 常見問題與解決方案

| 問題 | 為何發生 | 解決方案 |
|------|----------|----------|
| **空白 XPS 輸出** | 輸入串流未關閉或 `HTMLDocument` 指向錯誤檔案。 | 確保 `FileInputStream` 正確使用 try‑with‑resources 包裹，且檔案路徑正確。 |
| **頁面大小未套用** | `adjustToWidestPage` 保持為 `true`。 | 如第 4 步所示，設定 `pageSetup.setAdjustToWidestPage(false);`。 |
| **不支援的 CSS** | Aspose.HTML 只支援部分 CSS。 | 只使用基本的版面、字型與顏色，避免使用進階選擇器或 CSS Grid。 |
| **LicenseException** | 在正式環境未使用有效授權。 | 在渲染前套用臨時或正式授權 (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`)。 |

## 常見問答

**Q: 什麼是 Aspose.HTML for Java**  
A: Aspose.HTML for Java 是一套 Java 程式庫，讓開發者能操作並將 HTML 文件轉換為多種格式，如 XPS、PDF 與影像。

**Q: 在哪裡可以下載 Aspose.HTML for Java？**  
A: 您可從[此連結](https://releases.aspose.com/html/java/)下載 Aspose.HTML for Java 程式庫。

**Q: 是否提供 Aspose.HTML for Java 的免費試用？**  
A: 是的，您可以從[此處](https://releases.aspose.com/)取得 Aspose.HTML for Java 的免費試用版。

**Q: 如何取得 Aspose.HTML for Java 的臨時授權？**  
A: 若要取得臨時授權，請造訪[此頁面](https://purchase.aspose.com/temporary-license/)。

**Q: 我可以獲得 Aspose.HTML for Java 的支援嗎？**  
A: 可以，您可在 [Aspose Forum](https://forum.aspose.com/) 向 Aspose 社群尋求協助與支援。

**Q: 我可以在無頭伺服器上將 HTML 轉換為 XPS 嗎？**  
A: 完全可以。Aspose.HTML 可在沒有 GUI 的環境中執行，只要確保 Java 執行環境正確設定即可。

**Q: 此函式庫支援自訂頁邊距嗎？**  
A: 支援。於將 `PageSetup` 指派給渲染選項前，可使用 `PageSetup.setMarginTop()`、`setMarginBottom()` 等方法設定頁邊距。

## 結論

我們已完整示範 **將 HTML 轉換為 XPS** 並使用 Aspose.HTML for Java 調整頁面大小的全流程。依照這些步驟，您可以產生符合精確版面需求的可列印 XPS 文件。歡迎嘗試不同的頁面尺寸、樣式，甚至加入頁首與頁尾，以符合專案需求。

如有任何問題或需要進一步協助，請參考 [Aspose.HTML for Java 文件](https://reference.aspose.com/html/java/) 或前往 [Aspose Forum](https://forum.aspose.com/) 交流討論。

---

**最後更新：** 2025-11-29  
**測試環境：** Aspose.HTML for Java 24.11（撰寫時最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}