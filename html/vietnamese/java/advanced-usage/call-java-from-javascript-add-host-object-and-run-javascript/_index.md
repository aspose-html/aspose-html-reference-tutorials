---
category: general
date: 2026-03-14
description: Tìm hiểu cách gọi Java từ JavaScript bằng Aspose.HTML. Hướng dẫn này
  chỉ cách thêm đối tượng host, chạy JavaScript trong Java và ghi log từ JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: vi
og_description: Gọi Java từ JavaScript bằng Aspose.HTML. Thêm đối tượng host, chạy
  JavaScript trong Java và ghi log từ JavaScript trong một hướng dẫn duy nhất.
og_title: Gọi Java từ JavaScript – Hướng dẫn chi tiết với Đối tượng Host
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Gọi Java từ JavaScript – Thêm Đối tượng Host và Chạy JavaScript trong Java
url: /vi/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

sure to keep markdown formatting.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gọi Java từ JavaScript – Thêm Đối tượng Host và Chạy JavaScript trong Java

Bạn đã bao giờ **gọi Java từ JavaScript** trong một ứng dụng Java chưa? Có thể bạn đang xây dựng một engine báo cáo HTML động hoặc chỉ muốn cung cấp một logger Java cho một script bạn kiểm soát. Trong tutorial này, bạn sẽ thấy cách **thêm một đối tượng host**, **chạy JavaScript trong Java**, và thậm chí **ghi log từ JavaScript** trở lại JVM — tất cả đều với Aspose.HTML.

Chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy ngay, tạo một tài liệu HTML trống, tiêm một lớp `Logger` Java làm đối tượng host, thực thi một script nhỏ, và in kết quả ra console. Không cần trình duyệt web bên ngoài, không có “ma thuật” nào — chỉ là mã Java thuần túy mà bạn có thể sao chép‑dán và chạy ngay hôm nay.

## Yêu cầu trước

- Java 17 (hoặc bất kỳ JDK hiện đại nào) đã được cài đặt và cấu hình.
- Thư viện Aspose.HTML for Java (phiên bản 23.10 trở lên). Bạn có thể lấy nó từ Maven Central hoặc trang web Aspose.
- Một IDE đơn giản hoặc trình soạn thảo văn bản; ví dụ cũng chạy được từ dòng lệnh.

> **Mẹo:** Nếu bạn dùng Maven, thêm dependency sau vào file `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Hoặc, nếu dùng Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Bây giờ chúng ta đã có những kiến thức cơ bản, hãy bắt đầu giải pháp từng bước.

## Bước 1: Tạo một Dự án Java tối thiểu

Đầu tiên, tạo một lớp Java mới tên là `JsHostObjectDemo`. Lớp này sẽ chứa phương thức `main` và định nghĩa đối tượng host. Giữ mọi thứ trong một file giúp tutorial tự chứa và dễ sao chép.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### Tại sao lại dùng `HTMLDocument`?

Lớp `HTMLDocument` của Aspose.HTML khởi tạo một môi trường scripting tuân thủ HTML‑5 đầy đủ. Mặc dù chúng ta không tải bất kỳ markup nào, đối tượng `window` của tài liệu cung cấp quyền truy cập vào engine JavaScript, nơi **run JavaScript in Java** thực sự diễn ra.

## Bước 2: Thêm Đối tượng Host – “javaLogger”

Dòng

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

làm công việc nặng cho yêu cầu **add host object**. Bằng cách đăng ký instance `Logger` dưới tên `"javaLogger"`, bất kỳ script nào được đánh giá trong tài liệu này đều có thể gọi `javaLogger.log(...)`. Đây là cốt lõi của khái niệm **javascript host object**: một cầu nối cho phép JavaScript tiếp cận JVM.

### Những Cạm Bẫy Thường Gặp

- **Xung đột tên** – Nếu script của bạn đã có một biến toàn cục tên `javaLogger`, đối tượng host sẽ bị ghi đè. Hãy chọn một tên duy nhất.
- **An toàn đa luồng** – Đối tượng host được chia sẻ giữa các lần thực thi script trên cùng một tài liệu. Nếu bạn dự định chạy nhiều script đồng thời, hãy làm cho lớp host an toàn đa luồng (ví dụ: dùng `synchronized` hoặc các primitive của `java.util.concurrent`).

## Bước 3: Viết và Thực thi JavaScript

Script chúng ta đưa vào `eval` được viết rất ngắn gọn:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Khi `document.getWindow().eval(script)` chạy, engine sẽ tra cứu `javaLogger` trong phạm vi toàn cục, tìm thấy đối tượng Java mà chúng ta đã thêm, và gọi phương thức `log` với chuỗi đã cung cấp.

### Kết quả Mong đợi

Chạy phương thức `main` sẽ in dòng sau lên console:

```
[JS] Hello from JavaScript!
```

Dòng ngắn gọn này chứng minh chúng ta đã **call java from javascript** thành công, và **log from javascript** xuất hiện đúng như một thông điệp `System.out` thông thường của Java.

## Bước 4: Mở Rộng Đối tượng Host – Hơn Chỉ Ghi Log

Nếu bạn cần cung cấp thêm chức năng (ví dụ: truy cập file, truy vấn cơ sở dữ liệu), chỉ cần thêm các phương thức vào lớp `Logger` — hoặc tạo một lớp host mới. Dưới đây là một ví dụ nhanh cũng trả về giá trị:

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

Bây giờ console sẽ hiển thị:

```
[JS] 3+4=7
```

Điều này minh họa tính linh hoạt của mẫu **javascript host object**: bạn có thể phơi bày bất kỳ API Java nào bạn cần, miễn là các kiểu dữ liệu có thể chuyển đổi giữa Java và JavaScript (primitives, strings, arrays, …).

## Bước 5: Dọn Dẹp Tài Nguyên

Khi bạn đã xong với môi trường scripting, hãy giải phóng `HTMLDocument` để giải phóng tài nguyên gốc:

```java
document.dispose(); // Important for long‑running applications
```

Bỏ qua việc giải phóng có thể gây rò rỉ bộ nhớ, đặc biệt nếu bạn tạo nhiều tài liệu trong một vòng lặp.

## Ví dụ Hoàn chỉnh

Dưới đây là toàn bộ file nguồn mà bạn có thể biên dịch và chạy ngay lập tức. Lưu lại với tên `JsHostObjectDemo.java`, đảm bảo JAR Aspose.HTML nằm trong classpath, và thực thi `java JsHostObjectDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

