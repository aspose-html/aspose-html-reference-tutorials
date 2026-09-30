---
category: general
date: 2026-02-10
description: Học cách sử dụng một pool luồng cố định trong Java để đếm hình ảnh trong
  các tệp HTML, chạy các tác vụ đồng thời trong Java và tắt dịch vụ thực thi một cách
  đúng cách.
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: vi
og_description: Thành thạo việc sử dụng fixed thread pool trong Java để đếm ảnh, xử
  lý tệp song song và tắt dịch vụ executor một cách an toàn.
og_title: 'java fixed thread pool: Đếm hình ảnh trong các tệp song song'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'java fixed thread pool: Đếm hình ảnh trong các tệp song song'
url: /vi/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – Hướng Dẫn Đếm Ảnh Song Song

Bạn đã bao giờ tự hỏi làm sao **java fixed thread pool** để xử lý hàng chục tệp HTML và nhanh chóng đếm số ảnh? Có thể bạn đã nhìn vào một thư mục các trang, nghĩ “Tôi cần biết mỗi tệp có bao nhiêu thẻ `<img>`”, và rồi nhận ra một vòng lặp đơn luồng sẽ mất rất lâu.  

Tin tốt là bạn không cần viết một trình quản lý luồng tùy chỉnh hay đấu tranh với các đối tượng `Thread` cấp thấp. Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách **đếm ảnh** bằng cách sử dụng một *java fixed thread pool*, chạy các tác vụ **run tasks concurrently java**, và tắt **shutdown executor service** một cách nhẹ nhàng khi công việc hoàn thành.  

Chúng tôi sẽ bao phủ mọi thứ từ việc thiết lập pool, chuẩn bị danh sách tệp, gửi các tác vụ song song, xử lý các trường hợp biên, đến việc xác minh đầu ra. Khi kết thúc, bạn sẽ có một chương trình sẵn sàng chạy, thể hiện **java parallel file processing** một cách sạch sẽ và dễ bảo trì.  

## Yêu cầu trước

- Java 17 hoặc mới hơn (mã sử dụng từ khóa `var` để ngắn gọn, nhưng bạn có thể hạ cấp nếu cần).
- Aspose.HTML for Java trên classpath của bạn – bạn có thể tải nó từ Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- Một vài tệp HTML bạn muốn phân tích (hướng dẫn giả định chúng nằm trong `YOUR_DIRECTORY/`).
- Một IDE hoặc công cụ xây dựng mà bạn thoải mái sử dụng – IntelliJ IDEA, VS Code, hoặc `javac` thông thường đều hoạt động tốt.

Chỉ vậy thôi. Không cần máy chủ phụ, không Docker, chỉ cần Java thuần và một thư viện bên thứ ba nhỏ.

## Bước 1: Tạo java fixed thread pool

Một *java fixed thread pool* cung cấp cho bạn một tập hợp luồng làm việc có giới hạn, chúng tái sử dụng cho mỗi tác vụ được gửi. Điều này ngăn ngừa chi phí tạo luồng mới liên tục và giới hạn mức độ đồng thời, điều quan trọng khi bạn đọc tệp từ đĩa.

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**Why 4?** Nếu bạn có một laptop quad‑core, bốn luồng sẽ giữ mỗi lõi bận rộn mà không gây quá tải. Trên máy chủ có nhiều lõi hơn, bạn có thể tăng số lượng, nhưng hãy nhớ mỗi luồng sẽ mở một handle tệp, vì vậy quá nhiều có thể làm cạn kiệt giới hạn của hệ điều hành.

## Bước 2: Liệt kê các tệp HTML bạn muốn phân tích

Phần tiếp theo của **java parallel file processing** đơn giản là xây dựng một mảng (hoặc `List`) các đường dẫn tệp. Trong một dự án thực tế, bạn có thể duyệt thư mục một cách đệ quy, lọc theo phần mở rộng, hoặc đọc các đường dẫn từ cơ sở dữ liệu. Đây là cách tiếp cận đơn giản:

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

Nếu bạn cần xử lý một tập hợp động, hãy thay thế mảng tĩnh bằng một thứ gì đó như:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

Đoạn mã đó minh họa **java parallel file processing** cho bất kỳ số lượng tệp nào mà không cần thay đổi phần còn lại của mã.

## Bước 3: Gửi tác vụ tới **run tasks concurrently java**

Bây giờ là phần cốt lõi của hướng dẫn – chúng tôi sẽ **run tasks concurrently java** bằng cách gửi một lambda cho mỗi tệp. Mỗi tác vụ tải tài liệu HTML bằng Aspose.HTML, truy vấn tất cả các phần tử `<img>`, và in ra số lượng.

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

**Why use a lambda?** Nó giữ cho mã ngắn gọn và tránh tạo một lớp `Runnable` riêng. Lambda tự động bắt `filePath`, vì vậy mỗi tác vụ làm việc trên tệp của riêng mình.

