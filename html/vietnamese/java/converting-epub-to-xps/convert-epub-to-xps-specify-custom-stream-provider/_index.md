---
date: 2026-01-07
description: Chuyển đổi EPUB sang XPS một cách dễ dàng bằng Aspose.HTML cho Java.
  Hãy làm theo hướng dẫn từng bước này để có quy trình chuyển đổi liền mạch.
linktitle: How to Convert EPUB to XPS with a Custom Stream Provider
second_title: Java HTML Processing with Aspose.HTML
title: Cách chuyển đổi EPUB sang XPS với nhà cung cấp luồng tùy chỉnh
url: /vi/java/converting-epub-to-xps/convert-epub-to-xps-specify-custom-stream-provider/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi EPUB sang XPS với Trình cung cấp Stream Tùy chỉnh

Trong thế giới xuất bản kỹ thuật số ngày nay, **convert EPUB to XPS** là một yêu cầu phổ biến—cho dù bạn cần một bản thể hiện bố cục cố định để in ấn, lưu trữ, hay chia sẻ trên các thiết bị Windows. Aspose.HTML for Java giúp quá trình chuyển đổi này trở nên đơn giản, và bằng cách sử dụng một custom memory stream provider, bạn có thể giữ toàn bộ quá trình trong bộ nhớ, điều này rất phù hợp cho các kịch bản dựa trên đám mây hoặc hiệu năng cao. Dưới đây là mọi thứ bạn cần để bắt đầu, từ các yêu cầu trước đến một ví dụ hoàn chỉnh, có thể chạy được.

## Trả lời nhanh
- **Chuyển đổi tạo ra cái gì?** Một tài liệu XPS chứa bố cục và phông chữ.
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho thử nghiệm; cần giấy phép thương mại cho môi trường sản xuất.
- **Tôi có thể chạy cái này trong vùng chứa không?** Có—không cần ghi vào tệp hệ thống nếu bạn giữ mọi thứ trong bộ nhớ.
- **Phiên bản Java nào được hỗ trợ?** Java8hoặc cao hơn.
- **Nhà cung cấp luồng tùy chỉnh có bắt buộc không?** Không, nhưng nó cho phép bạn kiểm soát hoàn toàn việc sử dụng bộ nhớ và xử lý đầu ra.

## “chuyển đổi EPUB sang XPS” là gì?
Chuyển đổi một tệp EPUB sang định dạng điện tử biến XPS có thể tái sinh thành một định dạng tài liệu độc lập cho thiết bị. XPS (Đặc tả giấy XML) là phiên bản của PDF tương thích của Microsoft, lý tưởng cho các trường hợp bạn cần có thể hiển thị hình ảnh trung thực và không thay đổi trên nền tảng.

## Tại sao nên sử dụng nhà cung cấp luồng tùy chỉnh?
Một `MemoryStreamProvider` tùy chỉnh cho phép bạn giữ kết quả chuyển đổi trong RAM thay vì ghi tệp tạm thời vào đĩa. Cách tiếp cận này:
- Giảm tải I/O.
- Cải thiện tính năng cải tiến trong cấu trúc kiến ​​trúc server-less hoặc micro-service.
- Mang lại sự hoạt động để truyền trực tiếp kết quả tới khách hàng, lưu trữ đám mây hoặc API khác.

## Điều kiện tiên quyết

Để **chuyển đổi EPUB sang XPS** thành công, hãy đảm bảo bạn đã chuẩn bị đầy đủ các yêu cầu sau:

### 1. Thư viện Aspose.HTML cho Java

Bạn phải cài đặt và cấu hình thư viện Aspose.HTML cho Java trong môi trường Java của mình. Nếu chưa, bạn có thể tải thư viện từ [download link](https://releases.aspose.com/html/java/).

### 2. Đầu vào tệp EPUB

Bạn cần có một tệp EPUB hiện có mà muốn chuyển đổi sang XPS. Đảm bảo tệp bảo mật này đã sẵn sàng cho quá trình chuyển đổi.

Bây giờ bạn đã có tất cả các yêu cầu, hãy cùng thực hiện qua các bước chuyển đổi chi tiết.

## Nhập gói

Trước khi bắt đầu, hãy chắc chắn nhập các package cần thiết để Aspose.HTML for Java có thể sử dụng các chức năng của nó.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.saving.MemoryStreamProvider;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## Mở tập tin EPUB

Đầu tiên, bạn cần mở tệp EPUB hiện có để đọc. Trong bước này, chúng ta sử dụng `FileInputStream` để truy cập tệp EPUB.

```java
try (FileInputStream fileInputStream = new FileInputStream("path/to/your/input.epub")) {
    // Your code for Step 1
}
```

## Tạo MemoryStreamProvider

Tiếp theo, tạo một thể hiện của `MemoryStreamProvider`. Đối tượng này sẽ giữ đầu ra của quá trình chuyển đổi trong bộ nhớ.

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code for Step 2
}
```

## Chuyển đổi EPUB sang XPS

Bây giờ, chuyển đổi tệp EPUB sang XPS bằng phương thức `Converter.convertEPUB`. `MemoryStreamProvider` cung cấp stream đích.

```java
Converter.convertEPUB(
    fileInputStream,
    new XpsSaveOptions(),
    streamProvider.getStream().findFirst().get()
);
```

## Lấy dữ liệu kết quả

Sau khi quá trình chuyển đổi hoàn tất, lấy memory stream chứa dữ liệu XPS.

```java
InputStream inputStream = streamProvider.getStream().findFirst().get();
```

## Lưu kết quả (Tùy chọn)

Nếu bạn cần một tệp vật lý—có thể để gỡ lỗi hoặc kiểm tra ngoại tuyến—hãy ghi memory stream ra đĩa. Trong hầu hết các kịch bản sản xuất, bạn có thể bỏ qua bước này và stream dữ liệu trực tiếp tới client.

```java
try (FileOutputStream fileOutputStream = new FileOutputStream("path/to/your/output.xps")) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## Hoàn thành mã nguồn

