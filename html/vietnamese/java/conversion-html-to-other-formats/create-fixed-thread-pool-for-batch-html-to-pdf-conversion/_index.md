---
category: general
date: 2026-02-22
description: Tạo một pool luồng cố định để chuyển đổi HTML sang PDF hàng loạt một
  cách hiệu quả trong Java. Tìm hiểu ví dụ về pool luồng trong Java giúp lưu HTML
  thành PDF nhanh chóng.
draft: false
keywords:
- create fixed thread pool
- convert html to pdf
- batch html to pdf
- thread pool java example
- save html as pdf
language: vi
og_description: Tạo pool luồng cố định để chuyển đổi HTML sang PDF hàng loạt. Hướng
  dẫn này sẽ đưa bạn qua một ví dụ về pool luồng trong Java giúp lưu HTML dưới dạng
  PDF một cách hiệu quả.
og_title: Tạo Pool Luồng Cố Định cho Chuyển Đổi HTML sang PDF Hàng Loạt
tags:
- Java
- Concurrency
- PDF Generation
title: Tạo Pool Luồng Cố Định cho Chuyển Đổi HTML sang PDF Hàng Loạt
url: /vi/java/conversion-html-to-other-formats/create-fixed-thread-pool-for-batch-html-to-pdf-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Fixed Thread Pool cho Chuyển Đổi Hàng Loạt HTML sang PDF

Bạn đã bao giờ tự hỏi làm thế nào **create fixed thread pool** có thể chuyển một đống file HTML thành PDF mà không làm nghẹt CPU? Bạn không phải là người duy nhất. Khi bạn có hàng chục—hoặc thậm chí hàng trăm—trang để xử lý, chạy chúng từng cái một thật chán, nhưng khởi động một thread pool không giới hạn có thể nhanh chóng tiêu tốn bộ nhớ.  

Trong hướng dẫn này, chúng ta sẽ giải quyết vấn đề đó bằng cách cho bạn thấy một **thread pool Java example** mà **batch HTML to PDF**, lưu mỗi kết quả và tắt một cách sạch sẽ. Khi kết thúc, bạn sẽ có thể **convert HTML to PDF** song song, và bạn sẽ hiểu tại sao một fixed thread pool là lựa chọn tối ưu cho hầu hết các công việc batch.

## Những Điều Bạn Sẽ Nhận Được

- Một chương trình Java hoàn chỉnh, có thể chạy được, tạo một fixed thread pool.
- Giải thích chi tiết từng dòng, để bạn biết **why** chúng ta làm những gì chúng ta làm.
- Hướng dẫn chọn thư viện PDF (để bạn có thể **save HTML as PDF** mà không phải tìm kiếm các đoạn mã).
- Mẹo xử lý lỗi, điều chỉnh kích thước pool, và mở rộng giải pháp cho các batch lớn hơn.

**Prerequisites** – Java 8+ đã được cài đặt, một IDE cơ bản (IntelliJ, Eclipse, hoặc VS Code), và một thư viện chuyển đổi PDF trên classpath của bạn (chúng tôi sẽ dùng *OpenHTMLtoPDF* trong ví dụ). Không cần framework nào khác.

---

## Tạo Fixed Thread Pool – Tại Sao Nó Quan Trọng

Khi bạn **create fixed thread pool**, bạn nói với JVM chính xác có bao nhiêu worker thread được phép chạy đồng thời. Điều này ngăn chặn các cơn bão tạo thread, giữ việc sử dụng bộ nhớ dự đoán được, và cho phép OS lên lịch công việc một cách hiệu quả.  

Hãy tưởng tượng nó giống như một quầy thanh toán ở siêu thị: bạn mở một số lượng quầy cố định, để khách hàng xếp hàng, và đóng các quầy khi không còn hàng. Một `FixedThreadPool` hoạt động tương tự—các task chờ lượt mình, nhưng không có thread bổ sung nào được tạo ra ngay lập tức.

