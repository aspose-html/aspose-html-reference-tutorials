---
category: general
date: 2026-06-19
description: Cách khởi tạo thread trong Java bằng một Runnable có thể tái sử dụng,
  khởi động nhiều thread, in tên thread và phân tích HTML bằng Java. Ví dụ từng bước.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: vi
og_description: Cách khởi tạo luồng trong Java bằng Runnable, chạy nhiều luồng, in
  tên luồng và phân tích HTML với Java trong một ví dụ duy nhất, có thể chạy được.
og_title: Cách khởi tạo thread trong Java – Hướng dẫn đầy đủ
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
title: Cách bắt đầu luồng trong Java – Hướng dẫn chi tiết
url: /vi/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách bắt đầu thread trong Java – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi **cách bắt đầu thread** trong Java mà không bị ngập trong mã lặp lại? Bạn không phải là người duy nhất. Dù bạn đang xây dựng một trình thu thập web, một bộ cập nhật UI, hay chỉ cần chuyển một phép tính nặng sang nền, việc thành thạo tạo thread là kỹ năng không thể thiếu đối với bất kỳ lập trình viên Java nào.

Trong tutorial này, chúng ta sẽ đi qua một kịch bản thực tế: **phân tích HTML bằng Java**, in ra tên thread hiện tại, và **bắt đầu nhiều thread** chia sẻ cùng một logic. Khi kết thúc, bạn sẽ biết **cách sử dụng Runnable**, khởi tạo nhiều worker, và thấy kết quả mong muốn — tất cả trong một ví dụ tự chứa mà bạn có thể sao chép‑dán ngay lập tức.

## Những gì bạn sẽ học

- Các bước chính **cách bắt đầu thread** bằng cách sử dụng lớp `Thread` và một `Runnable`.
- Cách **bắt đầu nhiều thread** thực thi cùng một nhiệm vụ mà không sao chép mã.
- Cách đơn giản nhất để **in tên thread** cùng với kết quả xử lý của bạn.
- Phương pháp sạch sẽ để **phân tích HTML bằng Java** sử dụng một helper `HTMLDocument` nhẹ (hoặc bất kỳ trình phân tích nào bạn thích).
- Tại sao **cách sử dụng runnable** lại quan trọng cho mã có thể tái sử dụng và kiểm thử.

Không cần thư viện bên ngoài cho ví dụ cốt lõi, nhưng chúng tôi sẽ ghi chú nơi bạn có thể thay thế bằng Jsoup hoặc trình phân tích khác nếu cần sức mạnh hơn.

---

## Bước 1: Định nghĩa một nhiệm vụ có thể tái sử dụng – **how to use runnable**

Điều đầu tiên bạn cần biết **how to use runnable** là đóng gói công việc mà mỗi thread sẽ thực hiện. Một `Runnable` chỉ là một giao diện chức năng với một phương thức `run()`, khiến nó hoàn hảo cho các biểu thức lambda.

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

**Tại sao điều này quan trọng:** Bằng cách giữ logic bên trong một `Runnable`, bạn có thể truyền nó cho bất kỳ số lượng đối tượng `Thread`, một pool thread, hoặc thậm chí một executor service sau này. Điều này giúp mã của bạn DRY và dễ kiểm thử.

---

## Bước 2: **How to start thread** – tạo worker đầu tiên

Bây giờ chúng ta đã có một `Runnable`, việc khởi chạy một thread đơn giản như gọi constructor `Thread`. Câu hỏi **how to start thread** được trả lời trong một dòng duy nhất:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Lưu ý đối số thứ hai, `"Worker-1"`. Tên này sẽ xuất hiện khi chúng ta sau này **in tên thread**, giúp việc gỡ lỗi trở nên ít bí ẩn hơn.

---

## Bước 3: **Start multiple threads** – tái sử dụng cùng một Runnable

Muốn xử lý nhiều tệp HTML cùng lúc? Chỉ cần tạo thêm một `Thread` với cùng một `Runnable`. Điều này minh họa **start multiple threads** mà không cần sao chép mã nhiệm vụ:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Cả `Worker-1` và `Worker-2` sẽ thực thi khối được định nghĩa trong `extractTextLength` đồng thời. Vì nhiệm vụ không có trạng thái (chỉ đọc tệp), không có điều kiện tranh chấp nào cần lo lắng.

---

## Bước 4: **Print thread name** while parsing HTML

