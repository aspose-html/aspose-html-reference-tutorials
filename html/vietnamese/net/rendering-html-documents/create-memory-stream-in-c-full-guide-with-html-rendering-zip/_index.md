---
category: general
date: 2026-03-31
description: Tạo memory stream trong C# và học cách render HTML thành PNG, sử dụng
  trình xử lý tài nguyên tùy chỉnh, lưu HTML vào ZIP, và thiết lập kiểu phông chữ
  bằng mã—tất cả trong một hướng dẫn.
draft: false
keywords:
- create memory stream
- render html to png
- custom resource handler
- save html to zip
- set font style programmatically
language: vi
og_description: Tạo luồng bộ nhớ trong C# và ngay lập tức chuyển đổi HTML sang PNG,
  sử dụng trình xử lý tài nguyên tùy chỉnh, lưu HTML vào ZIP, và thiết lập kiểu phông
  chữ bằng chương trình.
og_title: Tạo Memory Stream trong C# – Hướng dẫn lập trình chi tiết
tags:
- C#
- HTML rendering
- Streams
- ZIP archives
- Image processing
title: Tạo Memory Stream trong C# – Hướng dẫn toàn diện với việc hiển thị HTML và
  xuất file ZIP
url: /vi/net/rendering-html-documents/create-memory-stream-in-c-full-guide-with-html-rendering-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Memory Stream trong C# – Hướng Dẫn Toàn Diện với Render HTML & Xuất ZIP

Bạn đã bao giờ tự hỏi làm thế nào để **tạo memory stream** trong C# và sau đó chuyển một tài liệu HTML thành ảnh PNG, file ZIP, hoặc thậm chí thay đổi kiểu font ngay lập tức? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần một biểu diễn tài liệu trong bộ nhớ nhưng không muốn chạm tới hệ thống tệp.

Trong tutorial này, chúng ta sẽ đi qua một giải pháp hoàn chỉnh, từ đầu đến cuối: xây dựng một custom resource handler, truyền HTML vào `MemoryStream`, nén cùng tài liệu vào ZIP, và cuối cùng render nó thành ảnh với antialiasing. Khi kết thúc, bạn sẽ có thể **render HTML thành PNG**, **lưu HTML vào ZIP**, và **đặt kiểu font bằng chương trình** mà không cần tạo file tạm trên đĩa.

## Prerequisites

- .NET 6.0 hoặc mới hơn (giao diện API ổn định trên các phiên bản gần đây).  
- Tham chiếu tới một thư viện HTML‑to‑image cung cấp `HTMLDocument`, `ImageRenderer`, và các kiểu liên quan – ví dụ, **HtmlRenderer.Core** (thay bằng package thực tế bạn dùng).  
- Kiến thức cơ bản về streams, câu lệnh `using`, và các mẫu OOP trong C#.

> **Pro tip:** Nếu bạn đang dùng Visual Studio, bật **nullable reference types** (`<Nullable>enable</Nullable>`) để phát hiện sớm các lỗi tiềm ẩn.

## Step 1: Create a Memory Stream with a Custom Resource Handler

Điều đầu tiên chúng ta cần là một handler thông báo cho engine HTML *địa điểm* ghi mỗi tài nguyên (hình ảnh, CSS, v.v.). Bằng cách kế thừa từ `ResourceHandler` chúng ta có thể đưa mọi output vào một `MemoryStream` duy nhất.

```csharp
using System;
using System.IO;

// Step 1: Define a handler that writes resources to an in‑memory stream
class MemoryResourceHandler : ResourceHandler
{
    // The stream lives for the whole lifetime of the handler
    public MemoryStream OutputStream = new MemoryStream();

    // The engine calls this for every resource it needs to write
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}
```

**Why this matters:**  
Một `MemoryStream` tồn tại hoàn toàn trong RAM, nghĩa là không có I/O đĩa, rất phù hợp cho các kịch bản hiệu năng cao như dịch vụ web hoặc unit test. Handler này cũng giữ cho API hài lòng vì engine mong đợi một `Stream` cho mỗi tài nguyên.

