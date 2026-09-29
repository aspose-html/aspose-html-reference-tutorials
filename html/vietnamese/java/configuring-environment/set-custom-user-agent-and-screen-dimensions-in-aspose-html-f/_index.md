---
category: general
date: 2026-09-29
description: Đặt user agent tùy chỉnh trong Aspose.HTML cho Java và tìm hiểu cách
  thiết lập kích thước màn hình ảo để hiển thị HTML một cách chính xác.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: vi
lastmod: 2026-09-29
og_description: Đặt user agent tùy chỉnh trong Aspose.HTML cho Java và tìm hiểu cách
  thiết lập kích thước màn hình ảo để hiển thị HTML một cách chính xác.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Thiết lập user agent tùy chỉnh và kích thước màn hình trong Aspose.HTML
  cho Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Đặt user agent tùy chỉnh và kích thước màn hình trong Aspose.HTML cho Java
url: /vi/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đặt custom user agent và kích thước màn hình trong Aspose.HTML for Java

Nếu bạn cần **set custom user agent** khi render HTML với Aspose.HTML for Java, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bằng cách cấu hình sandbox, bạn cũng có thể **set virtual screen size**, đảm bảo bố cục khớp với viewport của trình duyệt thực.

Bạn sẽ hoàn thành tutorial này với một chương trình đầy đủ, có thể chạy được mà **specifies user agent**, **sets screen width**, và **sets screen height**. Không cần công cụ bên ngoài—chỉ cần Aspose.HTML for Java và môi trường chạy Java 8+.

## Những gì bạn sẽ học

* Cách tạo một `SandboxConfiguration` để cô lập quá trình render.
* Cách **set custom user agent** và tại sao nó quan trọng đối với các trang responsive.
* Cách **set virtual screen size** (độ rộng và chiều cao màn hình) để có bố cục chính xác.
* Cách tải một tệp HTML vào sandbox và lưu kết quả đã xử lý.
* Các lỗi thường gặp và mẹo thực hành tốt cho việc render trong sandbox.

> **Prerequisites** – Bạn cần một giấy phép Aspose.HTML for Java hợp lệ, Java 8 hoặc mới hơn, và một IDE (IntelliJ IDEA, Eclipse, hoặc VS Code). Ví dụ sử dụng tệp `input.html` cục bộ, nhưng bất kỳ URL nào có thể truy cập đều hoạt động.

![Sandbox flow diagram](sandbox-flow.png "set custom user agent example in Java")

## Bước 1: Tạo cấu hình sandbox (nền tảng)

Sandbox cô lập môi trường render khỏi JVM host, điều này rất quan trọng khi bạn muốn **set custom user agent** hoặc thay đổi kích thước viewport.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Why this step?*  
`SandboxConfiguration` chứa tất cả các tùy chọn render, bao gồm **screen dimensions** và **user‑agent** strings. Bằng cách cấu hình trước khi tải tài liệu, bạn đảm bảo engine HTML tôn trọng các cài đặt này ngay từ yêu cầu đầu tiên.

## Bước 2: Đặt kích thước màn hình để mô phỏng thiết bị thực

Các trang responsive thường đọc `window.innerWidth` và `window.innerHeight`. Để engine nghĩ rằng nó đang chạy trên màn hình 1024 × 768, bạn **set virtual screen size**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Why this matters* – Nếu bạn bỏ qua **set screen dimensions**, renderer có thể mặc định một viewport rất nhỏ, khiến các media query CSS chọn bố cục mobile. Bằng cách rõ ràng **set screen width** và **set screen height**, bạn kiểm soát các quy tắc CSS nào được áp dụng.

## Bước 3: Chỉ định chuỗi user‑agent tùy chỉnh

Một số trang web cung cấp nội dung khác nhau dựa trên header user‑agent. Để **specify user agent** bạn chỉ cần đặt nó trên cấu hình sandbox:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Why use a custom user agent?*  
Một chuỗi tùy chỉnh có thể vượt qua việc phát hiện bot, kích hoạt các tính năng chỉ dành cho desktop, hoặc kiểm tra cách một trang hoạt động với một phiên bản trình duyệt cụ thể. Engine Aspose chuyển tiếp giá trị này trong mọi yêu cầu HTTP khi tải các tài nguyên bên ngoài (CSS, hình ảnh, script).

## Bước 4: Tải tài liệu HTML vào sandbox

Bây giờ sandbox đã được cấu hình đầy đủ, tải tệp HTML. Constructor nhận đường dẫn tệp và một `SandboxConfiguration` sẽ tự động áp dụng tất cả các cài đặt chúng ta đã định nghĩa.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Nếu bạn cần tải từ URL từ xa, thay thế đường dẫn tệp bằng chuỗi URL—Aspose.HTML vẫn sẽ tôn trọng **set custom user agent** và **screen dimensions**.

