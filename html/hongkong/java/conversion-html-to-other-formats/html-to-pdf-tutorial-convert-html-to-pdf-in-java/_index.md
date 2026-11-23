---
category: general
date: 2026-06-19
description: 學習如何使用簡單的 Java 範例從 HTML 產生 PDF。本 HTML 轉 PDF 教學將示範如何使用 OpenHTMLtoPDF 將
  HTML 檔案轉換為 PDF。
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: zh-hant
og_description: HTML 轉 PDF 教學示範如何使用 Java 從 HTML 產生 PDF。跟隨步驟快速將 HTML 檔案轉換為 PDF。
og_title: HTML 轉 PDF 教學：Java 轉換指南
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: HTML 轉 PDF 教學：在 Java 中將 HTML 轉換為 PDF
url: /zh-hant/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML 轉 PDF 教學 – 使用 Java 將 HTML 頁面轉換為 PDF

有沒有想過如何在不離開 IDE 的情況下，將靜態 HTML 頁面轉換成精美的 PDF 文件？你並不孤單。在這篇 **HTML 轉 PDF 教學** 中，我們將一步步示範一個完整、可直接執行的 Java 範例，讓你在幾分鐘內 **generate pdf from html**。

我們會涵蓋所有必備內容——專案設定、加入正確的函式庫、撰寫轉換程式碼，甚至還有將即時網頁轉成 PDF 的小技巧。完成後，你將能在自己的機器上 **convert html file pdf**，並了解如何 **create pdf from html** 以應用於未來的任何專案。

## 你需要的環境

- Java 17 或更新版本（此程式碼相容於任何近期的 JDK）
- Maven 或 Gradle（我們將示範 Maven 片段）
- 一個想要轉成 PDF 的小型 HTML 檔案（我們會即時建立）
- IDE 或簡易文字編輯器——自行決定

就這樣。無需龐大的伺服器、無需付費 SDK，僅使用純 Java 與免費開源函式庫。

## 步驟 1：HTML 轉 PDF 教學 – 建立 Maven 專案

首先，建立一個新的 Maven 專案（或在現有專案中加入）。唯一真正需要的相依性是 **OpenHTMLtoPDF**，它負責將 HTML 與 CSS 渲染成 PDF 的繁重工作。

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **小技巧：** 若你使用 Gradle，可以在 `build.gradle` 的 `implementation` 中加入相同的相依性。  

此步驟的重要性：若沒有此函式庫，JVM 無法將 HTML 標籤轉換為 PDF 繪圖指令。OpenHTMLtoPDF 輕量、持續維護，且支援 CSS‑2.1，確保你的樣式保持不變。

## 步驟 2：generate pdf from html – 準備範例 HTML 檔案

讓我們在 Java 原始碼旁邊建立一個小型的 `input.html`。這樣範例即可自給自足，並展示 **create pdf from html** 的工作流程。

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

你可以將內容換成任何東西——表格、圖片，甚至 JavaScript（雖然渲染器會忽略腳本）。重要的是檔案必須位於 classpath 上，讓轉換器能夠找到它。

## 步驟 3：convert html file pdf – 撰寫轉換工具類別

現在進入 **HTML 轉 PDF 教學** 的核心：一個小型的 `HtmlToPdfConverter` 類別，用來讀取 HTML 並輸出 PDF。以下程式碼是一個完整、可執行的範例，請直接貼到 `src/main/java/com/example/HtmlToPdfConverter.java` 中。

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### 為什麼這段程式碼可行

1. **資源彈性** – 方法會先檢查提供的路徑是否指向實體檔案；若不是，則回退至 classpath 資源。這表示你之後可以透過傳入 URL 字串來 **convert webpage to pdf**（只需將 `withHtmlContent` 呼叫換成 `withUri`）。
2. **自動建立目錄** – `Files.createDirectories` 確保 `target/` 資料夾存在，避免出現「No such file or directory」錯誤。
3. **單行轉換** – `PdfRendererBuilder` 內部處理 CSS、字型與頁面版面配置。無需手動管理 PDF 頁面；函式庫會替你完成，使範例保持簡潔，且聚焦於 **convert html file pdf** 的概念。

## 步驟 4：create pdf from html – 執行程式並驗證

在專案根目錄開啟終端機，執行以下指令：

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

若設定正確，你會看到：

```
✅ PDF successfully created at target/output.pdf
```

使用任何 PDF 檢視器開啟 `target/output.pdf`。你應該會看到已套用樣式的「Monthly Sales Report」標題、段落文字，以及在 HTML `<style>` 區塊中定義的相同邊距。

> **如果看不到樣式該怎麼辦？**  
> 請確認 CSS 為內嵌樣式或與 HTML 位於同一資料夾。OpenHTMLtoPDF 會根據傳入 `withHtmlContent` 的基礎 URI 解析相對 URL。上述程式碼中我們傳入 `null`，對於簡單的內嵌 CSS 可正常運作。若使用外部樣式表，請將目錄路徑作為第二個參數傳入。

## 步驟 5：convert webpage to pdf – 處理遠端 URL（可選）

有時你需要直接從網路上 **convert webpage to pdf**——例如保存線上收據。函式庫支援透過 `withUri` 方式。以下是一個快速的改寫範例：

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

呼叫方式如下：



## 接下來你可以學習什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎延伸。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 Aspose.HTML for Java 於 Java 轉換 HTML 為 PDF](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [在 Aspose.HTML 中設定環境 – Java 轉換 HTML 為 PDF](/html/english/java/configuring-environment/)
- [Java 轉換 HTML 為 PDF – 含頁面尺寸設定的逐步指南](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}