Dưới đây là ví dụ đầy đủ, sẵn sàng chạy, kết hợp tất cả các phần lại với nhau. Bạn có thể sao chép, dán và điều chỉnh nó cho dự án của mình.

```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of MemoryStreamProvider
            try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
                // Convert EPUB to XPS by using the MemoryStreamProvider
                com.aspose.html.converters.Converter.convertEPUB(
                        fileInputStream,
                        new com.aspose.html.saving.XpsSaveOptions(),
                        streamProvider.lStream
                );
                // Get access to the memory stream that contains the resulted data
                java.io.InputStream inputStream = streamProvider.lStream.stream().findFirst().get();
                // Flush the result data to the output file
                try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("output.xps"))) {
                    byte[] buffer = new byte[inputStream.available()];
                    inputStream.read(buffer);
                    fileOutputStream.write(buffer);
                }
            }
        }
```

## Các vấn đề thường gặp và giải pháp

| Vấn đề | Tại sao nó xảy ra | Sửa chữa |
|-------|-------|------|
| **`java.lang.OutOfMemoryError`** | Tệp EPUB lớn có thể vượt quá mặc định heap kích thước khi được giữ nguyên trong bộ nhớ. | Tăng JVM heap kích thước (`-Xmx`) hoặc xử lý EPUB theo từng phần nếu có thể. |
| **Thiếu phông chữ trong XPS** | Font chữ không được nhúng vào EPUB trên máy chuyển đổi. | Đảm bảo các phông chữ cần thiết đã được cài đặt trên máy chủ hoặc nhúng vào EPUB. |
| **`UnsupportedOperationException` từ `MemoryStreamProvider`** | Sử dụng cũ Aspose.HTML phiên bản. | Cập nhật lên phiên bản mới nhất của Aspose.HTML for Java. |

## Câu hỏi thường gặp

### 1. EPUB là gì?

EPUB, viết tắt của Electronic Publication, là một dạng phổ biến định dạng cho điện tử. Nó được thiết kế để dễ dàng đọc trên nhiều thiết bị khác nhau, chẳng hạn như máy đọc sách, máy tính bảng và điện thoại thông minh.

### 2. XPS là gì?

XPS là bản tắt của Đặc tả giấy XML, một tài liệu định dạng do Microsoft tạo ra. Nó được sử dụng để chia sẻ và lưu trữ tài liệu với giao diện và bố cục quán nhất.

### 3. Tại sao nên sử dụng Aspose.HTML cho Java?

Aspose.HTML for Java là một thư mạnh mẽ giúp đơn giản hóa các tác vụ tài liệu, chuyển đổi và kết xuất. Nó cung cấp nhiều tính năng phong phú và hỗ trợ nhiều loại tài liệu định dạng, là công cụ quý giá cho các nhà phát triển.

### 4. Tôi có thể chuyển đổi các định dạng tài liệu khác bằng Aspose.HTML cho Java không?

Có, Aspose.HTML for Java hỗ trợ chuyển đổi nhiều tài liệu định dạng, bao gồm HTML, EPUB, XPS và nhiều hơn nữa. Đây là một công cụ đa năng cho việc quản lý tài liệu.

### 5. Tôi có thể tìm thêm nguồn lực và hỗ trợ ở đâu?

Để xem tài liệu và nhận hỗ trợ, hãy truy cập [Tài liệu Aspose.HTML dành cho Java](https://reference.aspose.com/html/java/) và [support forum](https://forum.aspose.com/).

---

**Cập nhật lần cuối:** 2026-01-07
**Đã thử nghiệm với:** Aspose.HTML cho Java 24.12 (mới nhất tại thời điểm viết bài)
**Tác giả:** Giả định  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}