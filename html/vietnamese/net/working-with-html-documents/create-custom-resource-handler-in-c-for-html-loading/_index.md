---
category: general
date: 2026-08-15
description: Tạo trình xử lý tài nguyên tùy chỉnh bằng C# để quản lý các tài nguyên
  HTML như hình ảnh và CSS. Tìm hiểu HTMLLoadOptions, luồng bộ nhớ và việc tải HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: vi
lastmod: 2026-08-15
og_description: Tạo trình xử lý tài nguyên tùy chỉnh trong C# để kiểm soát cách các
  tài nguyên HTML được truyền. Hướng dẫn này trình bày cách thiết lập HTMLLoadOptions,
  xử lý luồng bộ nhớ và tải HTMLDocument với logic tùy chỉnh.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Tạo trình xử lý tài nguyên tùy chỉnh trong C# – hướng dẫn đầy đủ về quản
  lý tài nguyên HTML
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Tạo trình xử lý tài nguyên tùy chỉnh trong C# để tải HTML
url: /vi/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo bộ xử lý tài nguyên tùy chỉnh trong C# để tải HTML

Nếu bạn cần **tạo bộ xử lý tài nguyên tùy chỉnh** cho các tệp HTML, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ học cách chặn các hình ảnh, CSS và các tài nguyên khác khi tải tài liệu HTML, sử dụng `HTMLLoadOptions` và một luồng dựa trên bộ nhớ.

Bài học bao gồm mọi thứ cần thiết để triển khai một bộ xử lý có thể tái sử dụng, cấu hình các tùy chọn tải và xác minh rằng các tài nguyên được ghi nhận đúng cách. Không cần tài liệu bên ngoài—chỉ cần đoạn mã dưới đây và các giải thích kèm theo.

## Yêu cầu trước

- .NET 6.0 trở lên
- Kiến thức cơ bản về C#
- Tham chiếu tới thư viện xử lý HTML cung cấp `HTMLDocument`, `HtmlLoadOptions` và `ResourceHandler` (ví dụ: GroupDocs.Viewer for .NET)

## Tổng quan về giải pháp

Chúng ta sẽ:

1. **Tạo một bộ xử lý tài nguyên tùy chỉnh** bằng cách kế thừa `ResourceHandler`.
2. Cấu hình `HTMLLoadOptions` để sử dụng bộ xử lý này.
3. Tải tệp HTML bằng `HTMLDocument` trong khi bộ xử lý cung cấp luồng cho mỗi tài nguyên.
4. (Tùy chọn) Lưu các tài nguyên nhận được vào đĩa để kiểm tra.

Mỗi bước đều kèm theo mã nguồn đầy đủ và lý do thực hiện.

## Bước 1: Định nghĩa lớp bộ xử lý tài nguyên tùy chỉnh

Tạo một bộ xử lý tùy chỉnh có nghĩa là ghi đè `HandleResource` để thư viện có thể ghi byte tài nguyên vào một luồng bạn kiểm soát. Việc sử dụng `MemoryStream` giữ dữ liệu trong bộ nhớ, rất thích hợp cho việc thử nghiệm hoặc xử lý tiếp theo.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Tại sao điều này quan trọng:**  
Ghi đè `HandleResource` cho phép bạn kiểm soát hoàn toàn nơi dữ liệu tài nguyên được đưa tới. Nếu sau này bạn cần cache hình ảnh, biến đổi CSS, hoặc ghi log việc sử dụng tài nguyên, bạn có thể thay thế `MemoryStream` bằng bất kỳ triển khai luồng tùy chỉnh nào.

## Bước 2: Cấu hình `HTMLLoadOptions` để sử dụng bộ xử lý

`HTMLLoadOptions` cho phép bạn gắn bộ xử lý vào quy trình tải. Đặt thuộc tính `ResourceHandler` sẽ khiến viewer gọi `MyHandler` cho mỗi tài nguyên ngoại vi.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Tại sao điều này quan trọng:**  
Nếu không gán `ResourceHandler`, viewer sẽ ghi tài nguyên vào vị trí mặc định (thường là thư mục tạm). Bằng cách chỉ định bộ xử lý của riêng bạn, bạn **tạo bộ xử lý tài nguyên tùy chỉnh** phù hợp với chiến lược lưu trữ của ứng dụng.

