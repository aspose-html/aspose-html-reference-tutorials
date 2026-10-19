---
date: 2026-05-04
description: Tìm hiểu cách thực hiện chuyển đổi HTML sang PNG, chặn các yêu cầu mạng
  trong Java và xử lý các liên kết bị hỏng trong Java bằng Aspose.HTML cho Java.
keywords:
- html to png conversion
- intercept network requests java
- html to image conversion
- load html document java
- handle broken links java
linktitle: Sử dụng Trình xử lý Tin nhắn trong Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Chuyển đổi HTML sang PNG với Trình xử lý Tin nhắn Aspose.HTML trong Java
url: /vi/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển Đổi HTML sang PNG với Trình Xử Lý Tin Nhắn Aspose.HTML trong Java

## Giới Thiệu về Chuyển Đổi HTML sang PNG
Trong hướng dẫn này, bạn sẽ khám phá **cách chuyển đổi HTML sang PNG** đồng thời xử lý một cách nhẹ nhàng các tài nguyên bị thiếu bằng cách sử dụng Aspose.HTML cho Java. Chúng ta sẽ thực hiện các bước tạo một trang HTML nhỏ trỏ tới một hình ảnh không tồn tại, gắn một **trình xử lý tin nhắn tùy chỉnh** để **chặn các yêu cầu mạng**, cấu hình **dịch vụ mạng**, tải tài liệu, và cuối cùng thực hiện **chuyển đổi HTML sang hình ảnh**. Khi kết thúc, bạn sẽ có một mẫu vững chắc cho cả **xử lý liên kết hỏng java** và đầu ra PNG chất lượng cao—hoàn hảo cho báo cáo, hình thu nhỏ, hoặc bản xem trước email.

## Câu Trả Lời Nhanh
- **Trình xử lý tin nhắn làm gì?** Nó chặn các hoạt động mạng (như yêu cầu hình ảnh) và cho phép bạn phản hồi các mã trạng thái như 404.  
- **Aspose.HTML có thể chuyển đổi HTML sang PNG không?** Có—`Converter.convertHTML` thực hiện việc chuyển đổi trong một lần gọi.  
- **Tôi có cần giấy phép cho ví dụ này không?** Giấy phép tạm thời loại bỏ giới hạn đánh giá; giấy phép vĩnh viễn là bắt buộc cho việc sử dụng trong môi trường sản xuất.  
- **Phiên bản Java nào hoạt động?** Bất kỳ JDK 8+ nào (ví dụ chạy trên JDK 11).  
- **Tôi có thể cấu hình dịch vụ mạng không?** Chắc chắn—sử dụng `configuration.getService(INetworkService.class)` để thêm trình xử lý của bạn.  

## HTML sang PNG là gì?
Quá trình chuyển đổi HTML sang PNG sẽ render một trang web (hoặc một đoạn HTML) thành một hình ảnh raster. Điều này hữu ích khi bạn cần các bản xem trước tĩnh của nội dung động, tạo hình thu nhỏ cho bản tin email, hoặc lưu trữ các trang web dưới dạng hình ảnh.

## Tại sao nên sử dụng Trình Xử Lý Tin Nhắn để Chặn Yêu Cầu Mạng trong Java?
Trình xử lý tin nhắn cung cấp cho bạn **kiểm soát chi tiết** đối với mọi yêu cầu mạng—bất kể là hình ảnh, CSS, JavaScript hay tệp phông chữ. Bằng cách chặn các yêu cầu này, bạn có thể **ghi lại các tài nguyên bị thiếu**, cung cấp nội dung dự phòng, hoặc thậm chí thử lại các tải xuống thất bại, làm cho quy trình xử lý HTML của bạn **ổn định** và **sẵn sàng cho môi trường sản xuất**.

