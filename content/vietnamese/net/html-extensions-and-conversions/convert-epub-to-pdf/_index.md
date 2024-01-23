---
title: Chuyển đổi EPUB sang PDF trong .NET bằng Aspose.HTML
linktitle: Chuyển đổi EPUB sang PDF trong .NET
second_title: Aspose.HTML .NET HTML thao tác API
description: Tìm hiểu cách chuyển đổi EPUB sang PDF bằng Aspose.HTML cho .NET. Hướng dẫn từng bước này bao gồm các tùy chọn tùy chỉnh, Câu hỏi thường gặp, v.v. để chuyển đổi tài liệu liền mạch.
type: docs
weight: 12
url: /vi/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

Trong hướng dẫn này, chúng ta sẽ khám phá cách sử dụng Aspose.HTML cho .NET để chuyển đổi tệp EPUB sang PDF. Aspose.HTML là một thư viện .NET mạnh mẽ cung cấp nhiều chức năng khác nhau để làm việc với các tài liệu HTML và EPUB. Chúng tôi sẽ đề cập đến các điều kiện tiên quyết, nhập các không gian tên cần thiết và chia nhỏ nhiều ví dụ, giải thích chi tiết từng bước.

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn có sẵn các điều kiện tiên quyết sau:

1. Aspose.HTML for .NET: Đảm bảo bạn đã cài đặt Aspose.HTML for .NET trong dự án .NET của mình. Bạn có thể tải nó xuống từ[đây](https://releases.aspose.com/html/net/).

2. Thư mục dữ liệu của bạn: Bạn sẽ cần một thư mục dữ liệu nơi lưu trữ các tệp EPUB của bạn.

Bây giờ, hãy đi sâu vào quy trình từng bước chuyển đổi EPUB sang PDF bằng Aspose.HTML cho .NET.

## Chuyển đổi EPUB sang PDF

### Bước 1: Khởi tạo dự án của bạn

Đảm bảo bạn đã thiết lập dự án .NET và cài đặt Aspose.HTML cho .NET.

### Bước 2: Nhập không gian tên bắt buộc

Trong tệp mã C# của bạn, hãy nhập các vùng tên cần thiết:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Bước 3: Mở tệp EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Tiếp tục bước tiếp theo...
}
```

-  Thay thế`"Your Data Directory"` với thư mục thực nơi chứa tệp EPUB của bạn.
- Mã này mở tệp EPUB để đọc.

### Bước 4: Đặt tùy chọn PDF và thực hiện chuyển đổi

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Tạo một thể hiện của`PdfSaveOptions` để chỉ định cài đặt chuyển đổi PDF.
-  Sử dụng`Converter.ConvertEPUB` phương pháp chuyển đổi EPUB sang PDF với các tùy chọn đã cho.
- Lưu tệp PDF kết quả dưới dạng "output.pdf."

## Chỉ định tùy chọn lưu PDF

### Bước 1: Khởi tạo dự án của bạn

Đảm bảo bạn đã thiết lập dự án .NET và cài đặt Aspose.HTML cho .NET.

### Bước 2: Nhập không gian tên bắt buộc

Nhập các không gian tên cần thiết trong mã C# của bạn:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Bước 3: Mở tệp EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Tiếp tục bước tiếp theo...
}
```

-  Thay thế`"Your Data Directory"` bằng thư mục thực tế của tệp EPUB của bạn.
- Mở tệp EPUB để đọc.

### Bước 4: Tùy chỉnh tùy chọn PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Tạo một thể hiện của`PdfSaveOptions` và tùy chỉnh nó theo yêu cầu của bạn.
- Trong ví dụ này, chúng tôi đặt kích thước trang thành chiều rộng 3000 pixel và chiều cao 1000 pixel và màu nền thành Alice Blue.

### Bước 5: Thực hiện chuyển đổi

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Sử dụng`Converter.ConvertEPUB` phương pháp chuyển đổi EPUB sang PDF với các tùy chọn tùy chỉnh.
- Lưu tệp PDF kết quả dưới dạng "output.pdf."

## Sử dụng nhà cung cấp luồng tùy chỉnh

### Bước 1: Khởi tạo dự án của bạn

Thiết lập dự án .NET và cài đặt Aspose.HTML cho .NET.