Trong `Runnable` chúng ta đã gọi `Thread.currentThread().getName()`. Đó là cách chuẩn để **in tên thread**. Đầu ra sẽ trông giống như sau (giả sử phần thân HTML chứa 1 234 ký tự):

```
Worker-1: 1234
Worker-2: 1234
```

Nếu bạn chạy chương trình trên một tệp lớn hơn, mỗi dòng sẽ hiển thị cùng một độ dài vì cả hai thread đều đọc cùng một tệp. Thay đổi đường dẫn hoặc truyền tên tệp làm tham số để thấy kết quả khác nhau.

---

## Bước 5: Full, runnable example – from import to execution

Dưới đây là chương trình **tự chứa** đầy đủ mà bạn có thể đặt vào một file tên `HtmlThreadDemo.java`. Nó bao gồm một stub `HTMLDocument` nhỏ để mã biên dịch ngay cả khi bạn chưa có trình phân tích thực tế. Thay thế stub bằng Jsoup hoặc bất kỳ thư viện nào bạn thích cho môi trường production.

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

### Kết quả mong đợi

Giả sử `page.html` chứa 2 567 ký tự trong thẻ `<body>`, bạn sẽ thấy điều gì đó như:

```
Worker-1: 2567
Worker-2: 2567
```

Nếu tệp không đọc được, stack trace sẽ được in ra — nhờ khối `catch`.

---

## Các vấn đề thường gặp & Mẹo chuyên nghiệp

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| **File not found** | Đường dẫn `"YOUR_DIRECTORY/page.html"` là tương đối so với vị trí bạn khởi chạy JVM. | Sử dụng đường dẫn tuyệt đối hoặc `Paths.get("").toAbsolutePath()` để kiểm tra. |
| **Race conditions** | Nếu `Runnable` thay đổi trạng thái chung, các thread có thể xung đột. | Giữ nhiệm vụ không trạng thái, hoặc đồng bộ hoá truy cập tới các đối tượng chung. |
| **Too many threads** | Tạo ra hàng chục `Thread` có thể làm cạn kiệt tài nguyên hệ điều hành. | Chuyển sang `ExecutorService` với pool có kích thước giới hạn sau khi đã nắm vững các khái niệm cơ bản. |
| **Incorrect HTML parsing** | Stub `HTMLDocument` quá đơn giản; các trang phức tạp sẽ bị lỗi. | Thay thế bằng Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## Mở rộng ví dụ

Bây giờ bạn đã biết **cách bắt đầu thread**, bạn có thể muốn:

- **Phân tích các tệp khác nhau** bằng cách truyền tên tệp vào `Runnable` (sử dụng constructor hoặc lambda bắt biến).
- **Thu thập kết quả** bằng một `ConcurrentLinkedQueue<Integer>` thay vì chỉ in ra.
- **Sử dụng thread pool** (`Executors.newFixedThreadPool(4)`) để mở rộng quy mô tốt hơn.
- **Thay đổi trình phân tích** sang Jsoup, HtmlUnit, hoặc bất kỳ thư viện nào phù hợp với dự án của bạn.

Tất cả các bước này vẫn dựa trên ý tưởng cốt lõi mà chúng ta đã đề cập: định nghĩa một nhiệm vụ có thể tái sử dụng, giao nó cho một hoặc nhiều thread, và quan sát thread nào đang thực hiện công việc bằng cách **in tên thread**.

---

## Kết luận

Chúng ta đã bao quát **cách bắt đầu thread** trong Java, trình bày **cách sử dụng runnable** cho công việc tái sử dụng, chỉ ra cách **bắt đầu nhiều thread**, và minh họa một cách đơn giản để **phân tích HTML bằng Java** đồng thời **in tên thread** cho mỗi worker. Đoạn mã hoàn chỉnh ở trên đã sẵn sàng để chạy, và các khái niệm này có thể mở rộng tới các ứng dụng Java đa luồng phức tạp hơn.

Hãy thoải mái thử nghiệm: thay đổi đường dẫn tệp, tăng số lượng worker, hoặc tích hợp một trình phân tích HTML thực tế. Những nguyên tắc cơ bản vẫn giữ nguyên, và bạn đã có nền tảng vững chắc cho bất kỳ dự án Java đa luồng nào.

Có câu hỏi về an toàn thread, executor services, hay thư viện phân tích HTML? Hãy để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Fixed thread pool java – Làm sạch HTML song song với ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Cách chỉnh sửa HTML bằng Aspose.HTML cho Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Cách chuyển HTML sang PDF Java – Sử dụng Aspose.HTML cho Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}