## Bước 3: Tải tài liệu HTML với các tùy chọn đã cấu hình

Bây giờ tải tệp HTML. Viewer sẽ gọi `MyHandler.HandleResource` cho mỗi tài nguyên mà nó gặp.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

Tại thời điểm này nội dung HTML đã được phân tích, và tất cả các tài nguyên ngoại vi đã được truyền vào các bộ đệm bộ nhớ do `MyHandler` cung cấp.

## Bước 4 (tùy chọn): Truy cập các tài nguyên đã ghi nhận

Nếu bạn cần kiểm tra hoặc lưu trữ các tài nguyên, có thể sửa `MyHandler` để lưu mỗi `MemoryStream` vào một từ điển, khóa bằng tên tài nguyên.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Sau khi tải, bạn có thể duyệt `handler.Resources` và ghi mỗi tài nguyên ra đĩa:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Tại sao điều này quan trọng:**  
Lưu trữ tài nguyên cho phép xử lý hậu kỳ như tối ưu hoá hình ảnh, minify CSS, hoặc lưu trữ. Nó cũng cung cấp bằng chứng cụ thể rằng logic **tạo bộ xử lý tài nguyên tùy chỉnh** hoạt động như mong đợi.

## Bước 5: Dọn dẹp

Cả `HTMLDocument` và bất kỳ luồng nào cũng nên được giải phóng để giải phóng tài nguyên không quản lý.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Ví dụ đầy đủ có thể chạy được

Dưới đây là một chương trình tự chứa minh họa tất cả các bước từ định nghĩa lớp đến trích xuất tài nguyên.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Kết quả mong đợi**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

Bảng điều khiển sẽ liệt kê mỗi tài nguyên mà viewer đã truyền qua bộ xử lý tùy chỉnh của bạn, xác nhận quy trình **tạo bộ xử lý tài nguyên tùy chỉnh** đã thành công.

## Câu hỏi thường gặp và các trường hợp đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| *Nếu một tài nguyên quá lớn (ví dụ: ảnh độ phân giải cao)?* | Thay `MemoryStream` bằng `FileStream` trỏ tới thư mục tạm. Điều này ngăn việc tiêu thụ bộ nhớ quá mức. |
| *Tôi có thể lọc tài nguyên theo loại không?* | Trong `HandleResource`, kiểm tra `info.MimeType` hoặc `info.Extension` và trả về `null` cho các loại không muốn. Trả về `null` sẽ khiến viewer bỏ qua tài nguyên. |
| *Cần đảm bảo tính an toàn đa luồng không?* | Nếu cùng một thể hiện bộ xử lý được dùng cho nhiều lần tải đồng thời, hãy bảo vệ từ điển `Resources` bằng một lock hoặc dùng collection đồng thời. |
| *Làm sao hỗ trợ URL tương đối?* | `ResourceInfo` chứa URL gốc; bạn có thể kết hợp nó với đường dẫn cơ sở của tệp HTML để giải quyết các tham chiếu tương đối trước khi lưu. |

## Kết luận

Bạn đã biết cách **tạo bộ xử lý tài nguyên tùy chỉnh** trong C# để tải HTML, cấu hình `HTMLLoadOptions`, ghi nhận các tài nguyên được truyền luồng, và dọn dẹp một cách có trách nhiệm. Mô hình này cho phép bạn kiểm soát toàn bộ việc quản lý tài nguyên, hỗ trợ các kịch bản như xử lý ảnh ngay lúc tải, viết lại CSS, hoặc lưu trữ an toàn.

Tiếp theo, khám phá các chủ đề liên quan như **tải HTMLDocument** với các tùy chọn render khác nhau, hoặc mở rộng bộ xử lý để thực hiện **C# resource handler** ghi trực tiếp lên lưu trữ đám mây. Thử nghiệm phương thức `HandleResource` của bộ xử lý để phù hợp với quy trình tài nguyên cụ thể của dự án.

## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong bài viết này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ và giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}