---
category: general
date: 2026-10-25
description: Cách sử dụng ResourceHandler để kiểm soát việc tải tài nguyên và cách
  lưu HTML vào luồng bằng Aspose.HTML trong C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use resourcehandler
- how to save html to stream
- Aspose.HTML ResourceHandler
- HTML to MemoryStream C#
- custom resource handling C#
language: vi
lastmod: 2026-10-25
og_description: Cách sử dụng ResourceHandler để kiểm soát việc tải tài nguyên và cách
  lưu HTML vào luồng với Aspose.HTML cho .NET.
og_image_alt: Screenshot of C# code using ResourceHandler to save HTML to a memory
  stream
og_title: Cách sử dụng ResourceHandler và lưu HTML vào stream trong C#
schemas:
- author: Aspose
  dateModified: '2026-10-25'
  description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  headline: How to use ResourceHandler and save HTML to a stream in C#
  type: TechArticle
- description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  name: How to use ResourceHandler and save HTML to a stream in C#
  steps:
  - name: Expected output
    text: 'Running the code above prints:'
  - name: 1. Embedding real resources
    text: 'If you need to embed an image, modify `MyHandler` to return a stream that
      contains the image bytes:'
  - name: 2. Handling large documents
    text: For very large HTML files, consider using `BufferedStream` or writing directly
      to a file‑based `FileStream` if memory becomes a bottleneck. The pattern for
      **how to save HTML to a stream** stays the same; only the stream type changes.
  - name: 3. Thread safety
    text: '`ResourceHandler` instances are **not** guaranteed to be thread‑safe. If
      you plan to reuse a handler across parallel conversions, either:'
  - name: 4. Disposing resources
    text: Both `HTMLDocument` and any streams you create implement `IDisposable`.
      Wrapping them in `using` blocks, as shown in Step 4, guarantees clean release
      of unmanaged resources.
  - name: What’s next?
    text: '* **Embed real images or CSS** by extending `MyHandler` (see the “Embedding
      real resources” section). * **Convert the stream to PDF** with `HtmlConverter.ConvertHtml`
      if you need a printable version. * **Stream the result directly from a Web API**
      using `FileStreamResult` or `MemoryStream` in ASP.NE'
  type: HowTo
tags:
- Aspose.HTML
- C#
- Stream handling
title: Cách sử dụng ResourceHandler và lưu HTML vào stream trong C#
url: /vi/net/working-with-html-documents/how-to-use-resourcehandler-and-save-html-to-a-stream-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng ResourceHandler và lưu HTML vào stream trong C#

Nếu bạn cần **cách sử dụng ResourceHandler** khi render HTML với Aspose.HTML, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Bạn cũng sẽ học **cách lưu HTML vào stream** để có thể truyền kết quả mà không cần chạm vào hệ thống tệp.

Làm việc với HTML trong bộ nhớ là điều phổ biến khi bạn tạo email, phản hồi API, hoặc PDF một cách nhanh chóng. Khi kết thúc tutorial này, bạn sẽ có một chương trình C# tự chứa, tạo một `HTMLDocument`, cung cấp một `ResourceHandler` tùy chỉnh, và ghi kết quả vào một `MemoryStream`.

## Yêu cầu trước

* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Core 3.1 và .NET Framework 4.7+)
* Gói NuGet **Aspose.HTML for .NET**  
  ```bash
  dotnet add package Aspose.HTML
  ```
* Hiểu biết cơ bản về C# async/await (tùy chọn nhưng hữu ích)

## Nội dung tutorial

* Cách **cách sử dụng ResourceHandler** để chặn các yêu cầu hình ảnh, CSS, hoặc script
* Cách cấu hình `HtmlSaveOptions` với một handler tùy chỉnh
* Cách **cách lưu HTML vào stream** bằng `MemoryStream`
* Xử lý các trường hợp biên như tài nguyên thiếu và việc giải phóng stream
* Mẹo mở rộng handler để nhúng tài nguyên thực tế sau này

## Bước 1: Tạo một tài liệu HTML đơn giản từ chuỗi

Bước đầu tiên là khởi tạo một `HTMLDocument` từ HTML thô. Đối tượng này đại diện cho cây DOM mà Aspose.HTML sẽ render.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System.IO;

