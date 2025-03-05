---
title: Kết xuất HTML dưới dạng PNG trong .NET với Aspose.HTML
linktitle: Hiển thị HTML dưới dạng PNG trong .NET
second_title: Aspose.HTML .NET API thao tác HTML
description: Học cách làm việc với Aspose.HTML cho .NET. Thao tác HTML, chuyển đổi sang nhiều định dạng khác nhau và hơn thế nữa. Khám phá hướng dẫn toàn diện này!
type: docs
weight: 10
url: /vi/net/rendering-html-documents/render-html-as-png/
---

Trong hướng dẫn này, chúng ta sẽ đi sâu vào thế giới của Aspose.HTML cho .NET, một công cụ mạnh mẽ để làm việc với các tài liệu HTML theo chương trình. Cho dù bạn là một nhà phát triển dày dạn kinh nghiệm hay chỉ mới bắt đầu hành trình của mình trong thế giới lập trình .NET, hướng dẫn này sẽ hướng dẫn bạn qua các yếu tố cần thiết của Aspose.HTML, từ việc nhập không gian tên đến việc phân tích các ví dụ thực tế.

## Giới thiệu

Aspose.HTML for .NET là một thư viện đa năng cho phép các nhà phát triển dễ dàng thao tác các tài liệu HTML. Cho dù bạn cần chuyển đổi HTML sang các định dạng khác, trích xuất dữ liệu từ các tài liệu HTML hay tạo nội dung HTML động, Aspose.HTML đều có thể đáp ứng nhu cầu của bạn. Trong hướng dẫn này, chúng ta sẽ khám phá từng bước các khả năng của nó.

## Điều kiện tiên quyết

Trước khi đi sâu vào các ví dụ mã, bạn sẽ cần một số điều kiện tiên quyết:

1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio vì chúng ta sẽ viết mã .NET.

2.  Aspose.HTML cho .NET: Tải xuống và cài đặt thư viện Aspose.HTML cho .NET từ[liên kết này](https://releases.aspose.com/html/net/) . Bạn có thể lựa chọn giữa bản dùng thử miễn phí hoặc mua giấy phép[đây](https://purchase.aspose.com/buy).

3. .NET Framework hoặc .NET Core: Đảm bảo rằng bạn đã cài đặt .NET Framework hoặc .NET Core trên máy phát triển của mình, tùy thuộc vào yêu cầu của dự án.

4. Trình soạn thảo mã: Bạn có thể sử dụng Visual Studio hoặc bất kỳ trình soạn thảo mã nào khác mà bạn chọn.

## Nhập không gian tên

Để bắt đầu với Aspose.HTML cho .NET, trước tiên chúng ta cần nhập các không gian tên cần thiết. Mở dự án của bạn trong Visual Studio, tạo một lớp C# mới và nhập các không gian tên sau:

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;
```

Các không gian tên này cung cấp quyền truy cập vào nhiều lớp và phương thức khác nhau cần thiết để làm việc với các tài liệu HTML theo cách lập trình.

## Ví dụ về kết xuất HTML dưới dạng PNG

Chúng ta hãy xem xét kỹ hơn ví dụ mã mà bạn cung cấp và chia nhỏ nó thành nhiều bước:

```csharp
// Kết xuất HTML dưới dạng PNG trong .NET với Aspose.HTML
string dataDir = "Your Data Directory";

// Bước 1: Tạo một đối tượng tài liệu HTML
using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
{
    // Bước 2: Tạo trình kết xuất HTML
    using (HtmlRenderer renderer = new HtmlRenderer())
    using (ImageDevice device = new ImageDevice(dataDir + @"document_out.png"))
    {
        // Bước 3: Kết xuất tài liệu HTML thành PNG
        renderer.Render(device, document);
    }
}
```

### Bước 1: Tạo một đối tượng tài liệu HTML

 Trong bước này, chúng tôi tạo ra một`HTMLDocument` đối tượng, biểu diễn một tài liệu HTML. Bạn có thể truyền nội dung HTML dưới dạng chuỗi cho hàm tạo và bạn cũng có thể chỉ định đường dẫn cơ sở để giải quyết các đường dẫn tương đối.

### Bước 2: Tạo một trình kết xuất HTML

 Ở đây, chúng tôi tạo ra một`HtmlRenderer` đối tượng. Đây là thành phần cốt lõi chịu trách nhiệm hiển thị nội dung HTML. 

### Bước 3: Kết xuất tài liệu HTML thành PNG

 Cuối cùng, chúng tôi kết xuất tài liệu HTML thành hình ảnh PNG bằng cách sử dụng`HtmlRenderer` và một`ImageDevice` . Hình ảnh PNG kết quả sẽ được lưu trong thư mục đã chỉ định`dataDir`.

## Phần kết luận

Trong hướng dẫn này, chúng tôi đã giới thiệu cho bạn Aspose.HTML cho .NET và cung cấp một bản phân tích mã ví dụ. Đây chỉ là khởi đầu cho những gì bạn có thể thực hiện với thư viện mạnh mẽ này. Bạn có thể khám phá tài liệu mở rộng của nó[đây](https://reference.aspose.com/html/net/) và truy cập các nguồn lực bổ sung và hỗ trợ trên[Diễn đàn Aspose](https://forum.aspose.com/).

Nếu bạn có bất kỳ câu hỏi nào hoặc cần trợ giúp về Aspose.HTML cho .NET, hãy liên hệ với cộng đồng Aspose hoặc tham khảo tài liệu để được hướng dẫn thêm.

## Những câu hỏi thường gặp (FAQ)

### Aspose.HTML dành cho .NET là gì?
   Aspose.HTML for .NET là một thư viện cho phép các nhà phát triển thao tác và chuyển đổi các tài liệu HTML theo chương trình trong các ứng dụng .NET.

### Làm thế nào tôi có thể xin được giấy phép tạm thời cho Aspose.HTML dành cho .NET?
    Bạn có thể nhận được giấy phép tạm thời cho Aspose.HTML cho .NET[đây](https://purchase.aspose.com/temporary-license/).

### Tôi có thể chuyển đổi HTML sang các định dạng khác bằng Aspose.HTML cho .NET không?
   Có, Aspose.HTML cho .NET cung cấp nhiều bộ chuyển đổi khác nhau để chuyển đổi HTML sang các định dạng như PDF, XPS và hình ảnh.

### Có bản dùng thử miễn phí Aspose.HTML cho .NET không?
    Có, bạn có thể tải xuống bản dùng thử miễn phí của Aspose.HTML cho .NET[đây](https://releases.aspose.com/).

### Tôi có thể tìm thêm hướng dẫn và tài liệu ở đâu?
   Bạn có thể khám phá tài liệu và hướng dẫn toàn diện về[Trang tài liệu Aspose.HTML cho .NET](https://reference.aspose.com/html/net/).