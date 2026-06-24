---
category: general
date: 2026-06-19
description: 再利用可能なRunnableを使用してJavaでスレッドを開始し、複数のスレッドを起動し、スレッド名を出力し、JavaでHTMLを解析する方法。ステップバイステップの例。
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: ja
og_description: Runnable を使用して Java でスレッドを開始し、複数のスレッドを実行し、スレッド名を表示し、Java で HTML を解析する、単一の実行可能なサンプル。
og_title: Javaでスレッドを開始する方法 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Javaでスレッドを開始する方法 – 完全ガイド
url: /ja/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java でスレッドを開始する方法 – 完全ガイド

ボイラープレートコードに悩まされずに **Java でスレッドを開始する方法** を知りたくありませんか？ あなたは一人ではありません。Web クローラーを作るときでも、UI の更新処理でも、重い計算をオフロードしたいときでも、スレッド生成のマスターはすべての Java 開発者にとって必須のスキルです。

このチュートリアルでは、実践的なシナリオとして **Java で HTML をパース** し、現在のスレッド名を出力し、同じロジックを共有する **複数のスレッドを開始** する方法を順を追って解説します。最後まで読めば **Runnable の使い方**、複数のワーカーの起動方法、期待通りの出力の確認方法がすべて分かります。すぐにコピー＆ペーストできる自己完結型の例も用意しています。

## 学べること

- `Thread` クラスと `Runnable` を使った **スレッド開始手順** の全容
- 同じタスクを **複数のスレッドで実行** する方法（コードの重複なし）
- 処理結果とともに **スレッド名を出力** する最もシンプルな方法
- 軽量な `HTMLDocument` ヘルパー（またはお好みのパーサ）を用いた **Java での HTML パース** 方法
- 再利用可能でテストしやすいコードを書く上で **Runnable の使い方** が重要な理由

コア例では外部ライブラリは不要ですが、必要に応じて Jsoup などのパーサに差し替えるポイントも示します。

---

## Step 1: 再利用可能なタスクを定義 – **Runnable の使い方**

まず最初に **Runnable の使い方** を理解し、各スレッドが実行すべき作業をカプセル化します。`Runnable` は `run()` メソッドだけを持つ関数型インターフェースで、ラムダ式と相性抜群です。

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**ポイント:** ロジックを `Runnable` に閉じ込めておけば、任意の数の `Thread` オブジェクトやスレッドプール、さらには `ExecutorService` にも渡すことができます。これによりコードが DRY かつテストしやすくなります。

---

## Step 2: **スレッド開始** – 最初のワーカーを作成

`Runnable` が用意できたら、`Thread` コンストラクタを呼び出すだけでスレッドを起動できます。**スレッド開始** の答えはたった一行です。

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

第2引数の `"Worker-1"` に注目してください。この名前は後で **スレッド名を出力** したときに表示され、デバッグが格段に楽になります。

---

## Step 3: **複数スレッドの開始** – 同じ Runnable を再利用

複数の HTML ファイルを同時に処理したいですか？ 同じ `Runnable` を使って別の `Thread` を作るだけです。これで **複数スレッドの開始** がタスクコードのコピーなしで実現できます。

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

`Worker-1` と `Worker-2` はどちらも `extractTextLength` で定義したブロックを同時に実行します。タスクがステートレス（ファイルを読むだけ）なので、競合状態を心配する必要はありません。

---

## Step 4: **スレッド名を出力** しながら HTML をパース

`Runnable` 内ですでに `Thread.currentThread().getName()` を呼び出しています。これが **スレッド名を出力** する標準的な方法です。出力例は次のようになります（HTML の body が 1 234 文字の場合）:

```
Worker-1: 1234
Worker-2: 1234
```

大きなファイルで実行すれば、両スレッドが同じファイルを読むため長さは同じになります。パスを変えるか、ファイル名をパラメータとして渡せば異なる結果が得られます。

---

## Step 5: 完全な実行可能サンプル – インポートから実行まで

以下は **自己完結型** のプログラム全体です。`HtmlThreadDemo.java` という名前で保存すればすぐに動作します。実際のパーサが無くてもコンパイルできるよう、簡易的な `HTMLDocument` スタブを同梱しています。実運用では Jsoup などに差し替えてください。

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### 期待される出力

`page.html` の `<body>` 内に 2 567 文字があると仮定すると、次のような出力が得られます。

```
Worker-1: 2567
Worker-2: 2567
```

ファイルが読めない場合は `catch` ブロックによりスタックトレースが出力されます。

---

## よくある落とし穴とプロのコツ

| 問題 | 発生原因 | 対策 |
|------|----------|------|
| **File not found** | パス `"YOUR_DIRECTORY/page.html"` が JVM 起動ディレクトリからの相対パスになっている | 絶対パスを使用するか、`Paths.get("").toAbsolutePath()` でデバッグ |
| **Race conditions** | `Runnable` が共有状態を変更するとスレッドが衝突する | タスクをステートレスに保つか、共有オブジェクトへのアクセスを同期 |
| **Too many threads** | `Thread` を大量に生成すると OS リソースが枯渇する | 基本をマスターしたら、サイズ制限付きの `ExecutorService` に切り替える |
| **Incorrect HTML parsing** | スタブ `HTMLDocument` が簡易的すぎて複雑なページで失敗する | Jsoup に置き換える: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## 例の拡張

**スレッド開始** の基本が分かったら、次のような拡張が考えられます。

- **異なるファイルを処理** – ファイル名を `Runnable` に渡す（コンストラクタや変数キャプチャを使用）
- **結果を収集** – `ConcurrentLinkedQueue<Integer>` に格納して出力だけでなく集計も可能に
- **スレッドプールを活用** – `Executors.newFixedThreadPool(4)` でスケーラビリティ向上
- **パーサを差し替え** – Jsoup、HtmlUnit、またはプロジェクトに合った任意のライブラリへ

これらのステップもすべて、再利用可能なタスクを定義し、1 つまたは複数のスレッドに渡し、**スレッド名を出力** してどのスレッドが作業しているかを確認するというコアアイデアに基づいています。

---

## 結論

Java で **スレッドを開始する方法**、再利用可能な作業のための **Runnable の使い方**、**複数スレッドの開始**、そして **HTML をパースしながらスレッド名を出力** するシンプルな手法を網羅しました。上記のコードスニペットはすぐに実行可能で、概念はより大規模な本番アプリケーションにもスケールします。

ぜひ実験してみてください。ファイルパスを変えたり、ワーカー数を増やしたり、実際の HTML パーサを組み込んだりしてみましょう。基本は変わりません。これでマルチスレッド Java プロジェクトの土台が固まりました。

スレッド安全性、ExecutorService、HTML パーサに関する質問があれば下のコメント欄へどうぞ。ハッピーコーディング！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを発展させた関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や代替実装アプローチの探求に役立ちます。

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}