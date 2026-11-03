---
category: general
date: 2026-02-22
description: Đặt tỷ lệ pixel của thiết bị trong Java với sandbox Aspose.HTML. Tìm
  hiểu cách đặt user agent tùy chỉnh, lấy tiêu đề trang Java và chuyển đổi HTML sang
  PNG trong một hướng dẫn duy nhất.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: vi
og_description: Đặt tỷ lệ pixel của thiết bị trong Java bằng sandbox Aspose.HTML.
  Hướng dẫn này cho thấy cách đặt user agent tùy chỉnh, lấy tiêu đề trang bằng Java
  và chuyển đổi HTML sang PNG.
og_title: Thiết lập Tỷ lệ Pixel của Thiết bị trong Java – Hướng dẫn toàn diện
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Thiết lập Tỷ lệ Pixel của Thiết bị trong Java – Hướng dẫn toàn diện
url: /vi/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đặt Tỷ Lệ Pixel Thiết Bị trong Java – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi làm thế nào để **đặt tỷ lệ pixel thiết bị** khi render một trang web từ Java? Bạn không phải là người duy nhất. Nhiều nhà phát triển cần mô phỏng màn hình di động DPI cao để ảnh chụp màn hình trông sắc nét, đặc biệt khi họ sau này **lưu html dưới dạng hình ảnh** cho báo cáo hoặc tài sản marketing. Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ thực tế thực hiện đúng điều đó—cùng với việc chỉ cho bạn cách **đặt user agent tùy chỉnh**, **lấy tiêu đề trang java**, và **chuyển đổi html sang png** bằng Aspose.HTML.

Chúng ta sẽ bắt đầu với một cái nhìn tổng quan ngắn gọn về API sandbox, sau đó đi sâu vào từng bước cấu hình, và cuối cùng tạo ra một tệp PNG phản ánh màn hình iPhone thực tế. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng và chèn vào bất kỳ dự án Java nào. Không cần công cụ bên ngoài, chỉ cần Java thuần và Aspose.HTML 7.x (hoặc mới hơn).

---

## Yêu Cầu Trước

- Java 17 hoặc mới hơn (mã có thể biên dịch với các phiên bản cũ hơn nhưng khuyến nghị dùng 17).
- Thư viện Aspose.HTML cho Java (tải xuống từ trang chính thức của Aspose; tọa độ Maven: `com.aspose:aspose-html:23.10`).
- Một IDE hoặc trình soạn thảo văn bản tuỳ bạn (IntelliJ IDEA, VS Code, Eclipse… đều hoạt động).
- Kết nối Internet để truy cập URL demo (`https://example.com/responsive.html`), hoặc thay thế bằng bất kỳ trang HTML công cộng nào bạn sở hữu.

> **Mẹo:** Nếu bạn đang ở sau proxy, hãy cấu hình các thuộc tính hệ thống `http.proxyHost` và `http.proxyPort` của JVM trước khi chạy mã.

## Bước 1: Đặt Tỷ Lệ Pixel Thiết Bị và Các Tùy Chọn Sandbox Khác

Điều đầu tiên chúng ta cần là một thể hiện **SandboxOptions** trong đó chúng ta định nghĩa kích thước màn hình ảo và *tỷ lệ pixel thiết bị* (DPR). Hãy nghĩ DPR như một hệ số cho trình duyệt biết bao nhiêu pixel vật lý tương ứng với một pixel CSS. Trên iPhone Retina, DPR thường là **2.0**, vì vậy chúng ta sẽ sử dụng giá trị này.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Tại sao điều này quan trọng:** Nếu không đặt đúng DPR, hình ảnh được render sẽ bị mờ hoặc quá lớn vì rasterizer giả định một ánh xạ pixel 1:1.

## Bước 2: Đặt User Agent Tùy Chỉnh

Các trang web thường cung cấp markup khác nhau dựa trên header **User‑Agent**. Để đảm bảo trang của chúng ta hoạt động như trên một iPhone thực, chúng ta chèn một chuỗi tùy chỉnh mô phỏng Safari trên iOS.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Trường hợp đặc biệt:** Một số trang kiểm tra header `Accept-Language` nữa. Nếu bạn nhận thấy thiếu bản dịch, hãy thêm `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");`.

## Bước 3: Tải Trang Trong Sandbox và Lấy Tiêu Đề

Bây giờ chúng ta khởi động sandbox với các tùy chọn vừa định nghĩa. Đối tượng **Sandbox** cô lập quá trình render, đảm bảo các cài đặt DPR và user‑agent của chúng ta được áp dụng.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