## Step 2: Load the HTML Document and Save It to the Memory Stream

Bây giờ chúng ta tải một file HTML hiện có (hoặc một chuỗi) và chỉ định nó sử dụng `MemoryResourceHandler` của chúng ta. Sau lời gọi `Save`, `OutputStream` sẽ chứa toàn bộ payload HTML.

```csharp
using System.IO;

// Assume the HTML file lives under YOUR_DIRECTORY
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

// Instantiate the memory handler
MemoryResourceHandler memoryHandler = new MemoryResourceHandler();

// Save the document – all resources flow into the same MemoryStream
htmlDoc.Save(memoryHandler);
```

Tại thời điểm này con trỏ của stream đang ở cuối, vì vậy chúng ta cần quay lại đầu trước khi đọc nội dung.

```csharp
// Reset the stream position to the beginning
memoryHandler.OutputStream.Position = 0;

// Quick verification (optional)
// string htmlContent = new StreamReader(memoryHandler.OutputStream).ReadToEnd();
// Console.WriteLine(htmlContent);
```

> **Note:** Dòng `ReadToEnd` ở trên được comment vì trong môi trường production bạn có thể sẽ truyền stream này cho một component khác thay vì in ra.

## Step 3: Zip the Same HTML Using a Custom ZIP Resource Handler

Đôi khi bạn cần đóng gói HTML cùng với các tài nguyên của nó. Một handler tùy chỉnh thứ hai có thể tạo entry ZIP cho mỗi tài nguyên ngay lập tức.

```csharp
using System.IO.Compression;

// Step 4: Define a handler that writes each resource into a ZIP archive
class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(string zipPath)
    {
        // Open (or create) the archive in write mode
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);
    }

    // The engine calls this for each resource; we create a ZIP entry with the same name
    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    // Proper disposal of the underlying ZipArchive
    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}
```

Bây giờ chúng ta tái sử dụng cùng một instance `htmlDoc` và ghi nó vào file ZIP.

```csharp
// Step 5: Save the HTML document into a ZIP file
using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
{
    htmlDoc.Save(zipHandler);
}
```

**Edge case tip:** Nếu HTML tham chiếu cùng một hình ảnh nhiều lần, handler ZIP sẽ tạo các entry trùng lặp. Để tránh, bạn có thể giữ một `HashSet<string>` chứa các tên đã thêm và trả về stream của entry đã tồn tại.

## Step 4: Programmatically Set Font Style on the Default Stylesheet

Thay đổi giao diện tài liệu mà không sửa HTML nguồn thường rất tiện lợi—ví dụ, khi tạo preview PDF với tiêu đề in đậm. Thư viện cung cấp `DefaultViewStyleSheet` để bạn tùy chỉnh.

```csharp
// Step 6: Apply bold and italic styling to the default view stylesheet
htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

Bạn có thể kết hợp bất kỳ flag nào được định nghĩa trong `WebFontStyle`. Thay đổi có hiệu lực ngay lập tức và sẽ ảnh hưởng tới các lần render hoặc lưu tiếp theo.

## Step 5: Render the HTML Document to a PNG Image

Cuối cùng, hãy chuyển HTML thành ảnh raster. Khi bật antialiasing và hinting, chúng ta sẽ có văn bản sắc nét và các cạnh mượt mà.

```csharp
using System.Drawing; // For ImageRenderingOptions if needed

// Step 7: Render the document to an image with antialiasing and hinting
var renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    UseHinting = true
};

