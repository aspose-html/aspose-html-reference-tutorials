---
category: general
date: 2026-05-28
description: Javaで固定スレッドプールを使用したExecutorの使い方、HTMLからテキストを抽出して処理を高速化する – 完全なJavaスレッドプールの例。
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: ja
og_description: Javaで固定スレッドプールを使用したExecutorの使い方。HTMLファイルからテキストを効率的に抽出する完全なJavaスレッドプールの例を学びましょう。
og_title: JavaでExecutorを使用する方法 – 固定スレッドプールガイド
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: JavaでExecutorを使う方法 – 固定スレッドプールガイド
url: /ja/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでExecutorを使用する方法 – 固定スレッドプールガイド

メモリを大量に消費せずに多数のタスクを同時に実行する **how to use executor** を考えたことはありますか？ あなただけではありません。実際のアプリケーションでは、HTMLファイルが入ったフォルダをクロールし、本文テキストを抽出し、かつ高速に処理する必要があります――このチュートリアルが解決するシナリオです。

**fixed thread pool java** の実装を順に見ていきます。HTMLからテキストを抽出し、各ファイルの文字数を出力し、きれいにシャットダウンします。最後まで読めば、任意のプロジェクトに組み込める自己完結型の **java thread pool example** が手に入り、プールサイズのカスタマイズやエッジケースの処理に関するヒントも得られます。

> **What you’ll need**  
> * Java 17 (or any recent JDK)  
> * A tiny HTML‑parsing library – we’ll use *jsoup* because it’s battle‑tested and zero‑config.  
> * A handful of sample *.html* files in a directory of your choice.

---

## 固定スレッドプールでExecutorを使用する方法

Any concurrency‑heavy Java program の中心は `ExecutorService` です。**fixed thread pool** を作成することで、JVM に正確に N 個のワーカースレッドを常駐させ、スレッド生成のオーバーヘッドを防ぎ、リソース使用量を上限します。

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Why this matters:*  
各 HTML ファイルごとに新しい `Thread` を起動した場合、OS は多数のスレッドをスケジュールしなければならず、コンテキストスイッチが頻発してノートパソコンでも負荷が高くなります。固定プールは同じ 4 つのスレッドを再利用するため、CPU 使用率が予測可能になります。

---

## 処理するHTMLファイルの定義 – Fixed Thread Pool Java

次に、プールに投入するファイル一覧を作ります。実際のアプリではディレクトリツリーを走査するでしょうが、ここではシンプルにします。

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Tip:* `List.of` は不変リストを返すため、追加の同期なしでスレッド間で安全に共有できます。

---

## 各HTMLファイルに対して個別のタスクを送信する

各パスを executor に渡します。送信したラムダは **in parallel** に 4 つのワーカースレッドのいずれかで実行されます。

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**Why we wrap the logic in a method** (`extractBodyText`) will become clear in the next section—it keeps the lambda tidy and lets us reuse the extraction code elsewhere.

---

## HTMLからテキストを抽出する – コアロジック

Jsoup を使って実際に **extracts text from html** する再利用可能なヘルパーです。ファイルを開き、DOM を解析し、プレーンな本文テキストを返します。

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*Why Jsoup?* 軽量で、壊れたマークアップも優雅に処理し、フルブラウザエンジンは不要です。メソッドは `IOException` をスローするので、呼び出し側でログ出力やリカバリ方法を決められます――スレッドプール環境で単一の不良ファイルが executor 全体を終了させないようにするのに最適です。

---

## Executorを優雅にシャットダウンする – Create Fixed Thread Pool

すべてのジョブを送信し終えたら、プールに新規タスクの受け入れを停止させ、キューに残っている仕事を完了させる必要があります。

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*Explanation:* `shutdown()` は新規サブミッションを防ぎ、`awaitTermination` はすべての解析ジョブが終了する（またはタイムアウトになる）までブロックします。何かがハングした場合は `shutdownNow()` が実行中のタスクをキャンセルしようとします。このパターンが **create fixed thread pool** を安全に行う推奨方法です。

---

## 完全な実行可能サンプル

すべてをまとめた単一ファイルです。コンパイルして実行できます。必要なインポート、`main` メソッド、上記ヘルパーが含まれています。

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**Expected output** (assuming each file contains roughly 1 200 characters of body text):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

ファイルが欠損している、または不正な形式の場合は `stderr` にスタックトレースが出力されますが、他のタスクは影響を受けずに続行します――これは適切に動作する **java thread pool example** がすべきことです。

---

## よくある質問とエッジケース

| Question | Answer |
|----------|--------|
| *What if I have more than four files?* | The pool will queue the extra tasks and run them as soon as a thread becomes free. No extra code needed. |
| *Should I use `newCachedThreadPool` instead?* | `newCachedThreadPool` creates threads on demand and can grow unbounded, which is risky for I/O‑heavy jobs. A **fixed thread pool** gives you predictable memory and CPU usage. |
| *How do I change the pool size based on CPU cores?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` is a common pattern. |
| *What if parsing fails for one file?* | The `catch (IOException e)` inside the lambda isolates the failure, logs it, and lets the rest of the pool keep working. |
| *Can I return the extracted text to the caller?* | Yes—use `Future<String>` instead of `submit(Runnable)`. The code would look like `Future<String> f = executor.submit(() -> extractBodyText(path));` and later `String result = f.get();`. |

---

## 結論

**how to use executor** を使って **fixed thread pool java** を立ち上げ、HTML ファイル群を並列に処理し、本文テキストを抽出して文字数を報告する方法を解説しました。完全な **java thread pool example** は、適切なリソース管理、エラーハンドリング、再利用可能な抽出メソッドを示しています。

次のステップは？ `extractBodyText` の実装をより高度なスクレイパーに差し替えたり、プールサイズを大きくしたり、結果をデータベースに流し込んだりしてみてください。また、`CompletionService` を使えば、ファイルサイズが大きく異なる場合でも、結果が出た順に取得でき便利です。

ディレクトリパスを調整したり、ファイルを増やしたり、このスニペットを大規模なクローリングフレームワークに統合したりして自由に試してください。コアパターン――プールを作成し、独立タスクを送信し、優雅にシャットダウンする――は、ワークロードがどれだけ複雑になっても変わりません。

Happy coding, and may your threads always stay alive (until you shut them down, of course)!

## 関連チュートリアル

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Use Aspose.HTML for Java - Mastering HTML5 Canvas Rendering](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}