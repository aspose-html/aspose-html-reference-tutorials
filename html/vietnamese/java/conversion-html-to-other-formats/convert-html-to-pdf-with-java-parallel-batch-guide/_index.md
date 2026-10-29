---
category: general
date: 2026-06-07
description: Chuyển đổi HTML sang PDF bằng ExecutorService của Java. Tìm hiểu cách
  chuyển đổi hàng loạt các tệp HTML, lưu tài liệu HTML dưới dạng PDF và tắt ExecutorService
  một cách an toàn.
draft: false
keywords:
- convert html to pdf
- save html document as pdf
- shutdown executorservice gracefully
- batch convert html to pdf
language: vi
og_description: Chuyển đổi HTML sang PDF bằng ExecutorService của Java. Thực hiện
  chuyển đổi hàng loạt, lưu tài liệu HTML dưới dạng PDF và tắt ExecutorService một
  cách nhẹ nhàng.
og_title: Chuyển đổi HTML sang PDF bằng Java – Hướng dẫn batch song song
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  headline: Convert HTML to PDF with Java – Parallel Batch Guide
  type: TechArticle
- description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  name: Convert HTML to PDF with Java – Parallel Batch Guide
  steps:
  - name: The HTML file is read into a string.
    text: The HTML file is read into a string.
  - name: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
    text: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
  - name: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
    text: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
  type: HowTo
tags:
- Java
- Concurrency
- PDF Generation
title: Chuyển đổi HTML sang PDF bằng Java – Hướng dẫn batch song song
url: /vi/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-parallel-batch-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi HTML sang PDF với Java – Hướng dẫn Batch Song song

Bạn đã bao giờ cần **chuyển đổi HTML sang PDF** nhưng cảm thấy bế tắc vì phải xử lý hàng chục tệp? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn này khi xây dựng trình tạo báo cáo hoặc xuất hoá đơn. Tin tốt là gì? Chỉ với vài dòng Java và một thread pool thông minh, bạn có thể **batch chuyển đổi HTML sang PDF** trong chớp mắt, **lưu tài liệu HTML dưới dạng PDF**, và thậm chí **tắt ExecutorService một cách nhẹ nhàng** khi công việc đã hoàn thành.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy. Bạn sẽ thấy tại sao một thread pool có kích thước cố định là lựa chọn tối ưu cho việc chuyển đổi song song, cách mã chuyển đổi trông như thế nào, và các bước chính xác để kết thúc executor một cách sạch sẽ. Khi kết thúc, bạn sẽ có một chương trình tự chứa mà có thể đưa vào bất kỳ dự án nào—không thiếu bất kỳ thành phần nào, không có liên kết “xem tài liệu” mơ hồ.

---

## Những gì bạn sẽ xây dựng

- Một ứng dụng console Java đọc danh sách các tệp HTML cục bộ.  
- Mỗi tệp sẽ được giao cho một luồng làm việc để tạo phiên bản PDF.  
- Ứng dụng sử dụng **ExecutorService** để chạy các chuyển đổi song song.  
- Khi mọi tác vụ đã được đưa vào hàng, pool sẽ **shutdown một cách nhẹ nhàng**, đảm bảo không có luồng nào còn treo.

**Yêu cầu trước**  
- Java 17 (hoặc bất kỳ JDK hiện đại nào).  
- Thư viện PDF có khả năng render HTML, chẳng hạn **OpenHTMLtoPDF**, **iText**, hoặc **Flying Saucer**. Trong mã, chúng tôi sẽ tham chiếu tới lớp placeholder `HTMLDocument`; hãy thay thế bằng API của thư viện bạn dùng.  
- Kiến thức cơ bản về đồng thời trong Java (không cần gì phức tạp).

---

![Diagram showing batch conversion of HTML files to PDF using ExecutorService](batch-convert-diagram.png "Convert HTML to PDF in parallel with ExecutorService")

*Alt text: Sơ đồ minh họa cách chuyển đổi HTML sang PDF bằng một thread pool cho xử lý batch.*

---

## Chuyển đổi HTML sang PDF song song (Batch Convert HTML to PDF)

Khi bạn có hàng chục—hoặc thậm chí hàng nghìn—tệp HTML, việc chuyển đổi từng tệp một trên luồng chính sẽ trở thành nút thắt. Một thread pool có kích thước cố định cho phép JVM tái sử dụng một số lượng luồng làm việc nhất định, giữ cho CPU hoạt động mạnh mà không làm quá tải hệ thống.