```java
// Step 1: Build a fixed‑size thread pool with 4 workers
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

Số `4` là điểm khởi đầu tốt trên một laptop quad‑core; bạn có thể điều chỉnh nó dựa trên số core CPU và đặc điểm I/O của mình.

## Batch HTML to PDF: Chuyển Đổi Mỗi Trang

Bây giờ pool đã tồn tại, chúng ta cần đưa vào các task **convert HTML to PDF**. Mỗi task sẽ:

1. Tải tài liệu HTML từ đĩa.
2. Gửi nó cho thư viện PDF.
3. Ghi PDF kết quả trở lại cùng thư mục.

Vì công việc này nặng I/O (đọc file, ghi PDF), một pool nhỏ thường vượt trội hơn một pool lớn hơn chỉ ngồi chờ đĩa.

```java
// Step 2: Submit a conversion job for every HTML file you have
for (int i = 0; i < 4; i++) {
    final int pageIndex = i;               // capture loop variable for the lambda
    threadPool.submit(() -> {
        // Load the HTML file
        Path htmlPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".html");
        String html = Files.readString(htmlPath, StandardCharsets.UTF_8);

        // Convert and save as PDF
        Path pdfPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".pdf");
        convertHtmlToPdf(html, pdfPath);
    });
}
```

> **Pro tip:** Nếu bạn có nhiều hơn bốn trang, chỉ cần tăng giới hạn vòng lặp hoặc đọc danh sách file một cách động—`Files.list(Paths.get("YOUR_DIRECTORY")).filter(p -> p.toString().endsWith(".html"))` sẽ làm cho việc này trở nên dễ dàng.

## Giải Thích Ví Dụ Thread Pool Java

Hãy phân tích **thread pool Java example** từng dòng để bạn không chỉ sao chép mã, mà thực sự hiểu luồng thực thi.

| Dòng | Chức Năng | Tại Sao Quan Trọng |
|------|--------------|--------------------|
| `ExecutorService threadPool = Executors.newFixedThreadPool(4);` | Khởi tạo một pool với đúng bốn thread. | Đảm bảo số lượng chuyển đổi đồng thời có giới hạn, tránh lỗi hết bộ nhớ. |
| `for (int i = 0; i < 4; i++) { … }` | Lặp qua các trang bạn muốn xử lý. | Vòng lặp tạo ra các task; bạn có thể thay thế giới hạn tĩnh bằng danh sách động. |
| `final int pageIndex = i;` | Ghi lại chỉ số vòng lặp để sử dụng trong lambda. | Nếu không có `final` (hoặc hiệu quả cuối cùng) lambda sẽ thấy biến thay đổi, dẫn đến tên file sai. |
| `threadPool.submit(() -> { … });` | Gửi một `Runnable` tới pool để thực thi bất đồng bộ. | Pool lên lịch runnable trên một worker thread rảnh, giải phóng main thread để tiếp tục đưa công việc vào hàng. |
| `Files.readString(htmlPath, …);` | Đọc file HTML vào một `String`. | Cần thiết vì hầu hết các thư viện PDF chấp nhận HTML dưới dạng string hoặc stream. |
| `convertHtmlToPdf(html, pdfPath);` | Gọi một phương thức trợ giúp thực hiện chuyển đổi thực tế. | Giữ lambda gọn gàng và tách mã riêng cho thư viện. |

Dưới đây là phương thức trợ giúp đầy đủ sử dụng **OpenHTMLtoPDF**, một thư viện nhẹ cho phép **save HTML as PDF** chỉ với một lời gọi.

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

private static void convertHtmlToPdf(String html, Path outputPdf) throws IOException {
    try (OutputStream os = Files.newOutputStream(outputPdf)) {
        PdfRendererBuilder builder = new PdfRendererBuilder();
        builder.withHtmlContent(html, null);     // base URI is null because we use absolute paths
        builder.toStream(os);
        builder.run();                           // blocks until PDF is written
    } catch (Exception e) {
        // Wrap any checked exception as an unchecked one so the lambda can compile
        throw new RuntimeException("Failed to convert HTML to PDF for " + outputPdf, e);
    }
}
```

> **Why OpenHTMLtoPDF?** Nó thuần Java, không phụ thuộc native, và hỗ trợ CSS, giúp PDF kết quả trông giống hệt trang web gốc. Nếu bạn thích iText hoặc Flying Saucer, chỉ cần thay đổi phần cài đặt trong `convertHtmlToPdf`.

