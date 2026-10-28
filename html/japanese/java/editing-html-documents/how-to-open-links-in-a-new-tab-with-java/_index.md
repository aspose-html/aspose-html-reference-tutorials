---
category: general
date: 2026-10-28
description: JavaでHTMLを解析し、外部リンクを見つけて target="_blank" を追加することで、リンクを新しいタブで開く方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: ja
lastmod: 2026-10-28
og_description: Javaでリンクを新しいタブで開く：HTMLを解析し、外部リンクを見つけ、target="_blank"を追加し、修正したHTMLを保存する。
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Javaでリンクを新しいタブで開く – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Javaでリンクを新しいタブで開く方法
url: /ja/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaでリンクを新しいタブで開く方法

静的HTMLファイルから **リンクを新しいタブで開く** 必要がある場合、このガイドで手順をすべて解説します。**JavaでHTMLをパース**し、**外部リンクを検出**し、**target="_blank" を追加**し、**変更後のHTMLを保存**する方法を IDE を離れることなく学べます。

外部リンクを新しいブラウザタブで開くことでユーザー体験が向上し、訪問者が元のページにとどまることができます。以下のソリューションは任意のHTMLドキュメントで動作し、人気の **jsoup** ライブラリだけを必要とし、Java 8 以降で実行できます。

## 前提条件

開始する前に以下を用意してください：

* JDK 8 以上がインストール済み  
* **jsoup** 依存関係を取得できるビルドツール（Maven または Gradle）  
* `external` クラスが付与された `<a>` タグを含むHTMLファイル

Webサーバや追加フレームワークは不要です—jsoup がローカルで全て処理します。

## 手順 1: プロジェクトに jsoup を導入する

jsoup を依存関係として追加します。Maven を使用する場合は `pom.xml` に以下を記述してください：

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Gradle を使用する場合は `build.gradle` に次の行を追加します：

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

これらの座標は 2026年10月時点での最新安定版を取得します。同期後、Java ソースファイルで `org.jsoup` クラスをインポートできます。

## 手順 2: HTML ドキュメントをパースする

ファイルをパースすることが **リンクを新しいタブで開く** 最初のステップです。`Jsoup.parse` メソッドはファイルを可変な DOM ライク構造に読み込みます。

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*重要ポイント*: `Document` は CSS スタイルのセレクタを提供し、必要な要素の検索が非常に簡単になります。

## 手順 3: 外部リンクを見つける

次に、クラス `external` が付与されたすべての `<a>` 要素を取得します。これが **外部リンクを検出** する要件に該当します。

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` は一致したノードのコレクションです。セレクタが空集合を返す場合、HTML にクラスが無いか別の命名規則が使われています—セレクタを適宜調整してください。

## 手順 4: 各リンクに `target="_blank"` を追加する

**外部リンクを検出** で取得した各ノードに対し、`target` 属性を `_blank` に設定します。これが **target blank を追加** するステップであり、ブラウザがリンクを新しいタブで開くことを保証します。

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

`attr` メソッドは既存の `target` 値を上書きし、すべての外部アンカーで一貫した動作を実現します。

## 手順 5: 変更後の HTML を保存する

DOM を更新したら、変更をファイルに書き戻します。これでチュートリアルの **変更後の HTML を保存** 部分が完了します。

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` はドキュメント全体をシリアライズし、jsoup が最初にパースしたときのインデントやフォーマットを保持します。

## 完全動作例

すべての手順を組み合わせると、コピー＆ペーストで実行できる自己完結型プログラムが完成します。

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### 期待される出力

`sample.html` の内容が次のようになっているとします：

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

プログラム実行後、`updated.html` は以下のようになります：

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

外部リンクだけに `target="_blank"` 属性が付与され、ブラウザはそれを新しいタブで開くようになります。

## プロのコツとよくある落とし穴

* **プロのコツ:** CSS クラスが付いていなくても `http://` または `https://` で始まるリンクを外部とみなしたい場合は、セレクタを拡張します：`doc.select("a[href^=http]")`。
* **エッジケース:** すでに `target="_self"` が指定されているページがありますが、`attr` 呼び出しが上書きするため、一貫した動作が保証されます。
* **パフォーマンス:** 非常に大きな HTML ファイルを扱う場合は、メモリ使用量削減のためにストリーミングパース（`Jsoup.parse(File, String, String, Parser.htmlParser())`）を検討してください。
* **テスト:** `updated.html` をブラウザで開き、開発者ツールでリンクを確認し、`target` 属性が付与されているか検証します。

## 結論

これで **Javaでリンクを新しいタブで開く** 完全な実装例が手に入りました。チュートリアルでは **JavaでHTMLをパース**、**外部リンクを検出**、**target blank を追加**、**変更後のHTMLを保存** する方法を、軽量な jsoup ライブラリだけで解説しました。

ここからは次のように応用できます：

* セレクタを拡張して他のリンクパターン（例：`rel="external"`）に対応させる。  
* ビルドステップに組み込み、プロジェクト内のすべての HTML ファイルを自動処理する。  
* コードを大規模なコンテンツ管理パイプラインに統合する。

さまざまなセレクタや出力形式を試してみて、結果をコミュニティと共有してください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自の実装アプローチを探求したりするのに役立ちます。

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}