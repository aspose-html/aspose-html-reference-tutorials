---
date: 2025-12-05
description: Tìm hiểu cách tạo PDF từ HTML bằng cách thiết lập stylesheet người dùng
  tùy chỉnh trong Aspose.HTML cho Java và dễ dàng chuyển đổi HTML sang PDF với dịch
  vụ User Agent.
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Tạo PDF từ HTML – Đặt bảng kiểu người dùng trong Aspose.HTML cho Java
url: /vi/java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF từ HTML – Đặt User Style Sheet trong Aspose.HTML cho Java

## Giới thiệu
Trong hướng dẫn này, bạn sẽ học cách **tạo PDF từ HTML** bằng Aspose.HTML cho Java đồng thời áp dụng một stylesheet người dùng tùy chỉnh.  
Bạn đã bao giờ muốn tinh chỉnh giao diện của tài liệu HTML bằng phong cách riêng của mình? Hãy tưởng tượng bạn đang tạo một trang web và cần các tiêu đề nổi bật với màu sắc cụ thể hoặc các đoạn văn có giao diện nhất quán trên mọi thiết bị. Đó là lúc *user stylesheet* và **User Agent Service** trở nên quan trọng. Chúng tôi sẽ hướng dẫn từng bước — từ việc viết một tệp HTML đơn giản, cấu hình user agent, cho tới cuối cùng là **chuyển đổi HTML sang PDF** — để bạn có thể thấy kết quả ngay lập tức.

## Câu trả lời nhanh
- **“tạo PDF từ HTML” có nghĩa là gì?** Nó có nghĩa là render một tài liệu HTML (kèm CSS, hình ảnh, phông chữ, v.v.) và lưu kết quả hiển thị dưới dạng tệp PDF.  
- **Thành phần Aspose nào cần thiết?** Thư viện Aspose.HTML cho Java cung cấp engine chuyển đổi và User Agent Service.  
- **Có cần giấy phép để thử nghiệm không?** Bản dùng thử miễn phí đủ cho phát triển; cần giấy phép thương mại cho môi trường production.  
- **Có thể sử dụng tệp CSS bên ngoài không?** Có – bạn có thể liên kết stylesheet bên ngoài giống như trong trình duyệt thông thường.  
- **Quá trình chuyển đổi mất bao lâu?** Đối với tài liệu đơn giản như trong hướng dẫn này, quá trình chuyển đổi hoàn thành trong chưa tới một giây.

## Yêu cầu trước
Trước khi bắt đầu viết code, hãy chắc chắn bạn đã có:

