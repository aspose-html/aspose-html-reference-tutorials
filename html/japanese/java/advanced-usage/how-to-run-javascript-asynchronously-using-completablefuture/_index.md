---
category: general
date: 2026-02-16
description: CompletableFuture を使って Java で JavaScript を実行し、JS の遅延や非同期コードの評価方法を学びましょう。非同期
  JavaScript の評価に関するステップバイステップの完全ガイドです。
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: ja
og_description: この完全なチュートリアルで、JavaからJavaScriptを実行する方法、JSを遅延させる方法、そしてCompletableFutureを使用して非同期コードを評価する方法をマスターしましょう。
og_title: CompletableFuture を使って JavaScript を非同期に実行する方法
tags:
- javascript
- java
- asynchronous
- completablefuture
title: CompletableFuture を使用して JavaScript を非同期に実行する方法
url: /ja/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Run JavaScript Asynchronously Using CompletableFuture

Java アプリケーション内で **JavaScript を実行** し、メインスレッドをブロックしない方法をご存知ですか？ データ取得用の小さなスクリプトを呼び出したいが、UI がフリーズしてほしくない、というケースです。幸い、最新の Java ライブラリでは JavaScript を **非同期に** 評価でき、ブラウザと同様に遅延させることも可能です。本ガイドでは、Aspose HTML の `ScriptEngine` と `CompletableFuture` を組み合わせて **JavaScript を実行し**、結果を Java に戻す完全な実装例をご紹介します。

また、**CompletableFuture の使い方**、**JS の遅延方法**、**非同期コードの評価方法** についても解説し、**Java プロジェクトで JavaScript を非同期に評価** できるようになります。最後まで読めば、コピー＆ペーストして調整できるテンプレートが手に入ります。

---

## What You’ll Learn

- モダンな ES2022 JavaScript を実行できる Java `ScriptEngine` の設定方法。
- 遅延 (`how to delay js`) を含む `async` 関数の書き方。
- `evaluateAsync` を呼び出して `CompletableFuture` を取得する方法 (`how to use completablefuture`)。
- JavaScript の Promise が解決したら結果を取得する方法 (`how to evaluate async`)。
- エラーハンドリング、スレッド管理、パターン拡張のヒント。

外部のビルドツールは不要です。Aspose HTML for Java の JAR をクラスパスに入れるだけで始められます。さっそく見ていきましょう。

---

## Step 1: How to Run JavaScript – Initialize the Scripting Engine

まずはじめに。Aspose HTML ライブラリは JavaScript コードを実行できる `ScriptEngine` クラスを提供します。JVM 内で動作する小さな Chromium エンジンと考えてください。

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Why this matters:** `ScriptEngine` をインスタンス化することで、`async/await` を含む最新の JavaScript がすぐに使えるサンドボックス環境が手に入ります。外部の Node プロセスを起動する必要はありません。

---

## Step 2: How to Delay JS – Write an Async Function with a Promise‑Based Timer

JavaScript の `setTimeout` は実行を一時停止させる古典的な手段です。モダンなコードではこれを `Promise` でラップし、`await` できるようにします。スクリプト文字列でもまさに同じことを行います。

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **How to delay js:** `delay` ヘルパーは `ms` ミリ秒後に解決する Promise を作成します。`await` することで、Java スレッドをブロックせずに関数が一時停止します。

---

## Step 3: How to Evaluate Async – Run the Script and Get a CompletableFuture

同期的な `evaluate` メソッドの代わりに `evaluateAsync` を呼び出します。これにより、JavaScript の Promise が解決した時点で完了する `CompletableFuture<Object>` が即座に返されます。

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **How to evaluate async:** `evaluateAsync` は JavaScript のイベントループと Java の `CompletableFuture` を橋渡しします。これが **evaluate javascript asynchronously** の核心です。

---

## Step 4: How to Use CompletableFuture – Attach a Callback and Block for Demo

次に `thenAccept` でコールバックを登録し、結果をコンソールに出力します。デモ用にメインスレッドを少しだけブロックして完了を待ちます。

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Why we call `get()`:** 実際のアプリケーションでは別の処理を続行することが多いでしょう。ここでは例を完結させるためにブロックしています。

---

## Visual Overview

![CompletableFuture を使用して JavaScript を非同期に実行する方法を示す図](https://example.com/diagram.png "JavaScript の実行方法 – 非同期フロー")

*Alt text:* **CompletableFuture を使用して JavaScript を非同期に実行する方法を示す図** – 画像は Java からスクリプトエンジンへのフロー、非同期遅延、そして CompletableFuture の完了を示しています。

---

## Common Pitfalls & Best Practices (How to Evaluate Async Safely)

| Pitfall | What Happens | Fix |
|---------|--------------|-----|
| Promise を返すのを忘れる | `evaluateAsync` がすぐに `undefined` で解決される | スクリプトの最後の行を Promise（例: `fetchMessage();`）にする |
| JS 内で `Thread.sleep` のようなブロッキング呼び出しを使う | エンジンのイベントループが止まり、非同期が無意味になる | `delay` Promise パターンを使用する（上記参照） |
| 例外を無視する | Future が例外で完了しても見逃す | `.exceptionally(e -> { e.printStackTrace(); return null; })` を付与 |
| エンジンを閉じない | 長時間稼働するアプリでリソース漏れ | 使用後に `scriptEngine.dispose()` を呼び出す |

---

## Extending the Pattern (How to Use CompletableFuture in Real Projects)

複数の非同期 JavaScript 呼び出しをチェーンしたり、他の Future と組み合わせたり、カスタム `Executor` 上で実行したりできます。簡単な例を示します。

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **How to use CompletableFuture:** `Executor` を渡すことでスレッドプールを制御でき、UI の応答性を保ちつつスレッド枯渇を防げます。

---

## Expected Output

`JsAsyncDemo` クラスを実行すると、次のように表示されます。

```
JS result: Hello from async JS!
```

500 ms の待機はコンソール上では見えませんが、タイムスタンプを付加すれば遅延を確認できます。

---

## Recap – How to Run JavaScript with CompletableFuture

まず **Java 内で JavaScript を実行** し、`async` 関数で **JS の遅延** を実装、`evaluateAsync` で **非同期評価** を行い、**CompletableFuture** で結果を取得しました。これにより **evaluate javascript asynchronously** がシンプルかつ再利用可能な形で実現できました。

---

## What’s Next?

- **HTTP クライアントと統合:** 非同期 JS 内で REST エンドポイントからデータを取得し、Java に返す。
- **複数スクリプトの利用:** 複雑なパイプラインのために `evaluateAsync` を連鎖させる。
- **エンジンの差し替え:** 同じパターンは Nashorn、GraalVM、その他の JavaScript ランタイムでも動作します。`ScriptEngine` を差し替えるだけです。

遅延時間を伸ばしたり、例外を投げるスクリプトを試したり、WebAssembly モジュールを組み込んだりしてみてください。Java の並行処理プリミティブと最新の JavaScript を組み合わせれば、可能性は無限大です。

---

### Got Questions?

不明点があれば—たとえば、拒否された Promise の処理方法や、Java からスクリプトへ変数を渡す方法など—コメントでお気軽に質問してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}