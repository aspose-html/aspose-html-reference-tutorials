---
category: general
date: 2026-02-10
description: Đặt tỷ lệ pixel của thiết bị trong Java bằng sandbox Aspose.HTML. Tìm
  hiểu cách đặt chiều rộng và chiều cao màn hình và lấy tiêu đề trang trong Java với
  một ví dụ đầy đủ, có thể chạy được.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: vi
og_description: đặt tỷ lệ pixel của thiết bị trong Java với sandbox Aspose.HTML. Hướng
  dẫn này cho bạn cách đặt chiều rộng và chiều cao màn hình và lấy tiêu đề trang Java
  trong vài bước đơn giản.
og_title: Đặt tỷ lệ pixel của thiết bị trong Java – Hướng dẫn Mobile Sandbox
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Cài đặt tỷ lệ pixel của thiết bị trong Java – Hướng dẫn Mobile Sandbox
url: /vi/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cài đặt tỷ lệ pixel của thiết bị trong Java – Mobile Sandbox Tutorial

Bạn đã bao giờ cần **set device pixel ratio** khi kiểm thử một trang web đáp ứng trong Java chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi trang trông hoàn hảo trên máy tính để bàn nhưng bị lỗi trên các điện thoại high‑DPI. Tin tốt là gì? Với sandbox của Aspose.HTML, bạn có thể mô phỏng một iPhone X (hoặc bất kỳ thiết bị nào) ngay từ mã Java của mình—không cần trình duyệt.

Trong hướng dẫn này, chúng tôi sẽ hướng dẫn **how to set screen width height**, cấu hình **device pixel ratio**, và cuối cùng **get page title java** để xác minh mọi thứ được hiển thị đúng. Khi kết thúc, bạn sẽ có một chương trình tự chứa mà bạn có thể đưa vào bất kỳ dự án nào và bắt đầu kiểm thử bố cục di động ngay lập tức.

## Yêu cầu trước

- Java 8 hoặc mới hơn (mã nguồn biên dịch với JDK 11 cũng được)  
- Thư viện Aspose.HTML cho Java (phiên bản 23.7 hoặc mới hơn) – bạn có thể lấy từ Maven Central  
- Một IDE hoặc một thiết lập dòng lệnh đơn giản `javac`  
- Kết nối Internet cho URL demo (`https://responsive.example.com`)

Không cần framework bổ sung, không Selenium, chỉ Java thuần và Aspose.HTML.

---

## Bước 1: Đặt chiều rộng và chiều cao màn hình và tỷ lệ pixel của thiết bị

Điều đầu tiên chúng ta cần là một đối tượng `SandboxOptions` để chỉ cho sandbox biết chúng ta đang giả vờ là “thiết bị” nào. Ở đây chúng ta sẽ sử dụng kích thước iPhone X (375 × 812 pixel CSS) và một **device pixel ratio** là 3.0, mô phỏng màn hình retina high‑DPI.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Tại sao điều này quan trọng:**  
> Lệnh `setDevicePixelRatio` sẽ mở rộng mọi thứ—từ hình ảnh đến việc hiển thị phông chữ—để trang nghĩ rằng nó đang chạy trên một điện thoại thực. Nếu bỏ qua, bố cục có thể quay lại các truy vấn media CSS kiểu desktop, làm mất mục đích của việc kiểm thử di động.

---

## Bước 2: Tạo thể hiện sandbox

Bây giờ chúng ta chuyển các tùy chọn đó thành một sandbox hoạt động. Hãy nghĩ sandbox như một trình duyệt không giao diện, nhỏ gọn, tuân theo các kích thước và tỷ lệ pixel mà chúng ta vừa định nghĩa.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Mẹo chuyên nghiệp:** Bạn có thể tái sử dụng cùng một đối tượng `Sandbox` cho nhiều lần tải trang; chỉ cần thay đổi URL và sandbox sẽ giữ nguyên các đặc tính thiết bị.

---

## Bước 3: Tải trang bên trong sandbox

