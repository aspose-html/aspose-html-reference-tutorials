---
date: 2025-12-10
description: Tìm hiểu cách sử dụng Aspose để xử lý các liên kết bị hỏng trong Java,
  chuyển đổi HTML sang PNG và tải tài liệu HTML trong Java với Aspose.HTML cho Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Cách sử dụng Trình xử lý tin nhắn Aspose.HTML trong Java
url: /vi/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng Trình Xử Lý Tin Nhắn Aspose.HTML trong Java

## Giới thiệu
Trong hướng dẫn này, **cách sử dụng aspose** để xử lý các tài nguyên bị thiếu trong HTML được trình bày chi tiết từng bước. Chúng ta sẽ tạo một tài liệu HTML đơn giản tham chiếu tới một hình ảnh không tồn tại, gắn một trình xử lý tin nhắn tùy chỉnh, và chỉ cho bạn cách **load html document java** trong khi xử lý các liên kết hỏng một cách nhẹ nhàng. Khi kết thúc, bạn cũng sẽ thấy cách **convert html to png** bằng Aspose.HTML, cung cấp cho bạn một bức tranh toàn diện về việc chuyển đổi HTML sang hình ảnh trong Java.

## Trả lời nhanh
- **Mục đích chính của trình xử lý tin nhắn là gì?** Để chặn các hoạt động mạng và phản hồi lại các mã trạng thái như tài nguyên bị thiếu.  
- **Aspose.HTML có thể chuyển HTML sang PNG không?** Có, sử dụng `Converter.convertHTML` bạn có thể thực hiện chuyển đổi html sang hình ảnh.  
- **Tôi có cần giấy phép cho ví dụ này không?** Giấy phép tạm thời loại bỏ các giới hạn đánh giá; giấy phép vĩnh viễn là cần thiết cho môi trường sản xuất.  
- **Phiên bản Java nào được hỗ trợ?** Bất kỳ JDK 8+ nào (hướng dẫn này sử dụng JDK 11).  
- **Có thể xử lý nhiều liên kết hỏng cùng lúc không?** Chắc chắn – bạn có thể xâu chuỗi nhiều trình xử lý để quản lý các kịch bản khác nhau.

