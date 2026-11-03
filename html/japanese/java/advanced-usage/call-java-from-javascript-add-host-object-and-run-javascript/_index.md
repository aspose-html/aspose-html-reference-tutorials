---
category: general
date: 2026-10-14
description: Aspose.HTML を使用して javascript から java を呼び出す方法を紹介します。ホストオブジェクトの追加方法、java
  での javascript の実行方法、そして javascript からのログ出力を簡潔なチュートリアルで学びましょう。
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Aspose.HTML を使用して javascript から java を呼び出す方法です。このガイドでは、ホストオブジェクトの追加、java
  での javascript の実行、そして javascript からのログ出力を、数行のコードで実現する方法を示します。
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: java から javascript を呼び出す – ホストオブジェクトを追加して java で javascript を実行する
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: java から javascript を呼び出す – ホストオブジェクトを追加して java で javascript を実行する
url: /ja/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaScript から Java を呼び出す – ホストオブジェクトを追加して Java で JavaScript を実行する

Java アプリケーション内で **JavaScript から Java を呼び出す** 必要がありますか？ 動的な HTML レポートエンジンを構築している場合や、制御できるスクリプトに Java ロガーを公開したい場合に役立ちます。このチュートリアルでは、ホストオブジェクトの追加方法、Java で JavaScript を実行する方法、そして **JavaScript から Java にログを出力** する方法を Aspose.HTML を使って詳しく解説します。

空の HTML ドキュメントを作成し、Java の `Logger` クラスをホストオブジェクトとして注入し、簡単なスクリプトを実行してコンソールに結果を出力する、完全に実行可能なサンプルを順を追って見ていきます。外部のウェブブラウザは不要、魔法のようなものは一切なく、すぐにコピー＆ペーストして実行できる純粋な Java コードです。

## クイック回答
- **ホストオブジェクトはどうやって追加しますか？** `document.getWindow().addHostObject("name", object)` で Java インスタンスを登録します。  
- **Java で JavaScript を実行できますか？** はい、`document.getWindow().eval(yourScript)` を使用します。  
- **JavaScript からのロギングは可能ですか？** もちろんです。ホストオブジェクトは任意の `void log(String)` メソッドを公開できます。  
- **必要な Aspose.HTML のバージョンは？** バージョン 23.10 以降でフルホストオブジェクト API がサポートされています。  
- **ウェブブラウザは必要ですか？** いいえ、Aspose.HTML は組み込みエンジンを提供するため、ヘッドレスで動作します。

## JavaScript から Java を呼び出すとは？
**JavaScript から Java を呼び出す** とは、Java オブジェクトを JavaScript ランタイムに公開し、スクリプトから直接 Java メソッドを呼び出せるようにする技術です。Aspose.HTML は Java プロセス内に軽量な JavaScript エンジンを作り、外部ブラウザなしで双方向通信を実現します。

## Java で JavaScript を実行するために Aspose.HTML を使用する理由
Aspose.HTML は **50 以上の入力・出力フォーマット** をサポートし、完全に準拠した HTML5 環境で JavaScript を評価できます。シンプルなワンライナーコードは平均で 200 ms 以内に処理され、フルブラウザスタックをロードしないため、Selenium ベースのアプローチと比較してメモリ使用量を最大 80 % 削減できます。

## 前提条件

- Java 17（または最近の JDK）がインストールされ、設定済みであること。  
- Aspose.HTML for Java ライブラリ（バージョン 23.10 以降）。Maven Central または Aspose の公式サイトから取得できます。  
- シンプルな IDE またはテキストエディタ；コマンドラインからも実行可能です。

> **プロのコツ:** Maven を使用している場合は、`pom.xml` に以下の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Gradle を使用する場合は次のように記述します。

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

基本が整ったので、ステップバイステップの解決策に入りましょう。

## ホストオブジェクトを追加して Java で JavaScript を実行する方法
`addHostObject` は Java オブジェクトを JavaScript コンテキストのグローバル変数として登録します。`HTMLDocument` をロードし、`addHostObject` を使って `"javaLogger"` という名前で Java ロガーを登録し、`javaLogger.log` を呼び出す短いスクリプトを評価します。全体のフローはたった 3 つの API 呼び出しで完了し、任意の Java 17 ランタイムで動作します。

### 手順 1: 最小限の Java プロジェクトを作成する

まず、`JsHostObjectDemo` という新しい Java クラスを作成します。このクラスに `main` メソッドとホストオブジェクトの定義を配置します。すべてを 1 ファイルにまとめることで、チュートリアルが自己完結し、コピーしやすくなります。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### なぜ `HTMLDocument` なのか？
`HTMLDocument` はメモリ上の HTML ドキュメントを表し、JavaScript エンジンを提供します。`HTMLDocument` クラスはフル HTML‑5 準拠のスクリプト環境を起動します。マークアップをロードしなくても、`window` オブジェクトを通じて JavaScript エンジンにアクセスでき、**Java で JavaScript を実行** する魔法がここにあります。さらに、DOM 操作やリソースのロード、スクリプトの評価がブラウザなしで可能です。

## ホストオブジェクト – “javaLogger” を追加する方法
`Logger` は `log(String)` メソッドだけを持つシンプルな Java クラスで、コンソールにメッセージを書き出します。`Logger` インスタンスを `"javaLogger"` という名前で登録すると、このドキュメント内で評価される任意のスクリプトから `javaLogger.log(...)` を呼び出せます。これが **ホストオブジェクトを追加** する核心であり、JavaScript コードからグローバル変数としてロガーを利用できるようになります。

