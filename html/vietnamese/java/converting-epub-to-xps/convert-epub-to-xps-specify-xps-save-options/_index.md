---
date: 2026-03-29
description: Tìm hiểu cách sử dụng Aspose.HTML cho Java để chỉ định các tùy chọn lưu
  XPS, chuyển đổi EPUB sang XPS và xử lý giấy phép.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Cách sử dụng tùy chọn lưu Aspose HTML cho EPUB sang XPS
url: /vi/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng Tùy Chọn Lưu HTML của Aspose cho EPUB sang XPS

Trong hướng dẫn này, chúng tôi sẽ chỉ **cách sử dụng Aspose** HTML Save Options để chuyển đổi tài liệu EPUB sang XPS với khả năng kiểm soát đầy đủ kích thước trang, màu nền và các cân nhắc về giấy phép. Dù bạn đang xây dựng một quy trình xử lý hàng loạt hay một công cụ chuyển đổi một lần, các bước này sẽ giúp bạn đạt được kết quả đáng tin cậy một cách nhanh chóng.

## Câu Trả Lời Nhanh
- **Tùy chọn Lưu HTML của Aspose làm gì?** Nó cho phép bạn tùy chỉnh kích thước trang, màu nền và các cài đặt render khác khi lưu dưới các định dạng như XPS.  
- **Thư viện nào được yêu cầu?** Aspose.HTML for Java (phiên bản mới nhất).  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho việc đánh giá; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Tôi có thể thay đổi kích thước trang không?** Có – bạn có thể đặt bất kỳ chiều rộng và chiều cao nào qua `PageSetup`.  
- **Quá trình chuyển đổi có nhanh không?** Đối với các tệp EPUB thông thường, quá trình chuyển đổi hoàn thành trong vài giây trên một JVM hiện đại.

## “how to use aspose” là gì trong Ngữ Cảnh Này?
Cụm từ **how to use Aspose** đề cập đến các bước thực tế để tận dụng thư viện Aspose.HTML trong việc thao tác và chuyển đổi tài liệu dựa trên web. Trong hướng dẫn này, chúng tôi tập trung vào **aspose html save options** cho phép bạn tinh chỉnh đầu ra khi **chuyển đổi EPUB sang XPS**.

## Tại Sao Nên Sử Dụng Aspose.HTML cho Java Để Chuyển Đổi EPUB sang XPS?
- **Độ trung thực cao** – giữ nguyên bố cục phức tạp, phông chữ và đồ họa vector.  
- **Kiểm soát bằng chương trình** – tự động hoá chuyển đổi hàng loạt trong các ứng dụng Java.  
- **Không phụ thuộc bên ngoài** – thư viện thuần Java, không có thành phần gốc.  
- **Đầu ra có thể tùy chỉnh** – nhờ các tùy chọn lưu, bạn có thể điều chỉnh XPS theo nhu cầu chính xác, chẳng hạn **xác định kích thước trang** hoặc đặt nền tùy chỉnh.  

## Yêu Cầu Trước

Trước khi chúng ta bắt đầu với mã, hãy chắc chắn rằng bạn đã có những thứ sau:

1. **Môi trường Phát triển Java** – đã cài đặt JDK 8 hoặc cao hơn.  
2. **Thư viện Aspose.HTML cho Java** – tải xuống từ [liên kết tải xuống](https://releases.aspose.com/html/java/).  
3. **Tệp EPUB** – tệp EPUB nguồn mà bạn muốn **chuyển đổi EPUB sang XPS**.  

Có sẵn những thứ này sẽ cho phép bạn thực hiện các bước mà không bị gián đoạn.

## Nhập Gói

Đầu tiên, nhập các lớp cần thiết. Đặt các lệnh import ở đầu tệp nguồn Java của bạn:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

Các import này cung cấp cho bạn quyền truy cập vào động cơ chuyển đổi và **Aspose HTML Save Options** cần thiết để tinh chỉnh.

## Mở Tệp EPUB

Tiếp theo, mở EPUB mà bạn muốn chuyển đổi. Trợ giúp `Resources.input` tải tệp từ thư mục tài nguyên demo:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Sử dụng khối try‑with‑resources đảm bảo luồng được đóng tự động.

## Tạo XpsSaveOptions (Cấu Hình Kích Thước Trang & Nền)

Bây giờ chúng ta tạo một thể hiện `XpsSaveOptions` và tùy chỉnh nó. Đây là nơi **các tùy chọn lưu** thực sự tỏa sáng:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Kích thước trang** – đặt thành 3000 × 1000 pixel trong ví dụ này; điều chỉnh để phù hợp với kích thước giấy mục tiêu của bạn hoặc sử dụng `Length.fromInches` để **xác định kích thước trang** bằng inch.  
- **Màu nền** – `AliceBlue` minh họa cách thay đổi nền canvas; bạn có thể chọn bất kỳ `Color` nào.  

Các cài đặt này là một phần của **aspose html save options** ảnh hưởng đến tài liệu XPS cuối cùng.

## Chuyển Đổi EPUB sang XPS

Cuối cùng, gọi bộ chuyển đổi với luồng, các tùy chọn đã cấu hình và đường dẫn đầu ra:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Khi dòng này chạy, Aspose.HTML đọc EPUB, áp dụng cài đặt trang và màu nền bạn đã định nghĩa, và ghi một tệp XPS hoàn toàn tuân thủ.

## Các Vấn Đề Thường Gặp & Mẹo
- **Kích thước trang không đúng** – đảm bảo kích thước được biểu thị bằng pixel (hoặc sử dụng `Length.fromInches`).  
- **Thiếu phông chữ** – nhúng các phông chữ cần thiết vào EPUB hoặc cài đặt chúng trên máy chủ JVM để tránh fallback.  
- **Tệp lớn** – đối với các EPUB rất lớn, tăng bộ nhớ heap JVM (`-Xmx`) để tránh `OutOfMemoryError`.  
- **Giấy phép Aspose HTML** – đảm bảo bạn đã tải giấy phép hợp lệ trước khi chuyển đổi; nếu không, dấu bản quyền dùng thử sẽ xuất hiện.

## Kết Luận

Bằng cách tận dụng **Aspose HTML Save Options**, bạn có được kiểm soát chính xác cách một EPUB được render sang XPS. Các bước trên cho bạn thấy **cách chuyển đổi EPUB**, thiết lập **kích thước trang**, thay đổi nền, và thực hiện chuyển đổi chỉ với vài dòng mã Java. Tích hợp mẫu này vào các quy trình xử lý hàng loạt của bạn để tự động hoá các nhiệm vụ xuất bản một cách hiệu quả.

## Câu Hỏi Thường Gặp

**Q: Aspose.HTML cho Java là gì?**  
A: Đó là một thư viện Java cho phép các nhà phát triển tạo, chỉnh sửa, render và chuyển đổi HTML, EPUB và các tài liệu dựa trên web khác mà không cần trình duyệt.

**Q: Tôi có thể sử dụng điều này trong dự án thương mại không?**  
A: Có. Đối với môi trường sản xuất, bạn cần một giấy phép hợp lệ. Bạn có thể mua tại [trang mua](https://purchase.aspose.com/buy).

**Q: Có bản dùng thử miễn phí không?**  
A: Chắc chắn. Tải phiên bản dùng thử từ [đây](https://releases.aspose.com/).

**Q: Tôi có thể nhận hỗ trợ ở đâu?**  
A: Hỗ trợ cộng đồng và trợ giúp chính thức có sẵn qua các diễn đàn Aspose tại [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: Yêu cầu hệ thống là gì?**  
A: Một Java Development Kit (JDK) 8+ và hệ điều hành được hỗ trợ bởi runtime của Aspose. Đảm bảo môi trường của bạn đáp ứng các yêu cầu đã liệt kê ở trên.

---

**Cập Nhật Cuối Cùng:** 2026-03-29  
**Được Kiểm Tra Với:** Aspose.HTML for Java 24.12  
**Tác Giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}