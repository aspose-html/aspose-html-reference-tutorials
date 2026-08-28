---
category: general
date: 2026-02-10
description: 學習如何使用 Java 固定執行緒池來統計 HTML 檔案中的圖片數量、以 Java 同時執行任務，並正確關閉 Executor Service。
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: zh-hant
og_description: 精通 Java 固定執行緒池的使用，計算圖像、平行處理檔案，並安全關閉執行緒池服務。
og_title: Java 固定執行緒池：平行檔案中計算圖片數量
tags:
- Java
- Concurrency
- Aspose.HTML
title: java 固定執行緒池：平行檔案中的影像計數
url: /zh-hant/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – 平行影像計數教學

有沒有想過如何 **java fixed thread pool** 你的方式穿梭於數十個 HTML 檔案，快速取得影像計數？也許你曾盯著一個目錄的頁面，心想「我需要知道每個檔案有多少 `<img>` 標籤」，卻發現單執行緒的迴圈會花很久時間。  

好消息是，你不需要自行撰寫自訂執行緒管理器或與低階的 `Thread` 物件糾纏。在本指南中，我們將示範 **how to count images** 使用 *java fixed thread pool*，以及 **shutdown executor service**，在工作完成後優雅地關閉執行緒池。  

我們會從設定執行緒池、準備檔案清單、提交平行任務、處理邊緣案例，到驗證輸出全部說明。完成後，你將擁有一個可直接執行的程式，展示 **java parallel file processing** 的乾淨且易於維護的寫法。  

## 前置條件

在開始之前，請確認你已具備：

- Java 17 或更新版本（程式碼為簡潔起見使用 `var` 關鍵字，若需要亦可降級）。
- Aspose.HTML for Java 已加入 classpath – 你可以從 Maven Central 取得：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- 幾個想要分析的 HTML 檔案（本教學假設它們位於 `YOUR_DIRECTORY/`）。
- 你熟悉的 IDE 或建置工具 – IntelliJ IDEA、VS Code，或純粹使用 `javac` 都可以。

就這樣。沒有額外的伺服器、沒有 Docker，只有純 Java 加上一個小型的第三方函式庫。

## 步驟 1：建立 java fixed thread pool

*java fixed thread pool* 為你提供一組有界的工作執行緒，這些執行緒會在每次提交的任務之間重複使用。這樣可以避免不斷建立新執行緒的開銷，並限制同時併發的數量，對於從磁碟讀取檔案時尤為重要。

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**Why 4?** 如果你使用的是四核心筆記型電腦，四條執行緒即可讓每個核心保持忙碌而不會過度排程。若在核心更多的伺服器上，你可以將數量調高，但請記得每條執行緒都會開啟檔案句柄，過多可能會耗盡作業系統的限制。

## 步驟 2：列出要分析的 HTML 檔案

接下來的 **java parallel file processing** 只需要建立一個檔案路徑的陣列（或 `List`）。在實際專案中，你可能會遞迴走訪目錄、依副檔名過濾，或從資料庫讀取路徑。以下是最直接的寫法：

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

如果需要處理動態集合，可將靜態陣列改成類似下面的寫法：

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

上述程式碼示範了 **java parallel file processing**，不論檔案數量多少，都不需要改變其他程式碼。

## 步驟 3：提交任務至 **run tasks concurrently java**

現在進入教學的核心 – 我們會 **run tasks concurrently java**，為每個檔案提交一個 lambda。每個任務會使用 Aspose.HTML 讀取 HTML 文件，查詢所有 `<img>` 元素，並印出計數。

```java
import com.aspose.html.HTMLDocument;

public static void main(String[] args) throws InterruptedException {
    for (String filePath : htmlFiles) {
        executor.submit(() -> {
            // Load the document – Aspose.HTML does the heavy lifting
            HTMLDocument document = new HTMLDocument(filePath);
            // querySelectorAll returns a NodeList; its length is the image count
            int imageCount = document.querySelectorAll("img").length;
            System.out.println(filePath + " contains " + imageCount + " images.");
        });
    }

    // Step 4 is next – gracefully shut down the pool
    shutdownAndAwaitTermination();
}
```

**Why use a lambda?** Lambda 讓程式碼更簡潔，且不必額外建立 `Runnable` 類別。Lambda 會自動捕獲 `filePath`，因此每個任務都會在自己的檔案上執行。

### 如何 **count images** 高效執行

Aspose.HTML 只會解析一次檔案，建立 DOM，之後 `querySelectorAll("img")` 的執行時間為 O(n)，其中 *n* 為節點數量。對大多數 HTML 頁面而言，這幾乎可以忽略不計。若需要更快、僅串流的方式（例如處理 GB 級別的檔案），可以改用 SAX 解析器，但會犧牲本教學所追求的簡易性。