Khi sandbox đã sẵn sàng, việc tải một trang đơn giản như tạo một `HTMLDocument` và truyền sandbox làm đối số thứ hai. Điều này buộc tài liệu render bằng thiết bị ảo mà chúng ta đã thiết lập trước đó.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Nếu URL không truy cập được hoặc trang chứa lỗi, Aspose.HTML sẽ ném ra một ngoại lệ. Đối với mã sản xuất, bạn có thể bọc trong `try‑catch` và ghi lại lỗi, nhưng trong hướng dẫn này chúng tôi giữ đơn giản.

---

## Bước 4: Xác minh với get page title java

Kiểm tra nhanh nhất là đọc tiêu đề của tài liệu. Nếu sandbox đã áp dụng đúng **device pixel ratio**, tiêu đề sẽ giống hệt như trên một iPhone X thực.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Kết quả mong đợi (ví dụ):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Nếu bạn thấy tiêu đề được in ra, bạn đã thành công **set device pixel ratio**, **set screen width height**, và **got the page title** bằng Java.

---

## Ví dụ đầy đủ, có thể chạy

Dưới đây là chương trình hoàn chỉnh mà bạn có thể sao chép‑dán vào một tệp có tên `SandboxDemo.java`. Đảm bảo các JAR của Aspose.HTML có trong classpath (`-cp` flag) trước khi biên dịch.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Biên dịch và chạy:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Bạn sẽ thấy tiêu đề được in ra console, xác nhận rằng trang đã render với **device pixel ratio** mong muốn.

---

## Câu hỏi thường gặp & Trường hợp đặc biệt

| Question | Answer |
|----------|--------|
| **Có thể thay đổi pixel ratio tại thời gian chạy không?** | Có—chỉ cần tạo một `SandboxOptions` mới với giá trị `setDevicePixelRatio` khác và khởi tạo một `Sandbox` mới. Việc tái sử dụng cùng một sandbox sau khi thay đổi tùy chọn không được hỗ trợ. |
| **Nếu tôi cần kiểm thử nhiều thiết bị thì sao?** | Lặp qua một danh sách `SandboxOptions` (ví dụ: iPhone 8, Pixel 4) và thực hiện cùng logic tải‑và‑đọc tiêu đề cho mỗi thiết bị. |
| **Điều này có hoạt động với các site HTTPS có chứng chỉ tự ký không?** | Aspose.HTML tuân theo kho lưu trữ SSL mặc định của Java. Thêm chứng chỉ vào keystore của JVM hoặc tắt xác thực chỉ cho mục đích thử nghiệm (không khuyến nghị cho môi trường sản xuất). |
| **Làm sao để chụp ảnh màn hình thay vì chỉ lấy tiêu đề?** | API `HTMLDocument` cung cấp các phương thức `save` có thể xuất trang đã render ra PNG hoặc JPEG. Sử dụng `htmlDoc.save("output.png", SaveFormat.PNG);` sau khi tải. |
| **Sandbox có an toàn với đa luồng không?** | Mỗi thể hiện `Sandbox` là độc lập, nhưng bạn nên tránh chia sẻ cùng một instance giữa nhiều luồng mà không có đồng bộ. |

---

## Tổng quan trực quan

![Diagram showing set device pixel ratio in mobile sandbox](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

*Hình minh họa trên mô tả luồng từ việc cấu hình `SandboxOptions` (bao gồm **set screen width height** và **set device pixel ratio**) đến việc tải URL và trích xuất tiêu đề.*

---

## Kết luận

Bây giờ bạn đã biết **how to set device pixel ratio** trong Java, cách **set screen width height** để mô phỏng di động chính xác, và cách **get page title java** để xác nhận việc render thành công. Quy trình ngắn gọn này loại bỏ nhu cầu sử dụng các trình duyệt nặng trong kiểm thử UI tự động và dễ dàng tích hợp vào các pipeline CI.

Sẵn sàng cho bước tiếp theo? Hãy thử xuất trang đã render thành hình ảnh, hoặc thử nghiệm việc gỡ lỗi CSS media‑query bằng cách chuyển đổi `devicePixelRatio` giữa 1.0 và 3.0. Bạn cũng có thể khám phá tính năng chuyển đổi PDF của Aspose.HTML để tạo phiên bản có thể in của giao diện di động.

Chúc lập trình vui vẻ, và hy vọng các bố cục di động của bạn luôn sắc nét—bất kể mật độ pixel!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}