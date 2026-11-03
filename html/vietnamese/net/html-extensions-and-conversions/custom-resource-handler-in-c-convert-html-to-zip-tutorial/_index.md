---
category: general
date: 2026-02-10
description: Trình xử lý tài nguyên tùy chỉnh cho phép bạn chuyển đổi HTML sang ZIP
  trong C#. Tìm hiểu cách lưu HTML dưới dạng zip và truyền tải tài nguyên HTML một
  cách hiệu quả.
draft: false
keywords:
- custom resource handler
- convert html to zip
- save html as zip
- create zip with html
- stream html resources
language: vi
og_description: Trình xử lý tài nguyên tùy chỉnh cho phép bạn chuyển đổi HTML sang
  ZIP trong C#. Hãy làm theo hướng dẫn từng bước này để lưu HTML dưới dạng zip và
  truyền luồng tài nguyên HTML.
og_title: Trình xử lý tài nguyên tùy chỉnh trong C# – Chuyển đổi HTML sang ZIP
tags:
- Aspose.HTML
- C#
- ZIP archive
- file streaming
title: Trình xử lý tài nguyên tùy chỉnh trong C# – Hướng dẫn chuyển đổi HTML sang
  ZIP
url: /vi/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom Resource Handler – Chuyển đổi HTML sang ZIP trong C#

Bạn đã bao giờ tự hỏi làm thế nào để **custom resource handler** từ HTML thô trực tiếp thành một tệp ZIP? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần gói một trang HTML cùng các tài nguyên của nó mà không làm bám đọng các tệp tạm thời trên đĩa. Tin tốt là gì? Với Aspose.HTML, bạn có thể thực hiện mọi thứ trong bộ nhớ, và bí quyết nằm ở một custom resource handler.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ đầy đủ, có thể chạy được, cho thấy cách **convert HTML to ZIP**, **save HTML as ZIP**, và **stream HTML resources** ngay lập tức. Khi kết thúc, bạn sẽ có một phương thức duy nhất nhận một chuỗi HTML và tạo ra một tệp `result.zip` sẵn sàng tải xuống, chứa trang và mọi tài nguyên được liên kết.

> **Prerequisites** – .NET 6+ (hoặc .NET Framework 4.6+), đã cài đặt Aspose.HTML cho .NET, và hiểu biết cơ bản về streams. Không cần công cụ bên ngoài.

---

## Custom Resource Handler – Core Concept

Một *resource handler* trong Aspose.HTML là một đối tượng quyết định **nơi** mỗi phần của tài liệu sẽ được lưu—cho dù là một tệp trên đĩa, một bộ đệm bộ nhớ, hoặc, như chúng tôi sẽ trình bày, một mục bên trong một tệp ZIP. Bằng cách kế thừa `ResourceHandler`, bạn có toàn quyền kiểm soát điểm đến đầu ra cho tệp HTML chính **và** mọi tài nguyên phụ trợ (CSS, hình ảnh, phông chữ, v.v.).

Hãy nghĩ về nó như một người chỉ dẫn giao thông cho các tài sản của tài liệu: phương thức `HandleResource` cung cấp cho bạn một `Stream` cho HTML chính, trong khi sự kiện `ResourceSaving` cho phép bạn chặn mỗi tệp phụ thuộc ngay trước khi nó được ghi.

---

## Bước 1: Triển khai một Custom Resource Handler

Đầu tiên, tạo một lớp kế thừa từ `ResourceHandler`. Chúng ta sẽ ghi đè `HandleResource` để cung cấp cho Aspose một `MemoryStream` mới cho đầu ra HTML chính. Đối với các tài nguyên được liên kết, chúng ta sẽ gắn vào `ResourceSaving` sau này.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;