## Các Yêu Cầu Trước
1. **Java Development Kit (JDK)** – tải xuống từ [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – lấy thư viện từ [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse, hoặc NetBeans đều hoạt động tốt.  
4. **Kiến thức Java cơ bản** – bạn nên quen thuộc với các lớp, try‑with‑resources và xử lý ngoại lệ.  
5. **Giấy phép tạm thời** – nếu bạn đang dùng bản dùng thử, hãy lấy một [temporary license](https://purchase.aspose.com/temporary-license/) để tránh watermark.  

## Nhập Gói
Đầu tiên, nhập lớp Java I/O mà chúng ta sẽ cần cho việc xử lý tệp. Các lớp Aspose còn lại sẽ được tham chiếu bằng tên đầy đủ sau này, giúp danh sách import gọn gàng.

```java
import java.io.IOException;
```

## Bước 1: Chuẩn Bị Mã HTML
Chúng ta tạo một đoạn HTML tối thiểu cố ý tham chiếu tới một hình ảnh bị thiếu. Điều này sẽ kích hoạt trình xử lý của chúng ta khi engine cố gắng tải tài nguyên.

```java
String code = "<img src='missing.jpg'>";
```

## Bước 2: Ghi Mã HTML vào Tệp
Tiếp theo, chúng ta lưu đoạn mã vào *document.html*. Sử dụng khối try‑with‑resources đảm bảo `FileWriter` được đóng đúng cách.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Bước 3: Viết Trình Xử Lý Tin Nhắn Tùy Chỉnh
Bây giờ chúng ta xây dựng một **trình xử lý tin nhắn tùy chỉnh** để kiểm tra trạng thái HTTP của mỗi yêu cầu mạng. Nếu phản hồi không phải là `200`, chúng ta ghi một cảnh báo thân thiện. Lưu ý lời gọi `invoke(context);` ở cuối—điều này chuyển yêu cầu tới trình xử lý tiếp theo trong chuỗi, ngăn ngừa vòng lặp đệ quy.

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## Bước 4: Cấu Hình Dịch Vụ Mạng
Để Aspose.HTML nhận biết trình xử lý của chúng ta, chúng ta lấy **dịch vụ mạng** từ một thể hiện `Configuration` và thêm trình xử lý vào bộ sưu tập của nó. Đây là bước chúng ta **cấu hình dịch vụ mạng** cho hành vi tùy chỉnh.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Bước 5: Tải Tài Liệu HTML
Với cấu hình đã sẵn sàng, chúng ta tải *document.html*. Engine bây giờ sử dụng dịch vụ mạng của chúng ta, vì vậy yêu cầu hình ảnh bị thiếu sẽ bị chặn bởi trình xử lý mà chúng ta vừa thêm.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## Bước 6: Chuyển Đổi HTML sang PNG
Đây là phần cốt lõi của quy trình **chuyển đổi html sang hình ảnh**. Phương thức `Converter.convertHTML` nhận `HTMLDocument` đã tải, tùy chọn `ImageSaveOptions` (nơi bạn có thể điều chỉnh DPI hoặc chất lượng), và tên tệp đầu ra.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Bước 7: Dọn Dẹp Tài Nguyên
Thực hành tốt trong Java yêu cầu chúng ta giải phóng tất cả tài nguyên gốc. Khối `finally` đảm bảo `Configuration` được giải phóng ngay cả khi có ngoại lệ phát sinh.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Các Vấn Đề Thường Gặp và Giải Pháp
- **Đệ quy trình xử lý** – Gọi `invoke(context);` chỉ một lần để tránh vòng lặp vô hạn.  
- **Thiếu giấy phép** – Nếu không có giấy phép hợp lệ, PNG đầu ra sẽ chứa watermark.  
- **Đường dẫn tệp không đúng** – Sử dụng đường dẫn tuyệt đối hoặc thiết lập thư mục làm việc đúng khi tải `document.html`.  
- **Kiểu tài nguyên không được hỗ trợ** – Đảm bảo tài nguyên bạn muốn chặn (hình ảnh, CSS, v.v.) thực sự được yêu cầu bởi engine HTML.  

## Câu Hỏi Thường Gặp

**Q: Tôi có thể xâu chuỗi nhiều trình xử lý tin nhắn không?**  
A: Có, bạn có thể thêm nhiều trình xử lý vào bộ sưu tập `network.getMessageHandlers()`; chúng sẽ được thực thi theo thứ tự được thêm.  

**Q: Trình xử lý có hoạt động với tài nguyên CSS hoặc script không?**  
A: Hoàn toàn—bất kỳ yêu cầu mạng nào do engine HTML tạo ra (hình ảnh, CSS, JS, phông chữ) đều đi qua trình xử lý.  

**Q: Làm thế nào để thay đổi yêu cầu HTTP trước khi gửi?**  
A: Triển khai một trình xử lý thay đổi `context.getRequest()` trước khi gọi `invoke(context)`.  

**Q: Có cách nào để ẩn cảnh báo cho các URL cụ thể không?**  
A: Trong trình xử lý, kiểm tra `context.getRequest().getRequestUri()` và bỏ qua việc ghi log một cách có điều kiện.  

**Q: Phiên bản Aspose.HTML nào cần thiết cho các API này?**  
A: Mã này hoạt động với Aspose.HTML cho Java 22.10 trở lên.  

---

**Cập Nhật Cuối:** 2026-05-04  
**Kiểm Tra Với:** Aspose.HTML for Java 24.11  
**Tác Giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}