### Bước 2: Nhập không gian tên bắt buộc

Trong mã C# của bạn, hãy nhập các vùng tên cần thiết:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Bước 3: Mở tệp EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Tiếp tục bước tiếp theo...
}
```

-  Thay thế`"Your Data Directory"` bằng thư mục thực tế của tệp EPUB của bạn.
- Mở tệp EPUB để đọc.

### Bước 4: Sử dụng Nhà cung cấp luồng tùy chỉnh

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Tiếp tục bước tiếp theo...
}
```

-  Tạo một`MemoryStreamProvider` để quản lý kết quả chuyển đổi dưới dạng luồng bộ nhớ.
-  Sử dụng`Converter.ConvertEPUB` phương pháp với nhà cung cấp luồng tùy chỉnh.

### Bước 5: Lưu kết quả

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Truy cập luồng bộ nhớ chứa dữ liệu đã chuyển đổi.
- Đặt vị trí luồng về đầu.
- Tạo một tệp PDF đầu ra và sao chép nội dung từ luồng bộ nhớ vào đó.

### Mã nguồn lớp MemoryStreamProvider. 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Danh sách các đối tượng MemoryStream được tạo trong quá trình hiển thị tài liệu
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Phương thức này được gọi khi chỉ cần một luồng đầu ra, ví dụ như đối với các định dạng XPS, PDF hoặc TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Phương thức này được gọi khi cần tạo nhiều luồng đầu ra. Ví dụ: trong quá trình hiển thị HTML thành danh sách các tệp hình ảnh (JPG, PNG, v.v.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Tại đây Bạn có thể giải phóng luồng chứa đầy dữ liệu và, chẳng hạn, chuyển nó vào ổ cứng
            }
            public void Dispose()
            {
                // Giải phóng tài nguyên
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Bây giờ, bạn đã học cách chuyển đổi tệp EPUB sang PDF bằng Aspose.HTML cho .NET với nhiều tùy chọn và khả năng tùy chỉnh khác nhau. Aspose.HTML đơn giản hóa quy trình, mang lại sự linh hoạt và kiểm soát việc chuyển đổi tài liệu của bạn.

## Phần kết luận

Aspose.HTML for .NET là một công cụ linh hoạt để chuyển đổi tệp EPUB sang PDF, cung cấp các tùy chọn tùy chỉnh để điều chỉnh tài liệu PDF thu được theo nhu cầu của bạn. Cho dù bạn yêu cầu chuyển đổi đơn giản hay tùy chỉnh nâng cao, Aspose.HTML đều có thể đáp ứng được.

 Nếu chưa có, bạn có thể tải xuống Aspose.HTML for .NET từ[trang mạng](https://releases.aspose.com/html/net/) và bắt đầu sử dụng nó trong các ứng dụng .NET của bạn ngay hôm nay.

---

## Câu hỏi thường gặp

### Aspose.HTML cho .NET có được sử dụng miễn phí không?
    Aspose.HTML cho .NET là một sản phẩm thương mại nhưng có bản dùng thử miễn phí[đây](https://releases.aspose.com/).

### Tôi có thể tùy chỉnh giao diện của tệp PDF đã chuyển đổi không?
   Có, bạn có thể tùy chỉnh giao diện PDF bằng cách điều chỉnh các tùy chọn như kích thước trang và màu nền, như trong Ví dụ 2.

### Làm cách nào tôi có thể nhận được hỗ trợ cho Aspose.HTML cho .NET?
    Bạn có thể tìm thấy sự hỗ trợ và tài nguyên trên[Diễn đàn Aspose.HTML](https://forum.aspose.com/).

### Có định dạng nào khác mà tôi có thể chuyển đổi bằng Aspose.HTML cho .NET không?
   Có, Aspose.HTML for .NET hỗ trợ nhiều định dạng tài liệu khác nhau, bao gồm HTML, EPUB, v.v.

### Aspose.HTML cho ..NET có phù hợp để chuyển đổi tài liệu quy mô lớn không?
   Aspose.HTML for .NET được thiết kế để xử lý chuyển đổi tài liệu quy mô lớn một cách hiệu quả, làm cho nó phù hợp với nhiều ứng dụng.

