---
category: general
date: 2026-02-11
description: JavaでAspose.HTMLを使用してHTMLドキュメントを作成します。JSON JavaScript を取得し、script 要素を追加し、JSON
  から HTML を生成し、JSON を pre に変換する方法を学びます。
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: ja
og_description: Aspose.HTML を使用して Java で HTML ドキュメントを作成します。JSON の JavaScript を取得し、script
  要素を追加、JSON から HTML を生成し、JSON を pre に変換—すべてをひとつのチュートリアルで。
og_title: JavaでHTMLドキュメントを作成する – 完全ガイド
tags:
- Aspose.HTML
- Java
- Web Automation
title: JavaでHTMLドキュメントを作成 – JSONを取得してコンテンツを生成
url: /ja/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTMLドキュメントの作成 – 完全なJavaチュートリアル

オンザフライで **HTMLドキュメントを作成** したいが、リモートデータをどうやって取り込むか分からないことはありませんか？ あなたは一人ではありません。多くのプロジェクトで、JavaScriptでJSONを取得し、その結果をページに注入し、最終的なマークアップを静的ファイルとして保存したい場面があります。このガイドでは、Aspose.HTML for Java を使用してその手順をまさに実演します。

空のドキュメントのインスタンス化から **fetch JSON JavaScript** の作成、**script 要素の追加**、そして **JSON から HTML を生成** し **JSON を pre** タグに変換** するまで、すべてのステップを順に解説します。最後には、取得したデータが整形された JSON として表示された `fetchResult.html` が手に入ります。

## 前提条件

- Java 17 以上（コードは JDK 11+ でもコンパイル可能）
- Aspose.HTML for Java ライブラリ（Maven Central から入手可能）
- HTML と非同期 JavaScript の基本的な知識
- IDE もしくはシンプルな `javac`/`java` コマンドライン環境

追加のフレームワークは不要です。すべてローカルで実行できます。

## 手順 1: プロジェクトのセットアップと Aspose.HTML のインポート

まず、`pom.xml` に Aspose.HTML の依存関係を追加します（または JAR を手動でダウンロード）。

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **プロのヒント:** バージョン番号は常に最新に保ちましょう。新しいリリースではバグ修正やスクリプトエンジンの改善が行われています。

## 手順 2: **HTMLドキュメントの作成** – 空のキャンバス

空の `HTMLDocument` を作成します。これは後でスクリプトを差し込むための、真新しいページと考えてください。

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

なぜドキュメントオブジェクトが必要かというと、Aspose.HTML の `ScriptEngine` は文字列ではなく DOM 上で動作するからです。適切なドキュメントを構築することで、エンジンに **fetch JSON JavaScript** を実行する実環境を提供できます。

## 手順 3: JavaScript スニペットの作成 – **Fetch JSON JavaScript** と **JSON を pre に変換**

チュートリアルの核心はこの複数行文字列です。非同期 `fetch` を実行し、JSON を解析した後、整形されたデータを `<pre>` 要素に書き込みます。

```java
        // Step 3: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;
```

コメント *Convert JSON to <pre>* に注目してください。これは `JSON.stringify(..., null, 2)` が行っていることと同じで、インデントを付与して人間が読みやすい形にしています。

## 手順 4: **Script 要素の追加** をドキュメントに組み込む

`<script>` タグを作成し、コードを内部に入れ、`body` に添付します。これが **add script element** の部分です。

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

なぜ `body` に添付するのか？ 実際のブラウザでは、スクリプトは解析された瞬間に実行されます。DOM に追加することでその挙動を正確に再現し、非同期 fetch がエンジン呼び出し時に走るようにします。

## 手順 5: スクリプトエンジンの実行 – 非同期 fetch の完了を待つ

Aspose.HTML は DOM ベースの JavaScript を実行できる `ScriptEngine` を提供します。`run()` を呼び出し、プロミスチェーンが解決するまで待機します。

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

