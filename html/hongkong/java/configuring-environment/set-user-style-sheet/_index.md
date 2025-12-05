---
date: 2025-12-05
description: 學習如何在 Aspose.HTML for Java 中設定自訂使用者樣式表，從 HTML 建立 PDF，並使用使用者代理服務輕鬆將 HTML
  轉換為 PDF。
language: zh-hant
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 從 HTML 建立 PDF – 在 Aspose.HTML for Java 中設定使用者樣式表
url: /java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 HTML 建立 PDF – 在 Aspose.HTML for Java 中設定使用者樣式表

## 介紹
在本教學中，您將學會如何使用 Aspose.HTML for Java **從 HTML 建立 PDF**，同時套用自訂的使用者樣式表。  
是否曾想過要以自己的獨特樣式微調 HTML 文件的外觀？想像您正在製作網頁，需要標題以特定顏色突出，或段落在各裝置上保持一致的外觀。這時 **使用者樣式表** 與 **User Agent Service** 就派上用場了。我們將一步步說明——從撰寫簡易 HTML 檔案、設定使用者代理服務，到最終 **將 HTML 轉換為 PDF**——讓您即時看到結果。

## 快速回答
- **「從 HTML 建立 PDF」是什麼意思？** 即將包含 CSS、圖片、字型等的 HTML 文件渲染後，將視覺輸出保存為 PDF 檔案。  
- **需要哪個 Aspose 元件？** Aspose.HTML for Java 函式庫提供轉換引擎與 User Agent Service。  
- **測試時需要授權嗎？** 開發階段可使用免費試用版；正式上線則需商業授權。  
- **可以使用外部 CSS 檔案嗎？** 可以——就像一般瀏覽器一樣連結外部樣式表。  
- **轉換需要多久？** 以本指南中的簡單文件為例，轉換時間不到一秒。

## 前置條件
在開始撰寫程式碼之前，請先確保您已具備以下項目：

1. **Aspose.HTML for Java** – 從 [Aspose releases page](https://releases.aspose.com/html/java/) 下載最新 JAR。  
2. **Java Development Kit (JDK) 8+** – 確認 `java -version` 顯示 8 或更高版本。  
3. **IDE** – IntelliJ IDEA、Eclipse 或 NetBeans 均可。  
4. **基本的 HTML/CSS 知識** – 有助於理解，但非必須。

## 匯入套件
首先，匯入必要的 Java 類別。此範例唯一需要明確匯入的是 `java.io.IOException`；Aspose 類別稍後會以全限定名稱使用。

```java
import java.io.IOException;
```

## 步驟 1：建立簡易 HTML 文件
先撰寫一個最小的 HTML 檔案（`document.html`），作為 PDF 轉換的來源。

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **小技巧：** 將 HTML 檔案與 Java 原始碼放在同一目錄，可避免路徑相關的麻煩。

## 步驟 2：設定 Aspose.HTML 組態
建立 `Configuration` 物件。此物件是所有服務（包含 User Agent Service）的容器，稍後會用到。

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## 步驟 3：存取 User Agent Service  
**User Agent Service** 讓您注入自訂樣式表、設定預設字元集，並控制其他渲染選項。

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## 步驟 4：定義並套用使用者樣式表  
現在提供 CSS 規則，讓 HTML 在渲染時套用樣式。這裡會 **使用 User Agent Service** 來設定樣式表。

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **為什麼重要：** 在使用者代理層級套用樣式表，可確保即使原始 HTML 未引用 CSS 檔案，樣式仍會被遵守。

## 步驟 5：以自訂組態載入 HTML 文件  
將檔案路徑與 `Configuration` 實例一起傳入 `HTMLDocument` 建構子。如此即可將使用者樣式表綁定至文件。

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## 步驟 6：將 HTML 轉換為 PDF  
文件已完成樣式設定後，呼叫靜態 `convertHTML` 方法 **將 HTML 轉換為 PDF**。`PdfSaveOptions` 物件可讓您微調輸出（例如頁面大小、壓縮方式）。

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **結果：** `user-agent-stylesheet_out.pdf` 會呈現棕色標題與 GhostWhite 背景的段落，完全符合樣式表的定義。

## 步驟 7：清理資源  
務必釋放 Aspose 物件，以釋放原生記憶體。

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## 常見問題與解決方案
| 問題 | 原因 | 解決方式 |
|------|------|----------|
| **PDF 輸出空白** | 未套用樣式表或未以組態載入文件。 | 確認 `configuration` 已傳入 `HTMLDocument`，且在載入前已呼叫 `setUserStyleSheet`。 |
| **不支援的 CSS 屬性警告** | Aspose.HTML 不支援某些進階 CSS 功能。 | 僅使用 Aspose.HTML 文件中列出的 CSS 屬性，或改用較簡單的樣式。 |
| **FileNotFoundException** | `document.html` 路徑錯誤。 | 使用絕對路徑，或將 HTML 檔案放在專案根目錄。 |

## 常見問答

**Q: 可以為不同的 HTML 元素套用不同的樣式嗎？**  
A: 當然可以！您可以在使用者樣式表中定義任意數量的 CSS 規則。

**Q: 若需要動態變更樣式表該怎麼做？**  
A: 在建立新 `HTMLDocument` 實例前，再次呼叫 `setUserStyleSheet`；下一次轉換時即會套用新樣式。

**Q: Aspose.HTML for Java 能使用外部 CSS 檔案嗎？**  
A: 能——您可以在 HTML 中連結外部樣式表，或自行讀取內容後傳給 `setUserStyleSheet`。

**Q: Aspose.HTML 如何處理不支援的 CSS 屬性？**  
A: 不支援的屬性會被忽略，其他樣式仍會正常渲染，不會拋出錯誤。

**Q: 除了 PDF，還能將 HTML 轉換成其他格式嗎？**  
A: 能，Aspose.HTML 支援轉換為 XPS、TIFF、PNG、JPEG 等格式，只需使用對應的 `SaveOptions` 類別。

## 結論
現在您已了解如何透過 Aspose.HTML for Java 設定自訂使用者樣式表，**從 HTML 建立 PDF**。此工作流程讓您完整掌控產生 PDF 的視覺效果，適用於自動化報表、發票產生或任何需要一致樣式的情境。歡迎嘗試更複雜的 CSS、外部字型或其他轉換格式，進一步擴充此基礎。

---

**最後更新：** 2025-12-05  
**測試環境：** Aspose.HTML for Java 24.11（撰寫時的最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}