## Lưu HTML thành PDF – Lựa Chọn Thư Viện

Bạn có thể hỏi, “Thư viện nào nên **convert HTML to PDF**?” Dưới đây là so sánh nhanh:

| Thư viện | Maven Coordinates | Ưu điểm | Nhược điểm |
|----------|-------------------|----------|------------|
| OpenHTMLtoPDF | `com.openhtmltopdf:openhtmltopdf-pdfbox:1.0.10` | Thuần Java, hỗ trợ CSS tốt, nhẹ | Giới hạn các tính năng PDF nâng cao (ví dụ: mã hoá) |
| iText 7 + html2pdf | `com.itextpdf:html2pdf:3.0.6` | Bộ tính năng phong phú, hỗ trợ thương mại | Yêu cầu giấy phép trả phí cho nhiều trường hợp sử dụng |
| Flying Saucer | `org.xhtmlrenderer:flying-saucer-pdf:9.1.22` | Ổn định, hoạt động với các phiên bản Java cũ | Chậm hơn trên tài liệu lớn, ít hỗ trợ CSS hơn |

Chọn thư viện phù hợp với nhu cầu dự án của bạn. Đối với công việc **batch HTML to PDF**, OpenHTMLtoPDF thường là lựa chọn tối ưu: nhanh, đơn giản và miễn phí.

## Tắt Gọn Gàng và Xử Lý Lỗi

Để executor chạy liên tục có thể ngăn JVM của bạn thoát, và các ngoại lệ không bắt trong thread có thể khó phát hiện. Mẫu sau đảm bảo tắt gọn gàng:

```java
// Step 5: Initiate an orderly shutdown after all tasks are queued
threadPool.shutdown();                     // No new tasks accepted
try {
    // Wait up to 60 seconds for existing tasks to finish
    if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
        threadPool.shutdownNow();          // Force shutdown if tasks linger
    }
} catch (InterruptedException ex) {
    threadPool.shutdownNow();              // Preserve interrupt status
    Thread.currentThread().interrupt();
}
```

- `shutdown()` thông báo cho pool hoàn thành công việc hiện tại nhưng từ chối công việc mới.
- `awaitTermination` chặn cho đến khi mọi việc hoàn thành hoặc thời gian chờ hết.
- `shutdownNow()` cố gắng hủy các task đang chạy—hữu ích cho việc dừng ép buộc.

Nếu bất kỳ chuyển đổi nào thất bại, `RuntimeException` chúng tôi ném sẽ lên tới executor, mặc định nó sẽ ghi log ra console. Trong môi trường production, bạn có thể gắn một `ThreadPoolExecutor` tùy chỉnh với phương thức `afterExecute` được ghi đè để ghi log vào file hoặc hệ thống giám sát.

## Ví Dụ Hoàn Chỉnh Hoạt Động

Kết hợp tất cả lại, đây là một lớp Java tự chứa mà bạn có thể sao chép‑dán vào `src/main/java/com/example/BatchPdfConverter.java`. Đảm bảo phụ thuộc OpenHTMLtoPDF có trong classpath của bạn.

```java
package com.example;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;
import java.util.concurrent.*;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;

/**
 * Demonstrates how to create a fixed thread pool to batch HTML to PDF conversion.
 * Adjust POOL_SIZE and DIRECTORY constants to fit your environment.
 */
public class BatchPdfConverter {

    private static final int POOL_SIZE = 4;                     // Number of parallel workers
    private static final Path DIRECTORY = Paths.get("YOUR_DIRECTORY"); // Change to your folder

    public static void main(String[] args) {
        ExecutorService threadPool = Executors.newFixedThreadPool(POOL_SIZE);

        // Discover all *.html files in the target directory
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(DIRECTORY, "*.html")) {
            for (Path htmlPath : stream) {
                threadPool.submit(() -> processFile(htmlPath));
            }
        } catch (IOException e) {
            System.err.println("Failed to list HTML files: " + e.getMessage());
        }

        // Graceful shutdown
        thread

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}