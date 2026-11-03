---
category: general
date: 2026-05-28
description: cách sử dụng executor trong Java với một pool thread cố định, trích xuất
  văn bản từ HTML và tăng tốc xử lý – một ví dụ đầy đủ về thread pool trong Java.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: vi
og_description: Cách sử dụng executor trong Java với một pool luồng cố định. Tìm hiểu
  ví dụ đầy đủ về pool luồng Java để trích xuất văn bản từ các tệp HTML một cách hiệu
  quả.
og_title: Cách sử dụng Executor trong Java – Hướng dẫn Fixed Thread Pool
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
title: Cách sử dụng Executor trong Java – Hướng dẫn Fixed Thread Pool
url: /vi/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng Executor trong Java – Hướng Dẫn Fixed Thread Pool

Bạn đã bao giờ tự hỏi **cách sử dụng executor** để chạy nhiều tác vụ cùng lúc mà không làm tràn bộ nhớ chưa? Bạn không phải là người duy nhất. Trong nhiều ứng dụng thực tế, bạn sẽ cần duyệt một thư mục chứa các tệp HTML, trích xuất nội dung body, và thực hiện nhanh chóng — chính là kịch bản mà hướng dẫn này giải quyết.

Chúng ta sẽ đi qua một triển khai **fixed thread pool java** để trích xuất văn bản từ HTML, in ra số ký tự của mỗi tệp, và tắt một cách sạch sẽ. Khi kết thúc, bạn sẽ có một **java thread pool example** độc lập mà bạn có thể chèn vào bất kỳ dự án nào, cùng với một vài mẹo về việc tùy chỉnh kích thước pool và xử lý các trường hợp đặc biệt.

> **Bạn sẽ cần**  
> * Java 17 (hoặc bất kỳ JDK nào mới)  
> * Thư viện phân tích HTML nhỏ – chúng ta sẽ dùng *jsoup* vì nó đã được kiểm chứng và không cần cấu hình.  
> * Một vài tệp *.html* mẫu trong thư mục bạn chọn.

---

## Cách Sử Dụng Executor với Fixed Thread Pool

Trái tim của bất kỳ chương trình Java đa luồng nào là `ExecutorService`. Bằng cách tạo một **fixed thread pool**, chúng ta yêu cầu JVM duy trì chính xác N luồng làm việc, giúp ngăn ngừa chi phí tạo luồng và giới hạn việc sử dụng tài nguyên.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Tại sao điều này quan trọng:*  
Nếu bạn khởi chạy một `Thread` mới cho mỗi tệp HTML, hệ điều hành sẽ phải lên lịch hàng chục luồng trên một chiếc laptop thông thường, gây ra việc chuyển đổi ngữ cảnh quá mức. Một fixed pool tái sử dụng cùng bốn luồng, mang lại việc sử dụng CPU dự đoán được.

---

## Xác Định Các Tệp HTML Để Xử Lý – Fixed Thread Pool Java

Tiếp theo chúng ta liệt kê các tệp muốn đưa vào pool. Trong một ứng dụng thực tế, bạn có thể sẽ duyệt cây thư mục; ở đây chúng ta giữ đơn giản.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Mẹo:* `List.of` trả về một danh sách bất biến, an toàn để chia sẻ giữa các luồng mà không cần đồng bộ thêm.

---

## Gửi Một Nhiệm Vụ Riêng Cho Mỗi Tệp HTML

Bây giờ chúng ta đưa mỗi đường dẫn cho executor. Lambda mà chúng ta gửi sẽ chạy **song song** trên một trong bốn luồng làm việc.

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

**Tại sao chúng ta gói logic trong một phương thức** (`extractBodyText`) sẽ trở nên rõ ràng trong phần tiếp theo—giúp lambda gọn gàng và cho phép chúng ta tái sử dụng mã trích xuất ở nơi khác.

---

## Trích Xuất Văn Bản Từ HTML – Logic Cốt Lõi

Đây là hàm trợ giúp có thể tái sử dụng thực sự **trích xuất văn bản từ html** bằng Jsoup. Nó mở tệp, phân tích DOM, và trả về văn bản body thuần.

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

*Tại sao Jsoup?* Nó nhẹ, xử lý markup bị hỏng một cách nhẹ nhàng, và không cần một engine trình duyệt đầy đủ. Phương thức ném `IOException` để người gọi có thể quyết định cách ghi log hoặc phục hồi—hoàn hảo cho kịch bản thread‑pool nơi bạn không muốn một tệp lỗi làm dừng toàn bộ executor.