エンジンはすべての保留タスク（今回の fetch を含む）が解決されるまでブロックし、生成された HTML にデータがすでに組み込まれていることを保証します。

## 手順 6: **JSON から HTML を生成** – 結果の保存

最後にドキュメントをディスクに保存します。ファイルには `<pre>` ブロックに JSON ペイロードが入った状態になります。

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

プログラムを実行すると `fetchResult.html` が生成されます。任意のブラウザで開くと、次のような表示が得られます。

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

これが求めていた **generate HTML from JSON** の結果です。

## 完全動作サンプル

以下がそのまま実行可能なソースファイルです。コピーして貼り付け、出力パスを調整し、`java JsFetchExample` を実行してください。

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;

        // Step 3: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);

        // Step 4: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();

        // Step 5: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

## 期待される出力と検証

1. **コンソール:** `HTML with fetched data saved.` と表示されます。  
2. **ファイル (`fetchResult.html`):** 開くと JSON が `<pre>` ブロック内に整形されて表示されます。  
3. **検証:** ページソースを確認すると `<pre>` 要素だけが残っており、スクリプトタグはエンジン実行後に除去されています。

## よくある質問とエッジケース

| 質問 | 回答 |
|----------|--------|
| *API がエラーを返した場合は？* | `fetch` 呼び出しを `try…catch` で囲み、JSON の代わりにエラーメッセージを body に書き込むようにします。 |
| *複数のリソースを取得できるか？* | 可能です。追加の `await fetch(...)` をチェーンするか、`Promise.all` を使用してください。最終的な `innerHTML` には複数の `<pre>` ブロックを連結できます。 |
| *CORS ヘッダーは必要か？* | スクリプトは Aspose.HTML のサンドボックス内で実行されるため、同一オリジンポリシーが適用されます。公開されている JSONPlaceholder エンドポイントは既にクロスオリジンリクエストを許可しています。 |
| *実行時に出力ディレクトリを変更する方法は？* | コマンドライン引数 (`args[0]`) でパスを受け取り、`htmlDoc.save` のハードコードされた文字列を置き換えます。 |
| *CSS を埋め込んでスタイリングしたい* | もちろん可能です。`<style>` 要素を作成し、`textContent` に CSS を設定してから `<head>` に追加し、エンジン実行前に組み込みます。 |

## 本番環境での活用ヒント

- エンドポイントが遅い場合は **JSON をキャッシュ** し、取得した文字列をファイルに保存して再利用できます。  
- 信頼できないソースからのデータを注入する場合は **サニタイズ** を必ず行いましょう。`JSON.stringify` を安全に使用するか、HTML エンティティをエスケープしてください。  
- `ScriptEngine` のタイムアウトを設定 (`scriptEngine.setTimeout(5000)`) して、応答がないサービスでのハングアップを防止します。

## ビジュアルサマリー

![create html document example showing the generated HTML with JSON inside a pre tag](fetchResult.png "生成された HTML ドキュメントのスクリーンショット（JSON が pre 要素内に表示）")

*代替テキスト:* *create html document example – 生成された HTML ファイルが pre 要素内に取得した JSON を表示しています。*

## 結論

これで、Java で **HTMLドキュメントをプログラム的に作成** し、**fetch JSON JavaScript** を実行し、**script 要素を追加**、**JSON から HTML を生成**、そして **JSON を pre** に変換して可読な出力を得る方法が分かりました。ワークフローはオフラインで完結し、必要なのは Aspose.HTML だけ。静的ファイルとしてどこでも配信可能です。

次のステップとして、配列オブジェクトをループ処理したり、CSS スタイルを追加したり、同じ手法で複数ページを生成したりしてみてください。`fetch` の URL を自分の API に置き換えれば、動的データを静的スナップショットに変換でき、SEO フレンドリーな事前レンダリングに最適です。

Happy coding, and feel free to share your experiments in the comments!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}