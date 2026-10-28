---
category: general
date: 2026-10-28
description: JavaでHTMLを読み取り、HTMLファイルからテキストを抽出する方法。Jsoupを使用してHTMLをテキストに変換する方法を学び、ファイルからHTMLを読むことやJavaでHTMLをテキストに変換するテクニックをカバーします。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: ja
lastmod: 2026-10-28
og_description: JavaでHTMLを読み取り、HTMLファイルからテキストを抽出する方法。このチュートリアルでは、Jsoupを使用してHTMLをテキストに変換する完全なソリューションを示します。
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: JavaでHTMLを読み込んでテキストを抽出する方法 – クイックガイド
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: JavaでHTMLを読み取り、テキストを抽出する方法 – ステップバイステップガイド
url: /ja/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでHTMLを読み取りテキストを抽出する方法 – ステップバイステップガイド

ローカルファイルから **how to read html** を読み取る必要がある場合、このガイドは完全なソリューションを提供します。HTMLドキュメントの読み込み、プレーンテキストの抽出、そして必要に応じてHTMLを細かく制御しながらテキストに変換する方法を学びます。チュートリアルの最後には、サンプルコードを実行して抽出されたテキストがコンソールに出力されるのを確認できます。

HTMLファイルの読み取りは、ウェブスクレイピングで取得したデータの処理、レポートの生成、またはユーザー生成コンテンツのクリーンアップなど、さまざまな場面で一般的なタスクです。以下の手順では、必要なライブラリの追加から、壊れたマークアップや文字エンコーディングの問題といったエッジケースの処理まで、すべてを網羅しています。

## 必要なもの

- Java 17 以上（コードは以前のバージョンでもコンパイル可能です）
- 依存関係管理のための Maven または Gradle、または手動で Jsoup JAR を追加
- プロジェクトの `src/main/resources` ディレクトリに配置された `input.html` という名前の HTML ファイル（パスは後で変更可能）

## Jsoup ライブラリのセットアップ

Jsoup は軽量でドキュメントが充実したライブラリで、HTML を DOM ライクな構造にパースします。壊れた HTML も優雅に処理できるため、**extract text from html** のタスクに最適です。

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

手動でダウンロードする場合は、JAR をクラスパスに置き、ソースファイルで `org.jsoup.*` をインポートしてください。

## ファイルから HTML を読み込む

最初のプログラム的なステップは、ファイルを `Document` オブジェクトに読み込むことです。Jsoup は `File` と文字セット名を受け取る静的 `parse` メソッドを提供しています。

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Why this matters:** `Jsoup.parse(File, String)` は生のバイト列を読み取り、指定された文字セットでデコードし、クリーンな DOM を構築します。これは自分で文字列に読み込むより安全で、Jsoup が改行を正規化し、一般的なマークアップエラーを自動的に修正します。

## HTML からプレーンテキストを抽出する

`Document` が取得できたら、可視テキストの取得はメソッド呼び出し一つです。`text()` メソッドはすべての要素のテキストコンテンツを連結し、タグ、スクリプト、スタイルを除外します。

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

`body()` 呼び出しは抽出対象を `<body>` 要素に限定します。これは **read html from file** でコンテンツ分析を行う際の典型的な対象です。結果の文字列は空白が単一スペースに縮小され、ブラウザがテキストを表示する方式を模倣しています。

### 期待される出力

`input.html` に次のような内容があるとします:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

プログラムを実行すると次が出力されます:

```
Extracted text:
Hello World This is a demo page.
```

## 追加オプションで HTML をテキストに変換する

`text()` だけでは不十分な場合があります。たとえば改行を保持したり、リスト番号を残したり、特定のタグを無視したりしたいときです。Jsoup の `NodeTraversor` とカスタム `NodeVisitor` を組み合わせると、そうした柔軟性が得られます。

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

シンプルな `doc.body().text()` 呼び出しを次のように置き換えてください:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Why this works:** ビジターは DOM を深さ優先で走査し、ブロックレベル要素（例: `<p>`、`<div>`、`<h1>`）の前に改行を追加します。これにより段落の区切りが保たれ、**convert html to text** で可読性や下流の NLP パイプラインに役立ちます。

## よくある落とし穴とベストプラクティス

| 問題 | 発生理由 | 推奨される対策 |
|------|----------|----------------|
| 文字コードが間違っている | ISO‑8859‑1 で保存されたファイルを UTF‑8 として解析すると文字化けが発生します。 | ファイルの meta タグ (`<meta charset="...">`) から文字コードを検出するか、`Jsoup.parse` に正しい文字コード名を渡します。 |
| 大きなファイル | 非常に大きな HTML ファイルをメモリに読み込むと `OutOfMemoryError` が発生する可能性があります。 | `Jsoup.parse(File, String, String baseUri)` を使用してファイルをストリームし、ノードをインクリメンタルに処理するか、JVM のヒープサイズを増やします。 |
| 不要な script/style テキスト | `text()` は script と style の内容を除去しますが、カスタムビジターが意図せずそれらを含めてしまうことがあります。 | ビジターの `head` メソッド内でタグ名が `script` または `style` のノードをスキップします。 |
| 空白の保持 | スペースを縮小すると、markdown 変換に必要なフォーマットが失われることがあります。 | 生のテキストノードには `Element.wholeText()` を使用し、後で空白を手動で処理します。 |

これらの点に対処することで、**html to text java** ソリューションが多様な入力に対して信頼性を保ちます。

## 完全に実行可能な例

以下は依存関係の設定から出力の検証まで、ワークフロー全体を示す自己完結型プログラムです。コードを `HtmlToTextDemo.java` という名前のファイルにコピーし、同じディレクトリに `input.html` を置いて、示すように `javac && java` で実行してください。

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Running the program

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

コンソールにはシンプルな抽出結果と詳細な結果の両方が表示されます。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [JavaでXPathを使用する方法 – HTMLを読み取りテキストを抽出する](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [JavaでHTMLを解析する方法 – HTML記事からテキストを抽出する](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [JavaでHTMLからテキストを抽出する – 完全ステップバイステップガイド](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}