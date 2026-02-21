---
category: general
date: 2026-02-21
description: Cách sử dụng ExecutorService để chuyển đổi HTML sang PNG nhanh chóng.
  Tìm hiểu cách chuyển đổi hàng loạt các tệp HTML bằng các tác vụ song song trong
  Java.
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: vi
og_description: Cách sử dụng ExecutorService để chuyển đổi hàng loạt các tệp HTML
  sang PNG. Hướng dẫn chi tiết từng bước kèm ví dụ Java đầy đủ.
og_title: Cách sử dụng ExecutorService để chuyển đổi HTML sang PNG song song
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: Cách sử dụng ExecutorService để chuyển đổi HTML sang PNG hàng loạt song song
url: /vi/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

sections.

Make sure to keep code block placeholders unchanged.

Also blockquote > lines.

List items.

Ok.

Let's craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng ExecutorService để Chuyển Đổi Hàng Loạt HTML‑to‑PNG Song Song

Bạn đã bao giờ tự hỏi **cách sử dụng ExecutorService** khi có một thư mục đầy các trang HTML cần chuyển thành ảnh PNG chưa? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp phải vấn đề này khi quy trình báo cáo web của họ bị kẹt ở vòng lặp chuyển đổi đơn luồng.  

Tin tốt là gì? Với vài dòng Java và công cụ mạnh mẽ Aspose.HTML `Converter`, bạn có thể khởi tạo một pool các luồng làm việc, đưa từng tệp HTML vào bộ chuyển đổi, và quan sát các ảnh xuất hiện đồng thời. Trong hướng dẫn này, chúng tôi cũng sẽ đề cập tới các kiến thức cơ bản **convert html to png**, chỉ cho bạn cách **run parallel tasks**, và cung cấp một script **batch convert html files** đã sẵn sàng để chạy.

## Yêu Cầu Trước

- Java 17 trở lên (mã sử dụng API hiện đại `java.nio.file`).  
- Thư viện Aspose.HTML for Java có trong classpath. Bạn có thể tải từ Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- Một thư mục chứa các tệp `.html` nguồn và một thư mục đầu ra trống.  
- Một lượng RAM vừa phải—mỗi lần chuyển đổi chạy trong một luồng riêng, vì vậy kích thước pool nên khớp với số lõi CPU bạn có.

> **Pro tip:** Nếu máy của bạn hỗ trợ hyper‑threading, `Runtime.getRuntime().availableProcessors()` thường trả về số lõi tối ưu.

## Bước 1 – Xác Định Đường Dẫn Đầu Vào và Đầu Ra

Đầu tiên chúng ta cần chỉ cho Java biết HTML nằm ở đâu và PNG sẽ được lưu vào đâu. Sử dụng các đối tượng `Path` giúp mã không phụ thuộc vào nền tảng.

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

> **Tại sao lại quan trọng:** Tạo thư mục đầu ra trước sẽ ngăn `FileNotFoundException` khi luồng làm việc đầu tiên cố ghi tệp.

## Bước 2 – Xây Dựng Một Fixed‑Size Thread Pool

Trái tim của **cách sử dụng ExecutorService** nằm ở việc tạo một pool phù hợp với phần cứng của bạn. Một pool *fixed* đảm bảo chúng ta không tạo ra nhiều luồng hơn khả năng thực thi thực tế.

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **Giải thích:** `ExecutorService` trừu tượng hoá việc quản lý luồng cấp thấp. Bằng cách dùng `newFixedThreadPool`, chúng ta cho JVM tái sử dụng các luồng, giảm chi phí tạo và hủy luồng liên tục.

## Bước 3 – Gửi Một Nhiệm Vụ Chuyển Đổi cho Mỗi Tệp HTML

Bây giờ chúng ta duyệt qua thư mục đầu vào, chọn mọi tệp `*.html`, và đưa chúng vào pool. Mỗi nhiệm vụ là một lambda nhỏ gọi `Converter.convert`.

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

### Điều gì đang diễn ra phía sau?

1. **DirectoryStream** đọc tên tệp một cách lười biếng, vì vậy việc sử dụng bộ nhớ vẫn thấp ngay cả khi có hàng ngàn tệp.  
2. Lambda nắm bắt `htmlFile` và `outputDir`—không cần tạo một lớp `Runnable` riêng.  
3. `Converter.convert` là một lời gọi blocking đọc HTML, render và ghi PNG. Vì mỗi lời gọi chạy trong một luồng riêng, nhiều tệp được xử lý đồng thời—đúng như hành vi bạn mong đợi khi **run parallel tasks**.

