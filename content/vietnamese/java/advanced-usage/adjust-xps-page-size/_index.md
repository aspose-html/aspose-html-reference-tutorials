---
title: Điều chỉnh kích thước trang XPS bằng Aspose.HTML cho Java
linktitle: Điều chỉnh kích thước trang XPS
second_title: Xử lý HTML Java với Aspose.HTML
description: Tìm hiểu cách điều chỉnh kích thước trang XPS bằng Aspose.HTML cho Java. Kiểm soát kích thước đầu ra của tài liệu XPS của bạn một cách dễ dàng.
type: docs
weight: 16
url: /vi/java/advanced-usage/adjust-xps-page-size/
---

Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình điều chỉnh kích thước trang XPS bằng Aspose.HTML cho Java. Thư viện mạnh mẽ này cho phép bạn thao tác các tài liệu HTML và hiển thị chúng thành nhiều định dạng khác nhau, bao gồm cả XPS. Điều chỉnh kích thước trang là điều cần thiết khi bạn cần kiểm soát kích thước đầu ra của tài liệu XPS của mình.

## Điều kiện tiên quyết

Trước khi chúng ta bắt đầu, hãy đảm bảo bạn có sẵn các điều kiện tiên quyết sau:

1. Môi trường phát triển Java: Đảm bảo rằng bạn đã cài đặt Bộ công cụ phát triển Java (JDK) trên hệ thống của mình.

2.  Thư viện Aspose.HTML cho Java: Bạn cần tải xuống và đưa thư viện Aspose.HTML cho Java vào dự án Java của bạn. Bạn có thể tìm thấy thư viện[đây](https://releases.aspose.com/html/java/).

3. Tệp HTML đầu vào: Chuẩn bị tệp HTML mà bạn muốn hiển thị và điều chỉnh kích thước trang XPS. Bạn có thể sử dụng tệp HTML của riêng mình cho hướng dẫn này.

## Gói nhập khẩu

Trước tiên, bạn cần nhập các gói cần thiết để hoạt động với Aspose.HTML cho Java. Bao gồm các gói này vào đầu lớp Java của bạn:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Bước 1: Đặt tên tệp đầu vào

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 Trong bước này, chúng tôi đọc tệp đầu vào HTML của bạn bằng cách sử dụng`FileInputStream`.

## Bước 2: Tạo tài liệu HTML và đặt kiểu

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Bước này liên quan đến việc tạo một`HTMLDocument` và thêm phong cách cho nó.

## Bước 3: Tạo tùy chọn kết xuất XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Ở đây, chúng tôi tạo các tùy chọn kết xuất XPS để định cấu hình quá trình kết xuất.

## Bước 4: Điều chỉnh kích thước trang

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Bước này bao gồm việc thiết lập kích thước trang và chỉ định xem có điều chỉnh nó cho phù hợp với trang rộng nhất hay không.

## Bước 5: Kết xuất đầu ra

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

Ở bước cuối cùng, chúng tôi hiển thị đầu ra XPS bằng các tùy chọn đã định cấu hình.

## Phần kết luận

Trong hướng dẫn này, chúng tôi đã chỉ cho bạn cách điều chỉnh kích thước trang XPS bằng Aspose.HTML cho Java. Bạn có thể kiểm soát kích thước đầu ra của tài liệu XPS, đảm bảo chúng đáp ứng các yêu cầu cụ thể của bạn. Với mã và các bước được cung cấp, bạn có thể dễ dàng triển khai tính năng này trong các ứng dụng Java của mình.

 Nếu bạn có thắc mắc hoặc cần hỗ trợ thêm, vui lòng truy cập[Aspose.HTML cho tài liệu Java](https://reference.aspose.com/html/java/) hoặc yêu cầu trợ giúp về[Diễn đàn Aspose](https://forum.aspose.com/).

## Câu hỏi thường gặp

### Câu hỏi 1: Aspose.HTML dành cho Java là gì?

Câu trả lời 1: Aspose.HTML cho Java là thư viện Java cho phép các nhà phát triển thao tác và chuyển đổi tài liệu HTML sang nhiều định dạng khác nhau, chẳng hạn như XPS, PDF và hình ảnh.

### Câu hỏi 2: Tôi có thể tải xuống Aspose.HTML cho Java ở đâu?

 Câu trả lời 2: Bạn có thể tải xuống thư viện Aspose.HTML dành cho Java từ[liên kết này](https://releases.aspose.com/html/java/).

### Câu hỏi 3: Có bản dùng thử miễn phí cho Aspose.HTML cho Java không?

 Câu trả lời 3: Có, bạn có thể dùng thử miễn phí Aspose.HTML cho Java từ[đây](https://releases.aspose.com/).

### Câu hỏi 4: Làm cách nào tôi có thể nhận được giấy phép tạm thời cho Aspose.HTML cho Java?

 Câu trả lời 4: Để nhận giấy phép tạm thời cho Aspose.HTML dành cho Java, hãy truy cập[trang này](https://purchase.aspose.com/temporary-license/).

### Câu hỏi 5: Tôi có thể nhận hỗ trợ cho Aspose.HTML cho Java không?

 Câu trả lời 5: Có, bạn có thể tìm kiếm sự trợ giúp và hỗ trợ từ cộng đồng Aspose trên[Diễn đàn Aspose](https://forum.aspose.com/).