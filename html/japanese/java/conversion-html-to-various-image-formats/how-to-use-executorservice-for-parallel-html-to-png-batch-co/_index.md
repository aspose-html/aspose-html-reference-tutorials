---
category: general
date: 2026-02-21
description: ExecutorService を使用して HTML を PNG に素早く変換する方法。Java で並列タスクを活用し、HTML ファイルをバッチ変換する手順を学びましょう。
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: ja
og_description: ExecutorService を使用して HTML ファイルをバッチで PNG に変換する方法。完全な Java の例を用いたステップバイステップガイド。
og_title: ExecutorService を使って HTML を PNG に並列変換する方法
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: ExecutorService を使用した並列 HTML から PNG へのバッチ変換方法
url: /ja/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

produce final content with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ExecutorService の使用方法：HTML‑to‑PNG バッチ変換を並列で実行する方法

HTML ページが大量に入ったフォルダーを PNG 画像に変換する必要があるとき、**ExecutorService の使い方**を疑問に思ったことはありませんか？ あなただけではありません—多くの開発者が、Web レポーティング パイプラインがシングルスレッドの変換ループで停滞するという壁にぶつかります。

良いニュースです。数行の Java と強力な Aspose.HTML `Converter` を使えば、ワーカースレッドのプールを立ち上げ、各 HTML ファイルをコンバータに渡し、画像が並列に生成される様子を見ることができます。このチュートリアルでは **convert html to png** の基本にも触れ、**run parallel tasks** の方法を示し、すぐに実行できる **batch convert html files** スクリプトを提供します。

## 前提条件

- Java 17 以降（コードは最新の `java.nio.file` API を使用）  
- クラスパスに Aspose.HTML for Java ライブラリを配置します。Maven Central から取得できます：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- ソースの `.html` ファイルが入ったディレクトリと、空の出力フォルダーを用意します。  
- 適度な量の RAM—各変換は独自のスレッドで実行されるため、プールサイズは CPU コア数に合わせるべきです。

> **プロのコツ:** ハイパースレッディング対応のマシンを使用している場合、`Runtime.getRuntime().availableProcessors()` は通常、最適なコア数を返します。

## ステップ 1 – 入力と出力パスの定義

まず、HTML が存在する場所と PNG を出力すべき場所を Java に伝える必要があります。`Path` オブジェクトを使用することで、コードはプラットフォームに依存しません。

```java
import java.nio.file.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Input folder containing .html files
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        // Output folder for the generated .png files
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");

        // Ensure the output folder exists
        Files.createDirectories(outputDir);
```

> **なぜ重要か:** 出力ディレクトリを事前に作成しておくことで、最初のワーカースレッドがファイルを書き込もうとしたときに `FileNotFoundException` が発生するのを防げます。

## ステップ 2 – 固定サイズスレッドプールの構築

**ExecutorService の使い方** の核心は、ハードウェアに合わせたプールを作成することです。*固定* プールは、実際に実行できる数以上のスレッドを生成しないことを保証します。

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **説明:** `ExecutorService` は低レベルのスレッド管理を抽象化します。`newFixedThreadPool` を使用することで、JVM にスレッドの再利用を任せ、スレッドの生成と破棄に伴うオーバーヘッドを削減します。

## ステップ 3 – HTML ファイルごとに 1 つの変換タスクを送信

ここでは、入力ディレクトリを走査し、すべての `*.html` ファイルを選択してプールに渡します。各タスクは `Converter.convert` を呼び出す小さなラムダです。

```java
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        // Build the output filename by swapping .html for .png
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();

                        // Perform the actual conversion
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }
```

### 背後で何が起きているか

1. **DirectoryStream** はファイル名を遅延読み込みするため、数千ファイルでもメモリ使用量が低く抑えられます。  
2. ラムダは `htmlFile` と `outputDir` をキャプチャするので、別個の `Runnable` クラスは不要です。  
3. `Converter.convert` はブロッキング呼び出しで、HTML を読み込み、レンダリングし、PNG を書き出します。各呼び出しが独自のスレッドで実行されるため、複数のファイルが同時に処理されます—これは **run parallel tasks** を期待する動作そのものです。

