---
title: Quét web trong .NET bằng Aspose.HTML
linktitle: Quét web trong .NET
second_title: Aspose.HTML .NET HTML thao tác API
description: Tìm hiểu cách thao tác với tài liệu HTML trong .NET bằng Aspose.HTML. Điều hướng, lọc, truy vấn và chọn các phần tử một cách hiệu quả để nâng cao khả năng phát triển web.
type: docs
weight: 13
url: /vi/net/advanced-features/web-scraping/
---

Trong thời đại kỹ thuật số ngày nay, việc thao tác và trích xuất thông tin từ tài liệu HTML là nhiệm vụ chung của các nhà phát triển. Aspose.HTML for .NET là một công cụ mạnh mẽ giúp đơn giản hóa việc xử lý và thao tác HTML trong các ứng dụng .NET. Trong hướng dẫn này, chúng ta sẽ khám phá các khía cạnh khác nhau của Aspose.HTML dành cho .NET, bao gồm các điều kiện tiên quyết, không gian tên và ví dụ từng bước để giúp bạn khai thác toàn bộ tiềm năng của nó.

## Điều kiện tiên quyết

Trước khi đi sâu vào thế giới Aspose.HTML cho .NET, bạn sẽ cần một số điều kiện tiên quyết:

1. Môi trường phát triển: Đảm bảo bạn có môi trường phát triển hoạt động được thiết lập với Visual Studio hoặc bất kỳ IDE tương thích nào khác để phát triển .NET.

2.  Aspose.HTML for .NET: Tải xuống và cài đặt thư viện Aspose.HTML for .NET từ[Liên kết tải xuống](https://releases.aspose.com/html/net/). Bạn có thể chọn giữa phiên bản dùng thử miễn phí hoặc phiên bản được cấp phép dựa trên nhu cầu của bạn.

3. Kiến thức cơ bản về HTML: Làm quen với cấu trúc và các phần tử HTML là điều cần thiết để sử dụng Aspose.HTML cho .NET một cách hiệu quả.

## Nhập không gian tên

Để bắt đầu, bạn cần nhập các vùng tên cần thiết vào dự án C# của mình. Các không gian tên này cung cấp quyền truy cập vào Aspose.HTML cho các lớp và chức năng .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Với các điều kiện tiên quyết đã có và các không gian tên đã được nhập, chúng ta hãy chia nhỏ từng bước một số ví dụ chính để minh họa cách sử dụng Aspose.HTML cho .NET một cách hiệu quả.

## Điều hướng qua HTML

Trong ví dụ này, chúng ta sẽ điều hướng qua một tài liệu HTML và truy cập từng phần tử của nó.

```csharp
public static void NavigateThroughHTML()
{
    // Chuẩn bị một mã HTML
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

 Trong ví dụ này, chúng ta tạo một tài liệu HTML, truy cập phần con đầu tiên của nó (một`SPAN` phần tử), khoảng trắng giữa các phần tử và phần tử thứ hai`SPAN` phần tử, thể hiện điều hướng cơ bản.

## Sử dụng bộ lọc nút

Bộ lọc nút cho phép bạn xử lý có chọn lọc các phần tử cụ thể trong tài liệu HTML.

```csharp
public static void NodeFilterUsageExample()
{
    // Chuẩn bị một mã HTML
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

 Ví dụ này trình bày cách sử dụng bộ lọc nút tùy chỉnh để trích xuất các phần tử cụ thể (trong trường hợp này là`IMG` phần tử) từ tài liệu HTML.

## Truy vấn XPath

Truy vấn XPath cho phép bạn tìm kiếm các phần tử trong tài liệu HTML dựa trên các tiêu chí cụ thể.

```csharp
public static void XPathQueryUsageExample()
{
    // Chuẩn bị một mã HTML
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
        var result = document.Evaluate("//*[@class='hạnh phúc']//span",
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

Ví dụ này trình bày cách sử dụng truy vấn XPath để định vị các thành phần trong tài liệu HTML dựa trên thuộc tính và cấu trúc của chúng.

## Bộ chọn CSS

Bộ chọn CSS cung cấp một cách khác để chọn các thành phần trong tài liệu HTML, tương tự như cách nhắm mục tiêu các thành phần của biểu định kiểu CSS.

```csharp
public static void CSSSelectorUsageExample()
{
    // Chuẩn bị một mã HTML
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
        //Sử dụng bộ chọn CSS để trích xuất các phần tử dựa trên lớp và thứ bậc
        var elements = document.QuerySelectorAll(".happy span");
        
        // Lặp lại danh sách các phần tử được kết quả
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Đầu ra: Xin chào
            // Đầu ra: Thế giới!
        }
    }
}
```

Ở đây, chúng tôi trình bày cách sử dụng bộ chọn CSS để nhắm mục tiêu các phần tử cụ thể trong tài liệu HTML.

Với những ví dụ này, bạn đã hiểu biết cơ bản về cách điều hướng, lọc, truy vấn và chọn các thành phần trong tài liệu HTML bằng Aspose.HTML cho .NET.

## Phần kết luận

 Aspose.HTML for .NET là một thư viện đa năng hỗ trợ các nhà phát triển .NET làm việc hiệu quả với các tài liệu HTML. Với các tính năng mạnh mẽ để điều hướng, lọc, truy vấn và chọn các phần tử, bạn có thể xử lý liền mạch các tác vụ xử lý HTML khác nhau. Bằng cách làm theo hướng dẫn này và khám phá tài liệu tại[Aspose.HTML cho Tài liệu .NET](https://reference.aspose.com/html/net/), bạn có thể khai thác toàn bộ tiềm năng của công cụ này cho các ứng dụng .NET của mình.

## Câu hỏi thường gặp

### Q1. Aspose.HTML cho .NET có được sử dụng miễn phí không?

Câu trả lời 1: Aspose.HTML for .NET cung cấp phiên bản dùng thử miễn phí, nhưng để sử dụng trong sản xuất, bạn sẽ cần phải mua giấy phép. Bạn có thể tìm thấy chi tiết và tùy chọn cấp phép tại[Mua hàng Aspose.HTML](https://purchase.aspose.com/buy).

### Q2. Làm cách nào tôi có thể nhận được giấy phép tạm thời cho Aspose.HTML cho .NET?

 Câu trả lời 2: Bạn có thể xin giấy phép tạm thời cho mục đích thử nghiệm từ[Giấy phép tạm thời Aspose.HTML](https://purchase.aspose.com/temporary-license/).

### Q3. Tôi có thể tìm trợ giúp hoặc hỗ trợ cho Aspose.HTML cho .NET ở đâu?

 A3: Nếu bạn gặp bất kỳ vấn đề nào hoặc có thắc mắc, bạn có thể truy cập[Diễn đàn Aspose.HTML](https://forum.aspose.com/) để được hỗ trợ và hỗ trợ cộng đồng.

### Q4. Có tài nguyên bổ sung nào để học Aspose.HTML cho .NET không?

 Câu trả lời 4: Cùng với hướng dẫn này, bạn có thể khám phá thêm các hướng dẫn và tài liệu về[Trang tài liệu Aspose.HTML cho .NET](https://reference.aspose.com/html/net/).

### Q5. Aspose.HTML cho .NET có tương thích với các phiên bản .NET mới nhất không?

Câu trả lời 5: Aspose.HTML dành cho .NET được cập nhật thường xuyên để đảm bảo khả năng tương thích với các phiên bản và công nghệ .NET mới nhất.