### よくある落とし穴

- **名前衝突** – スクリプト内に既に `javaLogger` というグローバル変数がある場合、ホストオブジェクトが上書きされます。ユニークな名前を選んでください。  
- **スレッド安全性** – 同一ドキュメント上でスクリプトを並行実行する場合、ホストオブジェクトは共有されます。`synchronized` や `java.util.concurrent` パッケージのプリミティブを使ってスレッドセーフに実装してください。

## Java で JavaScript を記述して実行する方法
`eval` は文字列として渡された JavaScript をドキュメントのスクリプトエンジンで実行し、結果を返します。小さなスクリプトを `eval` に渡すと、エンジンはグローバルスコープから `javaLogger` を解決し、`log` メソッドを呼び出します。戻り値の取得や例外処理、複数評価のチェーンも可能です。

### 期待される出力

`main` メソッドを実行すると、コンソールに次の行が表示されます。

```
[JS] Hello from JavaScript!
```

## ホストを拡張する方法 – ロギング以外にも
ホストオブジェクトは `addHostObject` を通じて JavaScript に公開できる任意の Java インスタンスです。`Logger` クラスにメソッドを追加したり、新しいホストクラスを作成したりして機能を拡張できます。以下は、値を JavaScript に返す簡単な例です。ホストオブジェクトは複雑な型や I/O、他サービスとの連携も提供でき、値を返すことで双方向通信が可能になります。

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

この例を実行するとコンソールに次が表示されます。

```
[JS] 3+4=7
```

## スクリプト実行後にリソースをクリーンアップする方法
`dispose` は `HTMLDocument` インスタンスが保持するネイティブリソースを解放します。スクリプト環境の使用が終わったら必ず `HTMLDocument` を破棄してネイティブリソースを解放してください。`dispose()` を呼び忘れると、特にループや長時間稼働するサービスで多数のドキュメントを作成した場合にメモリリークが発生します。`try‑with‑resources` ブロックでラップするか、`finally` 節で `document.dispose()` を呼び出すようにしましょう。

```java
document.dispose(); // Important for long‑running applications
```

## 完全な動作例

以下がすぐにコンパイルして実行できる完全なソースファイルです。`JsHostObjectDemo.java` として保存し、Aspose.HTML の JAR をクラスパスに追加して `java JsHostObjectDemo` を実行してください。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

実行結果は次のようになります。

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## よくある質問

**Q: Android でも動作しますか？**  
A: はい。Aspose.HTML は純粋な Java ライブラリなので、Android の ART ランタイムを含む任意の JVM 上で動作します。

**Q: 複雑なオブジェクトを渡す必要がある場合は？**  
A: getter / setter を持つ POJO を公開すれば、エンジンが自動的に JavaScript オブジェクトにマッピングします。`java.util.List` や配列も変換可能です。

**Q: エラーハンドリングはどうなりますか？**  
A: スクリプトが JavaScript エラーをスローすると、`eval` は `ScriptException` を伝搬させます。`try‑catch` でラップしてログ出力やリカバリを行ってください。

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q: 複数のスクリプトを順次実行できますか？**  
A: 可能です。同一 `HTMLDocument` はグローバルスコープを保持するため、`eval` を何度でも呼び出せます。変数名の衝突にだけ注意してください。

**Q: ホストオブジェクトは信頼できないスクリプトに対して安全ですか？**  
A: 外部スクリプトはすべて信頼できない入力として扱うべきです。パラメータを検証し、必要最小限のメソッドだけを公開することでサンドボックス化を検討してください。

## ベストプラクティスとヒント

- **ホストオブジェクトの名前は分かりやすく**—`javaLogger`、`javaUtils` など—衝突を防ぎます。  
- **ホストメソッドは可能な限り小さく副作用なし** に保つとデバッグが楽になります。  
- **使用後は必ずドキュメントを破棄** し、Aspose.HTML が確保したネイティブメモリを解放してください。  
- **JavaScript からの入力は必ず検証** し、特に外部から取得したスクリプトの場合は外部データと同様に扱いましょう。

## 結論

これで **JavaScript から Java を呼び出す** 方法、**ホストオブジェクトを追加する** 方法、**Java で JavaScript を実行する** 方法、そして **JavaScript からロギングする** 方法を Aspose.HTML を使ってエンドツーエンドで実装できました。このパターンを使えば、任意の Java サービスをスクリプトに公開し、軽量なスクリプトプラットフォームとして Java アプリケーションを拡張できます。

次に試すべきこと:

- 完全な HTML ページを注入し、JavaScript から DOM を操作する。  
- ホストオブジェクトを使ってデータを Java 側にストリーム返却する（例: JSON シリアライズ）。  
- Nashorn や GraalVM など他のスクリプトエンジンと統合し、言語サポートを拡張する。

`Logger` や `Utils` クラスをいじってみて、**JavaScript ホストオブジェクト** の概念を自分のプロジェクトでどこまで活用できるか試してみてください。

---

**最終更新日:** 2026-10-14  
**テスト環境:** Aspose.HTML for Java 23.10  
**作者:** Aspose  






```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## 関連チュートリアル

- [Java でスクリプト実行を有効にする 完全 Aspose Html ガイド](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Java で Javascript を実行する 完全ガイド](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [Javascript をサンドボックス化する 完全 Aspose Html ガイド](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}