// Simple HTML markup – you can replace this with any valid HTML string.
string htmlContent = "<html><body>Hello World</body></html>";

// The HTMLDocument constructor parses the string into a DOM.
HTMLDocument document = new HTMLDocument(htmlContent);
```

> **Tại sao điều này quan trọng:** Tạo tài liệu từ một chuỗi giữ toàn bộ quy trình trong bộ nhớ, điều này rất cần thiết khi bạn sau này **cách lưu HTML vào stream** mà không chạm vào đĩa.

## Bước 2: Triển khai một ResourceHandler tùy chỉnh

`ResourceHandler` là điểm hook mà Aspose.HTML sử dụng mỗi khi nó cần một tài nguyên bên ngoài (hình ảnh, CSS, phông chữ, v.v.). Bằng cách ghi đè `HandleResource`, bạn quyết định stream nào sẽ được trả về cho mỗi yêu cầu.

```csharp
// Define a handler that supplies an empty stream for every resource request.
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // Returning an empty MemoryStream effectively disables external resources.
        // You could return a real image stream here if you need to embed assets.
        return new MemoryStream();
    }
}

// Instantiate the handler so it can be attached to the save options.
MyHandler customHandler = new MyHandler();
```

> **Tại sao bạn có thể cần điều này:** Khi tạo HTML cho email hoặc phản hồi API, bạn thường không muốn các cuộc gọi bên ngoài. Cung cấp các stream rỗng ngăn lỗi 404 và tăng tốc render. Điều này minh họa **cách sử dụng ResourceHandler** cho đầu ra “không tài nguyên”.

## Bước 3: Cấu hình HtmlSaveOptions để sử dụng handler tùy chỉnh

`HtmlSaveOptions` cho phép bạn kiểm soát quá trình lưu. Gán thuộc tính `ResourceHandler` tới triển khai tùy chỉnh của bạn.

```csharp
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Attach the handler so every resource request goes through MyHandler.
    ResourceHandler = customHandler
};
```

> **Mẹo:** Nếu sau này bạn cần nhúng CSS hoặc hình ảnh, hãy thay thế `MyHandler` bằng một phiên bản trả về các stream phù hợp dựa trên `resource.Uri`.

## Bước 4: Lưu tài liệu vào MemoryStream

Bây giờ bạn đã sẵn sàng để **cách lưu HTML vào stream**. Sử dụng `MemoryStream` giữ đầu ra trong RAM, giúp dễ dàng gửi qua HTTP, lưu trong cơ sở dữ liệu, hoặc truyền cho API khác.

```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    // The Save method writes the HTML (and any referenced resources) into the stream.
    document.Save(outputStream, saveOptions);

    // Reset the position so callers can read from the beginning.
    outputStream.Position = 0;

    // Example: Convert the stream to a string for debugging.
    using (StreamReader reader = new StreamReader(outputStream))
    {
        string resultHtml = reader.ReadToEnd();
        System.Console.WriteLine(resultHtml);
    }

    // At this point, outputStream can be returned from a web API, attached to an email,
    // or passed to another component without ever touching the file system.
}
```

### Kết quả mong đợi

Chạy đoạn mã trên sẽ in ra:

```html
<html><head></head><body>Hello World</body></html>
```

Vì handler tùy chỉnh trả về các stream rỗng, không có thẻ `<link>` hoặc `<img>` bên ngoài nào được giải quyết, và HTML vẫn sạch sẽ.

## Các biến thể phổ biến và trường hợp biên

### 1. Nhúng tài nguyên thực

Nếu bạn cần nhúng một hình ảnh, sửa đổi `MyHandler` để trả về một stream chứa byte của hình ảnh:

```csharp
public override Stream HandleResource(Resource resource)
{
    if (resource.Uri.EndsWith(".png"))
    {
        // Load the PNG from embedded resources or a database.
        byte[] imageBytes = File.ReadAllBytes("logo.png");
        return new MemoryStream(imageBytes);
    }
    return new MemoryStream(); // Fallback for other resources.
}
```

### 2. Xử lý tài liệu lớn

Đối với các tệp HTML rất lớn, hãy cân nhắc sử dụng `BufferedStream` hoặc ghi trực tiếp vào `FileStream` dựa trên tệp nếu bộ nhớ trở thành nút thắt. Mẫu cho **cách lưu HTML vào stream** vẫn giống nhau; chỉ loại stream thay đổi.

### 3. An toàn đa luồng

`ResourceHandler` không được đảm bảo **an toàn** khi đa luồng. Nếu bạn dự định tái sử dụng một handler cho các chuyển đổi song song, hoặc:

* Tạo một handler mới cho mỗi lần chuyển đổi, hoặc
* Bảo vệ trạng thái chia sẻ trong `HandleResource` bằng các lock.

### 4. Giải phóng tài nguyên

Cả `HTMLDocument` và bất kỳ stream nào bạn tạo đều triển khai `IDisposable`. Đặt chúng trong khối `using`, như đã minh họa ở Bước 4, đảm bảo giải phóng tài nguyên không quản lý một cách sạch sẽ.

## Mẹo chuyên nghiệp: Tái sử dụng cùng một MemoryStream

Nếu bạn cần nối nhiều đầu ra HTML vào một stream duy nhất, hãy đặt lại vị trí trước mỗi lần gọi `Save`:

```csharp
outputStream.Position = 0; // Clear previous content
document.Save(outputStream, saveOptions);
```

Hoặc, tạo một `MemoryStream` mới cho mỗi lần chuyển đổi để tránh trộn dữ liệu không mong muốn.

## Ví dụ hoàn chỉnh hoạt động

Dưới đây là chương trình đầy đủ mà bạn có thể sao chép và dán vào một ứng dụng console. Nó biên dịch với .NET 6.0 và Aspose.HTML 23.9 (hoặc mới hơn).

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System;
using System.IO;

namespace ResourceHandlerDemo
{
    // Custom handler that supplies empty streams for any requested resource.
    class MyHandler : ResourceHandler
    {
        public override Stream HandleResource(Resource resource)
        {
            // Return an empty stream to suppress external resources.
            return new MemoryStream();
        }
    }

    class Program
    {
        static void Main()
        {
            // Step 1: Create the HTML document.
            string htmlContent = "<html><body>Hello World</body></html>";
            HTMLDocument document = new HTMLDocument(htmlContent);

            // Step 2: Attach the custom ResourceHandler.
            MyHandler customHandler = new MyHandler();

            // Step 3: Configure save options.
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                ResourceHandler = customHandler
            };

            // Step 4: Save to a MemoryStream.
            using (MemoryStream outputStream = new MemoryStream())
            {
                document.Save(outputStream, saveOptions);
                outputStream.Position = 0;

                // Display the generated HTML for verification.
                using (StreamReader reader = new StreamReader(outputStream))
                {
                    string resultHtml = reader.ReadToEnd();
                    Console.WriteLine("Generated HTML:");
                    Console.WriteLine(resultHtml);
                }
            }
        }
    }
}
```

