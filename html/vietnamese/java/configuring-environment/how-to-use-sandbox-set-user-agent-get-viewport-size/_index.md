---
category: general
date: 2026-04-03
description: Học cách sử dụng sandbox trong Aspose.HTML Java để thiết lập user agent,
  thiết lập kích thước và lấy kích thước viewport ngay lập tức. Bao gồm mã đầy đủ,
  giải thích và mẹo.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: vi
og_description: Tìm hiểu cách sử dụng sandbox trong Aspose.HTML Java để đặt user agent,
  thiết lập kích thước và lấy kích thước viewport ngay lập tức. Hướng dẫn đầy đủ kèm
  mã và các thực tiễn tốt nhất.
og_title: Cách sử dụng Sandbox – Đặt User Agent và lấy kích thước viewport
tags:
- AsposeHTML
- Java
- Sandbox
title: Cách sử dụng Sandbox – Đặt User Agent và Lấy kích thước Viewport
url: /vi/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng Sandbox – Đặt User Agent & Lấy Kích Thước Viewport

Bạn đã bao giờ tự hỏi **cách sử dụng sandbox** khi render HTML với Aspose.HTML for Java chưa? Có thể bạn đã gặp khó khăn khi muốn mô phỏng một kích thước màn hình cụ thể hoặc cần giả mạo một chuỗi user‑agent để trang web hành xử như thể đang được truy cập từ trình duyệt di động.  

Tin tốt là API sandbox cho phép bạn làm chính xác điều đó, và bạn cũng có thể lấy kích thước viewport đã tính toán sau khi trang tải xong. Trong hướng dẫn này, chúng ta sẽ đi qua việc tạo sandbox, đặt kích thước, đặt user agent tùy chỉnh, tải một trang từ xa, và cuối cùng đọc các kích thước viewport. Khi kết thúc, bạn sẽ biết **cách đặt kích thước**, **cách lấy viewport**, và lý do tại sao các bước này quan trọng cho việc render headless đáng tin cậy.

> **Quick win:** bạn sẽ có một lớp Java có thể chạy được và in ra một thứ gì đó như `Viewport: 1280×800` trong vài giây.

---

## Những Gì Bạn Cần

- **Aspose.HTML for Java** phiên bản 24.6 hoặc mới hơn (API chúng tôi dùng được giới thiệu từ 24.5).  
- Bộ công cụ phát triển Java 17+ (bất kỳ JDK hiện đại nào cũng hoạt động).  
- Một IDE hoặc trình soạn thảo văn bản đơn giản—không cần plugin đặc biệt.  
- Kết nối Internet nếu bạn muốn tải một URL bên ngoài như `https://example.com`.

Chỉ vậy thôi. Không bắt buộc phải dùng Maven/Gradle; bạn có thể tự tay đặt các file JAR vào classpath nếu muốn.  

---

## Cách Sử Dụng Sandbox – Tổng Quan

Sandbox tách riêng engine render khỏi hệ điều hành host, cho phép bạn định nghĩa một màn hình ảo (width, height, DPI) và một chuỗi **user agent** tùy chỉnh. Hãy nghĩ nó như một cửa sổ trình duyệt thu nhỏ tồn tại hoàn toàn trong bộ nhớ. Khi bạn sau này yêu cầu `HTMLDocument` lấy view mặc định, engine sẽ báo cáo **kích thước viewport** mà nó tính dựa trên các thiết lập của sandbox.

Dưới đây là luồng cấp cao:

1. **Create** một `DocumentSandbox` và cấu hình width, height, DPI, và user‑agent.  
2. **Load** một `HTMLDocument` bên trong sandbox đó.  
3. **Query** view mặc định của tài liệu để lấy kích thước viewport.  

Hãy đi sâu vào từng bước.

---

## Bước 1: Tạo Sandbox và Đặt Kích Thước

