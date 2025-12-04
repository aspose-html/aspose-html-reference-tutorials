---
date: 2025-12-04
description: Tìm hiểu cách đặt charset trong Aspose.HTML cho Java, chuyển đổi HTML
  sang PDF và đảm bảo mã hóa văn bản cũng như hiển thị đúng.
language: vi
linktitle: Set Character Set in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Cách thiết lập Charset trong Aspose.HTML cho Java
url: /java/configuring-environment/set-character-set/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Đặt Charset trong Aspose.HTML cho Java

## Giới thiệu
Nếu bạn đang làm việc với tài liệu HTML trong Java, **biết cách đặt charset** một cách chính xác là rất quan trọng để mã hoá và hiển thị văn bản đúng. Trong hướng dẫn từng bước này, chúng tôi sẽ hướng dẫn cấu hình bộ ký tự với Aspose.HTML cho Java, sau đó cho bạn thấy cách **chuyển đổi HTML sang PDF** để kết quả đầu ra trông đúng như mong muốn.

## Câu trả lời nhanh
- **“charset” có nghĩa là gì?** Nó xác định bộ mã ký tự (ví dụ: ISO‑8859‑1, UTF‑8) được dùng để diễn giải văn bản trong tài liệu.  
- **Tại sao phải đặt charset trong Aspose.HTML?** Để đảm bảo các ký tự đặc biệt hiển thị đúng khi chuyển đổi HTML sang PDF hoặc các định dạng khác.  
- **Charset nào được sử dụng trong ví dụ này?** `ISO‑8859‑1` (được đặt qua `setCharSet`).  
- **Tôi có thể chuyển đổi HTML sang PDF sau khi đặt charset không?** Có – hướng dẫn kết thúc bằng việc chuyển đổi PDF bằng `Converter.convertHTML`.  
- **Tôi có cần giấy phép không?** Có bản dùng thử miễn phí; giấy phép thương mại cần thiết cho môi trường sản xuất.

## Charset là gì và Tại sao nó quan trọng?
Charset (bộ ký tự) ánh xạ các dãy byte thành các ký tự có thể đọc được. Sử dụng charset sai có thể làm hỏng văn bản, đặc biệt đối với các ngôn ngữ có dấu hoặc các script không phải Latin. Đặt charset đúng đảm bảo HTML được phân tích chính xác như tác giả mong muốn, điều này rất quan trọng khi bạn **tạo PDF từ HTML** sau này.

## Yêu cầu trước
Trước khi chúng ta bắt đầu với mã, hãy chắc chắn rằng bạn có những thứ sau:

