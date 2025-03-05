---
title: Thu thập dữ liệu web trong .NET với Aspose.HTML
linktitle: Thu thập dữ liệu web trong .NET
second_title: Aspose.HTML .NET API thao tác HTML
description: Học cách thao tác các tài liệu HTML trong .NET với Aspose.HTML. Điều hướng, lọc, truy vấn và chọn các thành phần hiệu quả để phát triển web nâng cao.
type: docs
weight: 13
url: /vi/net/advanced-features/web-scraping/
---

Trong thời đại kỹ thuật số ngày nay, việc thao tác và trích xuất thông tin từ các tài liệu HTML là một nhiệm vụ phổ biến đối với các nhà phát triển. Aspose.HTML cho .NET là một công cụ mạnh mẽ giúp đơn giản hóa việc xử lý và thao tác HTML trong các ứng dụng .NET. Trong hướng dẫn này, chúng ta sẽ khám phá nhiều khía cạnh khác nhau của Aspose.HTML cho .NET, bao gồm các điều kiện tiên quyết, không gian tên và các ví dụ từng bước để giúp bạn khai thác hết tiềm năng của nó.

## Điều kiện tiên quyết

Trước khi khám phá thế giới Aspose.HTML dành cho .NET, bạn sẽ cần một số điều kiện tiên quyết sau:

1. Môi trường phát triển: Đảm bảo bạn có môi trường phát triển đang hoạt động được thiết lập bằng Visual Studio hoặc bất kỳ IDE tương thích nào khác để phát triển .NET.

