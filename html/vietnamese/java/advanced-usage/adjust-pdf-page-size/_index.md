---
title: Điều chỉnh kích thước trang PDF bằng Aspose.HTML cho Java
linktitle: Điều chỉnh kích thước trang PDF
second_title: Xử lý HTML Java với Aspose.HTML
description: Tìm hiểu cách điều chỉnh kích thước trang PDF bằng Aspose.HTML cho Java. Tạo PDF chất lượng cao từ HTML một cách dễ dàng. Kiểm soát kích thước trang hiệu quả.
type: docs
weight: 15
url: /vi/java/advanced-usage/adjust-pdf-page-size/
---

Trong thời đại kỹ thuật số ngày nay, nhu cầu tạo PDF chất lượng cao từ nội dung HTML đang gia tăng. Aspose.HTML for Java là một thư viện Java mạnh mẽ cho phép bạn chuyển đổi tài liệu HTML sang định dạng PDF một cách dễ dàng. Trong hướng dẫn này, chúng tôi sẽ tập trung vào việc điều chỉnh kích thước trang khi chuyển đổi HTML sang PDF bằng Aspose.HTML for Java.

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn đã đáp ứng đủ các điều kiện tiên quyết sau:

- Môi trường phát triển Java: Đảm bảo rằng bạn đã cài đặt Java Development Kit (JDK) trên hệ thống của mình.
-  Aspose.HTML cho Java: Bạn cần tải xuống và cài đặt Aspose.HTML cho Java từ trang web[đây](https://releases.aspose.com/html/java/).
- Tài liệu HTML: Bạn phải có một tài liệu HTML sẵn sàng để chuyển đổi. Nếu không, hãy tạo một tài liệu hoặc sử dụng tệp HTML hiện có.

## Nhập gói

Để bắt đầu, bạn cần nhập các gói cần thiết để làm việc với Aspose.HTML cho Java. Đoạn mã sau đây minh họa cách thực hiện việc này:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Bây giờ bạn đã có đủ các điều kiện tiên quyết và đã nhập các gói cần thiết, chúng ta hãy chia nhỏ quá trình điều chỉnh kích thước trang PDF thành nhiều bước:

## Bước 1: Đọc nội dung HTML

Trước tiên, bạn cần đọc nội dung HTML mà bạn muốn chuyển đổi sang PDF. Trong ví dụ này, chúng ta sẽ đọc HTML từ tệp có tên "FirstFile.html".

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Bước 2: Viết nội dung HTML

Tiếp theo, bạn sẽ ghi nội dung HTML vào tệp có tên "FirstFileOut.html".

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Thêm kiểu HTML tùy chỉnh hoặc nội dung ở đây
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Bước 3: Chuyển HTML thành PDF

Bây giờ, bạn sẽ hiển thị nội dung HTML thành tệp PDF. Chúng tôi sẽ đề cập đến hai trường hợp: một là kích thước trang không được điều chỉnh theo chiều rộng nội dung và một là kích thước được điều chỉnh.

### Kích thước trang không được điều chỉnh

Trong trường hợp này, kích thước trang được đặt ở chiều rộng và chiều cao cố định, có thể cắt bớt nội dung nếu vượt quá các kích thước này.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Tạo một phiên bản HTMLDocument từ tệp HTML
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Thiết lập tùy chọn kết xuất PDF
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Hiển thị đầu ra
pdf_renderer.render(device, html_document);
```

### Kích thước trang được điều chỉnh theo chiều rộng nội dung

Trong trường hợp này, kích thước trang được điều chỉnh theo chiều rộng của nội dung.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Hiển thị đầu ra
pdf_renderer.render(device, html_document);
```

## Phần kết luận

Trong hướng dẫn này, chúng tôi đã khám phá cách điều chỉnh kích thước trang PDF khi chuyển đổi HTML sang PDF bằng Aspose.HTML cho Java. Bạn đã tìm hiểu các điều kiện tiên quyết, nhập các gói cần thiết và làm theo hướng dẫn từng bước để thực hiện nhiệm vụ này. Với Aspose.HTML cho Java, bạn có thể dễ dàng kiểm soát kích thước trang của các tệp PDF đã tạo, đảm bảo rằng nội dung của bạn được hiển thị như mong muốn.

 Hãy thoải mái thử nghiệm với các kích thước trang và cài đặt khác nhau để đáp ứng các yêu cầu cụ thể của bạn. Nếu bạn gặp bất kỳ vấn đề nào hoặc có thêm câu hỏi, đừng ngần ngại tìm kiếm sự trợ giúp từ[Tài liệu Aspose.HTML cho Java](https://reference.aspose.com/html/java/) hoặc[Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/).

## Câu hỏi thường gặp

### Câu hỏi 1: Aspose.HTML dành cho Java là gì?

A1: Aspose.HTML for Java là một thư viện Java cho phép bạn làm việc với các tài liệu HTML, chỉnh sửa, chuyển đổi và hiển thị chúng sang nhiều định dạng khác nhau, bao gồm cả PDF.

### Câu hỏi 2: Làm thế nào để điều chỉnh kích thước trang PDF khi chuyển đổi HTML sang PDF bằng Aspose.HTML cho Java?

 A2: Bạn có thể điều chỉnh kích thước trang PDF bằng cách sử dụng`PageSetup` lớp và thiết lập`AdjustToWidestPage` tài sản để`true` hoặc `false, tùy thuộc vào yêu cầu của bạn.

### Câu hỏi 3: Tôi có thể tùy chỉnh kiểu dáng của nội dung HTML trước khi chuyển đổi nó sang PDF không?

A3: Có, bạn có thể tùy chỉnh kiểu dáng bằng cách thêm các thành phần CSS và HTML vào nội dung HTML trước khi chuyển đổi sang PDF, như được trình bày trong hướng dẫn.

### Câu hỏi 4: Tôi có thể tìm tài liệu về Aspose.HTML cho Java ở đâu?

 A4: Bạn có thể tham khảo tài liệu[đây](https://reference.aspose.com/html/java/) để biết thông tin đầy đủ và ví dụ.

### Câu hỏi 5: Có bản dùng thử miễn phí Aspose.HTML cho Java không?

 A5: Có, bạn có thể truy cập bản dùng thử miễn phí Aspose.HTML cho Java từ[liên kết này](https://releases.aspose.com/).