Chạy chương trình này sẽ cho ra:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

Đó là toàn bộ quy trình **call java from javascript** chỉ trong vài dòng mã.

## Câu hỏi Thường gặp

### Có hoạt động trên Android không?

Aspose.HTML là thư viện thuần Java, vì vậy nó chạy trên bất kỳ JVM nào, bao gồm cả Dalvik/ART của Android. Chỉ cần đóng gói JAR và bạn sẽ có cùng khả năng host‑object.

### Nếu tôi cần truyền các đối tượng phức tạp thì sao?

Bạn có thể phơi bày các POJO (plain old Java objects) chứa các trường, getter và setter. Engine sẽ tự động ánh xạ chúng thành các đối tượng JavaScript. Đối với collection, dùng `java.util.List` hoặc mảng — cả hai đều có thể chuyển đổi.

### Xử lý lỗi như thế nào?

Nếu script ném ra lỗi JavaScript, `eval` sẽ truyền lên một `ScriptException`. Hãy bọc lời gọi trong khối try‑catch để ghi log hoặc phục hồi:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Tôi có thể chạy nhiều script liên tiếp không?

Chắc chắn rồi. Cùng một instance `HTMLDocument` giữ lại phạm vi toàn cục, vì vậy bạn có thể gọi `eval` nhiều lần. Chỉ cần chú ý tới việc trùng tên biến giữa các script.

## Các Thực hành Tốt nhất & Mẹo

- **Đặt tên đối tượng host một cách rõ ràng** — `javaLogger`, `javaUtils`, … — để tránh nhầm lẫn.
- **Giữ các phương thức host ngắn gọn và không gây side‑effect** khi có thể; điều này giúp việc debug dễ dàng hơn.
- **Giải phóng tài liệu** ngay khi không còn dùng; nó giải phóng bộ nhớ native mà Aspose.HTML cấp phát.
- **Kiểm tra đầu vào** từ JavaScript, đặc biệt nếu script đến từ nguồn không tin cậy. Xử lý chúng như bất kỳ dữ liệu bên ngoài nào khác.

## Kết luận

Bây giờ bạn đã có một ví dụ toàn diện, từ đầu tới cuối, về cách **call java from javascript** bằng cách **thêm một host object**, **chạy JavaScript trong Java**, và **ghi log từ JavaScript** sử dụng Aspose.HTML. Mô hình này mạnh mẽ: bất kỳ dịch vụ Java nào cũng có thể được phơi bày cho script, biến ứng dụng Java của bạn thành một nền tảng scripting nhẹ.

Tiếp theo, bạn có thể khám phá:

- Tiêm một trang HTML đầy đủ và thao tác DOM từ JavaScript.
- Sử dụng đối tượng host để truyền dữ liệu ngược lại Java (ví dụ: tuần tự hoá JSON).
- Tích hợp với các engine scripting khác như Nashorn hoặc GraalVM để hỗ trợ đa ngôn ngữ hơn.

Hãy thử, tùy chỉnh các lớp `Logger` hoặc `Utils`, và xem bạn có thể đẩy khái niệm **javascript host object** bao xa trong các dự án của mình.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}