```java
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * Simple demo that batch converts HTML files to PDF using a fixed thread pool.
 * Replace HTMLDocument with the actual class from your chosen PDF library.
 */
public class HtmlToPdfBatch {

    public static void main(String[] args) {
        // 1️⃣ Prepare a list of HTML files to convert
        List<String> htmlPaths = List.of(
            "src/main/resources/page1.html",
            "src/main/resources/page2.html",
            "src/main/resources/page3.html"
        );

        // 2️⃣ Create a fixed‑size thread pool – 4 workers is a good starting point
        ExecutorService pool = Executors.newFixedThreadPool(4);

        // 3️⃣ Submit a conversion task for each HTML file
        for (String htmlPath : htmlPaths) {
            pool.submit(() -> convertAndSave(htmlPath));
        }

        // 4️⃣ Shutdown ExecutorService gracefully – no new tasks, wait for running ones
        shutdownGracefully(pool);
    }

    /**
     * Core conversion logic – this is where we **save HTML document as PDF**.
     */
    private static void convertAndSave(String htmlPath) {
        try {
            // Imagine HTMLDocument is from OpenHTMLtoPDF, iText, etc.
            HTMLDocument doc = new HTMLDocument(htmlPath);
            String pdfPath = htmlPath.replace(".html", ".pdf");
            doc.save(pdfPath);
            System.out.println("✅ Converted: " + htmlPath + " → " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    }

    /**
     * Helper that **shutdowns ExecutorService gracefully**.
     */
    private static void shutdownGracefully(ExecutorService executor) {
        executor.shutdown(); // stop accepting new tasks
        try {
            // Wait a maximum of 60 seconds for existing tasks to finish
            if (!executor.awaitTermination(60, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("⚠️ Pool didn’t terminate in time – forcing shutdown");
                executor.shutdownNow(); // cancel currently executing tasks
            } else {
                System.out.println("🛑 All tasks completed – executor shut down cleanly.");
            }
        } catch (InterruptedException ie) {
            // Preserve interrupt status & force shutdown
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }
}
```

### Tại sao cách này hoạt động

- **Parallelism**: Mỗi lời gọi `submit` giao việc chuyển đổi cho một luồng làm việc, vì vậy bốn tệp có thể được xử lý đồng thời trên máy quad‑core.  
- **Isolation**: Phương thức `convertAndSave` chứa toàn bộ logic cần thiết để **save HTML document as PDF**, giúp bạn dễ dàng thay đổi thư viện nền tảng sau này.  
- **Graceful termination**: Bằng cách gọi `shutdown()` trước, chúng ta thông báo cho pool “không còn công việc mới, vui lòng hoàn thành những gì đang chạy”. Vòng lặp `awaitTermination` cho các luồng cơ hội kết thúc, và chỉ khi chúng “cứng đầu” chúng ta mới gọi `shutdownNow()`. Mẫu này là cách được khuyến nghị để **shutdown ExecutorService gracefully**.

---

## Lưu tài liệu HTML dưới dạng PDF – Logic chuyển đổi cốt lõi

Trái tim của bất kỳ quy trình **convert HTML to PDF** nào là thư viện chuyển đổi. Mặc dù ví dụ dùng một lớp dummy `HTMLDocument`, dưới đây là một đoạn nhanh về cách bạn có thể thực hiện với **OpenHTMLtoPDF**:

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HTMLDocument {
    private final String htmlPath;

    public HTMLDocument(String htmlPath) {
        this.htmlPath = htmlPath;
    }

    public void save(String pdfPath) throws IOException {
        try (OutputStream os = new FileOutputStream(pdfPath);
             InputStream is = new FileInputStream(htmlPath)) {

            PdfRendererBuilder builder = new PdfRendererBuilder();
            builder.withHtmlContent(new String(is.readAllBytes()), null);
            builder.toStream(os);
            builder.run();
        }
    }
}
```

**Điều gì đang diễn ra?**  
1. Tệp HTML được đọc vào một chuỗi.  
2. `PdfRendererBuilder` phân tích markup, áp dụng CSS, và stream kết quả ra tệp PDF.  
3. Bất kỳ `IOException` nào sẽ được truyền lên `convertAndSave`, nơi chúng ta ghi log thành công hoặc thất bại.

Bạn có thể thay thế đoạn này bằng `HtmlConverter.convertToPdf` của iText hoặc `ITextRenderer` của Flying Saucer. Phần code quản lý thread‑pool vẫn giữ nguyên, vì vậy chúng tôi nhấn mạnh **save HTML document as PDF** như một mối quan tâm riêng biệt.

---

## Tắt ExecutorService một cách nhẹ nhàng – Các thực tiễn tốt nhất

Một lỗi phổ biến là gọi `shutdownNow()` ngay sau khi submit các tác vụ. Điều này sẽ ngắt đột ngột các luồng, có thể để lại các tệp PDF chưa hoàn thiện trên đĩa. Mẫu chúng tôi sử dụng—`shutdown()` → `awaitTermination()` → tùy chọn `shutdownNow()`—đảm bảo:

- **No new tasks** được chấp nhận sau khi bạn đã đưa mọi thứ vào hàng.  
- **Running tasks** có cơ hội hoàn thành sạch sẽ.  
- **Blocked threads** chỉ bị ngắt nếu chúng vượt quá thời gian chờ hợp lý (ở đây, 60 giây).  

Nếu bạn dự đoán PDF rất lớn hoặc engine render chậm, hãy tăng thời gian chờ hoặc dùng `executor.invokeAll(tasks, timeout, unit)` để kiểm soát chặt chẽ hơn.

---

## Ví dụ làm việc đầy đủ (Tất cả các phần gộp lại)

Dưới đây là toàn bộ chương trình mà bạn có thể sao chép‑dán vào một file `HtmlToPdfBatch.java` duy nhất. Chỉ cần thêm dependency OpenHTMLtoPDF (hoặc thư viện bạn thích) vào `pom.xml` hoặc Gradle build, và bạn đã sẵn sàng.



## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn hoàn chỉnh cùng các giải thích chi tiết từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF Java – Configuring Environment in Aspose.HTML](/html/english/java/configuring-environment/)
- [Convert HTML to PDF in Java – Step‑by‑Step Guide with Page Size Settings](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}