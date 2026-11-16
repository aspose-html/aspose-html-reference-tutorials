---
category: general
date: 2026-06-19
description: シンプルなJavaの例を使って、HTMLからPDFを生成する方法を学びましょう。このHTMLからPDFへのチュートリアルでは、OpenHTMLtoPDFを使用してHTMLファイルをPDFに変換する方法を示します。
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: ja
og_description: HTMLからPDFへのチュートリアルでは、Javaを使用してHTMLからPDFを生成する方法を紹介します。手順に従ってHTMLファイルをすばやくPDFに変換しましょう。
og_title: HTMLからPDFへのチュートリアル：Java変換ガイド
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
title: HTMLからPDFへのチュートリアル：JavaでHTMLをPDFに変換
url: /ja/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to pdf チュートリアル – JavaでHTMLページをPDFに変換する

IDEを離れずに静的なHTMLページをスタイリッシュなPDFドキュメントに変換する方法を考えたことはありませんか？ あなたは一人ではありません。この **html to pdf tutorial** では、数分で **generate pdf from html** できる、完全に実行可能なJava例を順に解説します。

プロジェクトのセットアップ、適切なライブラリの追加、変換コードの記述、さらにはライブウェブページをPDFに変換するための簡単なヒントまで、必要なすべてをカバーします。最後までで、ローカル環境で **convert html file pdf** ができるようになり、将来のプロジェクトで **create pdf from html** を行う方法が理解できるようになります。

## 必要なもの

- Java 17 以上（コードは最新のJDKで動作します）
- Maven または Gradle（ここでは Maven のスニペットを示します）
- PDFに変換したい小さなHTMLファイル（その場で作成します）
- IDE でもシンプルなテキストエディタでも構いません

以上です。重いサーバーや有料SDKは不要で、純粋なJavaと無料のオープンソースライブラリだけです。

## ステップ 1: html to pdf チュートリアル – Mavenプロジェクトのセットアップ

まず最初に、Mavenプロジェクトを新規作成するか（既存プロジェクトに）追加します。必要な依存関係は **OpenHTMLtoPDF** だけで、HTML と CSS を PDF にレンダリングする重い処理を担います。

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

> **Pro tip:** Gradle を使用している場合、同じ依存関係を `build.gradle` の `implementation` に追加できます。  

このステップが重要な理由: ライブラリがなければ、JVM は HTML タグを PDF の描画コマンドに変換する方法を知りません。OpenHTMLtoPDF は軽量で、アクティブにメンテナンスされており、CSS‑2.1 に対応しているため、スタイリングがそのまま保持されます。

## ステップ 2: generate pdf from html – サンプルHTMLファイルの準備

Java ソースと同じディレクトリに小さな `input.html` を作成しましょう。これにより例が自己完結し、**create pdf from html** のワークフローを示すことができます。

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

内容はテーブルや画像、JavaScript でも構いません（ただしレンダラはスクリプトを無視します）。重要なのは、ファイルがクラスパス上にあることです。コンバータがそれを見つけられるようにします。

## ステップ 3: convert html file pdf – 変換ユーティリティの作成

これが **html to pdf tutorial** の核心です: HTML を読み込み PDF を出力する小さな `HtmlToPdfConverter` クラスです。以下のコードは完全な実行例ですので、`src/main/java/com/example/HtmlToPdfConverter.java` にコピー＆ペーストしてください。

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

### このコードが機能する理由

1. **Resource flexibility** – メソッドはまず指定されたパスが実際のファイルかどうかを確認し、そうでなければクラスパスリソースにフォールバックします。これにより、後で URL 文字列を渡すだけで **convert webpage to pdf** が可能です（`withHtmlContent` の呼び出しを `withUri` に置き換えるだけ）。

2. **Automatic directory creation** – `Files.createDirectories` が `target/` フォルダの存在を保証するため、“No such file or directory” エラーが発生しません。

3. **Single‑line conversion** – `PdfRendererBuilder` が内部で CSS、フォント、ページレイアウトを処理します。PDF ページを手動で管理する必要はなく、ライブラリがすべて行うため、例は短くなり **convert html file pdf** の概念に集中できます。

## ステップ 4: create pdf from html – プログラムを実行して確認

プロジェクトルートでターミナルを開き、次のコマンドを実行します:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

正しく設定されていれば、次のように表示されます:

```
✅ PDF successfully created at target/output.pdf
```

`target/output.pdf` を任意の PDF ビューアで開きます。スタイルが適用された “Monthly Sales Report” ヘッダー、段落テキスト、HTML の `<style>` ブロックで定義した余白が表示されるはずです。

> **スタイリングが表示されない場合は？**  
> CSS がインラインであるか、HTML と同じフォルダにあることを確認してください。OpenHTMLtoPDF は `withHtmlContent` に渡したベース URI を基に相対 URL を解決します。上記のスニペットでは `null` を渡しており、シンプルなインライン CSS には機能します。外部スタイルシートを使用する場合は、第二引数にディレクトリパスを指定してください。

## ステップ 5: convert webpage to pdf – リモートURLの処理（オプション）

インターネット上のページを直接 **convert webpage to pdf** したいこともあります（例：オンライン領収書の保存）。ライブラリは `withUri` でこれをサポートしています。以下は簡単な適用例です:

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

呼び出し例:



## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを扱っています。各リソースは完全な動作コード例とステップバイステップの解説を含んでおり、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [HTML を PDF に変換する方法（Java） – Aspose.HTML for Java を使用](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [HTML を PDF に変換する（Java） – Aspose.HTML の環境設定](/html/english/java/configuring-environment/)
- [Java で HTML を PDF に変換 – ページサイズ設定付きステップバイステップガイド](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}