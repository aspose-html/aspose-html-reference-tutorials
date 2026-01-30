---
date: 2026-01-02
description: Tìm hiểu cách chuyển đổi EPUB sang PDF trong Java với Aspose.HTML đồng
  thời thiết lập kích thước trang PDF tùy chỉnh và các tùy chọn lưu PDF khác.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'Kích thước trang PDF tùy chỉnh: Chỉ định các tùy chọn lưu PDF cho EPUB sang
  PDF'
url: /vi/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kích Thước Trang PDF Tùy Chỉnh: Đặt Tùy Chọn Lưu PDF cho EPUB sang PDF

## Giới thiệu

Aspose.HTML for Java giúp bạn dễ dàng **chuyển đổi EPUB sang PDF** và cung cấp toàn quyền kiểm soát đầu ra, bao gồm việc đặt **kích thước trang PDF tùy chỉnh**. Trong hướng dẫn từng bước này, chúng tôi sẽ đi qua mọi thứ bạn cần—từ việc chuẩn bị môi trường đến tinh chỉnh `PdfSaveOptions` để PDF được tạo ra khớp với kích thước trang chính xác mà bạn yêu cầu. Dù bạn đang xây dựng một quy trình xuất bản, một nền tảng e‑learning, hay chỉ cần tự động hoá việc chuyển đổi tài liệu, bạn sẽ thấy các kỹ thuật ở đây rất hữu ích.

## Câu trả lời nhanh
- **Mục đích chính của hướng dẫn này là gì?** Chuyển đổi một tệp EPUB sang PDF đồng thời áp dụng kích thước trang PDF tùy chỉnh.  
- **Thư viện nào được sử dụng?** Aspose.HTML for Java.  
- **Tôi có cần giấy phép không?** Có phiên bản dùng thử miễn phí; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Có thể thay đổi màu nền không?** Có, sử dụng `PdfSaveOptions`.  
- **Java 8+ có được hỗ trợ không?** Chắc chắn—bất kỳ môi trường Java hiện đại nào cũng hoạt động.

## Kích thước trang PDF tùy chỉnh là gì?

Kích thước trang PDF tùy chỉnh cho phép bạn xác định độ rộng và chiều cao chính xác của mỗi trang trong PDF đầu ra, thay vì dựa vào các kích thước tiêu chuẩn như A4 hoặc Letter. Điều này đặc biệt hữu ích cho sách điện tử, tờ rơi, hoặc bất kỳ trường hợp nào mà bố cục trực quan phải khớp với một thiết kế cụ thể.

## Tại sao nên sử dụng Aspose.HTML để chuyển đổi EPUB sang PDF?

- **Độ trung thực cao:** Bảo tồn bố cục phức tạp, phông chữ và hình ảnh.  
- **Kiểm soát chi tiết:** Điều chỉnh kích thước trang, nền, lề và hơn thế nữa qua `PdfSaveOptions`.  
- **Đa nền tảng:** Hoạt động trên Windows, Linux và macOS với cùng một mã Java.  
- **Hiệu suất:** Động cơ render được tối ưu cho việc chuyển đổi nhanh.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- **Môi trường phát triển Java:** JDK 8 trở lên đã được cài đặt và cấu hình.  
- **Aspose.HTML for Java:** Tải JAR mới nhất từ [website](https://releases.aspose.com/html/java/).  
- **Tệp EPUB:** Tài liệu `.epub` mà bạn muốn chuyển đổi.  

Bây giờ mọi thứ đã sẵn sàng, chúng ta hãy bắt đầu các bước chuyển đổi thực tế.

## Bước 1: Mở tệp EPUB

Đầu tiên, chúng ta cần mở tệp EPUB bằng một `FileInputStream`. Luồng này sẽ được truyền cho bộ chuyển đổi sau này.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Bước 2: Định nghĩa tùy chọn lưu PDF

Ở đây chúng ta thiết lập **kích thước trang PDF tùy chỉnh** và màu nền tùy chọn. Điều chỉnh các giá trị pixel để phù hợp với kích thước mong muốn.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

### Mẹo chuyên nghiệp:
- **Pixel so với Point:** `Length.fromPixels` chuyển pixel màn hình sang point PDF (1 point = 1/72 inch). Chọn các giá trị phản ánh kích thước in cuối cùng mà bạn cần.

## Bước 3: Chuyển đổi EPUB sang PDF

Khi luồng đầu vào và các tùy chọn tùy chỉnh đã sẵn sàng, gọi bộ chuyển đổi. PDF đầu ra sẽ được lưu vào vị trí bạn chỉ định.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Mã nguồn hoàn chỉnh

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Các vấn đề thường gặp và giải pháp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|----------|
| **Các trang PDF bị trắng** | Luồng đầu vào bị đóng trước khi chuyển đổi | Giữ khối `try‑with‑resources` mở cho đến sau khi thực hiện `convertEPUB`. |
| **Kích thước trang không đúng** | Sử dụng pixel không tương ứng với kích thước in mong muốn | Chuyển đổi inch mong muốn sang point (`1 inch = 72 points`) rồi sang pixel bằng `Length.fromPixels`. |
| **Thiếu phông chữ** | Phông chữ không được nhúng trong EPUB | Đảm bảo phông chữ được đóng gói trong EPUB hoặc cài đặt chúng trên máy chủ. |

## Câu hỏi thường gặp (FAQs)

### Aspose.HTML for Java là thư viện miễn phí?
Aspose.HTML for Java là thư viện thương mại, nhưng bạn có thể lấy phiên bản dùng thử miễn phí từ [website](https://releases.aspose.com/).

### Các định dạng EPUB nào được hỗ trợ để chuyển đổi?
Aspose.HTML for Java hỗ trợ chuyển đổi các định dạng EPUB khác nhau, đảm bảo tương thích với hầu hết các tài liệu EPUB.

### Tôi có thể tùy chỉnh đầu ra PDF thêm không?
Có, bạn có thể tùy chỉnh đầu ra PDF bằng cách điều chỉnh cài đặt trang, màu nền và các thiết lập khác trong `PdfSaveOptions`.

### Có bất kỳ hạn chế nào đối với phiên bản dùng thử của Aspose.HTML for Java không?
Phiên bản dùng thử có thể có một số hạn chế, vì vậy nên kiểm tra tài liệu để biết chi tiết.

### Tôi có thể nhận hỗ trợ cho Aspose.HTML for Java ở đâu?
Bạn có thể tìm câu trả lời và yêu cầu hỗ trợ trên [diễn đàn Aspose.HTML](https://forum.aspose.com/).

---

**Cập nhật lần cuối:** 2026-01-02  
**Kiểm tra với:** Aspose.HTML for Java 24.11 (phiên bản mới nhất tại thời điểm viết)  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}