Đầu tiên, chúng ta khởi tạo một sandbox và cho nó biết màn hình ảo nên có kích thước bao nhiêu. Đây là nơi bạn trả lời câu hỏi **cách đặt kích thước** cho việc render headless.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Pro tip:** Nếu bạn đang kiểm thử layout responsive, hãy thử độ rộng hẹp như `360` để mô phỏng điện thoại, hoặc rộng như `1920` cho máy tính để bàn. Sandbox tôn trọng DPI bạn đặt, vì vậy màn hình độ mật độ cao (ví dụ, 144 DPI) sẽ ảnh hưởng đến các media‑query sử dụng `device-pixel-ratio`.

---

## Bước 2: Đặt User Agent cho Sandbox

Tại sao phải lo lắng về một **user agent** tùy chỉnh? Một số trang cung cấp markup hoặc script khác nhau tùy vào trình duyệt được báo cáo. Bằng cách gọi `setUserAgent` bạn có thể lừa trang web nghĩ rằng nó đang được truy cập từ Chrome, Firefox, hoặc thiết bị di động.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Bây giờ trang sẽ nghĩ rằng nó đang render trên iPhone. Nếu bạn cần **đặt user agent** trở lại mặc định, chỉ cần sử dụng lại chuỗi “AsposeHTML/24.6 …” ở trên.

---

## Bước 3: Tải Tài Liệu HTML Bên Trong Sandbox

Khi sandbox đã sẵn sàng, chúng ta có thể tải bất kỳ URL hoặc file HTML cục bộ nào. Constructor của `HTMLDocument` nhận sandbox làm đối số thứ hai, liên kết hai thành phần lại với nhau.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

Khối `try‑with‑resources` đảm bảo tài liệu được giải phóng đúng cách, giải phóng các tài nguyên gốc mà Aspose.HTML cấp dưới lớp.

---

## Bước 4: Lấy Kích Thước Viewport Từ Tài Liệu

Đây là khoảnh khắc bạn đang chờ đợi: lấy **kích thước viewport** mà engine render đã tính toán. Điều này trả lời **cách lấy viewport** sau khi trang đã được bố trí.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Khi bạn chạy chương trình, bạn sẽ thấy một thứ gì đó như:

```
Viewport: 1280×800
```

Nếu bạn đã thay đổi kích thước sandbox trong Bước 1, các số được in ra sẽ phản ánh các giá trị mới—hoàn hảo cho các bài kiểm thử tự động xác minh các breakpoint responsive.

---

## Ví Dụ Hoàn Chỉnh Hoạt Động

Dưới đây là lớp hoàn chỉnh, sẵn sàng chạy, kết hợp tất cả các phần lại với nhau. Sao chép‑dán nó vào một file có tên `SandboxExample.java`, thêm các JAR của Aspose.HTML vào classpath, và thực thi `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Kết quả mong đợi** (giả sử các thiết lập sandbox ở trên):

```
Viewport: 1280×800
```

Nếu bạn đặt độ rộng/chiều cao khác trong sandbox, kết quả sẽ thay đổi tương ứng—đúng những gì bạn cần khi kiểm thử thiết kế responsive.

---

## Các Trường Hợp Cạnh & Câu Hỏi Thường Gặp

### Nếu trang sử dụng `window.innerWidth` thay vì các media query CSS thì sao?

Kích thước màn hình ảo của sandbox ảnh hưởng cả tới layout CSS và JavaScript `window.innerWidth/innerHeight`. Vì vậy **cách lấy viewport** qua JavaScript sẽ trả về cùng các số bạn thấy trong console Java.

### Tôi có thể chạy nhiều sandbox đồng thời không?

Có. Mỗi instance của `DocumentSandbox` là độc lập, vì vậy bạn có thể tạo một thread pool, cấp cho mỗi thread một sandbox riêng với các kích thước khác nhau, và render hàng chục trang đồng thời. Chỉ cần nhớ giữ các JAR thread‑safe (chúng đã được thiết kế như vậy).

### Cài đặt DPI có ảnh hưởng tới việc thu phóng ảnh không?

Chắc chắn. DPI cao hơn làm cho một pixel CSS tương ứng với nhiều pixel thiết bị hơn, có thể khiến ảnh độ phân giải cao trông sắc nét hơn. Nếu bạn đang kiểm thử các tài nguyên kiểu retina, hãy thử `sandbox.setDeviceDpi(144)`.

### Làm thế nào để xử lý các chứng chỉ HTTPS tự ký

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}