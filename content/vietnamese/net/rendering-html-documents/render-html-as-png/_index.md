---
title: Kết xuất HTML dưới dạng PNG trong .NET bằng Aspose.HTML
linktitle: Kết xuất HTML dưới dạng PNG trong .NET
second_title: Aspose.HTML .NET HTML thao tác API
description: Tìm hiểu cách làm việc với Aspose.HTML cho .NET. Thao tác HTML, chuyển đổi sang nhiều định dạng khác nhau và hơn thế nữa. Đi sâu vào hướng dẫn toàn diện này!
type: docs
weight: 10
url: /vi/net/rendering-html-documents/render-html-as-png/
---

Trong hướng dẫn này, chúng ta sẽ đi sâu vào thế giới của Aspose.HTML cho .NET, một công cụ mạnh mẽ để làm việc với các tài liệu HTML theo chương trình. Cho dù bạn là nhà phát triển dày dạn kinh nghiệm hay mới bắt đầu hành trình trong thế giới lập trình .NET, hướng dẫn này sẽ hướng dẫn bạn những điều cơ bản về Aspose.HTML, từ nhập vùng tên đến chia nhỏ các ví dụ thực tế.

## Giới thiệu

Aspose.HTML for .NET là một thư viện linh hoạt cho phép các nhà phát triển thao tác các tài liệu HTML một cách dễ dàng. Cho dù bạn cần chuyển đổi HTML sang các định dạng khác, trích xuất dữ liệu từ tài liệu HTML hay tạo nội dung HTML động, Aspose.HTML đều có thể đáp ứng được nhu cầu của bạn. Trong hướng dẫn này, chúng ta sẽ khám phá từng bước khả năng của nó.

## Điều kiện tiên quyết

Trước khi đi sâu vào các ví dụ về mã, bạn sẽ cần một số điều kiện tiên quyết:

1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio vì chúng tôi sẽ viết mã .NET.

2.  Aspose.HTML for .NET: Tải xuống và cài đặt thư viện Aspose.HTML for .NET từ[liên kết này](https://releases.aspose.com/html/net/) . Bạn có thể chọn giữa dùng thử miễn phí hoặc mua giấy phép[đây](https://purchase.aspose.com/buy).

3. .NET Framework hoặc .NET Core: Đảm bảo bạn đã cài đặt .NET Framework hoặc .NET Core trên máy phát triển của mình, tùy thuộc vào yêu cầu dự án của bạn.

4. Trình chỉnh sửa mã: Bạn có thể sử dụng Visual Studio hoặc bất kỳ trình soạn thảo mã nào khác mà bạn chọn.

## Nhập không gian tên

Để bắt đầu với Aspose.HTML cho .NET, trước tiên chúng ta cần nhập các vùng tên cần thiết. Mở dự án của bạn trong Visual Studio, tạo một lớp C# mới và nhập các không gian tên sau:

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;
```

Các không gian tên này cung cấp quyền truy cập vào các lớp và phương thức khác nhau cần thiết để làm việc với các tài liệu HTML theo chương trình.

## Kết xuất HTML dưới dạng PNG Ví dụ

Chúng ta hãy xem xét kỹ hơn mã ví dụ bạn đã cung cấp và chia nó thành nhiều bước:

```csharp
// Kết xuất HTML dưới dạng PNG trong .NET bằng Aspose.HTML
string dataDir = "Your Data Directory";

// Bước 1: Tạo đối tượng tài liệu HTML
using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
{
    // Bước 2: Tạo trình kết xuất HTML
    using (HtmlRenderer renderer = new HtmlRenderer())
    using (ImageDevice device = new ImageDevice(dataDir + @"document_out.png"))
    {
        // Bước 3: Kết xuất tài liệu HTML sang PNG
        renderer.Render(device, document);
    }
}
```

### Bước 1: Tạo đối tượng tài liệu HTML

 Ở bước này, chúng ta tạo một`HTMLDocument` đối tượng, đại diện cho một tài liệu HTML. Bạn có thể chuyển nội dung HTML dưới dạng chuỗi tới hàm tạo và bạn cũng có thể chỉ định đường dẫn cơ sở để phân giải các đường dẫn tương đối.

### Bước 2: Tạo Trình kết xuất HTML

 Ở đây, chúng tôi tạo ra một`HtmlRenderer` sự vật. Đây là thành phần cốt lõi chịu trách nhiệm hiển thị nội dung HTML. 

### Bước 3: Kết xuất tài liệu HTML thành PNG

 Cuối cùng, chúng tôi kết xuất tài liệu HTML thành hình ảnh PNG bằng cách sử dụng`HtmlRenderer` và một`ImageDevice` . Hình ảnh PNG thu được sẽ được lưu trong thư mục đã chỉ định`dataDir`.

## Phần kết luận

Trong hướng dẫn này, chúng tôi đã giới thiệu cho bạn về Aspose.HTML dành cho .NET và cung cấp phân tích mã ví dụ. Đây chỉ là bước khởi đầu cho những gì bạn có thể đạt được với thư viện mạnh mẽ này. Bạn có thể khám phá tài liệu mở rộng của nó[đây](https://reference.aspose.com/html/net/) và truy cập các tài nguyên và hỗ trợ bổ sung trên[diễn đàn giả định](https://forum.aspose.com/).

Nếu bạn có bất kỳ câu hỏi nào hoặc cần hỗ trợ về Aspose.HTML cho .NET, vui lòng liên hệ với cộng đồng Aspose hoặc tham khảo tài liệu để được hướng dẫn thêm.

## Câu hỏi thường gặp (FAQ)

### Aspose.HTML dành cho .NET là gì?
   Aspose.HTML for .NET là thư viện cho phép các nhà phát triển thao tác và chuyển đổi tài liệu HTML theo chương trình trong các ứng dụng .NET.

### Làm cách nào tôi có thể nhận được giấy phép tạm thời cho Aspose.HTML cho .NET?
    Bạn có thể nhận giấy phép tạm thời cho Aspose.HTML cho .NET[đây](https://purchase.aspose.com/temporary-license/).

### Tôi có thể chuyển đổi HTML sang các định dạng khác bằng Aspose.HTML cho .NET không?
   Có, Aspose.HTML for .NET cung cấp nhiều trình chuyển đổi khác nhau để chuyển đổi HTML sang các định dạng như PDF, XPS và hình ảnh.

### Có bản dùng thử miễn phí dành cho Aspose.HTML cho .NET không?
    Có, bạn có thể tải xuống bản dùng thử miễn phí Aspose.HTML cho .NET[đây](https://releases.aspose.com/).

### Tôi có thể tìm thêm hướng dẫn và tài liệu ở đâu?
   Bạn có thể khám phá tài liệu và hướng dẫn toàn diện về[Trang tài liệu Aspose.HTML cho .NET](https://reference.aspose.com/html/net/).