2.  Aspose.HTML cho .NET: Tải xuống và cài đặt thư viện Aspose.HTML cho .NET từ[liên kết tải xuống](https://releases.aspose.com/html/net/). Bạn có thể chọn phiên bản dùng thử miễn phí hoặc phiên bản có giấy phép tùy theo nhu cầu của mình.

3. Kiến thức cơ bản về HTML: Sự quen thuộc với cấu trúc và các thành phần HTML là điều cần thiết để sử dụng Aspose.HTML cho .NET một cách hiệu quả.

## Nhập không gian tên

Để bắt đầu, bạn cần nhập các không gian tên cần thiết vào dự án C# của mình. Các không gian tên này cung cấp quyền truy cập vào các lớp và chức năng Aspose.HTML cho .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Với các điều kiện tiên quyết đã được thiết lập và không gian tên đã được nhập, chúng ta hãy cùng phân tích từng bước một số ví dụ chính để minh họa cách sử dụng Aspose.HTML cho .NET hiệu quả.

## Điều hướng qua HTML

Trong ví dụ này, chúng ta sẽ điều hướng qua một tài liệu HTML và truy cập từng phần tử của tài liệu đó theo từng bước.

```csharp
public static void NavigateThroughHTML()
{
    // Chuẩn bị mã HTML
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Khởi tạo một tài liệu từ mã đã chuẩn bị
    using (var document = new HTMLDocument(html_code, "."))
    {
        // Lấy tham chiếu đến phần tử con đầu tiên (SPAN đầu tiên) của BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Đầu ra: Xin chào

        // Lấy tham chiếu đến khoảng trắng giữa các phần tử HTML
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Đầu ra: ''

        // Lấy tham chiếu đến phần tử SPAN thứ hai
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Đầu ra: Thế giới!
    }
}
```

 Trong ví dụ này, chúng ta tạo một tài liệu HTML, truy cập phần tử con đầu tiên của nó (a`SPAN` phần tử), khoảng trắng giữa các phần tử và phần tử thứ hai`SPAN` phần tử thể hiện khả năng điều hướng cơ bản.

## Sử dụng Bộ lọc nút

Bộ lọc nút cho phép bạn xử lý có chọn lọc các phần tử cụ thể trong tài liệu HTML.

```csharp
public static void NodeFilterUsageExample()
{
    // Chuẩn bị mã HTML
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Khởi tạo một tài liệu dựa trên mã đã chuẩn bị
    using (var document = new HTMLDocument(code, "."))
    {
        // Tạo TreeWalker với bộ lọc tùy chỉnh cho các thành phần hình ảnh
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Đầu ra: image1.png
                // Đầu ra: image2.png
            }
        }
    }
}
```

 Ví dụ này trình bày cách sử dụng bộ lọc nút tùy chỉnh để trích xuất các phần tử cụ thể (trong trường hợp này,`IMG` các phần tử) từ tài liệu HTML.

## Truy vấn XPath

Truy vấn XPath cho phép bạn tìm kiếm các phần tử trong tài liệu HTML dựa trên các tiêu chí cụ thể.

```csharp
public static void XPathQueryUsageExample()
{
    // Chuẩn bị mã HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    // Khởi tạo một tài liệu dựa trên mã đã chuẩn bị
    using (var document = new HTMLDocument(code, "."))
    {
        // Đánh giá biểu thức XPath để chọn các phần tử cụ thể
        var result = document.Evaluate("//*[@class='hạnh phúc']//khoảng cách",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Lặp lại các nút kết quả
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Đầu ra: Xin chào
            // Đầu ra: Thế giới!
        }
    }
}
```

Ví dụ này giới thiệu cách sử dụng truy vấn XPath để xác định vị trí các phần tử trong tài liệu HTML dựa trên thuộc tính và cấu trúc của chúng.

## Bộ chọn CSS

Bộ chọn CSS cung cấp một cách thay thế để chọn các phần tử trong tài liệu HTML, tương tự như cách các bảng định kiểu CSS nhắm mục tiêu vào các phần tử.

```csharp
public static void CSSSelectorUsageExample()
{
    // Chuẩn bị mã HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    // Khởi tạo một tài liệu dựa trên mã đã chuẩn bị
    using (var document = new HTMLDocument(code, "."))
    {
        //Sử dụng bộ chọn CSS để trích xuất các thành phần dựa trên lớp và phân cấp
        var elements = document.QuerySelectorAll(".happy span");
        
        // Lặp lại danh sách các phần tử đã tạo
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Đầu ra: Xin chào
            // Đầu ra: Thế giới!
        }
    }
}
```

Ở đây, chúng tôi sẽ trình bày cách sử dụng bộ chọn CSS để nhắm mục tiêu vào các phần tử cụ thể trong tài liệu HTML.

Với những ví dụ này, bạn đã có được hiểu biết cơ bản về cách điều hướng, lọc, truy vấn và chọn các phần tử trong tài liệu HTML bằng Aspose.HTML cho .NET.

## Phần kết luận

 Aspose.HTML for .NET là một thư viện đa năng giúp các nhà phát triển .NET làm việc hiệu quả với các tài liệu HTML. Với các tính năng mạnh mẽ để điều hướng, lọc, truy vấn và chọn các thành phần, bạn có thể xử lý nhiều tác vụ xử lý HTML một cách liền mạch. Bằng cách làm theo hướng dẫn này và khám phá tài liệu tại[Tài liệu Aspose.HTML cho .NET](https://reference.aspose.com/html/net/), bạn có thể khai thác toàn bộ tiềm năng của công cụ này cho các ứng dụng .NET của mình.

## Câu hỏi thường gặp

### Câu hỏi 1. Aspose.HTML cho .NET có miễn phí không?

A1: Aspose.HTML cho .NET cung cấp phiên bản dùng thử miễn phí, nhưng để sử dụng cho mục đích sản xuất, bạn sẽ cần mua giấy phép. Bạn có thể tìm thấy thông tin chi tiết và tùy chọn cấp phép tại[Mua Aspose.HTML](https://purchase.aspose.com/buy).

### Câu hỏi 2. Làm thế nào tôi có thể nhận được giấy phép tạm thời cho Aspose.HTML dành cho .NET?

 A2: Bạn có thể xin giấy phép tạm thời cho mục đích thử nghiệm từ[Giấy phép tạm thời Aspose.HTML](https://purchase.aspose.com/temporary-license/).

### Câu hỏi 3. Tôi có thể tìm kiếm sự trợ giúp hoặc hỗ trợ cho Aspose.HTML dành cho .NET ở đâu?

 A3: Nếu bạn gặp bất kỳ vấn đề hoặc có thắc mắc nào, bạn có thể truy cập[Diễn đàn Aspose.HTML](https://forum.aspose.com/) để được hỗ trợ và giúp đỡ cộng đồng.

### Câu hỏi 4. Có tài nguyên bổ sung nào để học Aspose.HTML cho .NET không?

 A4: Cùng với hướng dẫn này, bạn có thể khám phá thêm các hướng dẫn và tài liệu về[Trang tài liệu Aspose.HTML cho .NET](https://reference.aspose.com/html/net/).

### Câu hỏi 5. Aspose.HTML cho .NET có tương thích với các phiên bản .NET mới nhất không?

A5: Aspose.HTML cho .NET được cập nhật thường xuyên để đảm bảo khả năng tương thích với các phiên bản và công nghệ .NET mới nhất.