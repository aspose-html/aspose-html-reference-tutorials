---
category: general
date: 2026-04-05
description: Java 多執行緒教學，示範如何使用固定執行緒池平行執行任務，以及安全關閉 ExecutorService。
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: zh-hant
og_description: Java 多執行緒教學，帶你一步步執行平行任務、建立固定執行緒池、列印執行緒名稱，並乾淨地關閉 ExecutorService。
og_title: Java 多執行緒教學 – 使用固定執行緒池進行平行執行
tags:
- Java
- Concurrency
- ExecutorService
title: Java 多執行緒教學：使用固定執行緒池平行執行任務
url: /zh-hant/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java 多執行緒教學 – 簡易平行執行

有沒有想過如何在 Java 中 **run tasks parallel**，卻不被低階執行緒管理搞得焦頭爛額？在本 **java multithreading tutorial** 中，我們將一步步帶你完成：使用 **fixed thread pool java**、印出每個執行緒的名稱，並在工作完成後乾淨地 **shutdown executorservice**。

如果你曾寫過會在網路 I/O 上阻塞的迴圈，或需要同時抓取多個網頁，以下的模式將為你節省時間與麻煩。

我們會涵蓋所有必需的內容——不需要外部文件，只要純粹的 Java 程式碼，你可以直接 copy‑paste、執行並看到結果。完成後，你將了解為何固定執行緒池常是有界平行執行的最佳選擇、如何安全地終止它，以及如何透過印出執行緒名稱讓日誌更易讀。

> **Prerequisites**: Java 8+（`java.util.concurrent` 套件多年來已相當穩定）、IDE 或簡單的 `javac`/`java` 命令列，以及對 OOP 的基本認識。除你已擁有的 Aspose HTML for Java jar 外，無需其他額外函式庫。

---

![java multithreading tutorial diagram showing a thread pool feeding tasks](https://example.com/images/java-multithreading-tutorial.png "java multithreading tutorial diagram")

## java 多執行緒教學 – 設定固定執行緒池

**fixed thread pool** 會限制同時執行的執行緒數量，避免你的應用程式產生過多 OS 執行緒而耗盡資源。以下我們建立一個有四個工作者的池：

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Why four?* 它剛好符合我們要抓取的 URL 數量，但你可以根據 CPU 核心數、I/O 密集度或記憶體限制自行調整。`Executors` 工廠會幫你隱藏低階的 `Thread` 建構子，並提供乾淨的 `ExecutorService` 參考，之後你只要 **shutdown executorservice** 即可。

## 準備 URL 並定義平行任務

接下來，我們列出要處理的頁面。實際的爬蟲可能會從檔案或資料庫讀取，但靜態陣列讓範例保持自足：

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

現在進入 **run tasks parallel** 的部份。對每個 URL，我們提交一個 lambda，負責載入文件並印出標題。留意 `Thread.currentThread().getName()` 的使用——這就是我們的 **print thread name** 小技巧，讓除錯變得更簡單：

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

> **Pro tip**: 將 `HTMLDocument` 包在 try‑with‑resources 區塊中，可保證即使頁面載入失敗，底層串流也會被關閉。

## 優雅地關閉 ExecutorService

在工作完成後仍讓執行緒池存活會導致 JVM 卡住。正確的做法是 **shutdown executorservice**，然後等待終止：

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

*Why the timeout?* 它可防止某個永不回傳的惡意任務（例如卡住的網路呼叫）拖慢整體。如果池子在一分鐘內未結束，我們會呼叫 `shutdownNow()` 以中斷任何殘留的執行緒。

### 預期輸出

執行程式會印出類似以下內容：

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

實際順序可能會不同——畢竟任務是真正平行執行的。唯一不變的是 **print thread name** 前綴，讓你清楚知道是哪個工作者處理了哪個 URL。

---

## 常見變化與邊緣案例

| 情況 | 需要更改的項目 | 原因 |
|-----------|----------------|--------|
| **網址多於執行緒** | 保持相同的池大小；多餘的任務會自動排隊。 | 固定池會為你處理回壓。 |
| **CPU 密集型工作** | 將池大小設為 `Runtime.getRuntime().availableProcessors()`，而非硬編碼的 4。 | 在不過度訂閱的情況下最大化 CPU 使用率。 |
| **需要取消特定任務** | 保留從 `executor.submit()` 取得的 `Future<?>` 參考，並呼叫 `future.cancel(true)`。 | 提供對個別工作細緻的控制。 |
| **處理大型檔案** | 適度增加池大小 *或* 若預期突發則改用 `newCachedThreadPool()`。 | 快取池會按需建立執行緒，但需留意無限制成長的風險。 |

---

## 結論

你現在已掌握一套完整的 **java multithreading tutorial**，示範如何使用 **fixed thread pool java** 來 **run tasks parallel**、透過 **print thread name** 取得清晰日誌，並且 **shutdown executorservice** 乾淨收尾。完整、可執行的程式碼僅在單一類別中，你可以直接放入任何專案，立即擴展 I/O 密集型工作。

接下來可以嘗試將 `HTMLDocument` 換成自己的 HTTP 客戶端、實驗不同的池大小，或整合 `CompletionService` 以在任務完成時即時收集結果。若需要更進階的背壓處理，也可以探索 `java.util.concurrent.Flow` 來實作反應式串流。

祝程式開發順利，記得：只要選對執行緒池策略，並行處理就會變成 *piece of cake*，而不是 bug 的根源。如有任何問題，歡迎留下評論——我隨時樂於與你聊聊 Java 並行程式設計！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}