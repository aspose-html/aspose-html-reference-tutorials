---
category: general
date: 2026-04-05
description: Hướng dẫn đa luồng Java cho thấy cách chạy các tác vụ song song bằng
  cách sử dụng một pool luồng cố định và tắt ExecutorService một cách an toàn.
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: vi
og_description: Hướng dẫn đa luồng Java giúp bạn thực hiện các tác vụ song song, tạo
  một pool luồng cố định, in tên luồng và tắt ExecutorService một cách sạch sẽ.
og_title: hướng dẫn đa luồng Java – Thực thi song song với bộ luồng cố định
tags:
- Java
- Concurrency
- ExecutorService
title: 'Hướng dẫn đa luồng Java: Chạy các tác vụ song song với bộ luồng cố định'
url: /vi/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – Thực thi Song song Đơn giản

Bạn đã bao giờ tự hỏi làm thế nào để **run tasks parallel** trong Java mà không phải loay hoay với việc quản lý thread cấp thấp? Trong **java multithreading tutorial** này, chúng tôi sẽ hướng dẫn bạn từng bước: sử dụng **fixed thread pool java**, in tên của mỗi thread, và **shutdown executorservice** một cách sạch sẽ khi công việc hoàn thành.  

Nếu bạn từng viết một vòng lặp bị chặn vì I/O mạng hoặc cần thu thập dữ liệu từ nhiều trang web cùng lúc, mẫu code chúng tôi trình bày dưới đây sẽ giúp bạn tiết kiệm thời gian và giảm bớt rắc rối.  

Chúng tôi sẽ bao quát mọi thứ bạn cần—không cần tài liệu bên ngoài, chỉ có mã Java thuần túy mà bạn có thể copy‑paste, chạy và xem kết quả. Khi kết thúc, bạn sẽ hiểu vì sao một fixed thread pool thường là lựa chọn tối ưu cho parallelism có giới hạn, cách dừng nó một cách an toàn, và cách làm cho log của bạn dễ đọc hơn bằng cách in tên thread.  

> **Prerequisites**: Java 8+ (gói `java.util.concurrent` đã ổn định trong nhiều năm), một IDE hoặc dòng lệnh đơn giản `javac`/`java`, và kiến thức cơ bản về OOP. Không cần thư viện bổ sung nào ngoài file jar Aspose HTML for Java mà bạn đã có.

---

![java multithreading tutorial diagram showing a thread pool feeding tasks](https://example.com/images/java-multithreading-tutorial.png "sơ đồ tutorial đa luồng Java cho thấy một pool thread đang cấp nhiệm vụ")

## java multithreading tutorial – Thiết lập Fixed Thread Pool

Một **fixed thread pool** giới hạn số lượng thread chạy đồng thời, ngăn ứng dụng của bạn tạo ra quá nhiều thread của hệ điều hành và tiêu tốn tài nguyên. Ở đây chúng ta tạo một pool với bốn worker:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Tại sao lại bốn?* Vì nó khớp với số URL chúng ta sẽ tải, nhưng bạn có thể điều chỉnh con số này dựa trên số lõi CPU, mức độ I/O, hoặc giới hạn bộ nhớ. Factory `Executors` bảo vệ bạn khỏi việc dùng trực tiếp constructor `Thread` cấp thấp và cung cấp một tham chiếu `ExecutorService` sạch sẽ mà bạn sẽ **shutdown executorservice** sau này.

## Chuẩn bị URL và Định nghĩa Các Nhiệm vụ Song song

Tiếp theo, chúng ta liệt kê các trang cần xử lý. Trong một scraper thực tế, bạn có thể đọc chúng từ file hoặc cơ sở dữ liệu, nhưng một mảng tĩnh giúp ví dụ này tự chứa:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

Bây giờ đến phần **run tasks parallel**. Đối với mỗi URL, chúng ta submit một lambda tải tài liệu và in tiêu đề của nó. Lưu ý việc sử dụng `Thread.currentThread().getName()` – đây là mẹo **print thread name** giúp việc debug dễ dàng hơn rất nhiều:

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

> **Pro tip**: Đặt `HTMLDocument` trong khối try‑with‑resources đảm bảo luồng cơ bản được đóng lại, ngay cả khi trang không tải được.

## Dừng ExecutorService Một Cách Trơn Truồng

Để một thread pool còn tồn tại sau khi công việc đã xong có thể khiến JVM của bạn treo. Cách đúng là **shutdown executorservice**, sau đó chờ kết thúc:

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

*Tại sao có timeout?* Nó bảo vệ bạn khỏi một task "điên" không bao giờ trả về (ví dụ, một cuộc gọi mạng bị treo). Nếu pool không hoàn thành trong một phút, chúng ta gọi `shutdownNow()` để ngắt bất kỳ thread nào còn tồn tại.

### Kết quả Dự kiến

Chạy chương trình sẽ in ra một thứ gì đó tương tự:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

Thứ tự chính xác có thể thay đổi—vì các task thực sự chạy song song. Điều luôn cố định là tiền tố **print thread name**, cho biết chính xác worker nào đã xử lý mỗi URL.

---

## Các Biến thể Thông thường & Trường hợp Cạnh

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **More URLs than threads** | Keep the same pool size; extra tasks will queue automatically. | Fixed pool tự xử lý back‑pressure cho bạn. |
| **CPU‑bound work** | Set the pool size to `Runtime.getRuntime().availableProcessors()` instead of a hard‑coded 4. | Tối đa hoá việc sử dụng CPU mà không gây quá tải. |
| **Need to cancel a specific task** | Keep a `Future<?>` reference from `executor.submit()` and call `future.cancel(true)`. | Cung cấp kiểm soát chi tiết cho từng job. |
| **Processing large files** | Increase the pool size modestly *or* switch to `newCachedThreadPool()` if you expect bursts. | Cached pools tạo thread khi cần, nhưng cần chú ý tránh tăng vô hạn. |

---

## Kết luận

Bạn đã có một **java multithreading tutorial** vững chắc, minh họa cách **run tasks parallel** bằng **fixed thread pool java**, **print thread name** để log rõ ràng, và **shutdown executorservice** một cách sạch sẽ. Toàn bộ mã có thể chạy được nằm trong một lớp duy nhất, vì vậy bạn có thể đưa nó vào bất kỳ dự án nào và ngay lập tức mở rộng công việc I/O‑bound của mình.

Tiếp theo bạn muốn làm gì? Thử thay thế `HTMLDocument` bằng client HTTP của riêng bạn, thử nghiệm các kích thước pool khác nhau, hoặc tích hợp `CompletionService` để thu thập kết quả khi chúng hoàn thành. Bạn cũng có thể khám phá `java.util.concurrent.Flow` cho các stream phản ứng nếu cần xử lý back‑pressure phức tạp hơn một hàng đợi đơn giản.

Chúc bạn lập trình vui vẻ, và nhớ: với chiến lược thread‑pool phù hợp, concurrency trở thành *một miếng bánh*, không phải là nguồn gốc của lỗi. Nếu có câu hỏi, cứ để lại bình luận—tôi luôn sẵn sàng trò chuyện về concurrency trong Java!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}