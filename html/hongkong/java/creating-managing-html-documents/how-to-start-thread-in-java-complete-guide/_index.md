---
category: general
date: 2026-06-19
description: 如何在 Java 中使用可重用的 Runnable 開啟執行緒、啟動多個執行緒、印出執行緒名稱，並以 Java 解析 HTML。逐步範例。
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: zh-hant
og_description: 如何在 Java 中使用 Runnable 開啟執行緒、同時執行多個執行緒、列印執行緒名稱，並在單一可執行範例中以 Java 解析
  HTML。
og_title: 如何在 Java 中啟動執行緒 – 完整指南
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
title: 如何在 Java 中啟動執行緒 – 完整指南
url: /zh-hant/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中啟動執行緒 – 完整指南

有沒有想過 **how to start thread** 在 Java 中該怎麼做，卻不想被大量樣板程式碼淹沒？你並不是唯一有此困惑的人。無論你是在打造網路爬蟲、UI 更新器，或只是需要將繁重的計算交給背景執行，掌握執行緒的建立都是每位 Java 開發者必備的技能。

在本教學中，我們將以一個實務情境示範：**parse HTML with Java**、印出目前執行緒的名稱，並 **start multiple threads** 共享相同的邏輯。完成後，你將了解 **how to use Runnable**、如何啟動多個工作者，並看到預期的輸出——全部都是可以直接 copy‑paste 的自包含範例。

## 你將學會

- 使用 `Thread` 類別與 `Runnable` 的 **how to start thread** 完整步驟。  
- 如何 **start multiple threads** 以執行相同任務而不必重複程式碼。  
- 最簡單的 **print thread name** 方法，讓處理結果一目了然。  
- 使用輕量級 `HTMLDocument` 輔助工具（或任何你偏好的解析器）**parse HTML with Java** 的乾淨寫法。  
- 為何 **how to use runnable** 對於可重用、可測試的程式碼如此重要。

核心範例不需要外部函式庫，但我們會說明在需要更強大功能時，如何改用 Jsoup 或其他解析器。

---

## Step 1: 定義可重用的任務 – **how to use runnable**

首先，你需要了解 **how to use runnable**，即將每個執行緒要執行的工作封裝起來。`Runnable` 只是一個只有 `run()` 方法的函式介面，非常適合用 lambda 表達式。

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

**為什麼這很重要：** 把邏輯放在 `Runnable` 內，你可以把它交給任意數量的 `Thread` 物件、執行緒池，甚至日後的 executor service。這樣可以讓程式碼保持 DRY（不要重複自己）且易於測試。

---

## Step 2: **How to start thread** – 建立第一個工作者

有了 `Runnable` 後，啟動執行緒只需要呼叫 `Thread` 建構子。一行程式碼即可解答 **how to start thread** 的問題：

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

注意第二個參數 `"Worker-1"`。這個名稱會在之後 **print thread name** 時顯示，讓除錯變得不那麼神祕。

---

## Step 3: **Start multiple threads** – 重複使用相同的 Runnable

想同時處理多個 HTML 檔案嗎？只要再建立一個 `Thread`，使用相同的 `Runnable` 即可。這示範了 **start multiple threads** 而不必複製任務程式碼：

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

`Worker-1` 與 `Worker-2` 會同時執行 `extractTextLength` 中的程式區塊。因為任務是無狀態的（只讀檔案），所以不會產生競爭條件。

---

## Step 4: **Print thread name** 同時解析 HTML

在 `Runnable` 內，我們已經呼叫 `Thread.currentThread().getName()`。這是 **print thread name** 的標準做法。輸出大致會是這樣（假設 HTML body 含有 1 234 個字元）：

```
Worker-1: 1234
Worker-2: 1234
```

如果改用較大的檔案執行，兩行會顯示相同的長度，因為兩個執行緒讀取的是同一個檔案。你可以變更路徑或將檔名作為參數傳入，以看到不同的結果。

---

## Step 5: 完整、可執行的範例 – 從匯入到執行

以下是完整的 **self‑contained** 程式，你可以直接存成 `HtmlThreadDemo.java`。它內含一個簡易的 `HTMLDocument` stub，讓程式即使沒有真實的解析器也能編譯。正式環境可將 stub 換成 Jsoup 或其他你偏好的函式庫。

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

### 預期輸出

假設 `page.html` 的 `<body>` 內有 2 567 個字元，執行結果會類似：

```
Worker-1: 2567
Worker-2: 2567
```

若檔案無法讀取，會印出例外堆疊資訊——這是 `catch` 區塊的作用。

---

## 常見陷阱與專業技巧

| 問題 | 為什麼會發生 | 解決方式 |
|------|--------------|----------|
| **找不到檔案** | 路徑 `"YOUR_DIRECTORY/page.html"` 是相對於 JVM 啟動位置的相對路徑。 | 使用絕對路徑或 `Paths.get("").toAbsolutePath()` 來除錯。 |
| **競爭條件** | 若 `Runnable` 變更共享狀態，執行緒會相互衝突。 | 保持任務無狀態，或對共享物件加上同步機制。 |
| **執行緒過多** | 同時產生大量 `Thread` 可能耗盡作業系統資源。 | 在掌握基礎後，改用具有限制的 `ExecutorService`。 |
| **HTML 解析不正確** | Stub `HTMLDocument` 太簡易，複雜頁面會失效。 | 換成 Jsoup：`Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## 延伸範例

既然你已掌握 **how to start thread**，接下來可以：

- **解析不同檔案**：將檔名傳入 `Runnable`（使用建構子或捕獲變數的 lambda）。  
- **收集結果**：改用 `ConcurrentLinkedQueue<Integer>` 而非僅列印。  
- **使用執行緒池**：`Executors.newFixedThreadPool(4)` 提升可擴充性。  
- **更換解析器**：改用 Jsoup、HtmlUnit 或任何符合專案需求的函式庫。

所有這些步驟仍然依賴我們討論的核心概念：定義可重用的任務、交給一個或多個執行緒，並透過 **print thread name** 觀察是哪個執行緒在工作。

---

## 結論

我們已說明 **how to start thread** 在 Java 中的使用方式，示範了 **how to use runnable** 以建立可重用的工作，展示了 **start multiple threads** 的技巧，並以簡易方式 **parse HTML with Java** 同時 **print thread name**。上方的完整程式碼已可直接執行，概念亦能擴展至更複雜、正式的應用。

歡迎自行實驗：更改檔案路徑、增加工作者數量，或接入真實的 HTML 解析器。基礎不變，而你現在已具備堅實的多執行緒 Java 開發基礎。

對執行緒安全、executor service 或 HTML 解析函式庫有任何疑問嗎？在下方留言，我們一起討論，祝開發愉快！

## 接下來該學什麼？

以下教學與本指南的技巧密切相關，能進一步深化你的能力。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [固定執行緒池 Java – 使用 ExecutorService 並行 HTML 清理](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [如何使用 Aspose.HTML for Java 編輯 HTML](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [如何將 HTML 轉換為 PDF Java – 使用 Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}