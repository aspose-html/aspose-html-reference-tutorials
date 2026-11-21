---
category: general
date: 2026-11-20
description: Tìm hiểu cách lưu HTML bằng ResourceHandler tùy chỉnh trong C# và cũng
  lưu HTML vào các tệp zip với mã ngắn gọn, sẵn sàng cho môi trường sản xuất.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: vi
lastmod: 2026-11-20
og_description: Cách lưu HTML bằng ResourceHandler tùy chỉnh trong C# và tùy chọn
  lưu HTML vào file zip — hướng dẫn đầy đủ, có thể chạy được cho các nhà phát triển
  .NET.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Cách lưu HTML bằng trình xử lý tài nguyên tùy chỉnh trong C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: Cách lưu HTML với trình xử lý tài nguyên tùy chỉnh trong C#
url: /vi/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách lưu HTML bằng trình xử lý tài nguyên tùy chỉnh trong C#

Nếu bạn cần biết **cách lưu HTML** từ một chuỗi trong bộ nhớ hoặc một tài liệu đã phân tích, hướng dẫn này sẽ cung cấp giải pháp hoàn chỉnh. Sử dụng một `ResourceHandler` tùy chỉnh cho phép bạn kiểm soát luồng đích, nghĩa là bạn có thể **lưu HTML vào file zip** mà không cần tạo các tệp tạm thời.

Bạn sẽ hiểu vì sao `ResourceHandler` được ưu tiên hơn cách tiếp cận cũ `IOutputStorage`, cách thiết lập nó, và cách mở rộng để nén zip. Khi kết thúc tutorial này, bạn có thể nhúng mã vào bất kỳ dự án .NET 6+ nào và điều chỉnh cho các yêu cầu lưu trữ của riêng mình.

## Những gì bạn sẽ xây dựng

* Một `ResourceHandler` tối thiểu trả về một `MemoryStream`.
* Một `HtmlDocument` được tạo bằng **HtmlAgilityPack**.
* Một lời gọi `doc.Save` ghi HTML vào luồng do trình xử lý cung cấp.
* Một lớp bao tùy chọn nén HTML kết quả thành file zip.

Điều kiện tiên quyết:

* .NET 6 SDK hoặc mới hơn.
* Gói NuGet `HtmlAgilityPack` (`dotnet add package HtmlAgilityPack`).
* Kiến thức cơ bản về các luồng (streams) trong C#.

## Bước 1: Tạo trình xử lý tài nguyên tùy chỉnh (cách chính để **how to save html**)

Lớp cơ sở `ResourceHandler` (có sẵn từ phiên bản 24.2 của viewer SDK) định nghĩa một phương thức trừu tượng duy nhất, `HandleResource`. Việc triển khai phương thức này cho phép bạn kiểm soát hoàn toàn nơi HTML được ghi.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Tại sao điều này quan trọng:** Bằng cách trả về một `MemoryStream`, bạn tránh việc I/O đĩa, giảm độ trễ và giữ cho mã có tính quyết định cao trong các bài kiểm thử đơn vị. Trình xử lý được gọi tự động bởi phương thức `Save`, vì vậy bạn không bao giờ cần truyền một luồng một cách thủ công.

## Bước 2: Tải hoặc xây dựng tài liệu HTML

`HtmlAgilityPack` cung cấp lớp `HtmlDocument` tiện lợi có thể phân tích một chuỗi, một tệp hoặc một luồng. Trong ví dụ này chúng ta tải một literal đơn giản, nhưng cùng một đoạn mã sẽ hoạt động với bất kỳ nguồn HTML nào.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Tại sao điều này quan trọng:** Giữ tài liệu trong bộ nhớ phù hợp với cách tiếp cận dựa trên luồng của trình xử lý tùy chỉnh. Nó cũng cho phép bạn thao tác DOM trước khi lưu, chẳng hạn như chèn script hoặc sửa các thẻ bị lỗi.

## Bước 3: Lưu tài liệu bằng trình xử lý tùy chỉnh

Gọi `doc.Save` với một thể hiện của `MyHandler` sẽ kích hoạt phương thức `HandleResource`. HTML được ghi trực tiếp vào luồng bạn đã trả về.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

Sau khi `Save` hoàn tất, `MemoryStream` bên trong `MyHandler` chứa HTML đã được tuần tự hoá. Bạn có thể lấy nó như sau:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Kết quả:** Console sẽ in ra chính xác HTML bạn đã truyền vào `LoadHtml`. Điều này chứng minh rằng bạn đã hiểu **cách lưu HTML** bằng một trình xử lý tùy chỉnh.

