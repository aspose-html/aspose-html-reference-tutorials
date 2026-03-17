---
date: 2026-02-04
description: Tìm hiểu cách sử dụng Aspose.HTML để cấu hình phông chữ, áp dụng CSS
  tùy chỉnh, sử dụng giấy phép tạm thời và tạo PDF từ HTML trong Java.
linktitle: Configure Fonts in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Cách sử dụng Aspose.HTML để cấu hình phông chữ cho HTML‑to‑PDF Java
url: /vi/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cấu hình phông chữ cho HTML‑to‑PDF Java với Aspose.HTML

## Giới thiệu
Trong phần hướng dẫn này, bạn sẽ khám phá **cách sử dụng Aspose.HTML** để cấu hình phông chữ cho việc chuyển đổi HTML‑to-PDF trong Java. Khi làm việc với tài liệu HTML, công việc thiết lập phông chữ chữ đúng đảm bảo PDF được tạo ra ngoài cùng gốc trang web gốc - duy trì màu sắc thương hiệu, kiểu chữ và bố cục. Dù bạn đang xây dựng báo cáo, hóa đơn hay bất kỳ trình tạo tài liệu nào, cấu hình chữ đúng cấu hình là chìa khóa để có PDF chuyên nghiệp. Hãy cùng thực hiện toàn bộ quá trình, từ môi trường chuẩn đến chuyển đổi HTML sang PDF với phông chữ và tùy chỉnh CSS.

## Trả lời nhanh
- **Mục đích chính của hướng dẫn này là gì?**Định cấu hình phông chữ để chuyển đổi HTML‑to‑PDF trong Java bằng Aspose.HTML.
- **Thư viện nào xử lý việc chuyển đổi?**Aspose.HTML cho Java (lớp `Converter`).
- **Tôi có cần giấy phép không?**Giấy phép Aspose tạm thời sẽ loại bỏ các giới hạn đánh giá; phải có giấy phép đầy đủ để sản xuất.
- **Phông chữ tùy chỉnh của tôi nên đặt ở đâu?**Trong thư mục được tham chiếu bởi `FontsLookupFolder`, ví dụ: thư mục `fonts` bên cạnh dự án của bạn.
- **Tôi có thể tùy chỉnh đầu ra PDF không?**Có—sử dụng `PdfSaveOptions` để điều chỉnh kích thước trang, lề, v.v.

## Cách sử dụng Aspose.HTML cho cấu hình phông chữ
Dưới đây chúng tôi sẽ giải thích cách xử lý phông chữ quan trọng, cách áp dụng tùy chỉnh CSS và cách **sử dụng giấy phép tạm thời** để mở đầy đủ chức năng khóa khi bạn thử nghiệm giải pháp.

## Điều kiện tiên quyết
Trước khi bắt đầu, hãy chắc chắn rằng bạn có những thứ sau:

1. **Bộ công cụ phát triển Java (JDK) 1.8+** – mã chạy trên mọi JDK hiện đại.
2. **Aspose.HTML for Java** – tải xuống JAR mới nhất từ ​​[trang web Aspose](https://releases.aspose.com/html/java/).
3. **Môi trường phát triển tích hợp (IDE)** – IntelliJ IDEA, Eclipse, hoặc bất kỳ trình soạn thảo nào tương thích với Java.

4. **Kiến thức Java cơ bản** – bạn cần nắm vững các lớp, phương thức và thao tác nhập/xuất tệp.

5. **Giấy phép Aspose.HTML** – [giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) sẽ gỡ bỏ các hạn chế dùng thử.

## Nhập các gói
Đầu tiên, nhập các lớp Java và Aspose.HTML cốt lõi mà bạn sẽ cần.  

```java
import java.io.IOException;
```

Những lần nhập này cung cấp cho bạn quyền truy cập vào việc xử lý tệp và API Aspose.HTML.

## **html sang pdf java** là gì và tại sao cấu hình phông chữ lại quan trọng?
Quá trình **html sang pdf java** chuyển đổi một HTML tài liệu thành một trang PDF. Phông chữ là một phần quan trọng của công việc kết xuất vì chúng ảnh hưởng đến bố cục, khoảng cách dòng và hình ảnh thực tế ở mức độ trung bình. Bằng cách chỉ định cho Aspose.HTML một tùy chỉnh phông chữ thư mục, bạn phải đảm bảo PDF sử dụng đúng kiểu chữ mà bạn đã thiết kế cho trang web, loại bỏ phông chữ dự phòng và duy trì tính năng hiệu quả nhất.

## Hướng dẫn từng bước

### Bước 1: Tạo nội dung HTML

#### 1.1 Viết mã HTML
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

Đoạn mã này định nghĩa một tiêu đề và một đoạn văn. Bạn có thể mở rộng HTML với nhiều phần tử hơn nếu cần kiểm tra các kiểu bổ sung.

#### 1.2 Lưu mã HTML vào tệp
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

`FileWriter` ghi chuỗi vào `user-agent-fontsetting.html` trong thư mục dự án của bạn. Sau bước này, bạn sẽ có một file HTML thực tế sẵn sàng để xử lý.

### Bước 2: Cấu hình môi trường Aspose.HTML

#### 2.1 Tạo một thể hiện cấu hình
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

Đối tượng `Configuration` là điểm vào để tùy chỉnh các tùy chọn render như xử lý phông chữ và hành vi user‑agent.

#### 2.2 Truy cập Dịch vụ Tác nhân Người dùng
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

`IUserAgentService` quản lý các stylesheet, phông chữ và các chi tiết render khác. Chúng ta sẽ dùng nó để chèn CSS tùy chỉnh và chỉ định thư mục phông chữ.

### Bước 3: Áp dụng kiểu dáng và phông chữ tùy chỉnh

#### 3.1 Thiết lập CSS tùy chỉnh
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

CSS này tô màu tiêu đề thành màu nâu và đoạn văn thành màu xám. Bạn có thể thêm bất kỳ quy tắc CSS hợp lệ nào ở đây — Aspose.HTML hỗ trợ đầy đủ spec CSS2.1 và nhiều tính năng CSS3. *(Đây là một ví dụ của **apply custom css**.)*

#### 3.2 Trỏ đến thư mục phông chữ tùy chỉnh
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

Đặt bất kỳ file `.ttf` hoặc `.otf` nào bạn muốn sử dụng vào thư mục có tên `fonts` nằm ở gốc dự án. Aspose.HTML sẽ tự động tải các phông chữ này trong quá trình render.

> **Mẹo hay:** Nếu bạn có nhiều họ phông chữ, hãy sắp xếp chúng trong các thư mục con và thêm từng thư mục cha vào `FontsLookupFolder` bằng cách sử dụng danh sách phân tách bằng dấu chấm phẩy.

> **Mẹo chuyên nghiệp:** Nếu bạn có nhiều họ phông chữ, hãy sắp xếp chúng trong các thư mục con và thêm mỗi thư mục cha vào `FontsLookupFolder` bằng danh sách ngăn cách bằng dấu chấm phẩy.

### Bước 4: Tải tài liệu HTML với cấu hình

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

Đối tượng `HTMLDocument` hiện đại đại diện cho HTML đã được style sẵn sàng để chuyển đổi.

### Bước 5: Chuyển đổi HTML sang PDF

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

Đối tượng `PdfSaveOptions` cho phép bạn tinh chỉnh các cài đặt đầu ra như kích thước trang, nén và siêu dữ liệu. Đối với chuyển đổi cơ bản, các tùy chọn mặc định hoạt động hoàn hảo.

### Bước 6: Dọn dẹp tài nguyên

#### 6.1 Giải phóng HTMLDocument
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 Giải phóng cấu hình
```java
if (configuration != null) {
    configuration.dispose();
}
```

Các lời gọi này giải phóng tài nguyên gốc được Aspose.HTML cấp phát.

## Các Vấn Đề Thường Gặp & Giải Pháp
| Vấn Đề | Giải Pháp |

|-------|----------|

| **Phông chữ không hiển thị** | Kiểm tra xem thư mục `fonts` đã được tham chiếu chính xác và chứa các tệp `.ttf`/`.otf` hợp lệ chưa. Sử dụng đường dẫn tuyệt đối nếu thư mục nằm ngoài thư mục dự án. |

| **PDF trông trống** | Đảm bảo đường dẫn tệp HTML chính xác và tệp có thể đọc được. Kiểm tra xem đối tượng `Configuration` đã được truyền cho hàm tạo `HTMLDocument` chưa. |

| **Lỗi giấy phép** | Áp dụng giấy phép Aspose tạm thời hoặc đầy đủ trước khi gọi bất kỳ API Aspose nào. Đặt tệp giấy phép vào classpath và tải nó bằng `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`. |

| **Hiển thị CSS không mong muốn** | Aspose.HTML hỗ trợ hầu hết CSS nhưng không phải tất cả các tính năng hiện đại (ví dụ: CSS Grid). Đơn giản hóa kiểu hoặc sử dụng các thuộc tính CSS được hỗ trợ. |

## Câu hỏi thường gặp

**H: Tôi có thể sử dụng bất kỳ phông chữ nào với Aspose.HTML cho Java không?**

A: Có, bạn có thể sử dụng bất kỳ phông chữ TrueType (`.ttf`) hoặc OpenType (`.otf`) nào mà hệ điều hành của bạn hỗ trợ. Chỉ cần đặt các tệp vào thư mục bạn đã thiết lập bằng `FontsLookupFolder`.

**H: Tôi có cần giấy phép để sử dụng Aspose.HTML cho Java không?**

A: Mặc dù bạn có thể dùng thử thư viện mà không cần giấy phép, nhưng [giấy phép Aspose tạm thời](https://purchase.aspose.com/temporary-license/) sẽ loại bỏ các giới hạn dùng thử. Đối với môi trường sản xuất, cần có giấy phép đầy đủ.

**H: Làm thế nào tôi có thể tùy chỉnh đầu ra PDF?**

A: Truyền một thể hiện `PdfSaveOptions` đã được cấu hình cho `convertHTML`. Bạn có thể thiết lập kích thước trang, lề, mức độ nén, v.v.

**H: Có thể áp dụng các kiểu CSS phức tạp hơn không?**

A: Có, Aspose.HTML hỗ trợ nhiều kiểu CSS. Các bộ chọn phức tạp, truy vấn phương tiện và lớp giả hoạt động như trong trình duyệt, mặc dù một số tính năng CSS3/4 rất mới có thể chưa được hỗ trợ đầy đủ.

**Hỏi: Tôi có thể tìm thêm ví dụ và tài liệu ở đâu?**

**Trả lời:** Truy cập trang tài liệu chính thức [Aspose.HTML for Java](https://reference.aspose.com/html/java/) để xem tài liệu tham khảo API chi tiết và các mẫu mã bổ sung.

**Hỏi:** Giấy phép tạm thời của Aspose ảnh hưởng đến quá trình chuyển đổi như thế nào?**
**Trả lời:** Giấy phép tạm thời loại bỏ giới hạn 10 trang và hình mờ xuất hiện ở chế độ dùng thử, cho phép bạn kiểm tra đầy đủ quy trình **chuyển đổi HTML PDF của Aspose**.

---

**Cập nhật lần cuối:** 04/02/2026
**Đã kiểm thử với:** Aspose.HTML for Java 24.12 (phiên bản mới nhất tại thời điểm viết bài)
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}