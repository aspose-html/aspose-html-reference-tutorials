---
title: Tạo một tài liệu trong .NET bằng Aspose.HTML
linktitle: Tạo một tài liệu trong .NET
second_title: Aspose.HTML .NET HTML thao tác API
description: Giải phóng sức mạnh của Aspose.HTML cho .NET. Tìm hiểu cách tạo, thao tác và tối ưu hóa tài liệu HTML và SVG một cách dễ dàng. Khám phá các ví dụ và câu hỏi thường gặp từng bước.
type: docs
weight: 14
url: /vi/net/html-document-manipulation/creating-a-document/
---

Trong thế giới phát triển web không ngừng phát triển, việc đón đầu xu hướng là điều cần thiết. Aspose.HTML for .NET cung cấp cho các nhà phát triển một bộ công cụ mạnh mẽ để làm việc với các tài liệu HTML. Cho dù bạn đang bắt đầu từ đầu, tải từ tệp, lấy từ URL hay xử lý tài liệu SVG, thư viện này đều mang lại tính linh hoạt mà bạn cần.

Trong hướng dẫn từng bước này, chúng tôi sẽ đi sâu vào các nguyên tắc cơ bản của việc sử dụng Aspose.HTML cho .NET, đảm bảo bạn được trang bị tốt để sử dụng công cụ mạnh mẽ này trong các dự án phát triển web của mình. Trước khi đi sâu vào chi tiết, hãy xem qua các điều kiện tiên quyết và vùng chứa tên cần thiết để bắt đầu hành trình của bạn.

## Điều kiện tiên quyết

Để thực hiện thành công hướng dẫn này và khai thác sức mạnh của Aspose.HTML cho .NET, bạn sẽ cần những điều kiện tiên quyết sau:

- Máy Windows có cài đặt .NET Framework hoặc .NET Core.
- Một trình soạn thảo mã như Visual Studio.
- Kiến thức cơ bản về lập trình C#.

Bây giờ bạn đã có sẵn các điều kiện tiên quyết, hãy bắt đầu.

## Nhập không gian tên

Trước khi bắt đầu sử dụng Aspose.HTML cho .NET, bạn cần nhập các vùng tên cần thiết. Các không gian tên này chứa các lớp và phương thức quan trọng để làm việc với tài liệu HTML. Dưới đây là danh sách các không gian tên bạn nên nhập:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Với các không gian tên này đã được nhập, giờ đây bạn đã sẵn sàng đi sâu vào các ví dụ từng bước.

## Tạo một tài liệu HTML từ đầu

### Bước 1: Khởi tạo một tài liệu HTML trống

```csharp
// Khởi tạo một tài liệu HTML trống.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Tạo một thành phần văn bản và thêm nó vào tài liệu
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Lưu tài liệu vào đĩa.
    document.Save("document.html");
}
```

Trong ví dụ này, chúng tôi bắt đầu bằng cách tạo một tài liệu HTML trống và thêm dòng "Xin chào thế giới!" nhắn tin cho nó. Sau đó chúng tôi lưu tài liệu vào một tập tin.

## Tạo một tài liệu HTML từ một tập tin

### Bước 1: Chuẩn bị tệp 'document.html'

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Bước 2: Tải từ tệp 'document.html'

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Ghi nội dung tài liệu vào luồng đầu ra.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Ở đây, chúng tôi chuẩn bị một tệp có "Xin chào thế giới!" nội dung và sau đó tải nó dưới dạng tài liệu HTML. Chúng tôi in nội dung của tài liệu ra bàn điều khiển.

## Tạo một tài liệu HTML từ một URL

### Bước 1: Tải tài liệu từ một trang web

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Ghi nội dung tài liệu vào luồng đầu ra.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Trong ví dụ này, chúng tôi tải tài liệu HTML trực tiếp từ một trang web và hiển thị nội dung của nó.

## Tạo một tài liệu HTML từ một chuỗi

### Bước 1: Chuẩn bị mã HTML

```csharp
var html_code = "<p>Hello World!</p>";
```

### Bước 2: Khởi tạo tài liệu từ biến chuỗi

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Lưu tài liệu vào đĩa.
    document.Save("document.html");
}
```

Ở đây, chúng tôi tạo một tài liệu HTML từ một biến chuỗi và lưu nó vào một tệp.

## Tạo tài liệu HTML từ MemoryStream

### Bước 1: Tạo đối tượng luồng bộ nhớ

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Viết mã HTML vào đối tượng bộ nhớ
    sw.Write("<p>Hello World!</p>");
    // Đặt vị trí ở đầu
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Khởi tạo tài liệu từ luồng bộ nhớ
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Lưu tài liệu vào đĩa.
        document.Save("document.html");
    }
}
```