### Cách **count images** hiệu quả

Aspose.HTML phân tích tệp một lần, xây dựng DOM, và sau đó `querySelectorAll("img")` chạy trong O(n) trong đó *n* là số nút. Đối với hầu hết các trang HTML, điều này không đáng kể. Nếu bạn cần một cách tiếp cận nhanh hơn, chỉ streaming (ví dụ, cho các tệp có kích thước gigabyte), bạn có thể chuyển sang bộ phân tích SAX, nhưng điều đó sẽ làm mất đi sự đơn giản mà chúng tôi hướng tới.

## Bước 4: Đúng cách **shutdown executor service**

Đừng bao giờ quên tắt pool, nếu không JVM của bạn sẽ chạy mãi mãi. Mẫu dưới đây là cách được khuyến nghị để **shutdown executor service** trong khi chờ tất cả các tác vụ hoàn thành:

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

**What if a task hangs?** Lệnh `shutdownNow()` cố gắng ngắt các luồng đang chạy. Nếu logic đếm ảnh của bạn tôn trọng việc ngắt (mà Aspose.HTML không chặn I/O), pool sẽ kết thúc sạch sẽ. Mẫu này là tiêu chuẩn vàng cho bất kỳ việc sử dụng **java fixed thread pool** nào.

## Bước 5: Xác minh đầu ra

Chạy chương trình từ IDE của bạn hoặc qua dòng lệnh:

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

Đầu ra điển hình trông như sau:

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

Nếu bạn thấy các số đếm được in ra theo bất kỳ thứ tự nào, điều đó là bình thường – các luồng kết thúc vào các thời điểm khác nhau. Điều quan trọng là mọi tệp đều được tính và chương trình thoát sạch sẽ sau chuỗi tắt.

## Ví dụ Hoạt Động Đầy Đủ (Sẵn Sàng Sao Chép‑Dán)

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

### Kết Quả Mong Đợi

Chạy đoạn mã sẽ in ra mỗi đường dẫn tệp kèm theo số lượng thẻ `<img>` mà nó chứa, sau đó JVM sẽ thoát. Không có luồng treo, không rò rỉ bộ nhớ.

## Những Cạm Bẫy Thường Gặp & Mẹo Chuyên Gia

- **Pitfall:** Sử dụng `newCachedThreadPool()` thay vì pool *fixed*. Điều đó tạo ra các luồng không giới hạn, có thể làm cạn kiệt mô tả tệp trên các lô lớn. Hãy dùng `newFixedThreadPool`.
- **Pro tip:** Nếu các tệp HTML của bạn rất lớn, hãy cân nhắc tăng heap (`-Xmx2g`) hoặc chuyển sang bộ phân tích streaming. Đối với hầu hết các trang marketing, heap mặc định là đủ.
- **Pitfall:** Quên gọi `shutdown()` – ứng dụng của bạn sẽ treo sau khi in kết quả. Phương thức `shutdownAndAwaitTermination` ở trên xử lý nó một cách vững chắc.
- **Pro tip:** Ghi lại thời gian bắt đầu và kết thúc của mỗi tác vụ nếu bạn cần các chỉ số hiệu năng. Lệnh `System.nanoTime()` đơn giản trước và sau khi tạo `HTMLDocument` cho bạn biết thời gian phân tích mất bao lâu.
- **Pitfall:** Ghi cứng số lượng luồng. Sử dụng `Runtime.getRuntime().availableProcessors()` để chọn giá trị mặc định hợp lý:

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## Các Chủ Đề Liên Quan Bạn Có Thể Khám Phá Tiếp Theo

- **run tasks concurrently java** với `CompletableFuture` để có các pipeline biểu đạt hơn.
- Lưu trữ số lượng ảnh vào cơ sở dữ liệu cho bảng điều khiển phân tích.
- Sử dụng **java parallel file processing** với API `java.nio.file.Files.walk` kết hợp với streams.
- Triển khai một `ThreadFactory` tùy chỉnh để đặt tên có ý nghĩa cho các luồng (giúp việc gỡ lỗi).

## Kết Luận

Chúng tôi vừa đi qua một ví dụ hoàn chỉnh, tự chứa, cho thấy cách **java fixed thread pool** có thể được tận dụng để **how to count images** trên nhiều tệp HTML, đồng thời minh họa cách đúng để **shutdown executor service**. Mẫu này mở rộng tốt—thay mảng tệp bằng danh sách động, tăng kích thước pool, và bạn sẽ có một giải pháp mạnh mẽ cho bất kỳ khối lượng công việc **java parallel file processing** nào.  

Hãy thử chạy, điều chỉnh số lượng luồng, và có thể thêm xuất CSV cho kết quả. Không gì là không thể khi bạn kết hợp nền tảng đồng thời vững chắc với một thư viện tiện lợi như Aspose.HTML. Chúc lập trình vui!  

![java fixed thread pool diagram](image.png){alt="sơ đồ java fixed thread pool"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}