new ImageRenderer(renderingOptions).Render(htmlDoc, "YOUR_DIRECTORY/out.png");
```

**What you’ll see:** Một file PNG tên `out.png` nằm trong `YOUR_DIRECTORY` trông giống hệt như trình duyệt sẽ render HTML, nhưng với kiểu bold‑italic mà chúng ta đã thiết lập trước đó.

![Screenshot of create memory stream output](placeholder-image.png "create memory stream example")

*Văn bản alt của hình ảnh bao gồm từ khóa chính để đáp ứng SEO.*

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| **Can I reuse the same `HTMLDocument` after saving to a ZIP?** | Có. Đối tượng tài liệu vẫn tồn tại trong bộ nhớ; bạn có thể gọi `Save` nhiều lần với các handler khác nhau. |
| **What if the HTML contains large binary assets?** | `MemoryStream` sẽ tăng kích thước tương ứng. Đối với các file rất lớn, cân nhắc stream trực tiếp tới file hoặc dùng `BufferedStream`. |
| **Do I need to call `Dispose` on `MemoryResourceHandler`?** | Không bắt buộc vì nó chỉ giữ một `MemoryStream`, sẽ được giải phóng khi handler bị garbage‑collected. Tuy nhiên, gọi `Dispose` vẫn là thói quen tốt. |
| **How do I change the image format (e.g., JPEG instead of PNG)?** | Truyền phần mở rộng file khác vào `ImageRenderer.Render`, hoặc dùng `ImageRenderer.RenderToBitmap` rồi lưu bằng `bitmap.Save("out.jpg", ImageFormat.Jpeg)`. |
| **Is the ZIP handler thread‑safe?** | Không. `ZipArchive` không thread‑safe, vì vậy hãy tuần tự hoá truy cập hoặc tạo một handler riêng cho mỗi thread. |

## Full Working Example

Dưới đây là một chương trình sẵn sàng copy‑and‑paste, minh họa mọi bước đã thảo luận. Thay `YOUR_DIRECTORY` bằng đường dẫn thực tế trên máy của bạn.

```csharp
// FullExample.cs
using System;
using System.IO;
using System.IO.Compression;

// Assume these types come from your HTML rendering library
using HtmlRendering; // placeholder namespace

class MemoryResourceHandler : ResourceHandler
{
    public MemoryStream OutputStream = new MemoryStream();
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}

class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(string zipPath) =>
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);

    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML
        var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // 2️⃣ Write to a memory stream
        var memHandler = new MemoryResourceHandler();
        htmlDoc.Save(memHandler);
        memHandler.OutputStream.Position = 0;
        // Optional: verify content
        // Console.WriteLine(new StreamReader(memHandler.OutputStream).ReadToEnd());

        // 3️⃣ Zip the same document
        using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
        {
            htmlDoc.Save(zipHandler);
        }

        // 4️⃣ Change font style programmatically
        htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 5️⃣ Render to PNG with antialiasing & hinting
        var renderOpts = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            UseHinting = true
        };
        new ImageRenderer(renderOpts).Render(htmlDoc, "YOUR_DIRECTORY/out.png");

        Console.WriteLine("All operations completed successfully.");
    }
}
```

Khi chạy chương trình này, bạn sẽ nhận được ba artefact:

1. **HTML trong bộ nhớ** được lưu trong `memHandler.OutputStream`.  
2. **`output.zip`** chứa HTML và tất cả các tài nguyên liên kết.  
3. **`out.png`** – ảnh đã render, tuân theo kiểu bold‑italic.

## Conclusion

Chúng ta đã trình bày cách **tạo memory stream** trong C# và tích hợp liền mạch với render HTML, nén ZIP, và tạo ảnh. Điều quan trọng là một `HTMLDocument` có thể được lưu theo nhiều cách—vào `MemoryStream`, một archive ZIP, hoặc một file PNG—chỉ bằng cách hoán đổi `ResourceHandler`.

Nếu muốn tiến xa hơn, hãy thử:

- **Render to PDF** bằng một renderer PDF chấp nhận `Stream`.  
- **Nén memory stream** trước khi gửi qua mạng (ví dụ, `GZipStream`).  
- **Kết hợp nhiều trang HTML** thành một ZIP để xuất hàng loạt.

Hãy thoải mái thử nghiệm, và đừng ngại để lại bình luận nếu gặp khó khăn. Chúc bạn coding vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}