Trong ví dụ này, chúng tôi tạo một tài liệu HTML từ luồng bộ nhớ và lưu nó vào một tệp.

## Làm việc với tài liệu SVG

### Bước 1: Khởi tạo Tài liệu SVG từ một chuỗi

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Ghi nội dung tài liệu vào luồng đầu ra.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Ở đây, chúng tôi tạo và hiển thị tài liệu SVG từ một chuỗi.

## Tải tài liệu HTML không đồng bộ

### Bước 1: Tạo phiên bản của Tài liệu HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Bước 2: Đăng ký sự kiện 'ReadyStateChange'

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //Kiểm tra giá trị của thuộc tính 'ReadyState'.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Bước 3: Điều hướng không đồng bộ tại Uri được chỉ định

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Trong ví dụ này, chúng tôi tải tài liệu HTML không đồng bộ và xử lý sự kiện 'ReadyStateChange' để hiển thị nội dung khi quá trình tải hoàn tất.

## Xử lý sự kiện 'Đang tải'

### Bước 1: Tạo phiên bản của Tài liệu HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Bước 2: Đăng ký sự kiện 'OnLoad'

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Bước 3: Điều hướng không đồng bộ tại Uri được chỉ định

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Ví dụ này minh họa việc tải tài liệu HTML một cách không đồng bộ và xử lý sự kiện 'Đang tải' để hiển thị nội dung sau khi hoàn thành.

## Tóm lại là

Trong thế giới phát triển web năng động, việc có sẵn các công cụ phù hợp là điều vô cùng quan trọng. Aspose.HTML for .NET trang bị cho bạn các phương tiện để tạo, thao tác và xử lý tài liệu HTML và SVG một cách hiệu quả. Hướng dẫn toàn diện này đã hướng dẫn bạn những điều cần thiết, đảm bảo rằng bạn có thể khai thác sức mạnh của Aspose.HTML cho .NET trong các dự án của mình.

## Câu hỏi thường gặp

### Câu hỏi 1: Aspose.HTML dành cho .NET là gì?

Câu trả lời 1: Aspose.HTML for .NET là một thư viện .NET mạnh mẽ cho phép các nhà phát triển làm việc với các tài liệu HTML và SVG. Nó cung cấp nhiều tính năng, từ tạo tài liệu từ đầu đến phân tích cú pháp và thao tác với các tệp HTML và SVG hiện có.

### Câu hỏi 2: Tôi có thể sử dụng Aspose.HTML cho .NET với .NET Core không?

Câu trả lời 2: Có, Aspose.HTML cho .NET tương thích với cả .NET Framework và .NET Core, khiến nó trở thành lựa chọn linh hoạt cho các ứng dụng .NET hiện đại.

### Câu hỏi 3: Aspose.HTML dành cho .NET có phù hợp để quét và phân tích cú pháp web không?

A3: Chắc chắn rồi! Aspose.HTML for .NET là một lựa chọn tuyệt vời cho các tác vụ quét và phân tích cú pháp web, nhờ khả năng tải tài liệu HTML từ URL và chuỗi. Bạn có thể trích xuất dữ liệu, thực hiện phân tích và hơn thế nữa.

### Câu hỏi 4: Làm cách nào tôi có thể truy cập hỗ trợ cho Aspose.HTML cho .NET?

 Câu trả lời 4: Nếu bạn gặp bất kỳ sự cố nào hoặc có thắc mắc khi sử dụng Aspose.HTML cho .NET, bạn có thể truy cập[Diễn đàn Aspose](https://forum.aspose.com/) để nhận được sự hỗ trợ và giúp đỡ từ cộng đồng và các chuyên gia Aspose.

### Câu trả lời 5: Tôi có thể tìm tài liệu chi tiết và các tùy chọn tải xuống ở đâu?

Câu trả lời 5: Để có tài liệu đầy đủ và quyền truy cập vào các tùy chọn tải xuống, bạn có thể tham khảo các liên kết sau:

- [Tài liệu](https://reference.aspose.com/html/net/)
- [Tải xuống](https://releases.aspose.com/html/net/)
- [Mua](https://purchase.aspose.com/buy)
- [Dùng thử miễn phí](https://releases.aspose.com/)
- [Giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)