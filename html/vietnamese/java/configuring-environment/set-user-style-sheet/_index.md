---
date: 2026-02-04
description: Tìm hiểu cách tạo PDF từ HTML bằng cách thiết lập stylesheet người dùng
  tùy chỉnh trong Aspose.HTML cho Java và dễ dàng chuyển đổi HTML sang PDF với dịch
  vụ User Agent.
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Tạo PDF từ HTML – Thiết lập bảng kiểu người dùng trong Aspose.HTML cho Java
url: /vi/java/configuring-environment/set-user-style-sheet/
weight: 16
---

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF từ HTML – Đặt User Style Sheet trong Aspose.HTML cho Java

## Giới thiệu

## Câu trả lời nhanh
- **“tạo PDF từ HTML” có nghĩa là gì?** Nó có nghĩa là render một tài liệu HTML (kèm CSS, hình ảnh, phông chữ, v.v.) và lưu kết quả hiển thị dưới dạng file PDF.  
- **Thành phần Aspose nào được yêu cầu?** Thư viện Aspose.HTML cho Java cung cấp động cơ chuyển đổi và User Agent Service.  
- **Tôi có cần giấy phép để thử nghiệm không?** Bản dùng thử miễn phí hoạt động cho phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Tôi có thể sử dụng file CSS bên ngoài không?** Có – bạn có thể liên kết các stylesheet bên ngoài giống như trong trình duyệt thông thường.  
- **Quá trình chuyển đổi mất bao lâu?** Đối với một tài liệu đơn giản như trong hướng dẫn này, quá trình chuyển đổi hoàn thành trong chưa tới một giây.

