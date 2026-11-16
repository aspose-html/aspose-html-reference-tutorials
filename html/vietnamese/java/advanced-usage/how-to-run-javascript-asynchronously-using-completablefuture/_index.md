---
category: general
date: 2026-02-16
description: Học cách chạy JavaScript trong Java với CompletableFuture, trì hoãn JS
  và đánh giá mã bất đồng bộ. Hướng dẫn chi tiết từng bước cho việc đánh giá JavaScript
  bất đồng bộ.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: vi
og_description: Thành thạo cách chạy JavaScript từ Java, trì hoãn JS và đánh giá mã
  bất đồng bộ bằng CompletableFuture trong hướng dẫn toàn diện này.
og_title: Cách chạy JavaScript bất đồng bộ bằng CompletableFuture
tags:
- javascript
- java
- asynchronous
- completablefuture
title: Cách chạy JavaScript bất đồng bộ bằng CompletableFuture
url: /vi/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách chạy JavaScript bất đồng bộ bằng CompletableFuture

Bạn đã bao giờ tự hỏi **cách chạy JavaScript** bên trong một ứng dụng Java mà không làm chặn luồng chính chưa? Có thể bạn cần gọi một đoạn script nhỏ để lấy dữ liệu, nhưng không muốn giao diện người dùng bị đóng băng. Tin tốt là các thư viện Java hiện đại cho phép bạn đánh giá JavaScript **bất đồng bộ**, và bạn thậm chí có thể tạo độ trễ giống như trong trình duyệt. Trong hướng dẫn này, chúng tôi sẽ trình bày một ví dụ hoàn chỉnh, có thể chạy được, sử dụng `ScriptEngine` của Aspose HTML kết hợp với `CompletableFuture` để **cách chạy javascript** và nhận kết quả trở lại trong Java.

Chúng tôi cũng sẽ đề cập đến **cách sử dụng CompletableFuture**, **cách tạo độ trễ cho JS**, và **cách đánh giá mã async** để bạn có thể **đánh giá JavaScript bất đồng bộ** trong bất kỳ dự án Java nào. Khi kết thúc, bạn sẽ có một mẫu sẵn sàng để sao chép‑dán, tùy chỉnh và nhúng vào các hệ thống lớn hơn.

---

## Những gì bạn sẽ học

- Cài đặt một `ScriptEngine` Java có thể thực thi JavaScript hiện đại ES2022.  
- Viết một hàm `async` bao gồm độ trễ (`cách tạo độ trễ js`).  
- Gọi `evaluateAsync` và nhận một `CompletableFuture` (`cách sử dụng completablefuture`).  
- Lấy kết quả khi promise JavaScript được giải quyết (`cách đánh giá async`).  
- Mẹo xử lý lỗi, quản lý luồng, và mở rộng mẫu.

Không cần công cụ xây dựng bên ngoài nào ngoài JAR Aspose HTML for Java, bạn chỉ cần đưa nó vào classpath. Hãy bắt đầu.

---

## Bước 1: Cách chạy JavaScript – Khởi tạo Engine Script

Đầu tiên, thư viện Aspose HTML cung cấp lớp `ScriptEngine` có thể thực thi mã JavaScript. Hãy nghĩ nó như một công cụ Chromium nhỏ chạy bên trong JVM của bạn.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Tại sao điều này quan trọng:** Khi khởi tạo `ScriptEngine` chúng ta có được một môi trường sandboxed, nơi JavaScript hiện đại (bao gồm `async/await`) hoạt động ngay lập tức. Không cần khởi động một tiến trình Node bên ngoài.

---

## Bước 2: Cách tạo độ trễ cho JS – Viết hàm Async với Timer dựa trên Promise

`setTimeout` của JavaScript là cách cổ điển để tạm dừng thực thi. Trong mã hiện đại, chúng ta gói nó trong một `Promise` để có thể `await`. Đó chính là những gì chúng ta sẽ làm trong chuỗi script.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **Cách tạo độ trễ js:** Trợ giúp `delay` tạo một promise sẽ hoàn thành sau `ms` miligiây. Khi `await` nó, hàm sẽ tạm dừng mà không chặn luồng Java.

---

## Bước 3: Cách đánh giá async – Chạy script và nhận CompletableFuture

