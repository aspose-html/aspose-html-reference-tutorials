---
date: 2025-12-10
description: Tìm hiểu cách đặt thời gian chờ trong Aspose.HTML cho Java, cấu hình
  Runtime Service để chuyển đổi HTML sang PNG, ngăn chặn vòng lặp vô hạn và tăng hiệu
  suất.
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Cách thiết lập thời gian chờ trong Aspose.HTML cho Dịch vụ Java Runtime
url: /vi/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Đặt Thời Gian Hết Hạn trong Aspose.HTML cho Dịch Vụ Thời Gian Chạy Java

## Giới thiệu
Nếu bạn đang tìm cách **how to set timeout** cho các script khi làm việc với Aspose.HTML cho Java, bạn đã đến đúng nơi. Kiểm soát việc thực thi script không chỉ ngăn ngừa vòng lặp vô hạn mà còn giúp bạn **convert html to png** nhanh hơn và giữ cho ứng dụng của bạn phản hồi tốt. Trong hướng dẫn này, chúng tôi sẽ đi qua các bước cụ thể để cấu hình Runtime Service, giới hạn thời gian thực thi script, và cuối cùng tạo ra một hình ảnh PNG từ HTML mà không làm treo chương trình của bạn.

## Câu trả lời nhanh
- **Runtime Service làm gì?** It lets you control script execution time and manage resources while processing HTML.  
- **Làm thế nào để đặt timeout cho JavaScript?** Use `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **Tôi thể ngăn chặn vòng lặp vô hạn không?** Yes – the timeout stops loops that exceed the defined limit.  
- **Điều này có ảnh hưởng đến việc chuyển đổi HTML‑to‑PNG không?** No, the conversion proceeds once the script finishes or is terminated by the timeout.  
- **Phiên bản Aspose.HTML nào được yêu cầu?** The latest release from the Aspose downloads page.

## Yêu cầu trước
Trước khi chúng ta đi sâu vào các chi tiết, hãy chắc chắn rằng bạn có những thứ sau:

1. **Java Development Kit (JDK)** – cài đặt từ [Oracle's website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java Library** – tải bản mới nhất từ [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse hoặc NetBeans đều hoạt động tốt.  
4. **Basic Java & HTML knowledge** – cần thiết để theo dõi các đoạn mã.

## Nhập các Gói
Đầu tiên, nhập các lớp bạn sẽ cần. Lệnh import `java.io.IOException` cần thiết cho việc xử lý tệp.

```java
import java.io.IOException;
```

## Bước 1: Tạo tệp HTML với mã JavaScript
Chúng tôi sẽ bắt đầu bằng việc tạo một tệp HTML đơn giản chứa một vòng lặp JavaScript. Vòng lặp này sẽ chạy mãi mãi nếu chúng ta không áp dụng timeout, làm cho nó trở thành một ví dụ hoàn hảo cho Runtime Service.

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- Script `while(true) {}` đại diện cho một vòng lặp vô hạn tiềm năng.  
- `FileWriter` ghi nội dung HTML vào **runtime-service.html**.

## Bước 2: Thiết lập Đối tượng Cấu hình
Tiếp theo, tạo một thể hiện `Configuration`. Đối tượng này là xương sống cho tất cả các dịch vụ Aspose.HTML, bao gồm Runtime Service.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Bước 3: Cấu hình Runtime Service
Đây là nơi chúng ta thực sự **how to set timeout**. Bằng cách lấy `IRuntimeService` từ cấu hình, chúng ta có thể định nghĩa giới hạn thực thi JavaScript.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` giới hạn thời gian thực thi script ở **5 seconds**, hiệu quả **preventing infinite loops**.  
- Điều này cũng **limits script execution** cho bất kỳ mã client‑side nặng nào.

## Bước 4: Tải tài liệu HTML với Cấu hình
Bây giờ tải tệp HTML bằng cấu hình chứa quy tắc timeout của chúng ta.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Tài liệu tôn trọng timeout đã định nghĩa trước, vì vậy vòng lặp vô hạn sẽ bị dừng sau 5 giây.

## Bước 5: Chuyển đổi HTML sang PNG
Với tài liệu đã được tải an toàn, chúng ta có thể **convert html to png**. Quá trình chuyển đổi chỉ diễn ra sau khi script hoàn thành hoặc bị dừng bởi timeout.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` chỉ định cho Aspose.HTML xuất ra hình ảnh PNG.  
- Tệp kết quả, **runtime-service_out.png**, hiển thị HTML đã được render mà không treo.

## Bước 6: Dọn dẹp tài nguyên
Cuối cùng, giải phóng các đối tượng để giải phóng bộ nhớ và tránh rò rỉ.

```java
} finally {
    if (document != null) {
        document.dispose();
    }
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- Việc giải phóng đúng cách là cần thiết cho các ứng dụng chạy lâu dài.

## Kết luận
Bạn vừa học được **how to set timeout** cho việc thực thi JavaScript trong Aspose.HTML cho Java, cách **prevent infinite loops**, và cách **convert html to png** một cách an toàn. Bằng cách cấu hình Runtime Service, bạn có được kiểm soát chi tiết hành vi script, giúp thời gian khởi động nhanh hơn và chuyển đổi đáng tin cậy hơn. Thử nghiệm với các giá trị timeout khác nhau để phù hợp với khối lượng công việc của bạn, và bạn sẽ thấy hiệu năng được cải thiện đáng kể.

## Câu hỏi thường gặp

**Q: Mục đích của Runtime Service trong Aspose.HTML cho Java là gì?**  
A: Nó cho phép bạn kiểm soát thời gian thực thi script, giúp **prevent infinite loops** và giữ cho quá trình chuyển đổi đáp ứng tốt.

**Q: Làm sao tôi có thể tải Aspose.HTML cho Java?**  
A: Lấy phiên bản mới nhất từ [releases page](https://releases.aspose.com/html/java/).

**Q: Có cần thiết phải giải phóng các đối tượng `document` và `configuration` không?**  
A: Có, việc giải phóng giúp giải phóng tài nguyên gốc và ngăn ngừa rò rỉ bộ nhớ.

**Q: Tôi có thể đặt timeout JavaScript thành giá trị khác 5 giây không?**  
A: Chắc chắn – thay đổi đối số của `TimeSpan.fromSeconds()` thành bất kỳ giới hạn nào phù hợp với kịch bản của bạn.

**Q: Tôi có thể tìm kiếm trợ giúp ở đâu nếu gặp vấn đề?**  
A: Truy cập [Aspose.HTML forum](https://forum.aspose.com/c/html/29) để nhận hỗ trợ từ cộng đồng và nhân viên.

**Cập nhật lần cuối:** 2025-12-10  
**Kiểm tra với:** Aspose.HTML cho Java 24 (latest)  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}