Khi trang đã tải, việc lấy tiêu đề đơn giản chỉ cần gọi `getTitle()`. Điều này đáp ứng yêu cầu **get page title java**.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Kết quả mong đợi trên console**

```
Title: Responsive Demo – Mobile View
```

Nếu tiêu đề trống, hãy kiểm tra lại URL hoặc chắc chắn trang không bị chặn bởi chính sách CORS.

## Bước 4: Chuyển Đổi HTML sang PNG và Lưu HTML dưới Dạng Hình Ảnh

Aspose.HTML cho phép bạn render DOM trực tiếp thành tệp hình ảnh. Vì chúng ta đã đặt DPR là 2.0, PNG kết quả sẽ có mật độ pixel gấp đôi, mang lại ảnh chụp màn hình sắc nét.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

Phương thức `save` tự động phát hiện phần mở rộng tệp và chọn renderer phù hợp. Nếu bạn cần định dạng khác (JPEG, BMP), chỉ cần đổi tên tệp tương ứng.

> **Nếu bạn cần kích thước ảnh cụ thể?**  
> Sử dụng `ImageSaveOptions` để điều khiển chiều rộng, chiều cao và màu nền:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

## Ví Dụ Hoàn Chỉnh Hoạt Động

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy, kết hợp tất cả các bước lại với nhau. Sao chép‑dán vào tệp `SandboxDemo.java`, thêm phụ thuộc Aspose.HTML, và thực thi `java SandboxDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

Chạy chương trình sẽ tạo ra hai tệp PNG:

| Tệp | Mô tả |
|------|-------------|
| `mobile_view.png` | Render mặc định sử dụng DPR đã cấu hình. |
| `mobile_view_custom.png` | Render với chiều rộng/chiều cao cụ thể (hữu ích cho tài sản có kích thước cố định). |

Bạn có thể mở bất kỳ tệp nào trong bất kỳ trình xem ảnh nào để xác nhận đầu ra độ phân giải cao.

## Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

| Câu hỏi | Trả lời |
|----------|--------|
| **Nếu trang chứa JavaScript thay đổi DOM sau khi tải?** | Aspose.HTML thực thi script mặc định. Nếu bạn cần ảnh chụp tĩnh trước khi script chạy, hãy đặt `sandboxOptions.setEnableJavaScript(false)`. |
| **Tôi có thể render một trang cần xác thực không?** | Có. Sử dụng `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` hoặc chèn cookie qua `sandboxOptions.getCookies().add(...)`. |
| **DPR có giới hạn ở 2.0 không?** | Không. Bạn có thể đặt bất kỳ số double dương nào (ví dụ, 3.0 cho thiết bị ultra‑high‑DPI). Chỉ cần nhớ rằng DPR lớn hơn đồng nghĩa với tệp ảnh lớn hơn. |
| **Làm sao để xử lý các trang có tài nguyên lớn (hình ảnh, phông chữ)?** | Tăng giới hạn bộ nhớ của sandbox bằng `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (byte). Điều này ngăn lỗi hết bộ nhớ trên các trang nặng. |
| **Tôi có cần đóng sandbox thủ công không?** | `Sandbox` triển khai `AutoCloseable`. Bao bọc nó trong khối try‑with‑resources để tự động dọn dẹp. |

## Kết Luận

Chúng tôi đã chỉ ra cách **đặt tỷ lệ pixel thiết bị** trong sandbox Java, **đặt user agent tùy chỉnh**, **lấy tiêu đề trang java**, và **chuyển đổi html sang png** (thực chất **lưu html dưới dạng hình ảnh**) bằng Aspose.HTML. Ví dụ hoàn chỉnh minh họa quy trình thực tiễn mà bạn có thể áp dụng cho việc tạo ảnh chụp màn hình tự động, kiểm thử hồi quy trực quan, hoặc bất kỳ trường hợp nào cần biểu diễn trang web một cách pixel‑perfect.

Hãy thoải mái thử nghiệm—thay đổi DPR thành 3.0, đổi user‑agent sang chuỗi Android, hoặc trỏ URL tới tệp HTML cục bộ. Mẫu tương tự cũng hoạt động cho PDF, SVG, hoặc thậm chí render đa trang.

Nếu bạn thấy hướng dẫn này hữu ích, hãy khám phá các chủ đề liên quan như **tạo PDF với Aspose.HTML**, **các giải pháp thay thế headless Chrome**, hoặc **render hàng loạt nhiều URL**. Chúc lập trình vui vẻ, và hy vọng ảnh chụp màn hình của bạn luôn sắc nét!

![đặt tỷ lệ pixel thiết bị trong sandbox Java](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}