1. **Java Development Kit (JDK)** – bất kỳ JDK nào mới (8+). Tải về từ [trang web Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML cho Java** – lấy thư viện mới nhất từ [trang phát hành Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse, hoặc bất kỳ IDE nào hỗ trợ Java mà bạn thích.

## Nhập các Gói
Chúng ta chỉ cần một import duy nhất cho ví dụ này, nhưng các lớp Aspose.HTML sẽ được tham chiếu trực tiếp sau.

```java
import java.io.IOException;
```

Các import này bao gồm tất cả các lớp cần thiết để thiết lập charset, thao tác tài liệu HTML và chuyển đổi nó sang PDF.

## Bước 1: Tạo mã HTML
Đầu tiên, tạo một tệp HTML đơn giản mà chúng ta sẽ xử lý sau.

```java
String code = "<h1>Character Set</h1>\r\n" +
    "<p>The <b>CharSet</b> property sets the primary character-set for a document.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

- **Nội dung HTML** – Biến `code` chứa một đoạn HTML tối thiểu với tiêu đề và một đoạn văn.  
- **FileWriter** – Ghi chuỗi HTML vào `document.html`, trở thành nguồn cho quá trình chuyển đổi của chúng ta.

## Bước 2: Cấu hình Character Set
Bây giờ chúng ta tạo một đối tượng `Configuration` sẽ chứa các cài đặt tùy chỉnh của chúng ta.

```java
// Create an instance of Configuration
Configuration configuration = new Configuration();
```

Lớp `Configuration` là điểm khởi đầu để tùy chỉnh cách Aspose.HTML phân tích và render tài liệu.

## Bước 3: Truy cập và sửa đổi dịch vụ User Agent
Charset được định nghĩa thông qua `IUserAgentService`. Ở đây chúng tôi cũng trình bày lời gọi **set iso-8859-1 encoding**.

```java
try {
    // Get the IUserAgentService
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set ISO-8859-1 encoding to parse the document
    userAgent.setCharSet("ISO-8859-1");
```

- **IUserAgentService** – Quản lý các cài đặt cấp độ user‑agent, bao gồm charset.  
- **setCharSet** – Áp dụng charset `ISO‑8859‑1`, đảm bảo HTML được diễn giải đúng.

## Bước 4: Khởi tạo tài liệu HTML
Sau khi charset được cấu hình, tải tệp HTML bằng cùng một `Configuration`.

```java
    // Initialize an HTML document with the specified configuration
    HTMLDocument document = new HTMLDocument("document.html", configuration);
```

`HTMLDocument` hiện đại diện cho tệp nguồn, được phân tích với charset `ISO‑8859‑1`.

## Bước 5: Chuyển đổi HTML sang PDF
Cuối cùng, chuyển đổi tài liệu sang PDF. Điều này minh họa **aspose html convert pdf** đang hoạt động.

```java
    try {
        // Convert HTML to PDF
        Converter.convertHTML(
                document,
                new PdfSaveOptions(),
                "user-agent-charset_out.pdf"
        );
    } finally {
        if (document != null) {
            document.dispose();
        }
    }
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- **Converter.convertHTML** – Thực hiện chuyển đổi thực tế sang PDF.  
- **PdfSaveOptions** – Cho phép bạn điều chỉnh các cài đặt đặc thù của PDF nếu cần.  
- **Dọn dẹp tài nguyên** – Các lời gọi `dispose()` giải phóng tài nguyên gốc, ngăn ngừa rò rỉ bộ nhớ.

## Các vấn đề thường gặp và giải pháp
| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|----------|
| Ký tự bị rối trong PDF | Charset sai được đặt (ví dụ, mặc định UTF‑8) | Sử dụng `userAgent.setCharSet("ISO-8859-1")` hoặc charset phù hợp cho nguồn của bạn. |
| `NullPointerException` trên `document` | `configuration` bị giải phóng trước khi sử dụng tài liệu | Đảm bảo `configuration.dispose()` được gọi **sau** khi bạn hoàn thành việc sử dụng `HTMLDocument`. |
| Thiếu phông chữ | Charset mục tiêu yêu cầu phông chữ chưa được cài đặt | Cài đặt phông chữ cần thiết hoặc nhúng nó qua `PdfSaveOptions` (ví dụ, `setEmbedStandardFonts(true)`). |

## Câu hỏi thường gặp

**H: Charset là gì, và tại sao nó quan trọng?**  
Đ: Charset ánh xạ giá trị byte thành ký tự. Sử dụng charset đúng ngăn ngừa việc hỏng văn bản, đặc biệt với các ngôn ngữ không phải ASCII.

**H: Tôi có thể dùng charset khác ngoài ISO‑8859‑1 không?**  
Đ: Chắc chắn. Aspose.HTML hỗ trợ nhiều bộ mã (UTF‑8, Windows‑1252, v.v.). Chỉ cần thay `"ISO-8859-1"` bằng giá trị mong muốn trong `setCharSet`.

**H: Có thể chuyển đổi sang định dạng khác ngoài PDF không?**  
Đ: Có. Aspose.HTML có thể chuyển đổi HTML sang XPS, DOCX, PNG, JPEG và nhiều định dạng khác bằng cách thay `PdfSaveOptions` bằng lớp tùy chọn lưu phù hợp.

**H: Tôi có cần tự tay dọn dẹp tài nguyên không?**  
Đ: Mặc dù bộ thu gom rác của Java giúp, bạn nên gọi `dispose()` trên `Configuration` và `HTMLDocument` để giải phóng tài nguyên gốc kịp thời.

**H: Tôi có thể tải bản dùng thử miễn phí của Aspose.HTML cho Java ở đâu?**  
Đ: Tải bản dùng thử từ [trang phát hành Aspose](https://releases.aspose.com/).

## Kết luận
Bạn bây giờ đã biết **cách đặt charset** trong Aspose.HTML cho Java và cách **chuyển đổi HTML sang PDF** với mã hoá đúng. Xử lý charset đúng là rất quan trọng cho việc quốc tế hoá và đảm bảo PDF của bạn phản ánh chính xác nội dung HTML gốc. Bạn có thể tự do thử nghiệm các charset khác hoặc định dạng đầu ra để phù hợp với nhu cầu dự án của mình.

---

**Last Updated:** 2025-12-04  
**Tested With:** Aspose.HTML cho Java 24.12 (mới nhất tại thời điểm viết)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}