## Bước 4 – Tắt Pool Một Cách Trơn Truồng

Sau khi tất cả nhiệm vụ đã được đưa vào hàng, chúng ta yêu cầu pool ngừng nhận công việc mới và chờ mọi thứ hoàn thành. Nếu có gì đó treo, thời gian chờ sẽ dừng sau một giờ, đủ rộng rãi cho hầu hết các công việc batch.

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

> **Trường hợp đặc biệt:** Nếu bạn có các tệp HTML cực lớn, có thể muốn tăng thời gian chờ hoặc giám sát việc sử dụng bộ nhớ. Thêm `pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` buộc luồng gọi thực thi các nhiệm vụ dư thừa, ngăn `RejectedExecutionException`.

## Ví Dụ Đầy Đủ, Sẵn Sàng Chạy

Dưới đây là toàn bộ chương trình, có thể sao chép‑dán vào một tệp `ParallelBatchConversion.java` duy nhất.

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

### Kết quả mong đợi

Chạy chương trình sẽ in ra một dòng cho mỗi lần chuyển đổi thành công:

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

Nếu một tệp thất bại, bạn sẽ thấy một dòng lỗi kèm thông báo ngoại lệ, giúp việc gỡ lỗi trở nên đơn giản.

## Cách Mở Rộng Mẫu Này

- **Định dạng ảnh khác:** Thay đổi phần mở rộng `.png` thành `.jpg` hoặc `.bmp` và điều chỉnh các tùy chọn chuyển đổi của Aspose cho phù hợp.  
- **Số luồng động:** Đối với tải công việc I/O‑bound, bạn có thể tăng kích thước pool (`availableProcessors() * 2`).  
- **Giám sát tiến độ:** Thay `System.out.println` bằng một thư viện thanh tiến độ an toàn đa luồng như `jline` hoặc ghi log vào tệp.  
- **Xử lý lỗi:** Thu thập các đường dẫn thất bại vào một `List<Path>` và thử lại sau khi vòng lặp chính kết thúc.

## Câu Hỏi Thường Gặp

**Q: Điều này có hoạt động trên Windows và Linux không?**  
A: Có. `java.nio.file` trừu tượng hoá hệ thống tệp, vì vậy cùng một mã chạy mà không thay đổi trên bất kỳ OS nào hỗ trợ Java.

**Q: Nếu tôi có hơn 10 000 tệp HTML thì sao?**  
A: Bộ lặp `DirectoryStream` đọc các mục một cách lười biếng, nên bộ nhớ vẫn thấp. Chỉ cần chắc chắn ổ đĩa của bạn có đủ không gian trống cho đầu ra PNG.

**Q: Tôi có thể giới hạn bộ nhớ mỗi lần chuyển đổi sử dụng không?**  
A: Aspose.HTML cho phép cấu hình engine render qua `HtmlLoadOptions` và `ImageSaveOptions`. Bạn có thể đặt kích thước bitmap tối đa hoặc bật render chất lượng thấp để kiểm soát tiêu thụ RAM.

## Kết Luận

Chúng ta đã đi qua **cách sử dụng ExecutorService** để **batch convert html files** thành ảnh PNG, giải thích vì sao một pool kích thước cố định là lựa chọn tối ưu cho việc render CPU‑bound, và cung cấp cho bạn một chương trình Java hoàn chỉnh, có thể sao chép‑dán. Bằng cách làm theo các bước trên, bạn sẽ biến một vòng lặp đơn luồng chậm chạp thành một pipeline nhanh, mở rộng, có thể xử lý hàng ngàn tệp chỉ với một lệnh.

Sẵn sàng cho thử thách tiếp theo? Hãy thử thay `Converter.convert` bằng tính năng xuất PDF của Aspose để **convert html to pdf**, hoặc tích hợp logic này vào một microservice Spring Boot nhận yêu cầu tải lên và chuyển đổi. Ý tưởng cốt lõi—sử dụng `ExecutorService` để **run parallel tasks**—vẫn giữ nguyên, và bạn sẽ thấy nó hữu ích trong vô số kịch bản xử lý batch.

Chúc lập trình vui vẻ, và hy vọng các luồng của bạn luôn sống động! 

![how to use executorservice diagram](placeholder.png "Diagram illustrating the thread pool workflow for parallel HTML‑to‑PNG conversion")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}