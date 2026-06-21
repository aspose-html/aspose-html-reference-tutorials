---
category: general
date: 2026-03-14
description: Aspose.HTML を使用して JavaScript から Java を呼び出す方法を学びましょう。このガイドでは、ホストオブジェクトの追加、Java
  での JavaScript の実行、そして JavaScript からのログ出力方法を示します。
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: ja
og_description: Aspose.HTML を使用して JavaScript から Java を呼び出す。ホストオブジェクトを追加し、Java で JavaScript
  を実行し、JavaScript からログを出力する単一のチュートリアル。
og_title: JavaScript から Java を呼び出す – ホストオブジェクトを使った完全ガイド
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: JavaScriptからJavaを呼び出す – ホストオブジェクトを追加してJavaでJavaScriptを実行
url: /ja/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaからJavaScriptを呼び出す – ホストオブジェクトを追加してJavaでJavaScriptを実行する

Java アプリケーション内で **Java から JavaScript を呼び出す** 必要はありませんか？ 動的な HTML レポートエンジンを構築しているか、あるいは制御できるスクリプトに Java のロガーを公開したいだけかもしれません。このチュートリアルでは、ホストオブジェクトの追加方法、Java で JavaScript を実行する方法、そして **JavaScript から Java にログを出力** する方法を Aspose.HTML を使って具体的に解説します。

完全に実行可能なサンプルを通して、空の HTML ドキュメントを作成し、Java の `Logger` クラスをホストオブジェクトとして注入し、ちょっとしたスクリプトを実行して結果をコンソールに出力します。外部のウェブブラウザは不要、魔法のようなこともなく、今日すぐにコピー＆ペーストして実行できる純粋な Java コードだけです。

## 前提条件

- Java 17（または最近の JDK）がインストールされ、設定済みであること。
- Aspose.HTML for Java ライブラリ（バージョン 23.10 以降）。Maven Central または Aspose のウェブサイトから取得できます。
- シンプルな IDE またはテキストエディタ；コマンドラインからでも動作します。

> **プロのコツ:** Maven を使用している場合、`pom.xml` に以下の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Gradle を使用する場合は次の通りです。

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

基本が整ったので、ステップバイステップの解決策に入りましょう。

## 手順 1: 最小限の Java プロジェクトを作成する

まず、`JsHostObjectDemo` という名前の新しい Java クラスを作成します。このクラスは `main` メソッドとホストオブジェクトの定義を保持します。すべてを 1 ファイルにまとめることで、チュートリアルが自己完結し、コピーしやすくなります。

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

Aspose.HTML の `HTMLDocument` クラスは、完全な HTML‑5 準拠のスクリプト環境を立ち上げます。たとえマークアップを読み込まなくても、ドキュメントの `window` オブジェクトを通じて JavaScript エンジンにアクセスでき、ここで **Java で JavaScript を実行する** 魔法が起こります。

## 手順 2: ホストオブジェクト – “javaLogger” を追加する

以下の行

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

は **ホストオブジェクトを追加** するための重要な処理です。`Logger` インスタンスを名前 `"javaLogger"` で登録することで、このドキュメント内で評価される任意のスクリプトは `javaLogger.log(...)` を呼び出すことができます。これが **javascript host object** の核心であり、JavaScript が JVM に橋渡しできる仕組みです。

### よくある落とし穴

- **名前の衝突** – スクリプト内にすでに `javaLogger` というグローバル変数がある場合、ホストオブジェクトが上書きされます。ユニークな名前を選びましょう。
- **スレッド安全性** – ホストオブジェクトは同一ドキュメント上のスクリプト実行間で共有されます。並行してスクリプトを実行する予定がある場合は、クラスをスレッドセーフに（例: `synchronized` や `java.util.concurrent` のプリミティブを使用）してください。

## 手順 3: JavaScript を記述して実行する

`eval` に渡すスクリプトは意図的に小さくしています。

```javascript
javaLogger.log('Hello from JavaScript!');
```

`document.getWindow().eval(script)` が実行されると、エンジンはグローバルスコープで `javaLogger` を検索し、先ほど追加した Java オブジェクトを見つけて、渡された文字列でその `log` メソッドを呼び出します。