## Yêu cầu trước
Trước khi chúng ta bắt đầu hãy chắc chắn rằng bạn đã chuẩn bị đầy đủ:
1. Java Development Kit (JDK): Đảm bảo bạn đã cài đặt JDK trên hệ thống. Bạn có thể tải về từ [trang web Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. Aspose.HTML for Java: Bạn cần cài đặt Aspose.HTML for Java. Tải về từ [trang phát hành của Aspose](https://releases.aspose.com/html/java/).  
3. IDE: Sử dụng môi trường phát triển Java yêu thích như IntelliJ IDEA, Eclipse, hoặc NetBeans.  
4. Kiến thức cơ bản về Java: Hiểu biết về lập trình Java là cần thiết để theo dõi hướng dẫn này một cách hiệu quả.  
5. Giấy phép tạm thời: Nếu bạn đang dùng phiên bản dùng thử của Aspose.HTML, hãy xem xét lấy một [giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) để tránh các hạn chế trong quá trình phát triển.

## Nhập khẩu các gói
Trước khi bắt đầu, hãy chắc chắn rằng bạn đã nhập các gói cần thiết vào dự án Java của mình. Dưới đây là các import quan trọng mà bạn sẽ cần:
```java
import java.io.IOException;
```
Các import này sẽ cung cấp cho bạn quyền truy cập vào các lớp và phương thức cần thiết để xử lý các hoạt động mạng, tạo tài liệu HTML, và thực hiện chuyển đổi HTML‑to‑PNG.

## Bước 1: Chuẩn bị mã HTML
Điều đầu tiên chúng ta cần là một đoạn mã HTML đơn giản tham chiếu tới một tệp hình ảnh. Chúng ta sẽ cố ý tham chiếu tới một hình ảnh không tồn tại để kích hoạt cơ chế xử lý lỗi.
```java
String code = "<img src='missing.jpg'>";
```
Đoạn mã này tạo một thẻ `<img>` trỏ tới `missing.jpg`. Vì hình ảnh không tồn tại, dịch vụ mạng sẽ trả về mã trạng thái không phải 200, và trình xử lý tùy chỉnh của chúng ta sẽ bắt được.

## Bước 2: Ghi mã HTML vào tệp
Tiếp theo, chúng ta cần lưu đoạn mã HTML để Aspose.HTML có thể tải nó dưới dạng tài liệu.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Bằng cách sử dụng `FileWriter` chúng ta lưu HTML vào **document.html**. Tệp này sẽ trở thành nguồn cho bước **load html document java** sau này.

## Bước 3: Tạo Trình Xử Lý Tin Nhắn Tùy Chỉnh
Bây giờ chúng ta sẽ xây dựng một trình xử lý tin nhắn tùy chỉnh để phản hồi khi không tìm thấy hình ảnh. Trình xử lý sẽ kiểm tra mã trạng thái HTTP và in ra một thông báo thân thiện.
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
Phương thức `invoke` kiểm tra `context.getResponse().getStatusCode()`. Nếu không phải **200**, chúng ta sẽ xuất ra một cảnh báo rõ ràng rằng tệp bị thiếu. Lệnh `invoke(context);` cuối cùng sẽ chuyển quyền kiểm soát cho trình xử lý tiếp theo trong chuỗi.

## Bước 4: Cấu hình Dịch vụ Mạng
Để Aspose.HTML nhận biết trình xử lý của chúng ta, chúng ta đăng ký nó với dịch vụ mạng thông qua lớp `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Ở đây chúng ta tạo một thể hiện `Configuration`, lấy `INetworkService`, và thêm trình xử lý tùy chỉnh của mình vào bộ sưu tập của nó. Điều này đảm bảo trình xử lý sẽ chạy trong bất kỳ yêu cầu mạng nào, chẳng hạn như tải hình ảnh.

## Bước 5: Tải Tài liệu HTML
Với cấu hình đã sẵn sàng, chúng ta có thể tải tệp HTML mà chúng ta đã tạo trước đó. Bước này minh họa **load html document java** trong khi hình ảnh bị thiếu kích hoạt trình xử lý của chúng ta.
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
Bộ khởi tạo `HTMLDocument` nhận cả đường dẫn tệp và `configuration` tùy chỉnh. Khi tài liệu phân tích thẻ `<img>`, dịch vụ mạng sẽ cố gắng lấy `missing.jpg`, nhận được mã 404, và trình xử lý của chúng ta sẽ in ra cảnh báo.

## Bước 6: Chuyển Đổi HTML sang PNG
Để minh họa khả năng rộng hơn của Aspose.HTML, chúng ta sẽ chuyển đổi tài liệu đã tải sang hình ảnh PNG. Đây là một kịch bản điển hình của **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` nhận `HTMLDocument`, tùy chọn `ImageSaveOptions` (nơi bạn có thể đặt DPI, chất lượng, v.v.), và tên tệp đầu ra. Kết quả là một ảnh raster của HTML đã được render.

## Bước 7: Dọn Dẹp Tài Nguyên
Quản lý tài nguyên đúng cách là điều thiết yếu trong bất kỳ ứng dụng Java nào. Chúng ta sẽ giải phóng cả `Configuration` và `HTMLDocument` để tránh rò rỉ bộ nhớ.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Việc gói phần dọn dẹp trong một khối `finally` đảm bảo nó luôn được thực thi ngay cả khi có ngoại lệ xảy ra ở các bước trước.

## Tại sao nên dùng Trình Xử Lý Tin Nhắn?
Trình xử lý tin nhắn cho bạn khả năng kiểm soát chi tiết các hoạt động mạng như **handle broken links java**. Thay vì để thư viện thất bại im lặng, bạn có thể ghi log, thử lại, thay thế tài nguyên, hoặc cung cấp nội dung dự phòng—giúp việc xử lý HTML của bạn trở nên vững chắc và sẵn sàng cho môi trường sản xuất.

## Các vấn đề thường gặp và giải pháp
- **Đệ quy trình xử lý** – Đảm bảo bạn gọi `invoke(context);` chỉ một lần để tránh vòng lặp vô hạn.  
- **Thiếu giấy phép** – Nếu không có giấy phép hợp lệ, quá trình chuyển đổi có thể tạo ra hình ảnh có dấu watermark.  
- **Lỗi đường dẫn tệp** – Sử dụng đường dẫn tuyệt đối hoặc thiết lập đúng thư mục làm việc khi tải `document.html`.

## Câu hỏi thường gặp

**H: Tôi có thể xâu chuỗi nhiều trình xử lý tin nhắn không?**  
Đ: Có, bạn có thể thêm nhiều trình xử lý vào bộ sưu tập `network.getMessageHandlers()`; chúng sẽ được thực thi theo thứ tự đã thêm.

**H: Trình xử lý có hoạt động với tài nguyên CSS hoặc script không?**  
Đ: Chắc chắn—bất kỳ yêu cầu mạng nào do engine HTML thực hiện (hình ảnh, CSS, JS, phông chữ) đều sẽ đi qua trình xử lý.

**H: Làm sao để thay đổi yêu cầu HTTP trước khi gửi?**  
Đ: Triển khai một trình xử lý sửa đổi `context.getRequest()` trước khi gọi `invoke(context)`.

**H: Có cách nào để ẩn cảnh báo cho các URL cụ thể không?**  
Đ: Trong trình xử lý, kiểm tra `context.getRequest().getRequestUri()` và bỏ qua việc ghi log một cách có điều kiện.

**H: Phiên bản Aspose.HTML nào cần thiết cho các API này?**  
Đ: Mã hoạt động với Aspose.HTML for Java 22.10 trở lên.

## Kết luận
Vậy là bạn đã có một hướng dẫn toàn diện về **cách sử dụng aspose** trình xử lý tin nhắn trong Java. Chúng ta đã đi qua việc tạo tệp HTML, gắn một trình xử lý tùy chỉnh để **handle broken links java**, tải tài liệu, và thực hiện **convert html to png**. Với mẫu này, bạn có thể tự tin quản lý các tài nguyên bị thiếu, áp dụng các chính sách tùy chỉnh, và mở rộng khả năng mạng của Aspose.HTML trong bất kỳ ứng dụng Java nào.

---

**Cập nhật lần cuối:** 2025-12-10  
**Đã kiểm tra với:** Aspose.HTML for Java 24.11  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}