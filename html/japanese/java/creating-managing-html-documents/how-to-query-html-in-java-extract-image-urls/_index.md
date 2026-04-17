---
category: general
date: 2026-03-05
description: JavaでHTMLをクエリし、HTMLファイルを読み込んで画像を抽出する方法。JavaでHTMLファイルを読み込む方法、Javaで画像URLを取得する方法、そしてJavaでNodeListを反復処理する方法を学びましょう。
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: ja
og_description: JavaでHTMLをクエリし、画像URLを取得する方法。このガイドでは、JavaでHTMLファイルを読み込み、画像を特定し、NodeListを反復処理する方法を示します。
og_title: JavaでHTMLをクエリする方法 – 画像URLの抽出
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: JavaでHTMLをクエリする方法 – 画像URLを抽出する
url: /ja/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでHTMLをクエリする方法 – 画像URLを抽出

ページ上のすべての画像を取得するために、Javaで **HTMLをクエリする方法** を考えたことはありませんか？ あなただけではありません—開発者は常にHTMLファイルを読み取り、画像をスクレイプし、URLを有用に活用する必要があります。このチュートリアルでは、実践的な例を通じて **HTMLをクエリする方法**、JavaスタイルでHTMLファイルを読み込む方法、そしてJavaで画像URLを取得する方法を詳しく解説します。

本稿では Aspose.HTML for Java を使用しますが、XPath、CSSセレクタ、`NodeList` のイテレーションといった概念は任意の DOM ライブラリでも適用できます。このガイドの最後までに、**画像を抽出する方法** に慣れ、**NodeList を Java でイテレートする方法** を理解し、プロジェクトにすぐ組み込める実行可能なコードスニペットを手に入れることができます。

![JavaでHTMLをクエリする例](https://example.com/placeholder.png "JavaでHTMLをクエリする例")

---

## 学べること

- ディスクから HTML ドキュメントを読み込む (read HTML file Java)
- XPath と CSS セレクタの両方を使用して `<img>` タグを検索する (how to extract images)
- 取得した `NodeList` をループ処理する (iterate over NodeList Java)
- 各画像の `src` 属性を出力する (get image URLs Java)

外部サービスや複雑なビルドツールは不要です—純粋な Java と 1 つの Maven 依存関係だけです。

---

## 前提条件

- Java 8 以上がインストールされていること
- 依存関係管理のための Maven または Gradle
- HTML 構造に関する基本的な知識
- 任意だが便利: `<figure><img …></figure>` 要素を含むシンプルな HTML ファイル (`sample.html`)

これらが揃っていれば、すぐに始められます。

---

## ステップ 1: HTML ファイルを Java で読み込む – ドキュメントのロード

まず最初に、HTML をメモリに読み込む必要があります。Aspose.HTML の `HTMLDocument` クラスがその重い処理を担います。本を開いて任意のページをめくるイメージです。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**なぜ重要か:** ファイルをロードするとクエリ可能な DOM ツリーが得られます。パスが間違っていると `FileNotFoundException` が発生するので、実行前に場所を再確認してください。

---

## ステップ 2: XPath で画像を検索 – 画像を抽出する方法

XPath は強力なクエリ言語で、ノードをレーザーのように正確に特定できます。ここでは `alt` 属性を持つ `<figure>` 内のすべての `<img>` を取得します。

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**なぜ XPath?** 簡潔で、HTML が乱雑でも機能します。`//figure/img[@alt]` 式は「`alt` 属性を持つ `<figure>` 配下のすべての `<img>`」という意味です。他の属性でフィルタしたい場合は、ブラケット内を調整してください。

---

## ステップ 3: CSS セレクタで画像を検索 – 画像を抽出する代替方法

CSS の構文が好みの場合もあります。スタイルシートで書くのと同じ構文なので直感的です。`querySelectorAll` はブラウザで使用するのと同じセレクタを受け取ります。

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**なぜ両方?** 両方を示すことで、最も慣れたツールを選べることを示しています。実務ではどちらか一方に絞りますが、両例を提供することでチュートリアルがより完全になります。

---

## ステップ 4: NodeList を Java でイテレート – 画像 URL を取得する Java

コレクションが手に入ったので、これを順に処理します。ここで **NodeList を Java でイテレート** する必要があります。各画像の `src` 属性を取得して出力します。

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**なぜ従来の `for` ループか?** Aspose の `NodeList` は `Iterable` を実装していないため、拡張 `for‑each` 構文はコンパイルできません。インデックスループを使用することが **NodeList を Java でイテレート** する確実な方法です。

---

## 期待される出力

サンプル HTML に対してプログラムを実行すると、次のような出力が得られます。

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

以下のような結果が得られます。

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

ファイルに条件を満たす `<img>` タグが多いほど、数は増加します。

---

## よくある落とし穴とプロのコツ

- **ファイルパスの問題:** 絶対パスを使用するか、`sample.html` をプロジェクトの作業ディレクトリからの相対位置に置いてください。  
- **`alt` 属性がない:** 当方の XPath/CSS クエリは `[@alt]` でフィルタしています。すべての画像が必要な場合は属性フィルタを外してください（`//figure/img` または `figure img`）。  
- **パフォーマンス:** 大規模なドキュメントではストリーミングパーサーの使用を検討してください。ただし、ほとんどのウェブスクレイピングでは DOM アプローチで問題ありません。  
- **エンコーディングの問題:** Aspose.HTML は HTML に宣言された文字セットを尊重します。文字化けが発生した場合は、ファイルが UTF‑8 で保存されていることを確認してください。  

---

## 例の拡張

これで **画像 URL を Java で取得** できるようになったので、次のようなことをしたくなるかもしれません:

1. `java.net.URL` と `Files.copy` を使用して画像をダウンロードする。  
2. 後で処理できるように URL をデータベースに保存する。  
3. ファイル拡張子でフィルタする（`src.endsWith(".png")`）。

これらはすべて、ステップ 4 で示したループの簡単な拡張です。

---

## 結論

本ガイドでは、Java で **HTML をクエリする方法** を最初から最後までカバーしました：ファイルのロード、XPath と CSS セレクタの両方による画像の検索、そして **NodeList を Java でイテレート** して各画像の `src` を出力する方法です。これで **画像を抽出する方法** の確固たる基礎ができ、Aspose.HTML を使った **HTML ファイルを Java で読み込む方法** も正確に理解できました。

コードは自由にカスタマイズして、他の属性を取得したり、`<a>` タグを処理したり、URL をダウンローダに渡したりと、あなたのスクレイピングニーズに合わせてください。パターンは変わりません：ロード → クエリ → イテレート → アクション。

質問や面白いユースケースがあれば、下にコメントを残してください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}