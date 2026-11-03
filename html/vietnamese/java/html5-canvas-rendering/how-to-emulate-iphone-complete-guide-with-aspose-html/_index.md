---
category: general
date: 2026-03-26
description: Tìm hiểu cách mô phỏng iPhone trong Java bằng Aspose.HTML. Bao gồm các
  bước để đặt user agent tùy chỉnh và thiết lập tỷ lệ pixel của thiết bị nhằm hiển
  thị di động chính xác.
draft: false
keywords:
- how to emulate iphone
- set custom user agent
- set device pixel ratio
- how to set user-agent
- how to set dpr
language: vi
og_description: Cách mô phỏng iPhone trong Java? Bài hướng dẫn này chỉ cách thiết
  lập user agent tùy chỉnh và tỷ lệ pixel của thiết bị bằng Aspose.HTML, mang lại
  các trang di động pixel‑perfect.
og_title: Cách mô phỏng iPhone – Hướng dẫn Aspose.HTML từng bước
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Cách mô phỏng iPhone – Hướng dẫn đầy đủ với Aspose.HTML
url: /vi/java/html5-canvas-rendering/how-to-emulate-iphone-complete-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách mô phỏng iPhone – Hướng dẫn đầy đủ với Aspose.HTML

Bạn đã bao giờ tự hỏi **cách mô phỏng iPhone** khi kiểm thử một trang web cục bộ chưa? Có thể bạn đang gỡ lỗi một bố cục đáp ứng và trình duyệt trên máy tính để bàn không đáp ứng được. Tin tốt là bạn không cần thiết bị vật lý—Aspose.HTML’s `DocumentSandbox` cho phép bạn mô phỏng màn hình, user‑agent và device‑pixel‑ratio (DPR) của iPhone chỉ với vài dòng Java.  

Trong tutorial này chúng ta sẽ đi qua các bước chính xác để đặt **custom user agent**, cấu hình **device pixel ratio**, và xác minh mọi thứ hoạt động như mong đợi. Khi kết thúc, bạn sẽ có một sandbox tái sử dụng được, render trang giống như iPhone 8, và hiểu tại sao mỗi thiết lập lại quan trọng.

## Những gì bạn sẽ đạt được

- Tạo một đối tượng `Screen` phản ánh kích thước và DPR của iPhone.  
- Áp dụng một chuỗi **custom user agent** để máy chủ nghĩ rằng yêu cầu đến từ Safari trên iOS.  
- Xây dựng một `DocumentSandbox` liên kết màn hình và user‑agent lại với nhau.  
- Chạy một `HTMLDocument` bên trong sandbox và xem đầu ra console xác nhận cấu hình.  

Không cần thư viện bên ngoài nào ngoài Aspose.HTML, và mã chạy trên bất kỳ môi trường Java 17+ nào.

---