1. **Aspose.HTML cho Java** – tải JAR mới nhất từ [trang phát hành của Aspose](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – đảm bảo lệnh `java -version` trả về phiên bản 8 hoặc cao hơn.  
3. **IDE** – IntelliJ IDEA, Eclipse hoặc NetBeans đều hoạt động tốt.  
4. **Kiến thức cơ bản về HTML/CSS** – hữu ích nhưng không bắt buộc.

## Nhập khẩu các gói
Để bắt đầu, nhập các lớp Java cần thiết. Lớp duy nhất cần import một cách rõ ràng cho ví dụ này là `java.io.IOException`; các lớp Aspose sẽ được tham chiếu bằng tên đầy đủ sau này.

```java
import java.io.IOException;
```

## Bước 1: Tạo tài liệu HTML đơn giản
Đầu tiên, chúng ta sẽ viết một tệp HTML tối thiểu (`document.html`) sẽ làm nguồn cho quá trình chuyển đổi PDF.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Mẹo:** Giữ tệp HTML trong cùng thư mục với mã nguồn Java của bạn để tránh các vấn đề liên quan đến đường dẫn.

## Bước 2: Thiết lập cấu hình Aspose.HTML
Tạo một đối tượng `Configuration`. Đối tượng này hoạt động như một container cho tất cả các service (bao gồm User Agent Service) mà bạn sẽ sử dụng sau này.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Bước 3: Truy cập User Agent Service  
**User Agent Service** cho phép bạn chèn một stylesheet tùy chỉnh, đặt bộ mã ký tự mặc định và kiểm soát các tùy chọn render khác.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Bước 4: Định nghĩa và áp dụng User Stylesheet  
Bây giờ chúng ta cung cấp các quy tắc CSS sẽ định dạng HTML khi được render. Đây là nơi chúng ta **sử dụng user agent service** để đặt stylesheet.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Tại sao điều này quan trọng:** Bằng cách áp dụng stylesheet ở mức user‑agent, bạn đảm bảo các kiểu được tôn trọng ngay cả khi HTML gốc không tham chiếu tới tệp CSS nào.

## Bước 5: Tải tài liệu HTML với cấu hình tùy chỉnh  
Cung cấp cả đường dẫn tệp và thể hiện `Configuration` cho constructor `HTMLDocument`. Điều này sẽ gắn stylesheet người dùng vào tài liệu.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Bước 6: Chuyển đổi HTML sang PDF  
Khi tài liệu đã được định dạng đầy đủ, gọi phương thức tĩnh `convertHTML` để **chuyển đổi HTML sang PDF**. Đối tượng `PdfSaveOptions` cho phép bạn tinh chỉnh đầu ra (ví dụ: kích thước trang, nén).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Kết quả:** `user-agent-stylesheet_out.pdf` sẽ chứa tiêu đề màu nâu và đoạn văn với nền GhostWhite, chính xác như đã định nghĩa trong stylesheet.

## Bước 7: Dọn dẹp tài nguyên  
Luôn luôn giải phóng các đối tượng Aspose để giải bộ nhớ native.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Các vấn đề thường gặp & Giải pháp
| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|----------|
| **Blank PDF output** | Không có stylesheet được áp dụng hoặc tài liệu không được tải với cấu hình. | Kiểm tra rằng `configuration` được truyền vào `HTMLDocument` và `setUserStyleSheet` được gọi trước khi tải. |
| **Unsupported CSS property warning** | Aspose.HTML không hỗ trợ một số tính năng CSS nâng cao. | Chỉ sử dụng các thuộc tính CSS được liệt kê trong tài liệu Aspose.HTML hoặc chuyển sang các kiểu đơn giản hơn. |
| **FileNotFoundException** | Đường dẫn tới `document.html` sai. | Sử dụng đường dẫn tuyệt đối hoặc đặt tệp HTML trong thư mục gốc của dự án. |

## Câu hỏi thường gặp

**Q: Tôi có thể áp dụng các kiểu khác nhau cho các phần tử HTML khác nhau không?**  
A: Chắc chắn! Bạn có thể định nghĩa bao nhiêu quy tắc CSS tùy thích trong user stylesheet.

**Q: Nếu tôi cần thay đổi stylesheet một cách động thì sao?**  
A: Gọi lại `setUserStyleSheet` trước khi tạo một instance `HTMLDocument` mới; các kiểu mới sẽ được áp dụng cho lần chuyển đổi tiếp theo.

**Q: Có thể sử dụng tệp CSS bên ngoài với Aspose.HTML cho Java không?**  
A: Có – bạn có thể liên kết một stylesheet bên ngoài trong HTML hoặc tải nội dung của nó và truyền vào `setUserStyleSheet`.

**Q: Aspose.HTML xử lý các thuộc tính CSS không được hỗ trợ như thế nào?**  
A: Các thuộc tính không được hỗ trợ sẽ bị bỏ qua, cho phép phần còn lại của stylesheet được render mà không gây lỗi.

**Q: Tôi có thể chuyển đổi HTML sang các định dạng khác ngoài PDF không?**  
A: Có, Aspose.HTML hỗ trợ chuyển đổi sang XPS, TIFF, PNG, JPEG và nhiều định dạng khác bằng cách sử dụng lớp `SaveOptions` tương ứng.

## Kết luận
Bạn đã thấy cách **tạo PDF từ HTML** bằng cách thiết lập một user stylesheet tùy chỉnh với Aspose.HTML cho Java. Quy trình này cho phép bạn kiểm soát hoàn toàn giao diện của PDF được tạo, rất phù hợp cho việc tạo báo cáo tự động, hóa đơn, hoặc bất kỳ kịch bản nào yêu cầu phong cách nhất quán. Hãy thử nghiệm với CSS phức tạp hơn, phông chữ bên ngoài, hoặc các định dạng chuyển đổi khác để mở rộng nền tảng này.

---

**Cập nhật lần cuối:** 2025-12-05  
**Kiểm tra với:** Aspose.HTML cho Java 24.11 (phiên bản mới nhất tại thời điểm viết)  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}