## Bước 4: Mở rộng trình xử lý để **save HTML to zip**

Nếu bạn muốn lưu trữ HTML trong một archive, chỉnh sửa `MyHandler` để ghi vào một `ZipArchiveEntry`. Namespace .NET `System.IO.Compression` làm cho việc này trở nên đơn giản.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Bây giờ sử dụng trình xử lý mới:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Tại sao cách này hoạt động:** Phương thức `HandleResource` tạo một mục zip có tên `document.html`. Khi `doc.Save` ghi vào luồng trả về, dữ liệu sẽ được nén tự động. Vì zip được xây dựng trong bộ nhớ, bạn có thể trả về nó từ một web API, đính kèm vào email, hoặc lưu vào cơ sở dữ liệu mà không cần chạm tới hệ thống tệp.

## Các câu hỏi thường gặp và các trường hợp đặc biệt

### Nếu tôi cần nhiều tệp HTML trong cùng một zip thì sao?
Tạo một mục mới cho mỗi lần gọi `HandleResource`. Tham số `resourceName` thường chứa tên tệp, vì vậy bạn có thể dùng trực tiếp:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Làm sao xử lý tài liệu lớn mà không làm cạn kiệt bộ nhớ?
Thay `MemoryStream` bằng một `FileStream` trỏ tới tệp tạm thời. Trình xử lý sẽ trả về luồng tệp, và bạn có thể xóa tệp sau khi zip đã được tạo.

### Cách tiếp cận này có hoạt động trên .NET Core trên Linux không?
Có. Tất cả các API được sử dụng (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) đều đa nền tảng. Đảm bảo framework mục tiêu ít nhất là .NET 6 để có tính tương thích tốt nhất.

### Tôi có thể mã hoá archive zip không?
`ZipArchive` chỉ hỗ trợ mã hoá dựa trên mật khẩu thông qua các thư viện bên thứ ba (ví dụ, `SharpZipLib`). Nếu cần mã hoá, hãy bọc các byte đầu ra bằng một thư viện cung cấp mã hoá AES trước khi gửi tới client.

## Mẹo chuyên nghiệp

* **Tái sử dụng trình xử lý** khi xử lý nhiều tài liệu trong một batch; việc tạo một `ZipArchive` mới cho mỗi tệp sẽ gây tốn tài nguyên không cần thiết.
* **Đặt `LeaveOpen: true`** trên hàm khởi tạo `ZipArchive` nếu bạn cần đọc byte zip trong khi archive vẫn mở.
* **Kiểm tra HTML** trước khi lưu bằng cách gọi `doc.OptionCheckSyntax = true;` – điều này sẽ phát hiện sớm các thẻ sai cấu trúc.
* **Ghi lại kích thước** của zip đã tạo; đầu ra bất thường lớn thường cho thấy tài nguyên trùng lặp hoặc thiếu nén.

## Ví dụ hoàn chỉnh hoạt động

Dưới đây là một file duy nhất bạn có thể dán vào một dự án console (`dotnet new console`) và chạy. Nó minh hoạ cả việc lưu HTML thuần và nén zip.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using HtmlAgilityPack;

// ---------- Custom handlers ----------
class MyHandler : ResourceHandler
{
    public MemoryStream HtmlStream { get; } = new();

    public override Stream HandleResource(string resourceName) => HtmlStream;
}

class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open();
    }

    public byte[] GetZipBytes()
    {
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}

// ---------- Main program ----------
class Program
{
    static void Main()
    {
        // Build a simple HTML document.
        HtmlDocument doc = new HtmlDocument();
        doc.LoadHtml("<html><body>Hello World from HtmlAgilityPack</body></html>");

        // ---- Example 1: plain HTML save ----
        var plainHandler = new MyHandler();
        doc.Save(plainHandler);
        plainHandler.HtmlStream.Seek(0, SeekOrigin.Begin);
        using var reader = new StreamReader(plainHandler.HtmlStream);
        Console.WriteLine("Plain HTML output:");


## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách lưu HTML trong C# với Trình xử lý tài nguyên tùy chỉnh](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [Cách sử dụng ZipArchive – Lưu HTML và tài nguyên vào file ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [lưu html dưới dạng zip với trình xử lý tài nguyên tùy chỉnh – hướng dẫn chi tiết](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}