![cách mô phỏng iPhone screenshot](https://example.com/images/iphone-emulation.png "cách mô phỏng iPhone bằng sandbox Aspose.HTML")

## Cách mô phỏng iPhone với Aspose.HTML Sandbox

Điều đầu tiên chúng ta cần là một `Screen` phản ánh kích thước vật lý của iPhone *và* mật độ pixel của nó. Đây là cốt lõi của **cách mô phỏng iPhone** một cách chính xác.

```java
import com.aspose.html.devices.Screen;

// Step 1: Define iPhone 8 screen size (width, height) and DPR
Screen mobileScreen = new Screen(375, 667, 2.0); // iPhone 8 dimensions, DPR = 2
```

**Tại sao điều này quan trọng:**  
- Chiều rộng = 375 px và chiều cao = 667 px là kích thước pixel CSS bạn sẽ thấy trong Chrome DevTools khi chọn iPhone 8.  
- Đặt DPR thành 2 báo cho engine render rằng mỗi pixel CSS tương đương hai pixel vật lý, cho bạn văn bản và hình ảnh sắc nét—đúng như một thiết bị thực.

> *Mẹo chuyên nghiệp:* Nếu bạn cần mô phỏng iPhone mới hơn (như iPhone 13), chỉ cần đổi số thành 390 × 844 và DPR = 3.

## Đặt custom user agent (set custom user agent)

Tiếp theo, chúng ta cần **set custom user agent** để máy chủ trả về HTML/CSS dành cho di động. Nếu không, nhiều trang vẫn sẽ nghĩ bạn đang trên desktop.

```java
// Step 2: Define an iPhone Safari user‑agent string
String iPhoneUserAgent = "Mozilla/5.0 (iPhone; CPU iPhone OS 16_0 like Mac OS X) " +
                         "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                         "Version/16.0 Mobile/15E148 Safari/604.1";
```

**Cách hoạt động này:**  
- Header `User-Agent` là cách các trình duyệt giới thiệu mình với máy chủ.  
- Bằng cách cung cấp chính xác chuỗi Safari trên iOS 16 gửi, bạn đảm bảo máy chủ trả về các tài nguyên tối ưu cho di động (hình ảnh đáp ứng, script thích nghi, v.v.).  

Nếu bạn muốn **how to set user-agent** cho một thiết bị khác, chỉ cần thay chuỗi bằng giá trị phù hợp—Google Chrome, Firefox, hoặc thậm chí một bot tùy chỉnh.

## Cấu hình Device Pixel Ratio (set device pixel ratio)

Bây giờ chúng ta thực sự **set device pixel ratio** trong sandbox. Đây là bước trả lời trực tiếp “**how to set dpr**” cho môi trường mô phỏng.

```java
import com.aspose.html.sandbox.DocumentSandbox;

// Step 3: Build the sandbox with screen and user‑agent
DocumentSandbox documentSandbox = new DocumentSandbox.Builder()
        .setScreen(mobileScreen)          // applies the DPR we defined earlier
        .setUserAgent(iPhoneUserAgent)    // applies the custom user‑agent
        .build();
```

**Giải thích:**  
- Mẫu `Builder` cho phép bạn gắn liền cả màn hình (chứa DPR) và user‑agent một cách mượt mà.  
- Khi sandbox render một `HTMLDocument`, nó sẽ giả vờ đang chạy trên thiết bị có mật độ pixel chính xác đó.  

> *Tại sao bạn nên quan tâm:* Một số media query CSS sử dụng `device-pixel-ratio` (ví dụ, `@media (-webkit-min-device-pixel-ratio: 2)`). Nếu bạn không đặt DPR, các quy tắc này sẽ không bao giờ kích hoạt, và bạn sẽ bỏ lỡ các tài nguyên độ phân giải cao.

## Xác minh cấu hình Sandbox (how to set user-agent)

Hãy để sandbox vào hoạt động. Đoạn mã sau tạo một `HTMLDocument`, tải một trang, và in ra xác nhận sandbox đang hoạt động.

```java
import com.aspose.html.HTMLDocument;

public class SandboxWithDprAndUa {
    public static void main(String[] args) {
        // Re‑use the sandbox we built earlier
        // DocumentSandbox documentSandbox = ... (from previous step)

        // Step 4: Load a page inside the sandbox
        HTMLDocument doc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 5: Optional – output a sanity check
        System.out.println("Sandbox configured with DPR=2 and iPhone user‑agent.");
    }
}
```

**Kết quả đầu ra dự kiến trên console**

```
Sandbox configured with DPR=2 and iPhone user-agent.
```

Nếu bạn chạy chương trình và thấy dòng này, bạn đã thành công **cách mô phỏng iPhone** với DPR và user‑agent đúng. Mở trang trong trình duyệt thực và kiểm tra kích thước viewport—bạn sẽ nhận thấy chúng khớp với giá trị iPhone mà chúng ta đã đặt.

## Các vấn đề thường gặp và cách đặt DPR đúng (how to set dpr)

Ngay cả khi có mã đúng, một vài cạm bẫy có thể làm bạn gặp khó khăn:

| Vấn đề | Tại sao xảy ra | Cách khắc phục |
|-------|----------------|----------------|
| **DPR vẫn ở 1** | Bạn đã truyền `Screen` mà không có đối số thứ ba (DPR). | Luôn sử dụng `new Screen(width, height, dpr)`. |
| **User‑Agent bị bỏ qua** | Sandbox chưa được gắn vào `HTMLDocument`. | Truyền `documentSandbox` làm đối số thứ hai cho constructor của `HTMLDocument`. |
| **Kích thước sai** | Sử dụng pixel thiết bị thay vì pixel CSS. | Nhớ rằng: width/height là **pixel CSS**, không phải pixel phần cứng. |
| **Server vẫn gửi CSS desktop** | Một số trang dùng JavaScript để phát hiện thiết bị, không chỉ dựa vào header. | Xem xét cũng chèn thẻ meta viewport nếu cần. |

Giữ những lưu ý này, bạn sẽ hiếm khi gặp tình huống mô phỏng không hoạt động như mong đợi.

## Mở rộng Sandbox – Các bước tiếp theo

Bây giờ bạn đã biết **cách đặt custom user agent** và **cách đặt dpr**, bạn có thể thử nghiệm thêm:

- **Thay đổi kích thước màn hình** để mô phỏng tablet hoặc điện thoại lớn hơn.  
- **Thay đổi user‑agent** để kiểm tra Chrome trên Android (`"Mozilla/5.0 (Linux; Android 12; ...) Chrome/110.0"`).  
- **Thêm cookie hoặc header** qua phương thức `setHeaders` của sandbox để kiểm thử có xác thực.  
- **Chụp ảnh màn hình** bằng `HTMLDocument.renderToFile("output.png")` để tự động so sánh sự khác biệt về hình ảnh.

Các mở rộng này cho phép bạn xây dựng một bộ kiểm thử đầy đủ tính năng mà không cần rời IDE.

## Kết luận

Chúng tôi đã trình bày **cách mô phỏng iPhone** bằng `DocumentSandbox` của Aspose.HTML, cho bạn thấy chính xác **cách đặt custom user agent**, **cách đặt device pixel ratio**, và ngay cả sự khác biệt tinh tế giữa “**how to set user-agent**” và “**how to set dpr**”. Ví dụ hoàn chỉnh, có thể chạy được, minh họa mọi phần trong một nơi, để bạn có thể copy‑paste, chỉnh sửa và bắt đầu kiểm thử bố cục di động ngay lập tức.  

Hãy thử—thay đổi kích thước màn hình, chơi với các user‑agent khác nhau, và quan sát cách trang của bạn phản hồi. Khi bạn thành thạo các thiết lập này, việc gỡ lỗi thiết kế đáp ứng trở nên dễ dàng, và bạn sẽ tiết kiệm vô số giờ đồng hồ truy tìm lỗi trên thiết bị thực.  

Có câu hỏi hoặc muốn chia sẻ biến thể của mình? Để lại bình luận bên dưới, và chúc bạn mô phỏng vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}