---
date: 2025-12-05
description: Tìm hiểu cách thiết lập lề trang HTML trong Java bằng Aspose.HTML và
  thêm số trang cùng tiêu đề vào tài liệu của bạn.
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Cách đặt lề trang HTML trong Java bằng Aspose.HTML
url: /vi/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thiết lập lề trang HTML trong Java với Aspose.HTML

Trong hướng dẫn này, bạn sẽ khám phá **cách thiết lập lề trang HTML trong Java**‑style bằng cách sử dụng Aspose.HTML cho Java. Chúng tôi sẽ hướng dẫn cách tạo lề trang tùy chỉnh, chèn số trang và thêm tiêu đề tài liệu — tất cả với mã rõ ràng, từng bước mà bạn có thể sao chép vào dự án của mình.

## Câu trả lời nhanh
- **Thư viện nào cần thiết?** Aspose.HTML for Java  
- **Tôi có thể kiểm soát lề trang bằng lập trình không?** Có, thông qua quy tắc CSS `@page` trong bảng kiểu người dùng  
- **Định dạng đầu ra nào hỗ trợ lề?** XPS, PDF và các định dạng raster khác  
- **Tôi có cần giấy phép cho môi trường sản xuất không?** Một giấy phép Aspose.HTML hợp lệ là bắt buộc cho việc sử dụng không dùng thử  
- **Liệu nó có tương thích với Java 11+ không?** Chắc chắn – thư viện hoạt động với các phiên bản Java hiện đại  

## “Cài đặt lề trang HTML trong Java” là gì?
Cài đặt lề trang HTML trong Java có nghĩa là cấu hình engine render (do Aspose.HTML cung cấp) để áp dụng các thuộc tính CSS page‑box trước khi tài liệu được chuyển đổi sang định dạng có thể in như XPS hoặc PDF. Bằng cách định nghĩa một quy tắc `@page` tùy chỉnh, bạn kiểm soát khu vực có thể in, số trang và nội dung header/footer.

## Tại sao nên sử dụng Aspose.HTML để kiểm soát lề?
- **Bố cục chính xác** – CSS `@page` cung cấp cho bạn khả năng kiểm soát lề, header và footer một cách pixel‑perfect.  
- **Độ nhất quán đa định dạng** – Các định nghĩa lề giống nhau hoạt động cho XPS, PDF và các đầu ra hình ảnh.  
- **Không phụ thuộc vào trình duyệt** – Quá trình render diễn ra phía máy chủ, vì vậy bạn không cần trình duyệt không giao diện.  

## Yêu cầu trước

Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị các yêu cầu sau:

1. **Môi trường phát triển Java** – JDK 11 hoặc mới hơn đã được cài đặt.  
2. **Aspose.HTML for Java** – Tải xuống và cài đặt thư viện từ [here](https://releases.aspose.com/html/java/).  

## Nhập các gói

Để bắt đầu, nhập các lớp Aspose.HTML cần thiết:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Cách thiết lập lề trang HTML trong Java – Hướng dẫn từng bước

### Bước 1: Khởi tạo Configuration và Định nghĩa Lề Trang Tùy chỉnh

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

Trong khối này, chúng ta tạo một đối tượng `Configuration`, lấy `IUserAgentService`, và chèn một quy tắc CSS `@page` định nghĩa lề, bộ đếm trang ở góc dưới‑phải, và tiêu đề tài liệu ở giữa trên.

### Bước 2: Tạo tài liệu HTML

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Ở đây chúng ta khởi tạo một `HTMLDocument` với đoạn mã “Hello World” đơn giản. Cấu hình giống như Bước 1 được áp dụng, vì vậy lề tùy chỉnh sẽ được tôn trọng khi tài liệu được render.

### Bước 3: Render ra tệp XPS (hoặc bất kỳ đầu ra nào được hỗ trợ)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Bước này tạo một `XpsDevice` ghi các trang đã render vào `output.xps`. Lề, số trang và tiêu đề bạn đã định nghĩa trước đó sẽ xuất hiện trong tệp cuối cùng.

## Các vấn đề thường gặp & Mẹo

- **Lề không thay đổi** – Đảm bảo quy tắc `@page` không bị ghi đè bởi các stylesheet khác. Lệnh `setUserStyleSheet` buộc nó có độ ưu tiên cao nhất.  
- **Số trang hiển thị “NaN”** – Kiểm tra bạn đang sử dụng Aspose.HTML phiên bản 23.10 trở lên; các phiên bản cũ không có hàm `currentPageNumber()`.  
- **Tệp đầu ra trống** – Xác nhận đường dẫn `Resources.output` được giải quyết đúng và bạn có quyền ghi.  

## Câu hỏi thường gặp

### Hỏi 1: Aspose.HTML for Java là gì?

**A:** Aspose.HTML for Java là một thư viện Java cung cấp các công cụ mạnh mẽ để làm việc với tài liệu HTML trong các ứng dụng Java, bao gồm chuyển đổi, render và thao tác.

### Hỏi 2: Tôi có thể tùy chỉnh lề trang hơn nữa không?

**A:** Có, chỉ cần chỉnh sửa CSS trong `setUserStyleSheet`. Bạn có thể thay đổi bất kỳ giá trị `margin-*` nào hoặc thêm các hộp `@top-*` / `@bottom-*` bổ sung.

### Hỏi 3: Làm thế nào để thêm nội dung vào tài liệu HTML?

**A:** Thay thế chuỗi trong `new HTMLDocument("<div>Hello World!!!</div>", …)` bằng mã HTML của bạn, hoặc tải một tệp bên ngoài bằng constructor `HTMLDocument(String url, …)`.

### Hỏi 4: Aspose.HTML for Java có tương thích với các định dạng tài liệu khác không?

**A:** Chắc chắn. Cùng một `HTMLDocument` có thể được render ra PDF, XPS, hình ảnh, hoặc thậm chí EPUB bằng cách thay đổi thiết bị đầu ra (ví dụ: `PdfDevice`, `PngDevice`).

### Hỏi 5: Tôi có cần giấy phép để sử dụng Aspose.HTML cho Java không?

**A:** Có, giấy phép là bắt buộc cho việc sử dụng trong môi trường sản xuất. Bạn có thể nhận bản dùng thử hoặc mua giấy phép từ [here](https://purchase.aspose.com/buy) hoặc [here](https://releases.aspose.com/).

### Hỏi 6: Làm sao để đặt lề khác nhau cho trang lẻ và trang chẵn?

**A:** Sử dụng các pseudo‑class `@page :left` và `@page :right` trong stylesheet của bạn để định nghĩa lề riêng cho trang trái (chẵn) và trang phải (lẻ).

### Hỏi 7: Tôi có thể nhúng phông chữ tùy chỉnh vào tài liệu đã render không?

**A:** Có. Thêm các quy tắc `@font-face` vào stylesheet người dùng và tham chiếu các phông chữ trong nội dung HTML của bạn.

## Kết luận

Bạn đã nắm vững **cách thiết lập lề trang HTML trong Java** bằng Aspose.HTML, và biết cách thêm số trang và tiêu đề để tài liệu của bạn trông chuyên nghiệp. Hãy thoải mái thử nghiệm các hộp `@page` bổ sung, phông chữ tùy chỉnh, hoặc các định dạng đầu ra khác để phù hợp với nhu cầu dự án.

Nếu bạn gặp bất kỳ khó khăn nào, tài liệu chính thức [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) và [Aspose support forum](https://forum.aspose.com/) là những nơi tuyệt vời để nhận trợ giúp.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 23.12  
**Author:** Aspose  

---