/// <summary>
/// Supplies a stream for every resource the HTML document needs to save.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a new stream for the main HTML content.
    /// </summary>
    public override Stream HandleResource(ResourceInfo info)
    {
        // In real life you might return a FileStream or a ZipEntry stream.
        // Here we just hand back a clean MemoryStream.
        return new MemoryStream();
    }
}
```

**Tại sao điều này quan trọng:** Trả về một `MemoryStream` mới có nghĩa là HTML không bao giờ chạm tới hệ thống tệp. Đây là nền tảng cho việc tạo ZIP sạch, hoàn toàn trong bộ nhớ sau này.

---

## Bước 2: Lưu HTML vào một MemoryStream duy nhất

Bây giờ chúng ta đã có một handler, chúng ta có thể tạo một tài liệu HTML và nắm bắt toàn bộ trong bộ nhớ. Bước này là tùy chọn nếu bạn chỉ cần ZIP, nhưng nó minh họa cách handler hoạt động độc lập.

```csharp
using Aspose.Html;

// Sample HTML – replace with your own markup or load from a file.
string htmlContent = "<html><head><title>Demo</title></head><body>Hello world!</body></html>";

// Create the document from a string.
HTMLDocument htmlDocument = new HTMLDocument(htmlContent);

// Instantiate our custom handler.
MyHandler memoryHandler = new MyHandler();

using (MemoryStream htmlStream = new MemoryStream())
{
    // Save triggers HandleResource and writes the HTML into htmlStream.
    htmlDocument.Save(htmlStream, memoryHandler);

    // Reset position for potential reading.
    htmlStream.Position = 0;

    // For demo purposes, dump the HTML to console.
    using (StreamReader reader = new StreamReader(htmlStream))
    {
        Console.WriteLine("Generated HTML:");
        Console.WriteLine(reader.ReadToEnd());
    }
}
```

**Kết quả mong đợi** (định dạng để dễ đọc):

```
Generated HTML:
<html><head><title>Demo</title></head><body>Hello world!</body></html>
```

Nếu bạn chạy đoạn mã này, bạn sẽ thấy HTML chỉ tồn tại trong RAM—không có tệp tạm thời nào được tạo.

---

## Bước 3: Đóng gói HTML và các tài nguyên vào một tệp ZIP

Bây giờ là phần hấp dẫn: gói HTML **và** mọi tài nguyên được tham chiếu vào một tệp ZIP mà không bao giờ ghi các tệp trung gian lên đĩa. Chúng ta sẽ sử dụng `System.IO.Compression.ZipArchive` cùng với sự kiện `ResourceSaving`.

```csharp
using Aspose.Html;
using System.IO;
using System.IO.Compression;

// Re‑use the same HTMLDocument from the previous step.
HTMLDocument htmlDocument = new HTMLDocument("<html><body>Hello world!</body></html>");

// Path where the final ZIP will be written.
string zipPath = Path.Combine(Environment.CurrentDirectory, "result.zip");

// Open a FileStream for the ZIP file.
using (FileStream zipFile = new FileStream(zipPath, FileMode.Create))
using (ZipArchive zipArchive = new ZipArchive(zipFile, ZipArchiveMode.Update))
{
    // Create a fresh handler for the ZIP operation.
    MyHandler zipHandler = new MyHandler();

    // Hook the ResourceSaving event – this fires for every resource.
    zipHandler.ResourceSaving += (sender, e) =>
    {
        // Ensure we don't create leading folder entries like "/css/style.css".
        string entryName = e.ResourceInfo.Path.TrimStart('/');

        // Create a new entry inside the ZIP.
        ZipArchiveEntry entry = zipArchive.CreateEntry(entryName);

        // Provide the stream that Aspose will write into.
        e.Stream = entry.Open();
    };

    // Save the document; the handler will fill the ZIP for us.
    htmlDocument.Save(zipHandler);
}

