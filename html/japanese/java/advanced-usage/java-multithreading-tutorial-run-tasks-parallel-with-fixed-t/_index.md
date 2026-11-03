---
category: general
date: 2026-04-05
description: Javaマルチスレッドチュートリアル：固定スレッドプールを使用してタスクを並列に実行し、ExecutorServiceを安全にシャットダウンする方法を示す。
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: ja
og_description: Javaのマルチスレッドチュートリアル：タスクを並列に実行し、固定スレッドプールを作成し、スレッド名を出力し、ExecutorServiceをきれいにシャットダウンする方法を解説します。
og_title: Javaマルチスレッドチュートリアル – 固定スレッドプールによる並列実行
tags:
- Java
- Concurrency
- ExecutorService
title: Javaマルチスレッドチュートリアル：固定スレッドプールでタスクを並列実行
url: /ja/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – 並列実行をシンプルに

Javaで低レベルのスレッド管理に悩まされずに **タスクを並列に実行** したいと思ったことはありませんか？この **java multithreading tutorial** では、**fixed thread pool java** を使い、各スレッドの名前を出力し、作業が完了したら **shutdown executorservice** をきれいに行う方法をステップバイステップで解説します。  

ネットワーク I/O でブロックするループを書いたことがある方や、複数のウェブページを同時にスクレイピングしたい方には、以下で紹介するパターンが時間と手間を大幅に削減します。  

外部ドキュメントは不要です。コピー＆ペーストできる純粋な Java コードだけを提供します。最後まで読めば、固定スレッドプールがなぜ限定的な並列処理に最適なのか、どう安全に終了させるか、そしてスレッド名を出力してログを見やすくする方法が理解できるでしょう。  

> **前提条件**: Java 8 以上（`java.util.concurrent` パッケージは長年安定しています）、IDE またはシンプルな `javac`/`java` コマンドライン、そして OOP の基本的な理解。追加のライブラリは不要です（既に持っている Aspose HTML for Java の JAR だけで OK）。

---

![java multithreading tutorial diagram showing a thread pool feeding tasks](https://example.com/images/java-multithreading-tutorial.png "java multithreading tutorial diagram")

## java multithreading tutorial – 固定スレッドプールの設定

**固定スレッドプール** は同時に実行できるスレッド数を上限付けし、アプリケーションが過剰に OS スレッドを生成してリソースを枯渇させるのを防ぎます。ここでは 4 つのワーカーでプールを作成します:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*なぜ 4 つか？* 取得する URL の数に合わせていますが、CPU コア数や I/O の負荷、メモリ制限に応じて調整可能です。`Executors` ファクトリは低レベルの `Thread` コンストラクタから解放し、後で **shutdown executorservice** できるクリーンな `ExecutorService` 参照を提供します。

## URL を用意し、並列タスクを定義する

次に処理したいページのリストを作ります。実際のスクレイパーではファイルやデータベースから読み込むでしょうが、ここでは例を自己完結させるために静的配列を使用します:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

いよいよ **タスクを並列に実行** する段階です。各 URL に対して、ドキュメントを読み込みタイトルを出力するラムダを `submit` します。`Thread.currentThread().getName()` を使っているのが **print thread name** のコツで、デバッグが格段に楽になります:

```java
        // Step 3: Submit a task for each URL that loads the document and prints its title
        for (String url : pageUrls) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(url)) {
                    String title = doc.getTitle();
                    // Print the thread name alongside the title
                    System.out.println(Thread.currentThread().getName() + " – " + title);
                } catch (Exception e) {
                    System.err.println(Thread.currentThread().getName() + " failed: " + e.getMessage());
                }
            });
        }
```

> **プロのコツ**: `HTMLDocument` を try‑with‑resources ブロックでラップすれば、ページの読み込みに失敗した場合でも基になるストリームが確実にクローズされます。

## ExecutorService を優雅にシャットダウンする

作業が終わった後にスレッドプールが残っていると、JVM がハングし続けます。正しい手順は **shutdown executorservice** を呼び出し、終了を待機することです:

```java
        // Step 4: Shut down the pool and wait for all tasks to finish
        executor.shutdown();                         // No new tasks will be accepted
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            // Force shutdown if tasks exceed the timeout
            executor.shutdownNow();
        }
    }
}
```

*タイムアウトを設定する理由は？* 返ってこないタスク（例: ハングするネットワーク呼び出し）から保護するためです。プールが 1 分以内に終了しなければ `shutdownNow()` を呼び出して残存スレッドを割り込ませます。

### 期待される出力

プログラムを実行すると以下のような出力が得られます:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

実行順序はタスクが真に並列であるため変わることがありますが、**print thread name** プレフィックスは常に表示され、どのワーカーがどの URL を処理したかが一目で分かります。

---

## よくあるバリエーションとエッジケース

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **スレッド数より URL が多い** | プールサイズはそのままにし、余分なタスクは自動的にキューイングされます。 | 固定プールがバックプレッシャーを自動で処理します。 |
| **CPU バウンドの処理** | ハードコードした 4 の代わりに `Runtime.getRuntime().availableProcessors()` を使用します。 | オーバーサブスクライブせずに CPU 利用率を最大化します。 |
| **特定タスクをキャンセルしたい** | `executor.submit()` から返される `Future<?>` を保持し、`future.cancel(true)` を呼び出します。 | 個別ジョブに対する細かな制御が可能になります。 |
| **大容量ファイルを処理する** | プールサイズをやや増やす *または* バーストが予想される場合は `newCachedThreadPool()` に切り替えます。 | キャッシュプールは必要に応じてスレッドを生成しますが、無制限に増えないよう注意が必要です。 |

---

## 結論

これで **java multithreading tutorial** は完了です。**fixed thread pool java** を使って **タスクを並列に実行** し、**print thread name** でログを見やすくし、**shutdown executorservice** をきれいに行う方法を実演しました。完全な実行可能コードは単一クラスに収められているので、任意のプロジェクトに貼り付けてすぐに I/O バウンドの作業をスケールアウトできます。

次のステップは？`HTMLDocument` を自前の HTTP クライアントに置き換えてみる、プールサイズを変えて実験する、あるいは `CompletionService` を導入してタスク完了時に結果を取得してみるなどです。さらに高度なバックプレッシャー制御が必要なら `java.util.concurrent.Flow` を使ったリアクティブストリームも検討してください。

Happy coding, and remember: with the right thread‑pool strategy, concurrency becomes a *piece of cake*, not a source of bugs. If you have questions, feel free to drop a comment—I'm always up for a chat about Java concurrency!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}