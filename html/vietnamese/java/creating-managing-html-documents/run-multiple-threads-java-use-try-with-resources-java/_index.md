---
category: general
date: 2026-04-09
description: Chạy đa luồng Java hiệu quả bằng cách sử dụng try‑with‑resources Java.
  Tìm hiểu cách tải tài liệu HTML Java một cách an toàn và tránh các vấn đề đồng thời
  Java.
draft: false
keywords:
- run multiple threads java
- use try with resources java
- load html document java
- avoid concurrency issues java
language: vi
og_description: Chạy nhiều luồng Java với try‑with‑resources. Hướng dẫn này cho thấy
  cách tải tài liệu HTML trong Java một cách an toàn trong khi tránh các vấn đề đồng
  thời.
og_title: Chạy đa luồng Java – hướng dẫn try‑with‑resources
tags:
- java
- multithreading
- html-parsing
title: chạy đa luồng java – sử dụng try‑with‑resources java
url: /vi/java/creating-managing-html-documents/run-multiple-threads-java-use-try-with-resources-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# chạy đa luồng java – sử dụng try with resources java

Bạn đã bao giờ tự hỏi làm thế nào để **chạy đa luồng java** mà không gây xung đột không? Bạn không phải là người duy nhất—hầu hết các nhà phát triển đều gặp cùng một rào cản khi họ cố gắng chia sẻ một đối tượng có thể thay đổi giữa các luồng. Tin tốt? Có một cách sạch sẽ, hiện đại để làm điều đó, và nó bắt đầu với câu lệnh `try‑with‑resources`.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng sao chép‑dán mà **loads an HTML document java**, tạo ra một vài luồng, và đảm bảo mỗi luồng làm việc với một thể hiện tài liệu riêng. Khi kết thúc, bạn cũng sẽ thấy cách **avoid concurrency issues java** để ứng dụng của bạn ổn định khi tải cao.

> **Bạn sẽ nhận được:** một chương trình Java có thể chạy, giải thích từng bước, mẹo cho các dự án thực tế, và một bài kiểm tra nhanh mà bạn có thể chạy ngay lập tức.

![minh hoạ chạy đa luồng java](run-multiple-threads-java.png "Sơ đồ cho thấy mỗi luồng giữ một thể hiện HTMLDocument riêng")

## Yêu cầu trước

- Java 17 hoặc mới hơn (cú pháp `try‑with‑resources` hoạt động tương tự từ Java 7, nhưng chúng tôi sẽ sử dụng các tính năng ngôn ngữ mới để ngắn gọn).  
- Một lớp trợ giúp phân tích HTML nhỏ có tên `HTMLDocument`. Nếu bạn chưa có, bạn có thể tạo stub như được hiển thị sau.  
- Kiến thức cơ bản về các luồng (`java.lang.Thread`) và giao diện `Runnable`.

Nếu bất kỳ mục nào nghe lạ, đừng hoảng—mỗi khái niệm sẽ được xem lại trong các bước dưới đây.

## Bước 1: Tải tài liệu HTML java với một tham chiếu chia sẻ

Điều đầu tiên chúng ta cần là một tham chiếu *chia sẻ* trỏ tới tệp mà chúng ta muốn phân tích. Hãy nghĩ nó như một bản thiết kế: URL giống nhau cho mọi luồng, nhưng đối tượng tài liệu thực tế sẽ được tạo riêng cho mỗi luồng sau này.