// Verify the ZIP exists.
Console.WriteLine($"ZIP created at: {zipPath}");
```

### Những gì xảy ra bên trong?

1. **`ResourceSaving` được kích hoạt** cho tệp HTML chính và mỗi tài nguyên được liên kết.  
2. Lambda của chúng ta tạo một mục tương ứng (`CreateEntry`) bên trong ZIP đang mở.  
3. Bằng cách gán `e.Stream = entry.Open()`, chúng ta cung cấp cho Aspose một stream có thể ghi, ghi trực tiếp vào mục ZIP.  
4. Khi `htmlDocument.Save` hoàn thành, ZIP sẽ chứa một trang HTML hoàn chỉnh cùng bất kỳ CSS, hình ảnh hoặc phông chữ nào được tham chiếu trong markup.

**Kết quả:** Một tệp `result.zip` duy nhất mà bạn có thể phục vụ cho trình duyệt, đính kèm vào email, hoặc lưu trữ trong blob storage—không còn tệp tạm thời nào.

---

## Bonus: Sử dụng ZIP trong một Web API

Nếu bạn đang xây dựng một endpoint ASP.NET Core trả về ZIP theo yêu cầu, logic tương tự vẫn áp dụng. Dưới đây là một hành động controller ngắn gọn:

```csharp
[ApiController]
[Route("api/[controller]")]
public class HtmlZipController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult DownloadZip()
    {
        // Build the document (could be loaded from a DB, etc.).
        var html = "<html><body><h1>Dynamic report</h1></body></html>";
        var doc = new HTMLDocument(html);
        var handler = new MyHandler();

        // Prepare an in‑memory ZIP.
        using var zipStream = new MemoryStream();
        using (var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            handler.ResourceSaving += (s, e) =>
            {
                var entry = archive.CreateEntry(e.ResourceInfo.Path.TrimStart('/'));
                e.Stream = entry.Open();
            };
            doc.Save(handler);
        }

        zipStream.Position = 0;
        return File(zipStream, "application/zip", "report.zip");
    }
}
```

Bây giờ một yêu cầu GET tới `/api/HtmlZip/download` sẽ stream tệp zip được tạo trực tiếp tới client—hoàn hảo cho các báo cáo tạo ngay lập tức.

---

## Những cạm bẫy thường gặp & Mẹo chuyên nghiệp

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Thư mục trống trong ZIP** | `ResourceInfo.Path` bắt đầu bằng `/` gây ra một mục như `/` | Sử dụng `TrimStart('/')` như trong hàm xử lý sự kiện. |
| **Thiếu hình ảnh** | Các hình ảnh được tham chiếu bằng URL tuyệt đối không được tải tự động | Đặt `htmlDocument.Options.ResourceLoading = ResourceLoadingMode.Stream` và cung cấp một `ResourceHandler` tùy chỉnh để tải các tài nguyên từ xa. |
| **Tệp lớn gây áp lực bộ nhớ** | Tất cả các stream được giữ trong bộ nhớ cho đến khi ZIP được đóng | Chuyển `ZipArchiveMode.Update` sang `Create` và ghi mỗi mục trực tiếp mà không dùng bộ đệm, hoặc stream từ đĩa nếu kích thước vượt quá RAM. |
| **Ngoại lệ “The stream does not support seeking”** | Cố gắng tái sử dụng một stream không hỗ trợ seek cho nhiều tài nguyên | Luôn cung cấp một `MemoryStream` mới hoặc `entry.Open()` cho mỗi tài nguyên. |

---

## Kết luận

Chúng tôi vừa minh họa cách một **custom resource handler** cho phép bạn **convert HTML to ZIP**, **save HTML as ZIP**, và **stream HTML resources** mà không cần chạm tới hệ thống tệp. Bằng cách ghi đè `HandleResource` và sử dụng `ResourceSaving`, bạn có được kiểm soát chi tiết từng byte ra khỏi Aspose.HTML.

Mô hình này có thể mở rộng: thay thế `MemoryStream` trong bộ nhớ bằng một stream blob trên đám mây, thêm các cài đặt nén, hoặc gắn một lớp logging để kiểm tra tài nguyên nào được đóng gói. Không có giới hạn khi bạn kiểm soát toàn bộ pipeline tài nguyên.

Sẵn sàng cho bước tiếp theo? Hãy thử nhúng CSS và hình ảnh vào HTML của bạn, thử nghiệm tải tài nguyên từ xa, hoặc tích hợp quy trình này vào một Azure Function trả về ZIP theo yêu cầu. Chúc lập trình vui vẻ!

--- 

![luồng công việc của bộ xử lý tài nguyên tùy chỉnh](https://example.com/placeholder-image.png "luồng công việc của bộ xử lý tài nguyên tùy chỉnh")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}