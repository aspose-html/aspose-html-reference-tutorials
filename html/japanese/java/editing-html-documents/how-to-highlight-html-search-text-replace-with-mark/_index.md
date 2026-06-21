---
category: general
date: 2026-03-04
description: HTML内のテキストを検索し、マッチした部分を <mark> タグで囲んでハイライトする方法。テキストを <mark> 要素に置き換えるステップバイステップの
  Java ガイド。
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: ja
og_description: HTML内のテキストを検索し、マッチした部分を <mark> タグでラップしてハイライトする方法。テキストを <mark> で置換する完全な
  Java 例。
og_title: HTMLのハイライト方法 – テキストを検索して<mark>で置換
tags:
- Aspose.HTML
- Java
- Text Processing
title: HTMLのハイライト方法 – テキスト検索と<mark>で置換
url: /ja/java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML をハイライトする方法 – テキスト検索と `<mark>` で置換

特定の単語が複数回出現する場合、**HTML をハイライトする方法**を知りたくありませんか？ドキュメントサイトやブログエンジンを構築しているとき、あるいは静的ページでブランド名を強調したいときに役立ちます。実は、HTML 内のテキストを検索し、結果を `<mark>` 要素でラップすれば、かなりシンプルに実現できます。

このチュートリアルでは、HTML ファイルを読み込み、対象の単語を検索し、各出現箇所を `<mark>` タグで置換し、ハイライトされたバージョンを保存する完全な Java ソリューションを順を追って解説します。最後まで読めば、**HTML で単語をハイライトする**、**単語の出現箇所をハイライトする**、さらには **テキストを mark で置換する** 方法を、マークアップを壊すことなく実装できるようになります。

> **必要なもの**  
> • Java 17 以上（コードは以前のバージョンでも動作します）  
> • Aspose.HTML for Java ライブラリ（無料トライアルまたは正規ライセンス）  
> • 処理したいシンプルな HTML ファイル  

これらが揃ったら、さっそく始めましょう。  

![ハイライトされた HTML 出力を示すスクリーンショット – HTML のハイライト方法](/images/highlight-html-example.png "HTML のハイライト例")

## Step 1 – Load the HTML Document (How to Highlight HTML)

まずはソースファイルをメモリに読み込みます。Aspose.HTML の `Document` クラスが重い処理をすべて担当し、マークアップを DOM ライクな構造にパースしてクエリ可能にします。

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**ポイント:** ドキュメントをロードするとクリーンなオブジェクトモデルが得られるため、タグや属性を壊す心配なくテキストノードを安全に操作できます。また、空白が正規化されるので、後の **HTML でテキスト検索** ステップがより信頼性の高いものになります。

## Step 2 – Search Text in HTML for the Target Word

ドキュメントの準備ができたら、強調したい単語のすべての出現箇所を探します。`searchText` メソッドは `TextMatch` オブジェクトのリストを返し、各マッチが DOM のどこにあるかを示します。

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**プロのコツ:** デフォルトでは検索は大文字小文字を区別します。大文字小文字を無視した検索が必要な場合は、`searchText` を呼び出す前にドキュメントテキストと `searchTerm` を同じケースに変換するか、ライブラリが提供する正規表現ベースのアプローチを使用してください。

## Step 3 – Replace Text with `<mark>` (Highlight Word in HTML)

各マッチについて、対象ノードのテキストを再構築し、正確な単語の前後に `<mark>` 要素を挿入します。これにより、対象テキストだけが影響を受け、HTML の他の部分はそのまま残ります。

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**解説:**  
- `getStartOffset`/`getEndOffset` は、マッチが親ノード内で占める正確な文字位置を示します。  
- 元のテキストを `textBefore` と `textAfter` に分割することで、他の部分はそのまま保持します。  
- マッチを `<mark>` でラップするのが、**テキストを mark で置換する** 標準的な方法であり、追加の CSS が不要なブラウザネイティブのハイライトが得られます。

### エッジケースとヒント

- **同一ノード内での複数マッチ:** ループは各 `TextMatch` を順次処理します。ノード全体の内容を置換するたびにオフセットがシフトするため、Aspose.HTML はドキュメント順にマッチを返すので、ほとんどの場合シンプルな置換で対応可能です。重複するマッチがある場合は、すべてのマッチを先に収集し、1 回のパスでノードを再構築することを検討してください。  
- **生の HTML を含められない要素:** 親ノードが `<script>` や `<style>` ブロックの場合、`<mark>` を挿入するとページが壊れます。置換前に `parentNode.getNodeName()` をチェックして、該当ノードをスキップしてください。

## Step 4 – Save the Highlighted Document (Highlight Occurrences of Word)

すべての置換が完了したら、変更された DOM をディスクに保存します。出力ファイルには元のマークアップに加えて新しい `<mark>` タグが含まれ、実質的に **単語の出現箇所をハイライト** した状態になります。

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

`highlighted.html` を任意のブラウザで開くと、すべての “Aspose” が黄色がかった背景（`<mark>` のデフォルトスタイル）で囲まれているのが確認できます。カスタムデザインが必要な場合は、以下のように小さな CSS ルールを追加してください。

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## よくある質問 (Search Text in HTML – FAQs)

**Q: 単語が属性値の中に出現した場合はどうしますか？**  
A: `searchText` はノードのテキストコンテンツのみを対象とし、属性文字列は検索しません。属性値をハイライトしたい場合は、要素を走査して属性を手動でチェックする必要があります。

**Q: 1 回の処理で複数の異なる単語をハイライトできますか？**  
A: 可能です。単語リストを作成し、各単語に対して同じ置換ロジックを実行してください。ただし、マッチが重複する場合は注意が必要です。

**Q: `<section>` や `<article>` といった HTML5 専用タグでも動作しますか？**  
A: はい。Aspose.HTML は最新の HTML5 要素をフルサポートしているため、タグ種別に関係なく DOM トラバーサルが機能します。

## 完全動作サンプル (All Steps Combined)

以下は、ファイルの読み込みからハイライトされた出力の保存まで、全工程を実演する完全な Java プログラムです。

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**期待される出力:** `highlighted.html` を開くと、すべての “Aspose” がハイライト表示されます。ページの他の部分は変更されず、ファイルは有効な HTML ドキュメントのままです。

## 結論

プログラムで **HTML をハイライトする** 方法、すなわち **HTML でテキスト検索** して各マッチを `<mark>` タグでラップし、最終的に変更を永続化する手順を学びました。このアプローチにより、**HTML で単語をハイライトする**、**単語の出現箇所をハイライトする**、そして **テキストを mark で置換する** 作業を、壊れやすい文字列操作コードを書かずに実現できます。

次のステップは？

- 検索語をコマンドライン引数として受け取るようにする。  
- カスタムハイライト色を定義する CSS ファイルを生成する。  
- フォルダー内の複数 HTML ファイルを一括処理するバッチを作成する。  

これらのバリエーションに挑戦すれば、Aspose.HTML API と一般的なテキスト処理パターンの両方に対する理解が深まります。  

何か問題が発生したり、さらなる改善アイデアがあればコメントで教えてください。ハッピー・ハイライト！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}