### 期待される出力

`main` メソッドを実行すると、コンソールに次の行が表示されます。

```
[JS] Hello from JavaScript!
```

この小さな行が、**Java から JavaScript を呼び出す** に成功し、**JavaScript からのログ** が普通の Java `System.out` メッセージと同じ場所に出力されたことを示しています。

## 手順 4: ホストを拡張する – ロギング以外も提供する

追加機能（例: ファイルアクセス、データベースクエリ）を公開したい場合は、`Logger` クラスにメソッドを増やすか、全く新しいホストクラスを作成します。以下は値を返す簡単な例です。

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

コンソールは次のように表示されます。

```
[JS] 3+4=7
```

これにより **javascript host object** パターンの柔軟性が実証されます。必要な Java API を任意に公開でき、データ型が Java と JavaScript の間で変換可能であれば（プリミティブ、文字列、配列など）問題ありません。

## 手順 5: リソースのクリーンアップ

スクリプト環境の使用が終わったら、`HTMLDocument` を破棄してネイティブリソースを解放します。

```java
document.dispose(); // Important for long‑running applications
```

破棄を忘れると、特にループ内で多数のドキュメントを生成する場合にメモリリークの原因となります。

## 完全な動作例

以下がすぐにコンパイルして実行できる完全なソースファイルです。`JsHostObjectDemo.java` として保存し、Aspose.HTML の JAR をクラスパスに入れ、`java JsHostObjectDemo` を実行してください。

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

プログラムを実行すると次が出力されます。

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

これが **Java から JavaScript を呼び出す** ワークフロー全体です。

## FAQ（よくある質問）

### Android でも動作しますか？

Aspose.HTML は純粋な Java ライブラリなので、Android の Dalvik/ART を含む任意の JVM 上で動作します。JAR をバンドルすれば、同じホストオブジェクト機能が利用可能です。

### 複雑なオブジェクトを渡す必要がある場合は？

フィールド、getter、setter を持つ POJO（Plain Old Java Object）を公開できます。エンジンは自動的にそれらを JavaScript オブジェクトにマッピングします。コレクションは `java.util.List` や配列を使用すれば変換可能です。

### エラーハンドリングはどうなりますか？

スクリプトが JavaScript エラーを投げた場合、`eval` は `ScriptException` を伝播します。try‑catch でラップしてログを取るかリカバリしてください。

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### 複数のスクリプトを順次実行できますか？

もちろん可能です。同一 `HTMLDocument` インスタンスはグローバルスコープを保持するため、`eval` を何度でも呼び出せます。ただし、スクリプト間で変数名が衝突しないよう注意してください。

## ベストプラクティスとヒント

- **ホストオブジェクトの名前は分かりやすく** – `javaLogger`、`javaUtils` など、混乱を避けるために明示的に命名しましょう。
- **ホストメソッドは可能な限り小さく副作用を持たない** 設計にするとデバッグが楽になります。
- **ドキュメントは使用後すぐに破棄** – Aspose.HTML が確保したネイティブメモリを速やかに解放します。
- **JavaScript からの入力は検証** – スクリプトが信頼できないソースから来る場合は、外部データと同様に慎重に扱いましょう。

## 結論

これで **Java から JavaScript を呼び出す** 方法、**ホストオブジェクトを追加する** 方法、**Java で JavaScript を実行する** 方法、そして **JavaScript からログを出す** 方法を Aspose.HTML を使ってエンドツーエンドで実装できました。このパターンは強力で、任意の Java サービスをスクリプトに公開でき、Java アプリケーションを軽量なスクリプトプラットフォームに変換できます。

次に試すべきこと：

- 完全な HTML ページを注入し、JavaScript から DOM を操作する。
- ホストオブジェクトでデータを Java 側にストリーム戻し（例: JSON シリアライズ）。
- Nashorn や GraalVM など、他のスクリプトエンジンと統合して言語サポートを拡張する。

`Logger` や `Utils` クラスをいじってみて、**javascript host object** の概念を自分のプロジェクトでどこまで活用できるか試してみてください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}