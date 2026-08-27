---
date: 2026-02-10
description: Tìm hiểu cách sử dụng Aspose để xử lý các liên kết bị hỏng trong Java,
  chuyển đổi HTML sang PNG và tải tài liệu HTML trong Java với Aspose.HTML cho Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Chuyển đổi HTML sang PNG với bộ xử lý tin nhắn Aspose.HTML trong Java
url: /vi/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi HTML sang PNG với Trình xử lý Tin nhắn Aspose.HTML trong Java

## Giới thiệu
Trong hướng dẫn này, bạn sẽ khám phá **cách chuyển đổi HTML sang PNG** đồng thời xử lý một cách khéo léo các tài nguyên bị thiếu bằng cách sử dụng Aspose.HTML cho Java. Chúng ta sẽ đi qua việc tạo một trang HTML nhỏ trỏ tới một hình ảnh không tồn tại, gắn một **custom message handler** để **chặn các yêu cầu mạng**, cấu hình **network service**, tải tài liệu, và cuối cùng thực hiện **html to image conversion**. Khi hoàn thành, bạn sẽ có một mẫu vững chắc cho cả **handle broken links java** và đầu ra PNG chất lượng cao—hoàn hảo cho báo cáo, hình thu nhỏ, hoặc bản xem trước email.

## Câu trả lời nhanh
- **What does a message handler do?** Nó chặn các hoạt động mạng (như yêu cầu hình ảnh) và cho phép bạn phản hồi các mã trạng thái như 404.  
- **Can Aspose.HTML convert HTML to PNG?** Có—`Converter.convertHTML` thực hiện việc chuyển đổi trong một lần gọi.  
- **Do I need a license for this example?** Một giấy phép tạm thời loại bỏ các giới hạn đánh giá; giấy phép vĩnh viễn là bắt buộc cho việc sử dụng trong môi trường sản xuất.  
- **Which Java version works?** Bất kỳ JDK 8+ nào (ví dụ chạy trên JDK 11).  
- **Can I configure the network service?** Chắc chắn—sử dụng `configuration.getService(INetworkService.class)` để thêm trình xử lý của bạn.

## Yêu cầu trước
Trước khi chúng ta bắt đầu, hãy chắc chắn rằng bạn đã chuẩn bị các mục sau:

1. **Java Development Kit (JDK)** – tải xuống từ [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – lấy thư viện từ [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse, hoặc NetBeans đều hoạt động tốt.  
4. **Basic Java knowledge** – bạn nên quen thuộc với các lớp, try‑with‑resources, và xử lý ngoại lệ.  
5. **Temporary License** – nếu bạn đang dùng bản dùng thử, hãy lấy một [temporary license](https://purchase.aspose.com/temporary-license/) để tránh watermark.

## Nhập các gói
Đầu tiên, chúng ta nhập lớp Java I/O cần thiết cho việc xử lý tệp. Các lớp Aspose còn lại sẽ được tham chiếu bằng tên đầy đủ sau này, giúp danh sách import gọn gàng.

```java
import java.io.IOException;
```

## Bước 1: Chuẩn bị mã HTML
Chúng ta tạo một đoạn mã HTML tối thiểu cố ý tham chiếu tới một hình ảnh bị thiếu. Điều này sẽ kích hoạt trình xử lý của chúng ta khi engine cố gắng tải tài nguyên.

```java
String code = "<img src='missing.jpg'>";
```

## Bước 2: Ghi mã HTML vào tệp
Tiếp theo, chúng ta lưu đoạn mã vào *document.html*. Sử dụng khối try‑with‑resources đảm bảo `FileWriter` được đóng đúng cách.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Bước 3: Viết Trình xử lý Tin nhắn Tùy chỉnh
Bây giờ chúng ta xây dựng một **custom message handler** kiểm tra trạng thái HTTP của mỗi yêu cầu mạng. Nếu phản hồi không phải là `200`, chúng ta ghi lại một cảnh báo thân thiện. Lưu ý lời gọi `invoke(context);` ở cuối—điều này chuyển tiếp yêu cầu tới trình xử lý tiếp theo trong chuỗi, ngăn ngừa vòng lặp đệ quy.

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

## Bước 4: Cấu hình Dịch vụ Mạng
Để Aspose.HTML nhận biết trình xử lý của chúng ta, chúng ta lấy **network service** từ một thể hiện `Configuration` và thêm trình xử lý vào bộ sưu tập của nó. Đây là bước chúng ta **configure network service** cho hành vi tùy chỉnh.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Bước 5: Tải tài liệu HTML
Với cấu hình đã sẵn sàng, chúng ta tải *document.html*. Engine bây giờ sử dụng dịch vụ mạng của chúng ta, vì vậy yêu cầu hình ảnh bị thiếu sẽ được chặn bởi trình xử lý mà chúng ta vừa thêm.

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

## Bước 6: Chuyển đổi HTML sang PNG
Đây là phần cốt lõi của quá trình **html to image conversion**. Phương thức `Converter.convertHTML` nhận `HTMLDocument` đã tải, tùy chọn `ImageSaveOptions` (nơi bạn có thể điều chỉnh DPI hoặc chất lượng), và tên tệp đầu ra.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Bước 7: Dọn dẹp tài nguyên
Thực hành tốt trong Java yêu cầu chúng ta giải phóng tất cả tài nguyên gốc. Khối `finally` đảm bảo `Configuration` được giải phóng ngay cả khi có ngoại lệ phát sinh.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Tại sao nên sử dụng Trình xử lý Tin nhắn?
Trình xử lý tin nhắn cung cấp cho bạn **kiểm soát chi tiết** đối với mỗi yêu cầu mạng—dù là hình ảnh, CSS, JavaScript, hay tệp phông chữ. Thay vì để thư viện thất bại im lặng, bạn có thể ghi lại các tài nguyên bị thiếu, cung cấp nội dung dự phòng, hoặc thậm chí thử lại yêu cầu. Điều này làm cho quy trình xử lý HTML của bạn **đáng tin cậy**, **sẵn sàng cho môi trường sản xuất**, và dễ dàng gỡ lỗi hơn.

## Các vấn đề thường gặp và giải pháp
- **Handler recursion** – Gọi `invoke(context);` chỉ một lần để tránh vòng lặp vô hạn.  
- **Missing license** – Nếu không có giấy phép hợp lệ, PNG đầu ra sẽ chứa watermark.  
- **Incorrect file paths** – Sử dụng đường dẫn tuyệt đối hoặc đặt thư mục làm việc đúng khi tải `document.html`.  
- **Unsupported resource types** – Đảm bảo tài nguyên bạn muốn chặn (hình ảnh, CSS, v.v.) thực sự được yêu cầu bởi engine HTML.

## Câu hỏi thường gặp

**Q: Can I chain multiple message handlers?**  
A: Có, bạn có thể thêm nhiều trình xử lý vào bộ sưu tập `network.getMessageHandlers()`; chúng sẽ được thực thi theo thứ tự được thêm.

**Q: Does the handler work for CSS or script resources as well?**  
A: Chắc chắn—bất kỳ yêu cầu mạng nào do engine HTML thực hiện (hình ảnh, CSS, JS, phông chữ) đều đi qua trình xử lý.

**Q: How do I change the HTTP request before it’s sent?**  
A: Triển khai một trình xử lý thay đổi `context.getRequest()` trước khi gọi `invoke(context)`.

**Q: Is there a way to suppress the warning for specific URLs?**  
A: Trong trình xử lý, kiểm tra `context.getRequest().getRequestUri()` và bỏ qua việc ghi log một cách có điều kiện.

**Q: What version of Aspose.HTML is required for these APIs?**  
A: Mã này hoạt động với Aspose.HTML cho Java 22.10 trở lên.

## Kết luận
Bây giờ bạn đã có một ví dụ hoàn chỉnh, từ đầu đến cuối về **cách chuyển đổi HTML sang PNG** đồng thời sử dụng **custom message handler** để **chặn các yêu cầu mạng** và **handle broken links java**. Bằng cách cấu hình dịch vụ mạng, tải tài liệu và gọi bộ chuyển đổi, bạn có thể tạo ra các thumbnail PNG hoặc ảnh chụp toàn trang một cách đáng tin cậy trong bất kỳ ứng dụng Java nào.

---

**Cập nhật lần cuối:** 2026-02-10  
**Kiểm tra với:** Aspose.HTML for Java 24.11  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}