## ステップ 4 – プールを安全にシャットダウン

すべてのタスクがキューに入ったら、プールに新しい作業の受け付けを停止させ、すべてが完了するまで待機させます。何かがハングした場合、タイムアウトは 1 時間後に中止されますが、これはほとんどのバッチジョブに対して十分な時間です。

```java
        // No more tasks will be submitted
        pool.shutdown();

        // Wait up to 1 hour for all conversions to complete
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }

        System.out.println("All conversions completed.");
    }
}
```

> **エッジケース:** 非常に大きな HTML ファイルがある場合、タイムアウトを延長したりメモリ使用量を監視したりした方が良いかもしれません。`pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` を追加すると、呼び出し元スレッドが余剰タスクを実行するようになり、`RejectedExecutionException` を防げます。

## 完全な、すぐに実行できる例

以下は全プログラムです。`ParallelBatchConversion.java` という単一ファイルにコピー＆ペーストして使用できます。

```java
import com.aspose.html.converters.Converter;
import java.nio.file.*;
import java.util.concurrent.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Step 1: Define source and destination folders
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");
        Files.createDirectories(outputDir);

        // Step 2: Create a thread pool sized to the available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file found
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        pool.shutdown();
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }
        System.out.println("All conversions completed.");
    }
}
```

### 期待される出力

プログラムを実行すると、成功した変換ごとに 1 行が出力されます：

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

ファイルが失敗した場合、例外メッセージとともにエラー行が表示されるので、デバッグが簡単です。

## このパターンの拡張方法

- **異なる画像フォーマット:** `.png` 拡張子を `.jpg` や `.bmp` に置き換え、Aspose の変換オプションをそれに合わせて調整します。  
- **動的スレッド数:** I/O バウンドのワークロードの場合、プールサイズを (`availableProcessors() * 2`) に増やすことができます。  
- **進捗監視:** `System.out.println` を `jline` のようなスレッドセーフなプログレスバーライブラリに置き換えるか、ファイルにログ出力します。  
- **エラーハンドリング:** 失敗したパスを `List<Path>` に収集し、メインループ終了後に再試行します。

## よくある質問

**Q: Windows と Linux の両方で動作しますか？**  
A: はい。`java.nio.file` が基盤となるファイルシステムを抽象化しているため、Java をサポートする任意の OS でコードはそのまま動作します。

**Q: 10,000 以上の HTML ファイルがある場合はどうすればよいですか？**  
A: `DirectoryStream` イテレータはエントリを遅延読み込みするため、メモリ使用量は低く抑えられます。PNG 出力用にディスクの空き容量が十分あることを確認してください。

**Q: 各変換が使用するメモリを制限できますか？**  
A: Aspose.HTML では `HtmlLoadOptions` と `ImageSaveOptions` を使用してレンダリングエンジンを構成できます。最大ビットマップサイズを設定したり、低品質レンダリングを有効にしたりして、RAM 消費を抑えることができます。

## 結論

私たちは **ExecutorService の使い方** を通じて **HTML ファイルをバッチで PNG に変換** する方法を解説し、固定サイズプールが CPU バウンドのレンダリングに最適である理由を説明し、完全なコピー＆ペースト可能な Java プログラムを提供しました。上記の手順に従うことで、遅いシングルスレッドループを高速でスケーラブルなパイプラインに変換でき、数千ファイルをワンコマンドで処理できます。

次のチャレンジに備えましたか？`Converter.convert` を Aspose の PDF エクスポートに置き換えて **html to pdf** に変換してみるか、アップロードと変換リクエストを受け付ける Spring Boot マイクロサービスにこのロジックを組み込んでみてください。核心となる考え方—`ExecutorService` を使って **run parallel tasks** —は変わらず、無数のバッチ処理シナリオで役立つでしょう。

コーディングを楽しんで、スレッドが常に生き続けますように！

![ExecutorService の使用方法図](placeholder.png "並列 HTML‑to‑PNG 変換のためのスレッドプールワークフローを示す図")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}