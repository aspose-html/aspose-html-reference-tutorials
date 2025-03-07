---
title: Áp dụng CSS bên ngoài vào tài liệu HTML trong Aspose.HTML cho Java
linktitle: Áp dụng CSS bên ngoài vào tài liệu HTML trong Aspose.HTML cho Java
second_title: Xử lý HTML Java với Aspose.HTML
description: Khám phá cách áp dụng CSS bên ngoài vào tài liệu HTML bằng Aspose.HTML cho Java! Làm theo hướng dẫn từng bước này để biết hướng dẫn đầy đủ.
weight: 12
url: /vi/java/editing-html-documents/apply-external-css-html-documents/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Áp dụng CSS bên ngoài vào tài liệu HTML trong Aspose.HTML cho Java

## Giới thiệu
Khi làm việc với các tài liệu HTML, việc áp dụng các kiểu có thể tạo ra sự khác biệt lớn trong cách trình bày và trải nghiệm của người dùng. Nếu bạn đang tìm hiểu về Java và muốn tìm hiểu cách áp dụng các kiểu CSS bên ngoài vào các tài liệu HTML của mình bằng thư viện Aspose.HTML, bạn đã đến đúng nơi rồi! Hướng dẫn này nhằm mục đích làm sáng tỏ quy trình từng bước, giúp những người mới làm quen với Java hoặc CSS cũng có thể dễ dàng thực hiện.
## Điều kiện tiên quyết
Trước khi tìm hiểu về mã, bạn cần chuẩn bị một số thứ sau:
### 1. Bộ phát triển Java (JDK)
 Đảm bảo rằng bạn đã cài đặt JDK trên máy của mình. Bạn có thể tải xuống phiên bản mới nhất từ[Trang web Java của Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML cho Java
Bạn sẽ cần phải thiết lập Aspose.HTML cho Java. Nếu bạn chưa thực hiện việc này, hãy chuyển đến[Trang tải xuống Aspose](https://releases.aspose.com/html/java/) và lấy thư viện.
### 3. Một IDE hoặc Trình soạn thảo văn bản
Chọn một Môi trường phát triển tích hợp (IDE) như IntelliJ IDEA, Eclipse hoặc thậm chí là một trình soạn thảo văn bản đơn giản để viết mã Java.
### 4. Kiến thức cơ bản về Java
Sự quen thuộc với lập trình Java và kiến thức cơ bản về CSS chắc chắn sẽ giúp bạn theo dõi thoải mái hơn.
## Nhập gói
Sau khi bạn đã thiết lập mọi thứ, bước tiếp theo là nhập các gói cần thiết vào dự án Java của bạn. Sau đây là những gì bạn cần:
```java
import com.aspose.html.HTMLDocument;
```
Những lệnh nhập này sẽ cho phép bạn thao tác với các tài liệu HTML và chuyển chúng thành nhiều định dạng khác nhau, chẳng hạn như PDF.

Chúng tôi sẽ chia nhỏ hướng dẫn của mình thành các bước dễ quản lý. Mỗi bước sẽ hướng dẫn bạn quy trình áp dụng các kiểu CSS bên ngoài vào tài liệu HTML bằng Aspose.HTML cho Java.
## Bước 1: Tạo một tài liệu HTML
Trước tiên, chúng ta cần tạo tài liệu HTML. Chúng ta sẽ bắt đầu bằng cách xác định nội dung bằng cấu trúc HTML đơn giản.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Ở đây, chúng tôi đã định nghĩa một cấu trúc HTML cơ bản, bao gồm`<div>` với hai đoạn văn.`HTMLDocument` lớp được sử dụng để tạo ra một tài liệu biểu diễn nội dung HTML của chúng ta.
## Bước 2: Tạo phần tử kiểu
 Tiếp theo, chúng ta sẽ tạo ra một`style` phần tử để lưu giữ các quy tắc CSS của chúng ta.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 Sử dụng`createElement` phương pháp của`HTMLDocument` , chúng tôi tạo ra một cái mới`<style>` phần tử và thiết lập nội dung của nó để bao gồm các định nghĩa CSS của chúng tôi cho hai lớp:`frame1` Và`frame2`. Các lớp này xác định lề, khoảng đệm, kích thước, màu nền, phông chữ và màu chữ.
## Bước 3: Thêm Kiểu vào Tiêu đề Tài liệu
Bây giờ chúng ta đã có CSS, chúng ta cần thêm phần tử style vào phần đầu của tài liệu.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 Chúng tôi lấy lại phần đầu của tài liệu và thêm vào phần mới tạo của chúng tôi`style` phần tử. Hành động này tích hợp hiệu quả CSS của chúng ta vào tài liệu HTML, cho phép nó định dạng nội dung HTML của chúng ta.
## Bước 4: Áp dụng các lớp cho các phần tử HTML
Tiếp theo, chúng ta sẽ áp dụng các lớp CSS đã định nghĩa trước đó vào các phần tử đoạn văn của mình.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Ở đây, chúng ta truy cập các phần tử đoạn văn đầu tiên và cuối cùng trong tài liệu và gán cho chúng các lớp CSS mà chúng ta đã tạo. Việc gán này đảm bảo rằng chúng tuân thủ các kiểu được xác định trong CSS của chúng ta.
## Bước 5: Thiết lập các thuộc tính kiểu bổ sung
Để cải thiện giao diện hơn nữa, chúng ta sẽ thiết lập các thuộc tính kiểu bổ sung cho các đoạn văn.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

Trong bước này, chúng tôi tinh chỉnh các kiểu của mình. Kích thước phông chữ của đoạn văn đầu tiên được tăng lên và căn giữa, trong khi màu sắc, kích thước phông chữ và họ phông chữ của đoạn văn cuối cùng được xác định. Sự tinh chỉnh này rất quan trọng đối với khả năng đọc và tính thẩm mỹ.
## Bước 6: Lưu tài liệu HTML
Sau khi áp dụng các kiểu, đã đến lúc lưu tài liệu HTML.
```java
document.save("edit-internal-css.html");
```

 Ở đây, chúng tôi sử dụng`save` phương pháp của`HTMLDocument` lớp để ghi nội dung HTML đã sửa đổi vào một tệp, do đó giữ nguyên kiểu dáng và những thay đổi của chúng ta.
## Bước 7: Kết xuất tài liệu thành PDF
Cuối cùng, hãy chuyển tài liệu sang định dạng PDF để xuất ra.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 Sử dụng`PdfDevice` lớp, chúng tôi thiết lập việc hiển thị tài liệu HTML của mình thành PDF. Bước này rất quan trọng khi bạn muốn chia sẻ tài liệu được định dạng theo định dạng có thể truy cập chung.
## Phần kết luận
Và bạn đã có nó rồi—áp dụng CSS bên ngoài vào tài liệu HTML bằng Aspose.HTML cho Java vừa đơn giản vừa bổ ích! Chỉ với một vài dòng mã, bạn có thể biến văn bản thuần túy thành tài liệu hấp dẫn về mặt thị giác và có phong cách chuyên nghiệp. Vì vậy, cho dù bạn đang thiết kế để sử dụng cá nhân, tạo báo cáo hay phát triển nội dung web, hiểu cách thao tác HTML và CSS trong Java là một kỹ năng mạnh mẽ cần có trong bộ công cụ của bạn.
## Câu hỏi thường gặp
### Aspose.HTML dành cho Java là gì?
Aspose.HTML for Java là một thư viện mạnh mẽ cho phép các nhà phát triển làm việc với các tài liệu HTML trong các ứng dụng Java, cung cấp nhiều tính năng, từ thao tác HTML đến kết xuất.
### Tôi có cần kết nối Internet để sử dụng Aspose.HTML không?
Không, sau khi bạn đã tải xuống các tệp thư viện cần thiết, bạn có thể sử dụng Aspose.HTML ngoại tuyến.
### Tôi có thể áp dụng nhiều tệp CSS vào một tài liệu HTML không?
 Có, bạn có thể tạo nhiều`<link>` các phần tử và thêm chúng vào phần đầu của tài liệu cho nhiều tệp CSS khác nhau.
### Có sự khác biệt giữa CSS nội bộ và CSS bên ngoài không?
Có! CSS nội bộ được định nghĩa trong tài liệu HTML, trong khi CSS bên ngoài được đặt trong một tệp riêng và liên kết đến tài liệu.
### Làm thế nào tôi có thể nhận được hỗ trợ cho Aspose.HTML dành cho Java?
 Bạn có thể truy cập hỗ trợ cộng đồng thông qua[Diễn đàn Aspose](https://forum.aspose.com/c/html/29) cho bất kỳ câu hỏi hoặc vấn đề nào bạn có thể gặp phải.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