```java
// Step 1: Load the source HTML document (shared reference for its URL)
HTMLDocument sharedDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

### Tại sao lại là tham chiếu chia sẻ?

Nếu bạn cố gắng cung cấp cho mỗi luồng cùng một thể hiện `HTMLDocument`, chúng sẽ cùng đọc và ghi vào các bộ đệm nội bộ. Đó là công thức cổ điển cho các race condition—chính là loại **concurrency issues java** mà chúng ta muốn tránh. Bằng cách chỉ chia sẻ *URL*, mỗi luồng có thể an toàn mở luồng riêng của mình sau này.

> **Mẹo chuyên nghiệp:** Lưu URL trong một biến `final` nếu bạn không bao giờ định thay đổi nó. Trình biên dịch sẽ coi nó như một hằng số, giảm thiểu việc thay đổi ngoài ý muốn.

## Bước 2: Tạo một tác vụ an toàn với luồng bằng try with resources java

Bây giờ chúng ta định nghĩa công việc thực tế mỗi luồng thực hiện. Mánh khóe là bọc việc tạo `HTMLDocument` cho mỗi luồng bên trong một khối `try‑with‑resources`. Điều này đảm bảo tài liệu được đóng tự động, ngay cả khi có ngoại lệ xảy ra.

```java
// Step 2: Define a task that creates its own document instance per thread
Runnable task = () -> {
    // Each thread works with its own copy to avoid concurrency issues
    try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
        // Perform thread‑specific operations on threadDoc here
        System.out.println("Thread " + Thread.currentThread().getName()
                + " loaded: " + threadDoc.getTitle());
    } catch (Exception e) {
        System.err.println("Error in thread " + Thread.currentThread().getName()
                + ": " + e.getMessage());
    }
};
```

### Cách `try‑with‑resources` giúp ích

Lớp `HTMLDocument` triển khai `java.lang.AutoCloseable`. Khi khối `try` kết thúc, JVM tự động gọi `threadDoc.close()`. Điều này an toàn hơn nhiều so với việc dùng câu lệnh `finally` thủ công và loại bỏ rủi ro quên giải phóng tài nguyên gốc—điều có thể dễ dàng gây rò rỉ bộ nhớ trong các ứng dụng đa luồng chạy lâu.

## Bước 3: Khởi chạy các luồng và tránh concurrency issues java

Với tác vụ đã sẵn sàng, chúng ta có thể tạo bao nhiêu luồng tùy thích. Để minh họa, chúng ta sẽ khởi chạy hai luồng, nhưng không có gì ngăn bạn tạo một pool luồng với hàng chục worker.

```java
// Step 3: Launch multiple threads that execute the same task
Thread t1 = new Thread(task, "Worker‑1");
Thread t2 = new Thread(task, "Worker‑2");

// Start the threads
t1.start();
t2.start();

// Optional: wait for them to finish (join) if you need deterministic ordering
t1.join();
t2.join();
```

### Tại sao không dùng `ExecutorService`?

Trong mã sản xuất, bạn có thể **sẽ** sử dụng `ExecutorService` để quản lý một pool worker. Ví dụ `Thread` đơn giản giữ cho tutorial tập trung vào ý tưởng cốt lõi—tạo một tài liệu riêng cho mỗi luồng khi sử dụng `try‑with‑resources`. Bạn có thể thay thế các lời gọi `Thread` bằng `FixedThreadPool` nếu phù hợp với kiến trúc dự án của mình.

## Ví dụ đầy đủ, có thể chạy

Kết hợp mọi thứ lại, đây là một chương trình tự chứa mà bạn có thể đặt vào tệp có tên `MultiThreadHtmlDemo.java`. Nó bao gồm một stub tối thiểu cho `HTMLDocument` để bạn có thể biên dịch và chạy ngay lập tức.

```java
// MultiThreadHtmlDemo.java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

// --- Minimal stub for demonstration purposes ---
class HTMLDocument implements AutoCloseable {
    private final String url;
    private String content;

    public HTMLDocument(String url) throws IOException {
        this.url = url;
        // Simulate loading the file (replace with real parser in production)
        this.content = Files.readString(Path.of(url));
    }

    public String getUrl() {
        return url;
    }

    public String getTitle() {
        // Very naive title extraction – just for demo
        int start = content.indexOf("<title>");
        int end = content.indexOf("</title>");
        if (start != -1 && end != -1 && end > start) {
            return content.substring(start + 7, end).trim();
        }
        return "Untitled";
    }

    @Override
    public void close() {
        // In a real library you’d release native buffers here
        content = null;
        System.out.println("Closed document for URL: " + url);
    }
}

// --- Main class that runs multiple threads java ---
public class MultiThreadHtmlDemo {
    public static void main(String[] args) throws InterruptedException, IOException {
        // Step 1: Load the source HTML document (shared reference for its URL)
        HTMLDocument sharedDoc = new HTMLDocument("sample.html");

        // Step 2: Define a task that creates its own document instance per thread
        Runnable task = () -> {
            try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
                System.out.println("Thread " + Thread.currentThread().getName()
                        + " loaded title: " + threadDoc.getTitle());
            } catch (Exception e) {
                System.err.println("Error in thread " + Thread.currentThread().getName()
                        + ": " + e.getMessage());
            }
        };