## Yêu cầu trước
1. **Aspose.HTML for Java** – tải JAR mới nhất từ [Aspose releases page](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – đảm bảo `java -version` báo cáo 8 hoặc cao hơn.  
3. **IDE** – IntelliJ IDEA, Eclipse hoặc NetBeans đều hoạt động tốt.  
4. **Kiến thức cơ bản về HTML/CSS** – hữu ích nhưng không bắt buộc.

## Nhập các gói
Để bắt đầu, nhập các lớp Java cần thiết. Lệnh import duy nhất bạn cần cho ví dụ này là `java.io.IOException`; các lớp Aspose sẽ được tham chiếu bằng tên đầy đủ sau này.

```java
import java.io.IOException;
```

## Bước 1: Tạo một tài liệu HTML đơn giản
Đầu tiên, chúng ta sẽ viết một file HTML tối thiểu (`document.html`) sẽ làm nguồn cho quá trình chuyển đổi PDF của chúng ta.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Mẹo chuyên nghiệp:** Giữ file HTML trong cùng thư mục với mã nguồn Java của bạn để tránh các rắc rối liên quan đến đường dẫn.

## Bước 2: Thiết lập cấu hình Aspose.HTML
Tạo một đối tượng `Configuration`. Đối tượng này hoạt động như một container cho tất cả các dịch vụ (bao gồm User Agent Service) mà bạn sẽ sử dụng sau.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Tại sao nên sử dụng User Agent Service?
**User Agent Service** cung cấp cho bạn quyền kiểm soát mức thấp đối với các tùy chọn render như bộ ký tự mặc định, ngôn ngữ, phông chữ, và—quan trọng nhất cho tutorial này—a custom user stylesheet. Bằng cách áp dụng các style ở mức này, bạn đảm bảo đầu ra hình ảnh nhất quán ngay cả khi HTML gốc không có CSS riêng.

## Bước 3: Truy cập User Agent Service  
**User Agent Service** cho phép bạn chèn một stylesheet tùy chỉnh, đặt bộ ký tự mặc định, và kiểm soát các tùy chọn render khác.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Bước 4: Định nghĩa và áp dụng User Stylesheet  
Bây giờ chúng ta cung cấp các quy tắc CSS sẽ định dạng HTML khi nó được render. Đây là nơi chúng ta **sử dụng user agent service** để đặt stylesheet.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Tại sao điều này quan trọng:** Bằng cách áp dụng một stylesheet ở mức user‑agent, bạn đảm bảo các style được tôn trọng ngay cả khi HTML gốc không tham chiếu tới file CSS.

## Bước 5: Tải tài liệu HTML với cấu hình tùy chỉnh  
Truyền cả đường dẫn file và thể hiện `Configuration` vào constructor của `HTMLDocument`. Điều này gắn stylesheet người dùng vào tài liệu.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Bước 6: Chuyển đổi HTML sang PDF  
Với tài liệu đã được định dạng đầy đủ, gọi phương thức tĩnh `convertHTML` để **chuyển đổi HTML sang PDF**. Đối tượng `PdfSaveOptions` cho phép bạn tinh chỉnh đầu ra (ví dụ: kích thước trang, nén).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Kết quả:** `user-agent-stylesheet_out.pdf` sẽ chứa tiêu đề màu nâu và đoạn văn với nền GhostWhite, chính xác như đã định nghĩa trong stylesheet.

## Bước 7: Dọn dẹp tài nguyên  
Luôn giải phóng các đối tượng Aspose để giải phóng bộ nhớ gốc.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Các vấn đề thường gặp & Giải pháp
| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| **PDF trống** | Không có stylesheet được áp dụng hoặc tài liệu không được tải với cấu hình. | Xác minh rằng `configuration` được truyền vào `HTMLDocument` và `setUserStyleSheet` được gọi trước khi tải. |
| **Cảnh báo thuộc tính CSS không được hỗ trợ** | Aspose.HTML không hỗ trợ một số tính năng CSS nâng cao. | Chỉ sử dụng các thuộc tính CSS được liệt kê trong tài liệu Aspose.HTML hoặc chuyển sang các style đơn giản hơn. |
| **FileNotFoundException** | Đường dẫn tới `document.html` sai. | Sử dụng đường dẫn tuyệt đối hoặc đặt file HTML trong thư mục gốc của dự án. |

## Câu hỏi thường gặp

**Q: Tôi có thể áp dụng các style khác nhau cho các phần tử HTML khác nhau không?**  
A: Chắc chắn! Bạn có thể định nghĩa bao nhiêu quy tắc CSS tùy thích trong user stylesheet.

**Q: Nếu tôi cần thay đổi stylesheet một cách động thì sao?**  
A: Gọi lại `setUserStyleSheet` trước khi tạo một thể hiện `HTMLDocument` mới; các style mới sẽ được áp dụng trong lần chuyển đổi tiếp theo.

**Q: Có thể sử dụng file CSS bên ngoài với Aspose.HTML cho Java không?**  
A: Có – bạn có thể liên kết một stylesheet bên ngoài trong HTML hoặc tải nội dung của nó và truyền vào `setUserStyleSheet`.

**Q: Aspose.HTML xử lý các thuộc tính CSS không được hỗ trợ như thế nào?**  
A: Các thuộc tính không được hỗ trợ sẽ bị bỏ qua, cho phép phần còn lại của stylesheet được render mà không có lỗi.

**Q: Tôi có thể chuyển đổi HTML sang các định dạng khác ngoài PDF không?**  
A: Có, Aspose.HTML hỗ trợ chuyển đổi sang XPS, TIFF, PNG, JPEG và nhiều định dạng khác bằng cách sử dụng lớp `SaveOptions` phù hợp.

## Kết luận
Bây giờ bạn đã thấy cách **tạo PDF từ HTML** bằng cách đặt một user stylesheet tùy chỉnh với Aspose.HTML cho Java. Quy trình này cho phép bạn kiểm soát hoàn toàn giao diện hình ảnh của PDF được tạo ra, rất phù hợp cho việc tạo báo cáo tự động, tạo hoá đơn, hoặc bất kỳ trường hợp nào mà việc giữ phong cách nhất quán là quan trọng. Bạn có thể thoải mái thử nghiệm với CSS phức tạp hơn, phông chữ bên ngoài, hoặc các định dạng chuyển đổi bổ sung để mở rộng nền tảng này.

---

**Cập nhật lần cuối:** 2026-02-04  
**Đã kiểm tra với:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}