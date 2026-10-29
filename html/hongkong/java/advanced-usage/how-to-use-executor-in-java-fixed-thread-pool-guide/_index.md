---
category: general
date: 2026-05-28
description: 如何在 Java 中使用固定執行緒池的 Executor，從 HTML 中提取文字並加快處理速度——完整的 Java 執行緒池範例。
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: zh-hant
og_description: 如何在 Java 中使用具有固定執行緒池的執行器。學習完整的 Java 執行緒池範例，能有效率地從 HTML 檔案提取文字。
og_title: 如何在 Java 中使用執行器 – 固定執行緒池指南
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
title: 如何在 Java 中使用 Executor – 固定執行緒池指南
url: /zh-hant/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Executor – 固定執行緒池指南

有沒有想過 **如何使用 executor** 來一次執行大量任務而不會耗盡記憶體？你並不孤單。在許多實務應用中，你需要爬取一個資料夾內的 HTML 檔案，抽取正文，且要快速完成——這正是本教學要解決的情境。

我們將逐步說明一個 **fixed thread pool java** 的實作範例，該範例會從 HTML 中抽取文字、列印每個檔案的字元數，並且能安全關閉。完成後，你將擁有一個可直接放入任何專案的 **java thread pool example**，同時也會得到一些關於自訂池大小與處理例外情況的技巧。

> **你需要的環境**  
> * Java 17（或任何較新的 JDK）  
> * 一個輕量的 HTML 解析函式庫——我們會使用 *jsoup*，因為它經過實戰驗證且免設定。  
> * 幾個範例 *.html* 檔案，放在你自行選擇的目錄中。

---

## 如何使用固定執行緒池的 Executor

任何大量使用併發的 Java 程式的核心都是 `ExecutorService`。透過建立 **fixed thread pool**，我們告訴 JVM 僅保留 N 個工作執行緒，從而避免頻繁建立執行緒的開銷，並限制資源使用量。

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*為什麼這很重要:*  
如果為每個 HTML 檔案都啟動一個新的 `Thread`，作業系統必須在普通筆記型電腦上排程數十條執行緒，導致大量上下文切換的損耗。固定池會重複使用同樣的四條執行緒，讓 CPU 使用更可預測。

---

## 定義要處理的 HTML 檔案 – Fixed Thread Pool Java

接下來我們列出要送入執行緒池的檔案。在實際應用中，你可能會遍歷目錄樹；此處為了簡化示範，我們直接手動列出。

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*提示:* `List.of` 會回傳不可變的 List，能在多執行緒間安全共享，無需額外同步。

---

## 為每個 HTML 檔案提交獨立任務

現在我們將每個路徑交給 executor。提交的 lambda 會在四條工作執行緒中的其中一條 **平行** 執行。

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

**為什麼要把邏輯包在方法中**（`extractBodyText`），在下一節會說明——這樣可以讓 lambda 更簡潔，且方便在其他地方重複使用抽取程式碼。

---

## 從 HTML 抽取文字 – 核心邏輯

以下是可重複使用的輔助函式，實際上使用 Jsoup **抽取 html 文字**。它會開啟檔案、解析 DOM，並回傳純文字的 body 內容。

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

*為什麼選擇 Jsoup？* 它輕量、能優雅處理不完整的標記，且不需要完整的瀏覽器引擎。此方法會拋出 `IOException`，讓呼叫端自行決定如何記錄或復原——這在執行緒池情境中非常適合，因為你不希望單一壞檔案導致整個 executor 終止。

---

## 優雅關閉 Executor – 建立固定執行緒池

在提交完所有工作後，我們必須告訴執行緒池停止接受新任務，並完成已排隊的工作。

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

*說明:* `shutdown()` 會阻止新的提交，而 `awaitTermination` 會阻塞直到所有解析工作結束（或逾時）。若有任務卡住，`shutdownNow()` 會嘗試取消執行中的任務。此模式是安全 **create fixed thread pool** 的推薦做法。

---

## 完整、可執行的範例

將所有部份組合起來，以下是一個可直接編譯執行的單一檔案。它包含必要的匯入、`main` 方法，以及前述的輔助函式。

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

**預期輸出**（假設每個檔案的 body 文字大約有 1 200 個字元）：

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

如果有檔案遺失或格式錯誤，會在 `stderr` 印出堆疊追蹤，但其他任務仍會繼續執行——這正是良好 **java thread pool example** 應有的行為。

---

## 常見問題與邊緣情況

| 問題 | 答案 |
|----------|--------|
| *如果我有超過四個檔案呢？* | 執行緒池會將多出的任務排入佇列，待有執行緒空閒時即會執行。無需額外程式碼。 |
| *我應該改用 `newCachedThreadPool` 嗎？* | `newCachedThreadPool` 會根據需求動態建立執行緒，且可能無限制成長，對 I/O 密集的工作來說風險較高。**fixed thread pool** 能提供可預測的記憶體與 CPU 使用量。 |
| *如何根據 CPU 核心數調整池大小？* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` 是常見的做法。 |
| *如果某個檔案解析失敗會怎樣？* | lambda 內的 `catch (IOException e)` 會將失敗隔離、記錄錯誤，並讓執行緒池的其他任務繼續運作。 |
| *我可以把抽取的文字回傳給呼叫端嗎？* | 可以——改用 `Future<String>` 取代 `submit(Runnable)`。程式碼會是 `Future<String> f = executor.submit(() -> extractBodyText(path));`，之後再用 `String result = f.get();` 取得結果。 |

---

## 結論

我們已說明 **如何使用 executor** 來啟動一個 **fixed thread pool java**，平行處理一系列 HTML 檔案、抽取其 body 文字並回報字元數。完整的 **java thread pool example** 展示了正確的資源管理、錯誤處理以及可重複使用的抽取方法。

接下來的步驟？可以嘗試將 `extractBodyText` 換成更進階的爬蟲實作、實驗更大的池大小，或將結果寫入資料庫。你也可以探索 `CompletionService`，讓結果在完成時即時取得，這在檔案大小差異很大時特別有用。

隨意調整目錄路徑、加入更多檔案，或將此程式碼片段整合到更大的爬蟲框架中。核心模式——建立池、提交獨立任務、優雅關閉——不論工作負載多複雜，都保持不變。

祝編程愉快，願你的執行緒永遠保持活躍（當然，最後還是要好好關閉它們）！

## 相關教學

- [固定執行緒池 Java – 使用 ExecutorService 進行平行 HTML 清理](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [如何在 Java 中查詢 HTML – 完整教學](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [如何在 Java 中使用 Aspose.HTML - 精通 HTML5 Canvas 渲染](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}