        // Step 3: Launch multiple threads that execute the same task
        Thread t1 = new Thread(task, "Worker‑1");
        Thread t2 = new Thread(task, "Worker‑2");

        t1.start();
        t2.start();

        // Wait for both threads to finish
        t1.join();
        t2.join();

        System.out.println("All threads completed.");
    }
}
```

#### Kết quả mong đợi (giả sử `sample.html` chứa `<title>Hello World</title>`)

```
Thread Worker-1 loaded title: Hello World
Closed document for URL: sample.html
Thread Worker-2 loaded title: Hello World
Closed document for URL: sample.html
All threads completed.
```

Chú ý cách mỗi luồng in ra *tiêu đề đã tải* của riêng mình và sau đó phương thức `close()` được chạy tự động—đúng như lời hứa của `try‑with‑resources`.

## Các câu hỏi thường gặp & xử lý các trường hợp biên

**Nếu tệp không được tìm thấy thì sao?**  
Constructor ném `IOException`. Trong ví dụ chúng ta bắt ngoại lệ này trong `Runnable` và ghi log lỗi, vì vậy tệp thiếu sẽ không làm sập toàn bộ ứng dụng.

**Tôi có thể tái sử dụng cùng một thể hiện `HTMLDocument` giữa các luồng không?**  
Chỉ nếu lớp này được tài liệu rõ ràng là thread‑safe. Hầu hết các trình phân tích giữ trạng thái có thể thay đổi (ví dụ, cây DOM), vì vậy việc chia sẻ một thể hiện thường dẫn đến **concurrency issues java**. Mẫu được trình bày ở đây—một thể hiện cho mỗi luồng—là lựa chọn an toàn nhất.

**Tôi có cần đồng bộ hoá gì không?**  
Không. Vì mỗi luồng làm việc với `HTMLDocument` riêng, không có trạng thái có thể thay đổi chung cần bảo vệ. Thành phần duy nhất được chia sẻ là chuỗi URL, vốn bất biến.

**Cách này sẽ trông như thế nào khi dùng `ExecutorService`?**  

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
for (int i = 0; i < 4; i++) {
    executor.submit(task);
}
executor.shutdown();
executor.awaitTermination(1, TimeUnit.MINUTES);
```

Logic cốt lõi vẫn giống nhau; pool chỉ quản lý vòng đời luồng cho bạn.

## Mẹo chuyên nghiệp cho đa luồng cấp sản xuất

1. **Giới hạn số lượng luồng** – tạo hàng chục đối tượng `Thread` thô có thể làm quá tải hệ điều hành. Hãy sử dụng một thread pool có giới hạn thay thế.  
2. **Ưu tiên cấu hình bất biến** – giữ các URL, đường dẫn tệp và cài đặt parser bất biến để bạn không vô tình thay đổi chúng từ worker.  
3. **Giám sát việc sử dụng tài nguyên** – ngay cả khi dùng `try‑with‑resources`, mở nhiều tệp cùng lúc có thể làm cạn kiệt mô tả tệp. Hạn chế số lượng tác vụ đồng thời nếu gặp giới hạn.  
4. **Tắt máy một cách nhẹ nhàng** – luôn tắt executor hoặc join các luồng của bạn để JVM có thể thoát sạch sẽ.

## Kết luận

Bạn đã có một mẫu vững chắc, sẵn sàng sao chép‑dán để **run multiple threads java** trong khi an toàn **using try with resources java**, **loading html document java**, và **avoiding concurrency issues java**. Bài học chính đơn giản: cung cấp cho mỗi luồng một thể hiện tài liệu riêng, để cấu trúc `try‑with‑resources` xử lý việc dọn dẹp, và giữ dữ liệu chia sẻ bất biến.

Từ đây bạn có thể khám phá:

- Mở rộng mẫu với `ExecutorService` và một hàng đợi công việc.  
- Chuyển sang một parser HTML thực tế như *jsoup* (cũng triển khai `Closeable`).  
- Thêm xử lý lỗi tinh vi hơn hoặc logic thử lại cho I/O không ổn định.

Hãy chạy thử, điều chỉnh số lượng worker, và quan sát đầu ra console vẫn gọn gàng—không

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}