---
date: 2025-11-29
description: Học cách chuyển đổi HTML sang XPS và điều chỉnh kích thước trang XPS
  bằng Aspose.HTML cho Java. Dễ dàng kiểm soát kích thước đầu ra.
language: vi
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Chuyển đổi HTML sang XPS và Điều chỉnh kích thước trang XPS với Aspose.HTML
  cho Java
url: /java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi HTML sang XPS và Điều chỉnh Kích thước Trang XPS với Aspose.HTML cho Java

Trong hướng dẫn này, bạn sẽ khám phá **cách chuyển đổi HTML sang XPS** và tinh chỉnh kích thước trang kết quả bằng Aspose.HTML cho Java. Dù bạn đang tạo báo cáo có thể in, hoá đơn hay tài liệu lưu trữ, việc kiểm soát kích thước XPS giúp đầu ra trông chính xác như mong muốn. Chúng tôi sẽ hướng dẫn từng bước—từ thiết lập môi trường đến tạo file XPS cuối cùng—để bạn có thể tích hợp khả năng này ngay vào ứng dụng Java của mình.

## Câu trả lời nhanh
- **“Chuyển đổi HTML sang XPS” có nghĩa là gì?** Nó chuyển đổi một tài liệu HTML thành file XPS, giữ nguyên bố cục và kiểu dáng.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho việc phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Phiên bản Java nào được hỗ trợ?** Java 8 hoặc cao hơn (khuyến nghị JDK 11+).  
- **Có thể thay đổi kích thước trang không?** Có – Aspose.HTML cho phép bạn chỉ định kích thước tùy chỉnh trước khi render.  
- **Quá trình chuyển đổi mất bao lâu?** Thông thường dưới một giây cho các trang tiêu chuẩn; tài liệu lớn hơn có thể mất lâu hơn.

## Chuyển đổi HTML sang XPS là gì?
Chuyển đổi HTML sang XPS có nghĩa là lấy một tệp markup hướng web và tạo ra một tài liệu XPS (XML Paper Specification)—một định dạng bố cục cố định, sẵn sàng in, tương tự như PDF. Điều này hữu ích khi bạn cần các tài liệu độ chính xác cao, không phụ thuộc vào thiết bị, để lưu trữ hoặc in từ các ứng dụng Java.

## Tại sao cần điều chỉnh kích thước trang XPS?
Điều chỉnh kích thước trang cho phép bạn kiểm soát kích thước vật lý của tài liệu cuối cùng (ví dụ: A4, Letter, nhãn tùy chỉnh). Nó ngăn ngừa việc phóng to/thu nhỏ không mong muốn, đảm bảo nội dung vừa vặn hoàn hảo và có thể giảm kích thước file bằng cách loại bỏ khoảng trắng thừa.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã chuẩn bị các yêu cầu sau:

1. **Môi trường phát triển Java** – JDK đã được cài đặt trên hệ thống của bạn.  
2. **Thư viện Aspose.HTML cho Java** – Tải và đưa thư viện Aspose.HTML cho Java vào dự án. Bạn có thể tìm thư viện [tại đây](https://releases.aspose.com/html/java/).  
3. **Tệp HTML đầu vào** – Chuẩn bị một tệp HTML mà bạn muốn render và điều chỉnh kích thước trang XPS. Bạn có thể sử dụng tệp HTML của riêng mình cho hướng dẫn này.

## Nhập gói

Đầu tiên, nhập các lớp cần thiết. Các gói này cung cấp quyền truy cập vào xử lý tài liệu, render và các tính năng thiết lập trang.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Bước 1: Đặt tên tệp đầu vào

Đọc tệp HTML nguồn bằng `FileInputStream`. Luồng này sẽ cung cấp HTML thô cho engine Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Bước 2: Tạo tài liệu HTML và đặt kiểu

Tạo một thể hiện `HTMLDocument` đại diện cho nội dung bạn sẽ render. Trong ví dụ này, chúng tôi cũng chèn một khối CSS nhỏ để minh họa kiểu dáng—bạn có thể thay thế bằng markup của riêng mình.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

## Bước 3: Tạo tùy chọn render XPS

Khởi tạo `XpsRenderingOptions` để chứa tất cả các cài đặt ảnh hưởng đến quá trình chuyển đổi từ HTML sang XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Bước 4: Điều chỉnh kích thước trang

Xác định kích thước trang tùy chỉnh (rộng × cao tính bằng điểm) và cho renderer biết liệu nó có tự động mở rộng tới trang rộng nhất hay không. Đặt `adjustToWidestPage` thành `false` sẽ giữ nguyên kích thước bạn chỉ định.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Bước 5: Render đầu ra

Cuối cùng, tạo một `XpsDevice` với các tùy chọn đã cấu hình và render tài liệu HTML. Kết quả là một tệp XPS hoàn chỉnh với kích thước trang tùy chỉnh mà bạn đã đặt.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Các vấn đề thường gặp và giải pháp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|------------|----------|
| **Kết quả XPS trống** | Luồng đầu vào không được đóng hoặc `HTMLDocument` trỏ tới tệp sai. | Đảm bảo `FileInputStream` được bao trong khối try‑with‑resources và đường dẫn tệp chính xác. |
| **Kích thước trang không được áp dụng** | `adjustToWidestPage` để mặc định là `true`. | Đặt `pageSetup.setAdjustToWidestPage(false);` như trong Bước 4. |
| **CSS không được hỗ trợ** | Aspose.HTML chỉ hỗ trợ một phần của CSS. | Giữ các layout, font và màu cơ bản; tránh các selector phức tạp hoặc CSS Grid. |
| **LicenseException** | Chạy mà không có giấy phép hợp lệ trong môi trường sản xuất. | Áp dụng giấy phép tạm thời hoặc mua trước khi render (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Câu hỏi thường gặp

**Hỏi: Aspose.HTML cho Java là gì?**  
Đáp: Aspose.HTML cho Java là một thư viện Java cho phép các nhà phát triển thao tác và chuyển đổi tài liệu HTML sang nhiều định dạng, như XPS, PDF và hình ảnh.

**Hỏi: Tôi có thể tải Aspose.HTML cho Java ở đâu?**  
Đáp: Bạn có thể tải thư viện Aspose.HTML cho Java từ [liên kết này](https://releases.aspose.com/html/java/).

**Hỏi: Có bản dùng thử miễn phí cho Aspose.HTML cho Java không?**  
Đáp: Có, bạn có thể nhận bản dùng thử miễn phí của Aspose.HTML cho Java từ [đây](https://releases.aspose.com/).

**Hỏi: Làm sao để có giấy phép tạm thời cho Aspose.HTML cho Java?**  
Đáp: Để lấy giấy phép tạm thời cho Aspose.HTML cho Java, truy cập [trang này](https://purchase.aspose.com/temporary-license/).

**Hỏi: Tôi có thể nhận hỗ trợ cho Aspose.HTML cho Java không?**  
Đáp: Có, bạn có thể tìm kiếm trợ giúp và hỗ trợ từ cộng đồng Aspose trên [Diễn đàn Aspose](https://forum.aspose.com/).

**Hỏi: Tôi có thể chuyển đổi HTML sang XPS trên máy chủ không có giao diện (headless) không?**  
Đáp: Hoàn toàn có thể. Aspose.HTML hoạt động trong môi trường không có GUI; chỉ cần đảm bảo runtime Java được cấu hình đúng.

**Hỏi: Thư viện có hỗ trợ tùy chỉnh lề trang không?**  
Đáp: Có. Sử dụng `PageSetup.setMarginTop()`, `setMarginBottom()`, v.v., trước khi gán `PageSetup` vào tùy chọn render.

## Kết luận

Chúng ta đã đi qua toàn bộ quy trình **chuyển đổi HTML sang XPS** và điều chỉnh kích thước trang bằng Aspose.HTML cho Java. Khi thực hiện các bước này, bạn có thể tạo ra các tài liệu XPS sẵn sàng in, đáp ứng chính xác yêu cầu bố cục của mình. Hãy thử nghiệm với các kích thước trang khác nhau, kiểu dáng, hoặc thậm chí thêm header và footer để phù hợp với dự án của bạn.

Nếu bạn có bất kỳ câu hỏi nào hoặc cần hỗ trợ thêm, hãy khám phá tài liệu [Aspose.HTML cho Java](https://reference.aspose.com/html/java/) hoặc tham gia thảo luận trên [Diễn đàn Aspose](https://forum.aspose.com/).

---

**Cập nhật lần cuối:** 2025-11-29  
**Được kiểm tra với:** Aspose.HTML cho Java 24.11 (phiên bản mới nhất tại thời điểm viết)  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}