---
title: Chuyển đổi EPUB sang XPS trong .NET với Aspose.HTML
linktitle: Chuyển đổi EPUB sang XPS trong .NET
second_title: Aspose.HTML .NET API thao tác HTML
description: Tìm hiểu cách chuyển đổi EPUB sang XPS trong .NET bằng Aspose.HTML cho .NET. Làm theo hướng dẫn từng bước của chúng tôi để chuyển đổi dễ dàng.
type: docs
weight: 13
url: /vi/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Bạn đang tìm kiếm một cách liền mạch để chuyển đổi các tệp EPUB sang định dạng XPS trong các ứng dụng .NET của mình? Aspose.HTML cho .NET cung cấp một giải pháp mạnh mẽ để đạt được điều này một cách dễ dàng. Trong hướng dẫn từng bước này, chúng tôi sẽ hướng dẫn bạn quy trình chuyển đổi EPUB sang XPS bằng Aspose.HTML. Hãy bắt đầu nào!

## Điều kiện tiên quyết

Trước khi bắt đầu quá trình chuyển đổi EPUB sang XPS, bạn cần đảm bảo rằng mình đã đáp ứng đủ các điều kiện tiên quyết sau:

### 1. Aspose.HTML cho thư viện .NET

 Hãy đảm bảo bạn đã cài đặt thư viện Aspose.HTML cho .NET trong dự án của mình. Nếu bạn chưa làm như vậy, bạn có thể lấy nó từ[Trang tải xuống Aspose.HTML cho .NET](https://releases.aspose.com/html/net/).

### 2. Nhập tệp EPUB

Bạn sẽ cần một tệp EPUB mà bạn muốn chuyển đổi sang XPS. Đảm bảo rằng bạn có tệp EPUB để chuyển đổi.

### 3. Môi trường phát triển .NET

Hướng dẫn này giả định rằng bạn đã thiết lập xong môi trường phát triển .NET trên máy của mình.

## Nhập không gian tên

Để bắt đầu, bạn nên nhập không gian tên cần thiết cho Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Chuyển đổi EPUB sang XPS

Chúng ta hãy chia nhỏ quá trình chuyển đổi tệp EPUB sang định dạng XPS thành nhiều bước.

### Bước 1.1: Mở tệp EPUB

Đầu tiên, hãy mở tệp EPUB hiện có để đọc bằng FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Tiếp tục quá trình chuyển đổi
}
```

### Bước 1.2: Tạo XpsSaveOptions

Tạo một phiên bản của XpsSaveOptions. Bước này rất quan trọng để cấu hình đầu ra XPS:

```csharp
var options = new XpsSaveOptions();
```

### Bước 1.3: Chuyển đổi EPUB sang XPS

Bây giờ, hãy gọi phương thức ConvertEPUB để chuyển đổi EPUB sang XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Chỉ định Tùy chọn XPS Tùy chỉnh

Bạn có thể tùy chỉnh thêm đầu ra XPS bằng cách chỉ định các tùy chọn tùy chỉnh như kích thước trang và màu nền.

### Bước 2.1: Tùy chỉnh kích thước trang và màu nền

Tạo một phiên bản XpsSaveOptions với kích thước trang và màu nền tùy chỉnh:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Bước 2.2: Chuyển đổi EPUB sang XPS với Tùy chọn tùy chỉnh

Bây giờ, hãy gọi phương thức ConvertEPUB để chuyển đổi EPUB sang XPS với các tùy chọn tùy chỉnh:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Sử dụng Nhà cung cấp luồng tùy chỉnh

Ở bước này, chúng ta sẽ chuyển đổi EPUB sang XPS bằng cách sử dụng nhà cung cấp luồng tùy chỉnh, cho phép bạn thao tác với dữ liệu kết quả.

### Bước 3.1: Tạo MemoryStreamProvider

Tạo một thể hiện của MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Tiếp tục quá trình chuyển đổi
}
```

### Bước 3.2: Chuyển đổi EPUB sang XPS bằng Stream Provider

Chuyển đổi EPUB sang XPS bằng cách sử dụng MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Bước 3.3: Truy cập và lưu kết quả

Truy xuất luồng bộ nhớ chứa dữ liệu đã chuyển đổi và lưu vào tệp đầu ra:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Mã nguồn của lớp MemoryStreamProvider

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Danh sách các đối tượng MemoryStream được tạo trong quá trình kết xuất tài liệu
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Phương pháp này được gọi khi chỉ cần một luồng đầu ra, ví dụ như đối với các định dạng XPS, PDF hoặc TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Phương pháp này được gọi khi cần tạo nhiều luồng đầu ra. Ví dụ trong quá trình kết xuất HTML thành danh sách các tệp hình ảnh (JPG, PNG, v.v.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Tại đây bạn có thể giải phóng luồng dữ liệu và, ví dụ, xóa nó vào ổ cứng
            }
            public void Dispose()
            {
                // Giải phóng tài nguyên
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Xin chúc mừng! Bạn đã chuyển đổi thành công tệp EPUB sang định dạng XPS bằng Aspose.HTML cho .NET.

## Phần kết luận

Trong hướng dẫn toàn diện này, chúng tôi đã khám phá cách tận dụng Aspose.HTML cho .NET để chuyển đổi tệp EPUB sang định dạng XPS với nhiều tùy chọn tùy chỉnh khác nhau. Cho dù bạn là nhà phát triển dày dạn kinh nghiệm hay mới bắt đầu, Aspose.HTML đều đơn giản hóa quy trình, cho phép bạn xử lý chuyển đổi EPUB sang XPS một cách dễ dàng.

 Có bất kỳ câu hỏi hoặc gặp phải vấn đề nào không? Kiểm tra[Tài liệu Aspose.HTML](https://reference.aspose.com/html/net/) để có thêm hiểu biết sâu sắc hoặc tìm kiếm sự giúp đỡ từ[Diễn đàn cộng đồng Aspose.HTML](https://forum.aspose.com/).

## Những câu hỏi thường gặp

### Aspose.HTML dành cho .NET là gì?
Aspose.HTML for .NET là một thư viện mạnh mẽ cho phép các nhà phát triển làm việc với các tài liệu HTML, EPUB và XPS trong các ứng dụng .NET.

### Tôi có thể tải Aspose.HTML cho .NET ở đâu?
 Bạn có thể tải xuống Aspose.HTML cho .NET từ[trang tải xuống](https://releases.aspose.com/html/net/).

### Có bản dùng thử miễn phí Aspose.HTML cho .NET không?
 Có, bạn có thể nhận được bản dùng thử miễn phí từ[đây](https://releases.aspose.com/).

### Làm thế nào tôi có thể xin được giấy phép tạm thời cho Aspose.HTML dành cho .NET?
 Để có được giấy phép tạm thời, hãy truy cập[trang giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).

### Tôi có thể tìm thêm hướng dẫn và tài liệu về Aspose.HTML cho .NET ở đâu?
 Khám phá nhiều hướng dẫn và tài liệu chi tiết về[Tài liệu Aspose.HTML](https://reference.aspose.com/html/net/) trang.