## 步驟 4：正確 **shutdown executor service**

千萬別忘記關閉執行緒池，否則 JVM 會一直跑下去。以下模式是推薦的 **shutdown executor service** 實作方式，會等所有任務完成後再關閉：

```java
private static void shutdownAndAwaitTermination() {
    executor.shutdown(); // Disable new tasks from being submitted
    try {
        // Wait a while for existing tasks to terminate
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            executor.shutdownNow(); // Cancel currently executing tasks
            // Wait a second for tasks to respond to being cancelled
            if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                System.err.println("Pool did not terminate");
        }
    } catch (InterruptedException ie) {
        // (Re-)Cancel if current thread also interrupted
        executor.shutdownNow();
        // Preserve interrupt status
        Thread.currentThread().interrupt();
    }
}
```

**What if a task hangs?** `shutdownNow()` 會嘗試中斷仍在執行的執行緒。只要你的影像計數邏輯能響應中斷（Aspose.HTML 本身不會在 I/O 上阻塞），執行緒池就能乾淨地終止。這個模式是任何 **java fixed thread pool** 使用的黃金標準。

## 步驟 5：驗證輸出

從 IDE 或命令列執行程式：

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

典型的輸出會是：

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

如果看到計數以任意順序印出，這是預期的行為 – 執行緒會在不同時間完成。重要的是每個檔案都有被計算，且程式在關閉序列後能乾淨退出。

## 完整範例（可直接複製貼上）

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelImageCounter {
    // 1️⃣ Fixed thread pool – change size based on your hardware
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);

    public static void main(String[] args) throws InterruptedException {
        // 2️⃣ List of HTML files – replace with your own directory
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a counting task for each file
        for (String filePath : htmlFiles) {
            executor.submit(() -> {
                HTMLDocument document = new HTMLDocument(filePath);
                int imageCount = document.querySelectorAll("img").length;
                System.out.println(filePath + " contains " + imageCount + " images.");
            });
        }

        // 4️⃣ Gracefully shut down the pool
        shutdownAndAwaitTermination();
    }

    // 5️⃣ Helper method to cleanly stop the executor
    private static void shutdownAndAwaitTermination() {
        executor.shutdown(); // Disable new tasks
        try {
            if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
                executor.shutdownNow(); // Cancel currently executing tasks
                if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                    System.err.println("Pool did not terminate");
            }
        } catch (InterruptedException ie) {
            executor.shutdownNow();
            Thread.currentThread().interrupt();
        }
    }
}
```

### 預期結果

執行此程式碼會印出每個檔案路徑以及其包含的 `<img>` 標籤數量，之後 JVM 結束。沒有殘留的執行緒，也不會有記憶體洩漏。

## 常見陷阱與專業提示

- **Pitfall:** 使用 `newCachedThreadPool()` 而非 *fixed* 池。前者會產生無界的執行緒，於大量批次時可能耗盡檔案描述子。請使用 `newFixedThreadPool`。
- **Pro tip:** 若 HTML 檔案非常龐大，考慮增加堆積大小 (`-Xmx2g`) 或改用串流解析器。對大多數行銷頁面而言，預設堆積已足夠。
- **Pitfall:** 忘記呼叫 `shutdown()` – 程式會在印出結果後卡住。上面的 `shutdownAndAwaitTermination` 方法能穩健處理。
- **Pro tip:** 若需要效能指標，可記錄每個任務的開始與結束時間。簡單的 `System.nanoTime()` 包住 `HTMLDocument` 建構，即可得知解析耗時。
- **Pitfall:** 硬編碼執行緒數量。可使用 `Runtime.getRuntime().availableProcessors()` 取得合理的預設值：

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## 相關主題您可能想進一步探索

- **run tasks concurrently java** 搭配 `CompletableFuture`，打造更具表達力的管線。
- 將影像計數結果持久化至資料庫，以供分析儀表板使用。
- 使用 **java parallel file processing** 結合 `java.nio.file.Files.walk` API 與 streams。
- 實作自訂的 `ThreadFactory`，為執行緒命名以利除錯。

## 結論

我們剛剛走過一個完整且自包含的範例，說明如何利用 **java fixed thread pool** 來 **how to count images**，同時示範正確的 **shutdown executor service** 方法。此模式具備良好的擴充性——只要把檔案陣列換成動態清單、調整池大小，即可應付任何 **java parallel file processing** 工作負載。  

試著執行、調整執行緒數量，甚至加入 CSV 匯出結果。結合穩固的併發基礎與 Aspose.HTML 這類好用的函式庫，幾乎沒有做不到的事。祝程式開發順利！  

![java fixed thread pool diagram](image.png){alt="java fixed thread pool diagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}