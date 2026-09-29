---
category: general
date: 2026-09-29
description: Javaでクラスで要素を選択し、ファイルからHTMLを読み込み、外部リンクを見つける方法を学びましょう。このステップバイステップガイドでは、NodeListを効率的にイテレートする方法を解説します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: ja
lastmod: 2026-09-29
og_description: Javaでクラス名で要素を選択し、ファイルからHTMLを読み込み、querySelectorAllを使用して外部リンクを取得します。NodeListをイテレートする完全なサンプルに従ってください。
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Javaでクラス指定で要素を選択する – querySelectorAllによる完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: JavaでquerySelectorAllを使用してクラスで要素を選択する方法
url: /ja/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでquerySelectorAllを使用してクラスで要素を選択する方法

JavaでHTMLファイルを処理する際に **クラスで要素を選択** する必要がある場合、このガイドではその手順を正確に示します。ファイルからHTMLを読み取り、`querySelectorAll` を使用して外部リンクを見つけ、結果の `NodeList` を安全に反復処理する方法を学びます。

JavaでHTMLを扱うことはしばしば重く感じられますが、モダンなライブラリを使えば簡潔な CSS セレクタベースの API が利用できます。以下の例では **jsoup**（バージョン 1.17.2）を使用しています。jsoup は `querySelectorAll` スタイルのセレクタを実装しており、`NodeList` のように振る舞う `Elements` コレクションを返します。必要に応じて同じロジックを他の DOM 実装に適用することも可能です。

## 前提条件

* JDK 17 以上がインストールされていること。
* 依存関係管理のための Maven または Gradle。
* Java ストリームと DOM モデルに関する基本的な知識。

プロジェクトに jsoup を追加します:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## 手順 1: ファイルから HTML を読み込む

最初のタスクはディスクから HTML ドキュメントを読み込むことです。`Jsoup.parse(Path, Charset)` はファイルを読み取り、クエリ可能な DOM ツリーを構築します。

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Why this matters*: ファイルを一度だけ読み込むことで、後で要素を反復処理する際の繰り返し I/O を回避できます。`Document` オブジェクトは完全な DOM を保持し、迅速なセレクタクエリを可能にします。

## 手順 2: `querySelectorAll` を使用してクラスで要素を選択する

ドキュメントがメモリ上にあるので、CSS セレクタを使って **クラスで要素を選択** できます。セレクタ `"a.external"` は `external` クラスを持つ `<a>` タグにマッチします—これは **外部リンクを見つける** のに正確に必要なものです。

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Why this matters*: クラスセレクタを使用することで、表現力が高くパフォーマンスも良くなります。ライブラリはセレクタを最適化された走査に変換するため、すべてのノードに対して手動ループを書く必要がありません。

## 手順 3: Javaで NodeList (Elements) を反復処理する

`Elements` は `Iterable<Element>` を実装しているため、標準的な `for‑each` ループを使って **NodeList Java** オブジェクトを **反復処理** できます。以下のループは各リンクの `href` 属性を出力します。

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Why this matters*: 直接反復することでコードが読みやすくなり、単純な出力だけが必要な場合にコレクションをストリームに変換するオーバーヘッドを回避できます。

## 完全な動作例

3 つの手順を組み合わせると、コマンドラインから実行できる自己完結型プログラムが得られます。

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### 期待される出力

`input.html` に次のような内容が含まれているとします:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

プログラムを実行すると次のように出力されます:

```
External link: https://example.com
External link: https://openai.com
```

## プロのコツと一般的な落とし穴

* **Encoding matters** – 常に UTF‑8（またはソースに合わせた文字セット）でファイルを読み込んでください。エンコーディングが間違っていると属性値の文字が破損する可能性があります。
* **Multiple classes** – 要素に複数のクラスがある場合（例: `class="btn external"`）、セレクタ `"a.external"` は依然としてマッチします。CSS のクラスセレクタはトークンの有無をチェックするだけで、文字列全体と一致させるわけではありません。
* **Performance tip** – `href` 属性だけが必要な場合は、`doc.select("a.external[href]").eachAttr("href")` で直接取得できます。これにより、各マッチに対して完全な `Element` オブジェクトを作成する必要がなくなります。
* **Null safety** – `link.attr("href")` は属性が存在しない場合空文字列を返すため、出力前に null チェックを行う必要はありません。

## よくある質問

**Q: `<html>` ルートがない HTML フラグメントでも動作しますか？**  
A: はい。`Jsoup.parse` は入力をフラグメントとして扱い、欠落しているルート要素を自動的に追加するため、セレクタはフラグメントの body 上で機能します。

**Q: jsoup なしで `querySelectorAll` を使用できますか？**  
A: 標準の Java DOM API（`org.w3c.dom`）には `querySelectorAll` が含まれていません。**HTMLUnit** や **jodd-lagarto** などのライブラリが類似のメソッドを提供しています。ここで示したパターン（ロード → CSS で選択 → 反復）は同じです。

**Q: リンクを単に出力するだけでなく、変更したい場合はどうすればよいですか？**  
A: 各 `Element` を取得した後、`link.attr("href", "newUrl")` を呼び出し、`Files.writeString` でドキュメントをディスクに書き戻すことができます。

## 結論

これで、`querySelectorAll` スタイルのセレクタを使用して **クラスで要素を選択**、**ファイルから HTML を読み込み**、**外部リンクを見つけ**、そして **Java で NodeList を反復処理** する方法が分かりました。完全な例は、クリーンで本番環境でも使えるワークフローを示しており、より大規模なスクレイピングや変換パイプラインに組み込むことができます。

次に、**HTMLUnit を使った動的コンテンツの解析**、**変更した HTML をディスクに書き戻す**、または **Java ストリームを使用してリンク URL をリストに収集する** といった関連トピックを探求してください。これらはすべて、本稿で示したクラスベースの選択というコアテクニックに基づいています。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [JavaでHTMLをクエリする方法 – 要素を選択し、属性でフィルタリングし、テキストを取得](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [NodeList Java を反復 – HTML を読み込み画像 src を取得](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Aspose.HTML for Java でファイルから HTML ドキュメントをロード](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}