Thay vì phương thức đồng bộ `evaluate`, chúng ta gọi `evaluateAsync`. Nó ngay lập tức trả về một `CompletableFuture<Object>` sẽ được hoàn thành khi promise JavaScript được giải quyết.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Cách đánh giá async:** `evaluateAsync` kết nối vòng lặp sự kiện JavaScript với `CompletableFuture` của Java. Đây là lõi của **đánh giá javascript bất đồng bộ**.

---

## Bước 4: Cách sử dụng CompletableFuture – Gắn callback và chặn để demo

Bây giờ chúng ta gắn một callback bằng `thenAccept` để in kết quả, và chặn luồng chính đủ lâu để bản demo hoàn thành.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Tại sao chúng ta gọi `get()`:** Trong một ứng dụng thực tế, bạn có thể sẽ tiếp tục xử lý ở nơi khác. Ở đây chúng ta chặn để ví dụ tự chứa.

---

## Tổng quan trực quan

![Diagram showing how to run JavaScript asynchronously with CompletableFuture](https://example.com/diagram.png "How to Run JavaScript – Async Flow")

*Alt text:* **Diagram showing how to run JavaScript asynchronously with CompletableFuture** – hình ảnh minh họa luồng từ Java tới engine script, độ trễ async, và việc hoàn thành CompletableFuture.

---

## Những lỗi thường gặp & Thực hành tốt (Cách đánh giá async một cách an toàn)

| Pitfall | What Happens | Fix |
|---------|--------------|-----|
| Quên trả về promise | `evaluateAsync` giải quyết ngay lập tức với `undefined` | Đảm bảo dòng cuối cùng của script là promise (`fetchMessage();`) |
| Dùng `Thread.sleep` chặn trong JS | Chặn vòng lặp sự kiện của engine, mất đi tính async | Sử dụng mẫu promise `delay` (như đã minh họa) |
| Bỏ qua ngoại lệ | Future hoàn thành bất thường, nhưng bạn không thấy | Gắn `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Không tắt engine | Rò rỉ tài nguyên trong các ứng dụng chạy lâu | Gọi `scriptEngine.dispose()` khi xong |

---

## Mở rộng mẫu (Cách sử dụng CompletableFuture trong dự án thực tế)

Bạn có thể nối chuỗi nhiều lời gọi JavaScript async, kết hợp chúng với các future khác, hoặc thậm chí chạy chúng trên một `Executor` tùy chỉnh. Dưới đây là một bản phác thảo nhanh:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **Cách sử dụng CompletableFuture:** Bằng cách truyền một `Executor` bạn kiểm soát pool luồng, giữ UI phản hồi và tránh tình trạng thiếu luồng.

---

## Kết quả mong đợi

Chạy lớp `JsAsyncDemo` và bạn sẽ thấy:

```
JS result: Hello from async JS!
```

Khoảng dừng 500 ms không hiển thị trong console, nhưng bạn có thể thêm dấu thời gian để xác nhận độ trễ nếu muốn.

---

## Tóm tắt – Cách chạy JavaScript với CompletableFuture

Chúng ta đã bắt đầu bằng **cách chạy javascript** trong Java, viết một hàm `async` để **cách tạo độ trễ js**, thực thi nó bằng `evaluateAsync` (**cách đánh giá async**), và lấy kết quả bằng **cách sử dụng completablefuture**. Toàn bộ luồng này minh họa **đánh giá javascript bất đồng bộ** trong một mẫu sạch, có thể tái sử dụng.

---

## Tiếp theo?

- **Tích hợp với client HTTP:** Lấy dữ liệu từ endpoint REST trong JS async và trả về Java.  
- **Sử dụng nhiều script:** Nối chuỗi nhiều lời gọi `evaluateAsync` cho các pipeline phức tạp.  
- **Thay đổi engine:** Mẫu tương tự hoạt động với Nashorn, GraalVM, hoặc các runtime JavaScript khác—chỉ cần thay `ScriptEngine`.

Hãy thử nghiệm với độ trễ dài hơn, script ném lỗi, hoặc thậm chí các mô-đun WebAssembly. Khi kết hợp các primitive đồng thời của Java với JavaScript hiện đại, khả năng là vô hạn.

---

### Có câu hỏi?

Nếu có gì chưa rõ—có thể bạn đang thắc mắc cách xử lý promise bị từ chối hoặc cách truyền biến từ Java vào script—hãy để lại bình luận bên dưới. Chúc bạn lập trình vui!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}