## Bước 5: Lưu kết quả đã xử lý

Sau khi tài liệu tải xong, bạn có thể lưu nó ở bất kỳ định dạng hỗ trợ nào. Ở đây chúng tôi ghi một tệp HTML đã được sandboxed phản ánh bất kỳ thay đổi DOM nào do các cài đặt tùy chỉnh gây ra.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

Tệp đã lưu sẽ chứa cùng một markup, nhưng bất kỳ script nào truy vấn `navigator.userAgent` hoặc kiểm tra `window.innerWidth` bây giờ sẽ thấy các giá trị bạn cung cấp.

## Ví dụ đầy đủ, có thể chạy

Kết hợp tất cả các bước lại với nhau sẽ cho bạn một chương trình tự chứa mà bạn có thể sao chép, dán và chạy.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ tạo `sandboxed_output.html`. Nếu bạn mở nó trong trình duyệt và kiểm tra `navigator.userAgent` qua console, bạn sẽ thấy **AsposeHTML/1.0**. Tương tự, `window.innerWidth` sẽ báo **1024**, xác nhận rằng **set screen dimensions** đã hoạt động như mong đợi.

## Các câu hỏi thường gặp & xử lý trường hợp biên

| Câu hỏi | Câu trả lời |
|----------|--------|
| **Nếu trang tải thêm tài nguyên từ một miền khác?** | Sandbox chuyển tiếp **custom user agent** trong mọi yêu cầu, nhưng các chính sách cross‑origin vẫn được áp dụng. Sử dụng `sandboxConfig.setAllowCrossDomain(true)` nếu bạn cần nới lỏng các hạn chế đó. |
| **Tôi có thể thay đổi kích thước màn hình sau khi tài liệu đã được tải không?** | Không. Kích thước màn hình được đọc trong lần layout ban đầu. Để render với kích thước khác, tạo một `SandboxConfiguration` mới và tải lại tài liệu. |
| **Tôi có cần gọi `document.close()` không?** | `HTMLDocument` triển khai `AutoCloseable`. Sử dụng khối try‑with‑resources đảm bảo dọn dẹp đúng cách, nhưng việc gọi `close()` một cách rõ ràng là tùy chọn trong các script đơn giản. |
| **Điều này khác như thế nào so với việc đặt user‑agent trong một HTTP client?** | Việc đặt user‑agent trên sandbox ảnh hưởng đến **tất cả** các yêu cầu tài nguyên do engine HTML thực hiện, không chỉ yêu cầu HTML ban đầu. Điều này mô phỏng trình duyệt thực tế gần hơn. |
| **Sandbox có an toàn cho HTML không đáng tin cậy không?** | Có. Sandbox cô lập quyền truy cập hệ thống tệp và giới hạn các cuộc gọi mạng theo cấu hình, giảm nguy cơ script độc hại ảnh hưởng tới JVM host của bạn. |

## Mẹo chuyên nghiệp

* **Reuse configurations** – Nếu bạn render nhiều trang với cùng viewport, tạo một `SandboxConfiguration` duy nhất và tái sử dụng nó để tránh chi phí tạo đối tượng.
* **Debug with logging** – Bật logging của Aspose.HTML (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) để xem tài nguyên nào đã được fetch với custom user‑agent.
* **Combine with CSS media queries** – Bằng cách điều chỉnh **set screen width** bạn có thể kiểm tra cách thiết kế responsive của mình hoạt động trên tablet, điện thoại, hoặc desktop lớn mà không cần mở trình duyệt thực.

## Kết luận

Bây giờ bạn đã biết cách **set custom user agent** và **set screen dimensions** khi render HTML với Aspose.HTML for Java. Bằng cách cấu hình sandbox, bạn cô lập môi trường, kiểm soát viewport, và đảm bảo các tài nguyên bên ngoài nhận được đúng header bạn chỉ định. Kỹ thuật này rất cần thiết để kiểm thử bố cục responsive, vượt qua các chặn bot, hoặc tái tạo các tính năng chỉ dành cho desktop trong các pipeline tự động.

Tiếp theo, bạn có thể khám phá **how to set custom cookies** hoặc **capture rendered screenshots** bằng API render của Aspose.HTML—cả hai khái niệm đều dựa trên mẫu cấu hình sandbox mà bạn vừa nắm vững.

Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, hoạt động với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [High DPI Rendering in Java – Capture Webpage Screenshots with Custom User Agent](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Create HTML File Java & Set Up Network Service (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}