Chạy chương trình và bạn sẽ thấy HTML được tạo ra được in ra console, xác nhận rằng **cách sử dụng ResourceHandler** và **cách lưu HTML vào stream** hoạt động liền mạch cùng nhau.

## Kết luận

Tutorial này đã trình bày **cách sử dụng ResourceHandler** để kiểm soát việc tải tài nguyên bên ngoài và các bước chính xác **cách lưu HTML vào stream** bằng Aspose.HTML trong C#. Bây giờ bạn có một mẫu có thể tái sử dụng cho việc tạo HTML trong bộ nhớ, rất phù hợp cho các API web, mẫu email, và quy trình chuyển đổi PDF.

### Tiếp theo là gì?

* **Nhúng hình ảnh hoặc CSS thực** bằng cách mở rộng `MyHandler` (xem phần “Nhúng tài nguyên thực” ở trên).
* **Chuyển đổi stream sang PDF** bằng `HtmlConverter.ConvertHtml` nếu bạn cần một phiên bản có thể in.
* **Stream kết quả trực tiếp từ Web API** bằng `FileStreamResult` hoặc `MemoryStream` trong ASP.NET

## Bạn nên học gì tiếp theo?

Các tutorial sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách lưu HTML trong C# – Hướng dẫn hoàn chỉnh sử dụng Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Cách lưu HTML trong C# với Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [cách sử dụng handler trong Aspose.HTML – Load HTML, Save as ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-handler-in-aspose-html-load-html-save-as-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}