---
title: Tạo một tài liệu trong .NET với Aspose.HTML
linktitle: Tạo một tài liệu trong .NET
second_title: Aspose.HTML .NET API thao tác HTML
description: Giải phóng sức mạnh của Aspose.HTML cho .NET. Học cách tạo, thao tác và tối ưu hóa tài liệu HTML và SVG một cách dễ dàng. Khám phá các ví dụ từng bước và câu hỏi thường gặp.
weight: 14
url: /vi/net/html-document-manipulation/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo một tài liệu trong .NET với Aspose.HTML


Trong thế giới phát triển web không ngừng thay đổi, việc đi trước một bước là điều cần thiết. Aspose.HTML cho .NET cung cấp cho các nhà phát triển một bộ công cụ mạnh mẽ để làm việc với các tài liệu HTML. Cho dù bạn đang bắt đầu từ đầu, tải từ tệp, kéo từ URL hay xử lý các tài liệu SVG, thư viện này cung cấp tính linh hoạt mà bạn cần.

Trong hướng dẫn từng bước này, chúng tôi sẽ đi sâu vào những điều cơ bản khi sử dụng Aspose.HTML cho .NET, đảm bảo bạn được trang bị đầy đủ để sử dụng công cụ mạnh mẽ này trong các dự án phát triển web của mình. Trước khi đi sâu vào chi tiết, chúng ta hãy xem qua các điều kiện tiên quyết và không gian tên cần thiết để bắt đầu hành trình của bạn.

## Điều kiện tiên quyết

Để thực hiện thành công hướng dẫn này và khai thác sức mạnh của Aspose.HTML cho .NET, bạn sẽ cần những điều kiện tiên quyết sau:

- Máy tính chạy Windows có cài đặt .NET Framework hoặc .NET Core.
- Một trình soạn thảo mã như Visual Studio.
- Kiến thức cơ bản về lập trình C#.

Bây giờ bạn đã có đủ điều kiện tiên quyết, chúng ta hãy bắt đầu nhé.

## Nhập không gian tên

Trước khi bạn bắt đầu sử dụng Aspose.HTML cho .NET, bạn cần nhập các không gian tên cần thiết. Các không gian tên này chứa các lớp và phương thức quan trọng để làm việc với các tài liệu HTML. Dưới đây là danh sách các không gian tên bạn nên nhập:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Sau khi nhập các không gian tên này, giờ bạn đã sẵn sàng để xem các ví dụ từng bước.

## Tạo một tài liệu HTML từ đầu

### Bước 1: Khởi tạo một tài liệu HTML trống

```csharp
// Khởi tạo một tài liệu HTML trống.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Tạo một phần tử văn bản và thêm nó vào tài liệu
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Lưu tài liệu vào đĩa.
    document.Save("document.html");
}
```

Trong ví dụ này, chúng ta bắt đầu bằng cách tạo một tài liệu HTML trống và thêm văn bản "Hello World!" vào đó. Sau đó, chúng ta lưu tài liệu vào một tệp.

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

Ở đây, chúng ta chuẩn bị một tệp có nội dung "Hello World!" rồi tải nó dưới dạng tài liệu HTML. Chúng ta in nội dung của tài liệu vào bảng điều khiển.

## Tạo một tài liệu HTML từ một URL

### Bước 1: Tải tài liệu từ trang web

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Ghi nội dung tài liệu vào luồng đầu ra.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Trong ví dụ này, chúng tôi tải một tài liệu HTML trực tiếp từ một trang web và hiển thị nội dung của nó.

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

Ở đây, chúng ta tạo một tài liệu HTML từ một biến chuỗi và lưu nó vào một tệp.

## Tạo một tài liệu HTML từ MemoryStream

### Bước 1: Tạo một đối tượng luồng bộ nhớ

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

Trong ví dụ này, chúng ta tạo một tài liệu HTML từ luồng bộ nhớ và lưu nó vào một tệp.