---

## Tắt Executor Một Cách Gọn Gàng – Tạo Fixed Thread Pool

Sau khi chúng ta đã gửi mọi công việc, chúng ta phải thông báo cho pool ngừng nhận công việc mới và hoàn thành những công việc đã được xếp hàng.

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

*Giải thích:* `shutdown()` ngăn chặn các submission mới, trong khi `awaitTermination` chặn cho đến khi mọi công việc phân tích kết thúc (hoặc thời gian chờ hết). Nếu có gì đó bị treo, `shutdownNow()` cố gắng hủy các nhiệm vụ đang chạy. Mẫu này là cách được khuyến nghị để **create fixed thread pool** một cách an toàn.

---

## Ví Dụ Đầy Đủ, Có Thể Chạy

Kết hợp mọi thứ lại, đây là một tệp duy nhất bạn có thể biên dịch và chạy. Nó bao gồm các import cần thiết, phương thức `main`, và hàm trợ giúp đã mô tả ở trên.

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

**Kết quả mong đợi** (giả sử mỗi tệp chứa khoảng 1 200 ký tự của nội dung body):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Nếu bất kỳ tệp nào bị thiếu hoặc sai định dạng, bạn sẽ thấy một stack trace được in ra `stderr`, nhưng các nhiệm vụ khác sẽ tiếp tục không bị ảnh hưởng — chính xác những gì một **java thread pool example** hoạt động tốt nên làm.

---

## Câu Hỏi Thường Gặp & Các Trường Hợp Đặc Biệt

| Question | Answer |
|----------|--------|
| *Nếu tôi có nhiều hơn bốn tệp?* | Pool sẽ xếp hàng các nhiệm vụ dư và chạy chúng ngay khi một luồng trở nên rảnh. Không cần thêm mã nào. |
| *Tôi có nên dùng `newCachedThreadPool` thay thế không?* | `newCachedThreadPool` tạo luồng theo nhu cầu và có thể tăng vô hạn, điều này rủi ro cho các công việc I/O nặng. Một **fixed thread pool** cung cấp việc sử dụng bộ nhớ và CPU dự đoán được. |
| *Làm sao tôi thay đổi kích thước pool dựa trên số lõi CPU?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` là một mẫu phổ biến. |
| *Nếu việc phân tích một tệp thất bại thì sao?* | `catch (IOException e)` bên trong lambda cô lập lỗi, ghi log, và cho phép phần còn lại của pool tiếp tục làm việc. |
| *Tôi có thể trả về văn bản đã trích xuất cho người gọi không?* | Có—sử dụng `Future<String>` thay vì `submit(Runnable)`. Mã sẽ trông như `Future<String> f = executor.submit(() -> extractBodyText(path));` và sau đó `String result = f.get();`. |

---

## Kết Luận

Chúng ta đã trình bày **cách sử dụng executor** để khởi tạo một **fixed thread pool java** xử lý một tập hợp các tệp HTML song song, trích xuất nội dung body của chúng, và báo cáo số ký tự. **java thread pool example** hoàn chỉnh thể hiện quản lý tài nguyên đúng cách, xử lý lỗi, và một phương thức trích xuất có thể tái sử dụng.

Bước tiếp theo? Hãy thử thay thế triển khai `extractBodyText` bằng một scraper tinh vi hơn, thử nghiệm với kích thước pool lớn hơn, hoặc đưa kết quả vào cơ sở dữ liệu. Bạn cũng có thể khám phá `CompletionService` để lấy kết quả ngay khi chúng sẵn sàng, rất hữu ích khi kích thước tệp đa dạng.

Bạn có thể tự do chỉnh sửa đường dẫn thư mục, thêm nhiều tệp, hoặc tích hợp đoạn mã này vào một khung crawl lớn hơn. Mẫu cốt lõi—tạo pool, gửi các nhiệm vụ độc lập, và tắt một cách gọn gàng—vẫn luôn giống nhau, bất kể khối lượng công việc của bạn có phức tạp đến đâu.

Chúc lập trình vui vẻ, và mong các luồng của bạn luôn hoạt động (cho đến khi bạn tắt chúng, tất nhiên)!

## Hướng Dẫn Liên Quan

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Use Aspose.HTML for Java - Mastering HTML5 Canvas Rendering](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}