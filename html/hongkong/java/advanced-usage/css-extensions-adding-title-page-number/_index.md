---
date: 2025-12-05
description: 學習如何使用 Aspose.HTML 設定 HTML 頁面邊距，並為文件加入頁碼與標題。
language: zh-hant
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: 如何使用 Aspose.HTML 在 Java 中設定 HTML 頁面邊距
url: /java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.HTML for Java 設定 HTML 頁面邊距

在本教學中，您將會了解 **如何以 Java 方式設定 HTML 頁面邊距**，並使用 Aspose.HTML for Java。我們將一步步示範如何建立自訂頁面邊距、插入頁碼以及加入文件標題，所有程式碼皆可直接複製到您的專案中。

## 快速答覆
- **需要的函式庫是什麼？** Aspose.HTML for Java  
- **可以程式化控制邊距嗎？** 可以，透過使用者樣式表中的 CSS `@page` 規則  
- **哪些輸出格式支援邊距設定？** XPS、PDF 以及其他點陣圖格式  
- **正式環境需要授權嗎？** 非試用版使用時必須擁有有效的 Aspose.HTML 授權  
- **是否相容於 Java 11 以上版本？** 完全相容 – 此函式庫支援現代 Java 版本  

## 什麼是「Setting HTML Page Margins Java」？
在 Java 中設定 HTML 頁面邊距，指的是在 Aspose.HTML 提供的渲染引擎上，於文件轉換為可列印格式（如 XPS 或 PDF）之前，設定 CSS 頁盒屬性。透過自訂 `@page` 規則，您可以控制可列印區域、頁碼以及頁首/頁尾內容。

## 為什麼使用 Aspose.HTML 來控制邊距？
- **精確版面** – CSS `@page` 讓您以像素為單位精準控制邊距、頁首與頁尾。  
- **跨格式一致性** – 相同的邊距定義同時適用於 XPS、PDF 與影像輸出。  
- **不依賴瀏覽器** – 渲染於伺服器端完成，無需使用 headless 瀏覽器。  

## 前置條件

在開始之前，請先確保已具備以下條件：

1. **Java 開發環境** – 已安裝 JDK 11 或更新版本。  
2. **Aspose.HTML for Java** – 從 [此處](https://releases.aspose.com/html/java/) 下載並安裝函式庫。  

## 匯入套件

開始之前，先匯入必要的 Aspose.HTML 類別：

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## 如何設定 HTML 頁面邊距 Java – 步驟說明

### 步驟 1：初始化 Configuration 並定義自訂頁面邊距

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

在此程式碼區塊中，我們建立 `Configuration` 物件，取得 `IUserAgentService`，並注入一段 CSS `@page` 規則，定義邊距、右下角頁碼以及上方置中文件標題。

### 步驟 2：建立 HTML 文件

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

此處我們以簡單的「Hello World」片段建立 `HTMLDocument`。步驟 1 中的相同設定會被套用，確保在渲染文件時使用自訂邊距。

### 步驟 3：渲染為 XPS 檔案（或其他支援的輸出）

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

此步驟會建立 `XpsDevice`，將渲染後的頁面寫入 `output.xps`。先前定義的邊距、頁碼與標題將會出現在最終檔案中。

## 常見問題與技巧

- **邊距未變更** – 確認 `@page` 規則未被其他樣式表覆寫。`setUserStyleSheet` 會將其設定為最高優先權。  
- **頁碼顯示「NaN」** – 請確認使用 Aspose.HTML 23.10 或更新版本；較舊版本不支援 `currentPageNumber()` 函式。  
- **輸出檔案為空白** – 確認 `Resources.output` 路徑正確解析且具寫入權限。  

## 常見問答

### Q1：什麼是 Aspose.HTML for Java？

**A：** Aspose.HTML for Java 是一套 Java 函式庫，提供在 Java 應用程式中處理 HTML 文件的強大工具，包含轉換、渲染與操作功能。

### Q2：我可以進一步自訂頁面邊距嗎？

**A：** 可以，只要編輯 `setUserStyleSheet` 內的 CSS，即可變更任何 `margin-*` 值，或加入額外的 `@top-*` / `@bottom-*` 盒子。

### Q3：如何在 HTML 文件中加入更多內容？

**A：** 將 `new HTMLDocument("<div>Hello World!!!</div>", …)` 中的字串替換為您自己的 HTML 標記，或使用 `HTMLDocument(String url, …)` 建構子載入外部檔案。

### Q4：Aspose.HTML for Java 是否相容其他文件格式？

**A：** 完全相容。相同的 `HTMLDocument` 可渲染為 PDF、XPS、影像，甚至 EPUB，只要切換輸出裝置（例如 `PdfDevice`、`PngDevice`）。

### Q5：使用 Aspose.HTML for Java 是否需要授權？

**A：** 需要。正式環境必須使用授權。您可從 [此處](https://purchase.aspose.com/buy) 或 [此處](https://releases.aspose.com/) 取得試用或正式授權。

### Q6：如何為奇數頁與偶數頁設定不同的邊距？

**A：** 在樣式表中使用 `@page :left` 與 `@page :right` 偽類別，分別定義左手（偶數）與右手（奇數）頁面的邊距。

### Q7：我可以在渲染的文件中嵌入自訂字型嗎？

**A：** 可以。將 `@font-face` 規則加入使用者樣式表，並在 HTML 內容中引用該字型。

## 結論

您現在已掌握 **如何使用 Aspose.HTML for Java 設定 HTML 頁面邊距**，並了解如何加入頁碼與標題，使文件更具專業感。歡迎嘗試額外的 `@page` 盒子、自訂字型或不同的輸出格式，以符合您的專案需求。

若遇到任何問題，官方的 [Aspose.HTML for Java 文件](https://reference.aspose.com/html/java/) 與 [Aspose 支援論壇](https://forum.aspose.com/) 均是絕佳的求助管道。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**最後更新：** 2025-12-05  
**測試環境：** Aspose.HTML for Java 23.12  
**作者：** Aspose  

---