## Làm việc với Tài liệu SVG

### Bước 1: Khởi tạo Tài liệu SVG từ một chuỗi

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Ghi nội dung tài liệu vào luồng đầu ra.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Ở đây, chúng ta tạo và hiển thị một tài liệu SVG từ một chuỗi.

## Tải một tài liệu HTML không đồng bộ

### Bước 1: Tạo phiên bản của Tài liệu HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Bước 2: Đăng ký sự kiện 'ReadyStateChange'

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // Kiểm tra giá trị của thuộc tính 'ReadyState'.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Bước 3: Điều hướng không đồng bộ tại Uri đã chỉ định

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Trong ví dụ này, chúng tôi tải một tài liệu HTML không đồng bộ và xử lý sự kiện 'ReadyStateChange' để hiển thị nội dung khi quá trình tải hoàn tất.

## Xử lý sự kiện 'OnLoad'

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

### Bước 3: Điều hướng không đồng bộ tại Uri đã chỉ định

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Ví dụ này minh họa cách tải một tài liệu HTML không đồng bộ và xử lý sự kiện 'OnLoad' để hiển thị nội dung sau khi hoàn tất.

## Kết luận

Trong thế giới năng động của phát triển web, việc có các công cụ phù hợp là rất quan trọng. Aspose.HTML for .NET trang bị cho bạn các phương tiện để tạo, thao tác và xử lý các tài liệu HTML và SVG một cách hiệu quả. Hướng dẫn toàn diện này đã hướng dẫn bạn những điều cần thiết, đảm bảo rằng bạn có thể khai thác sức mạnh của Aspose.HTML for .NET trong các dự án của mình.

## Câu hỏi thường gặp

### Câu hỏi 1: Aspose.HTML dành cho .NET là gì?

A1: Aspose.HTML for .NET là một thư viện .NET mạnh mẽ cho phép các nhà phát triển làm việc với các tài liệu HTML và SVG. Nó cung cấp nhiều tính năng, từ việc tạo tài liệu từ đầu đến phân tích và xử lý các tệp HTML và SVG hiện có.

### Câu hỏi 2: Tôi có thể sử dụng Aspose.HTML cho .NET với .NET Core không?

A2: Có, Aspose.HTML cho .NET tương thích với cả .NET Framework và .NET Core, khiến nó trở thành lựa chọn linh hoạt cho các ứng dụng .NET hiện đại.

### Câu hỏi 3: Aspose.HTML cho .NET có phù hợp để thu thập và phân tích dữ liệu web không?

A3: Chắc chắn rồi! Aspose.HTML cho .NET là lựa chọn tuyệt vời cho các tác vụ trích xuất và phân tích web, nhờ khả năng tải các tài liệu HTML từ URL và chuỗi. Bạn có thể trích xuất dữ liệu, thực hiện phân tích và nhiều hơn nữa.

### Câu hỏi 4: Làm thế nào tôi có thể truy cập hỗ trợ cho Aspose.HTML dành cho .NET?

 A4: Nếu bạn gặp bất kỳ vấn đề hoặc có thắc mắc nào khi sử dụng Aspose.HTML cho .NET, bạn có thể truy cập[Diễn đàn Aspose](https://forum.aspose.com/) để được hỗ trợ và giúp đỡ từ cộng đồng và các chuyên gia của Aspose.

### A5: Tôi có thể tìm tài liệu chi tiết và tùy chọn tải xuống ở đâu?

A5: Để biết tài liệu đầy đủ và quyền truy cập vào các tùy chọn tải xuống, bạn có thể tham khảo các liên kết sau:

- [Tài liệu](https://reference.aspose.com/html/net/)
- [Tải về](https://releases.aspose.com/html/net/)
- [Mua](https://purchase.aspose.com/buy)
- [Dùng thử miễn phí](https://releases.aspose.com/)
- [Giấy phép tạm thời](https://purchase.aspose.com/temporary-license/)
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
