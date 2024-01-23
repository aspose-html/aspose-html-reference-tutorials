---
title: Tinh chỉnh bộ chuyển đổi trong .NET với Aspose.HTML
linktitle: Tinh chỉnh bộ chuyển đổi trong .NET
second_title: Aspose.HTML .NET HTML thao tác API
description: Tìm hiểu cách chuyển đổi HTML sang PDF, XPS và hình ảnh bằng Aspose.HTML cho .NET. Hướng dẫn từng bước với các ví dụ về mã và Câu hỏi thường gặp.
type: docs
weight: 16
url: /vi/net/advanced-features/fine-tuning-converters/
---

## Giới thiệu

Aspose.HTML for .NET là một thư viện mạnh mẽ cho phép các nhà phát triển thao tác và chuyển đổi tài liệu HTML ở nhiều định dạng khác nhau. Cho dù bạn cần chuyển đổi HTML sang PDF, XPS hay hình ảnh hay thực hiện các tác vụ khác liên quan đến HTML, Aspose.HTML đều cung cấp một bộ công cụ mạnh mẽ để giúp bạn hoàn thành công việc.

Trong hướng dẫn này, chúng ta sẽ khám phá một số tính năng cần thiết của Aspose.HTML cho .NET và cung cấp giải thích từng bước cho từng ví dụ. Đến cuối hướng dẫn này, bạn sẽ hiểu rõ về cách sử dụng Aspose.HTML cho .NET trong các ứng dụng .NET của mình.

## Điều kiện tiên quyết

Trước khi chúng ta đi sâu vào các ví dụ, hãy đảm bảo bạn có sẵn các điều kiện tiên quyết sau:

-  Aspose.HTML cho .NET: Bạn nên cài đặt thư viện Aspose.HTML cho .NET. Bạn có thể tải nó xuống từ[Liên kết tải xuống](https://releases.aspose.com/html/net/).

- Giấy phép tạm thời (Tùy chọn): Nếu bạn không có giấy phép hợp lệ, bạn có thể xin giấy phép tạm thời từ[đây](https://purchase.aspose.com/temporary-license/).

Bây giờ, hãy khám phá một số trường hợp sử dụng phổ biến với Aspose.HTML cho .NET.

## Nhập không gian tên

Trong mã C# của bạn, hãy bắt đầu bằng cách nhập các vùng tên cần thiết:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Chuyển đổi HTML sang PDF

### Bước 1: Chuẩn bị mã HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Bước 2: Khởi tạo tài liệu HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Bước 3: Tạo thiết bị PDF và chỉ định tệp đầu ra

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Bước 4: Kết xuất HTML thành PDF

```csharp
document.RenderTo(device);
```

Ví dụ này chuyển đổi đoạn mã HTML thành tài liệu PDF. Bạn có thể tùy chỉnh mã HTML và tệp đầu ra nếu cần.

## Đặt kích thước trang tùy chỉnh

### Bước 1: Chuẩn bị mã HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Bước 2: Khởi tạo tài liệu HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Bước 3: Tạo tùy chọn hiển thị PDF

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Bước 4: Tạo thiết bị PDF và chỉ định các tùy chọn cũng như tệp đầu ra

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Bước 5: Kết xuất HTML thành PDF

```csharp
document.RenderTo(device);
```

Ví dụ này trình bày cách đặt kích thước trang tùy chỉnh cho tài liệu PDF thu được.

## Điều chỉnh độ phân giải

### Bước 1: Chuẩn bị mã HTML và lưu vào tệp

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Bước 2: Khởi tạo tài liệu HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Bước 3: Tạo tùy chọn hiển thị PDF cho độ phân giải thấp

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Bước 4: Tạo thiết bị PDF và chỉ định các tùy chọn cũng như tệp đầu ra cho độ phân giải thấp

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Bước 5: Kết xuất HTML thành PDF để có độ phân giải thấp

```csharp
document.RenderTo(device);
```

### Bước 6: Tạo tùy chọn hiển thị PDF cho độ phân giải cao

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Bước 7: Tạo thiết bị PDF và chỉ định các tùy chọn cũng như tệp đầu ra cho độ phân giải cao

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Bước 8: Kết xuất HTML sang PDF để có độ phân giải cao

```csharp
document.RenderTo(device);
```

Ví dụ này minh họa cách điều chỉnh độ phân giải khi hiển thị HTML sang PDF, xem xét cả màn hình có độ phân giải thấp và cao.

## Chỉ định màu nền

### Bước 1: Chuẩn bị mã HTML và lưu vào tệp

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Bước 2: Khởi tạo tài liệu HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Bước 3: Khởi tạo các tùy chọn hiển thị PDF với màu nền

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Bước 4: Tạo thiết bị PDF và chỉ định các tùy chọn cũng như tệp đầu ra

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Bước 5: Kết xuất HTML thành PDF

```csharp
document.RenderTo(device);
```

Ví dụ này trình bày cách chỉ định màu nền khi chuyển đổi HTML sang PDF.

## Đặt kích thước trang bên trái và bên phải

### Bước 1: Chuẩn bị mã HTML

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Bước 2: Khởi tạo tài liệu HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Bước 3: Tạo tùy chọn hiển thị PDF với kích thước trang trái và phải

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Bước 4: Tạo thiết bị PDF và chỉ định các tùy chọn cũng như tệp đầu ra

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Bước 5: Kết xuất HTML thành PDF

```csharp
document.RenderTo(device);
```

Ví dụ này cho thấy cách đặt kích thước trang khác nhau cho trang bên trái và bên phải khi chuyển đổi HTML sang PDF.

## Điều chỉnh kích thước trang theo nội dung

### Bước 1: Chuẩn bị mã HTML

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Bước 2: Khởi tạo tài liệu HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Bước 3: Tạo tùy chọn hiển thị PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Bước 4: Tạo thiết bị PDF và chỉ định các tùy chọn cũng như tệp đầu ra

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Bước 5: Kết xuất HTML thành PDF

```csharp
document.RenderTo(device);
```

Ví dụ này trình bày cách điều chỉnh kích thước trang cho nội dung rộng nhất khi chuyển đổi HTML sang PDF.

## Chỉ định quyền PDF

### Bước 1: Chuẩn bị mã HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Bước 2: Khởi tạo tài liệu HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Bước 3: Tạo tùy chọn hiển thị PDF có quyền

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Bước 4: Tạo thiết bị PDF và chỉ định các tùy chọn cũng như tệp đầu ra

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Bước 5: Kết xuất HTML thành PDF

```csharp
document.RenderTo(device);
```

Ví dụ này trình bày cách chỉ định quyền và mã hóa khi chuyển đổi HTML sang tệp PDF được bảo vệ.

## Chỉ định các tùy chọn dành riêng cho hình ảnh

### Bước 1: Chuẩn bị mã HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Bước 2: Khởi tạo tài liệu HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Bước 3: Tạo tùy chọn kết xuất hình ảnh

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Bước 4: Tạo thiết bị hình ảnh và chỉ định các tùy chọn và tệp đầu ra

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Bước 5: Kết xuất HTML thành hình ảnh

```csharp
document.RenderTo(device);
```

Ví dụ này trình bày cách chuyển đổi HTML thành hình ảnh với các tùy chọn hiển thị cụ thể, chẳng hạn như định dạng, độ phân giải và chế độ làm mịn.

## Chỉ định tùy chọn kết xuất XPS

### Bước 1: Chuẩn bị mã HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Bước 2: Khởi tạo tài liệu HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Bước 3: Tạo tùy chọn hiển thị XPS với kích thước trang

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Bước 4: Tạo thiết bị XPS và chỉ định các tùy chọn cũng như tệp đầu ra

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Bước 5: Kết xuất HTML sang XPS

```csharp
document.RenderTo(device);
```

Ví dụ này cho thấy cách chuyển đổi HTML sang XPS với các tùy chọn hiển thị và kích thước trang tùy chỉnh.

## Kết hợp nhiều tài liệu HTML thành PDF

### Bước 1: Chuẩn bị mã HTML cho nhiều tài liệu

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Bước 2: Tạo tài liệu HTML để hợp nhất

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Bước 3: Khởi tạo Trình kết xuất HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Bước 4: Tạo thiết bị PDF cho đầu ra được hợp nhất

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Bước 5: Hợp nhất tài liệu HTML thành PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

Ví dụ này trình bày cách kết hợp nhiều tài liệu HTML thành một tệp PDF bằng cách sử dụng Aspose.HTML cho .NET.

## Đặt thời gian chờ kết xuất

### Bước 1: Chuẩn bị mã HTML bằng JavaScript

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Bước 2: Khởi tạo tài liệu HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Bước 3: Khởi tạo Trình kết xuất HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Bước 4: Tạo thiết bị PDF và đặt thời gian chờ kết xuất

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Bước 5: Kết xuất HTML thành PDF với thời gian chờ

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Ví dụ này trình bày cách đặt thời gian chờ hiển thị khi chuyển đổi HTML sang PDF, điều này có thể hữu ích khi xử lý nội dung động hoặc tập lệnh chạy dài.

## Phần kết luận

Aspose.HTML for .NET là một thư viện đa năng hỗ trợ các nhà phát triển làm việc với các tài liệu HTML một cách hiệu quả. Trong hướng dẫn này, chúng tôi đã đề cập đến nhiều ví dụ khác nhau, từ chuyển đổi HTML cơ bản sang PDF đến các tính năng nâng cao hơn như kích thước trang, độ phân giải và quyền tùy chỉnh. Bằng cách làm theo các ví dụ này, bạn có thể khai thác toàn bộ tiềm năng của Aspose.HTML cho .NET trong các ứng dụng .NET của mình.

 Nếu bạn có thắc mắc hoặc cần hỗ trợ thêm, đừng ngần ngại truy cập[Diễn đàn Aspose.HTML](https://forum.aspose.com/) để được hỗ trợ và hướng dẫn.

## Câu hỏi thường gặp

### Q1. Aspose.HTML dành cho .NET là gì?
   
Câu trả lời 1: Aspose.HTML for .NET là thư viện .NET cho phép các nhà phát triển thao tác và chuyển đổi tài liệu HTML theo chương trình. Nó cung cấp nhiều tính năng để làm việc với nội dung HTML, bao gồm HTML sang PDF, XPS và chuyển đổi hình ảnh cũng như các tùy chọn kết xuất nâng cao.

### Q2. Tôi có thể tải xuống Aspose.HTML cho .NET ở đâu?

 Câu trả lời 2: Bạn có thể tải xuống Aspose.HTML cho .NET từ[Liên kết tải xuống](https://releases.aspose.com/html/net/).

### Q3. Tôi có cần giấy phép để sử dụng Aspose.HTML cho .NET không?

Câu trả lời 3: Mặc dù bạn có thể sử dụng Aspose.HTML cho .NET mà không cần giấy phép, nhưng bạn nên lấy giấy phép sử dụng sản xuất để mở khóa tất cả các tính năng và xóa mọi hình mờ hoặc giới hạn.

### Q4. Làm cách nào tôi có thể bảo vệ các tệp PDF được tạo bằng Aspose.HTML cho .NET?

Câu trả lời 4: Bạn có thể chỉ định các quyền và cài đặt mã hóa PDF khi hiển thị HTML thành PDF bằng Aspose.HTML cho .NET. Điều này cho phép bạn kiểm soát ai có thể truy cập và sửa đổi các tệp PDF kết quả.

### Q5. Tôi có thể chuyển đổi HTML sang các định dạng khác như XPS hoặc hình ảnh không?

Câu trả lời 5: Có, Aspose.HTML for .NET hỗ trợ chuyển đổi HTML sang nhiều định dạng khác nhau, bao gồm PDF, XPS và hình ảnh (ví dụ: JPEG). Bạn có thể tùy chỉnh cài đặt chuyển đổi để đáp ứng các yêu cầu cụ thể của mình.