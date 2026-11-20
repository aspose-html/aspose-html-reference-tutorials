---
category: general
date: 2026-09-10
description: Tìm hiểu cách sử dụng HtmlSaveOptions trong C# để kiểm soát kiểu chữ
  web‑font và lưu các tệp HTML với Aspose.HTML. Bao gồm ví dụ mã đầy đủ và các mẹo
  thực tế.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use htmlsaveoptions
- Aspose HTML library
- WebFontStyle flags
- HTMLDocument conversion
- C# save HTML
- Aspose.Html SaveOptions
language: vi
lastmod: 2026-09-10
og_description: Cách sử dụng HtmlSaveOptions trong C# để bật các kiểu chữ đậm và nghiêng
  của web‑font khi lưu HTML bằng Aspose.HTML. Theo dõi ví dụ đầy đủ và các mẹo thực
  hành tốt nhất.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: Cách sử dụng HtmlSaveOptions trong C# với Aspose.HTML – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  headline: How to use HtmlSaveOptions in C# with Aspose.HTML
  type: TechArticle
- description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  name: How to use HtmlSaveOptions in C# with Aspose.HTML
  steps:
  - name: Why configure WebFontStyle?
    text: 'When you export an HTML document, Aspose.HTML can embed web fonts that
      match the original styling. By setting `WebFontStyle`, you tell the exporter
      which font variants to include. This reduces the final file size when you only
      need specific styles and guarantees that the rendered output matches the '
  - name: 5.1 Controlling CSS embedding
    text: 'You can decide whether to embed CSS inline, keep external links, or embed
      everything:'
  - name: 5.2 Saving to a specific encoding
    text: '```csharp saveOptions.Encoding = Encoding.UTF8; ```'
  - name: 5.3 Handling large documents
    text: 'For very large HTML files, consider streaming the output to avoid high
      memory consumption:'
  - name: 5.4 Error handling best practice
    text: 'Wrap the entire workflow in a try‑catch block and log the exception details.
      This ensures that any I/O or parsing errors are captured:'
  - name: Expected console output
    text: '``` HTML saved successfully to ''YOUR_DIRECTORY/output.html''. ```'
  type: HowTo
tags:
- Aspose.HTML
- C#
- HTML processing
title: Cách sử dụng HtmlSaveOptions trong C# với Aspose.HTML
url: /vi/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng HtmlSaveOptions trong C# với Aspose.HTML

Nếu bạn cần kiểm soát cách Aspose.HTML lưu một tài liệu HTML, **việc học cách sử dụng HtmlSaveOptions là rất quan trọng**. Hướng dẫn này sẽ chỉ cho bạn từng bước cách sử dụng HtmlSaveOptions để bật các kiểu phông chữ web in đậm và nghiêng khi lưu tài liệu.

Thư viện Aspose HTML cung cấp một API phong phú để tải, thao tác và xuất nội dung HTML. Sau khi hoàn thành hướng dẫn này, bạn sẽ có thể:

* Tải một tệp HTML hiện có vào `HTMLDocument`.
* Cấu hình `HtmlSaveOptions` để áp dụng các cờ `WebFontStyle` cụ thể.
* Lưu tài liệu đã chỉnh sửa vào một vị trí mới hoặc một luồng.
* Mở rộng giải pháp cho các kiểu phông chữ khác, CSS tùy chỉnh và xử lý lỗi.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 trở lên đã được cài đặt.
* Giấy phép hợp lệ cho **Aspose.HTML for .NET** (bản dùng thử miễn phí cũng hoạt động cho ví dụ này).
* Visual Studio 2022 (hoặc bất kỳ IDE C# nào) để biên dịch và chạy mã.

Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.HTML`.

## Bước 1: Thiết lập dự án và nhập không gian tên

Tạo một dự án **Console App** mới và thêm gói NuGet Aspose.HTML:

```bash
dotnet add package Aspose.HTML
```

Sau đó, ở đầu file `Program.cs`, nhập các không gian tên cần thiết:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Các không gian tên này cung cấp các kiểu `HTMLDocument`, `HtmlSaveOptions` và `WebFontStyle` mà bạn sẽ sử dụng trong suốt hướng dẫn.

## Bước 2: Tải tài liệu HTML nguồn

Hoạt động đầu tiên là đọc HTML bạn muốn xử lý. Thay thế `"YOUR_DIRECTORY/input.html"` bằng đường dẫn thực tế tới tệp của bạn.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` phân tích cú pháp markup, xây dựng cây DOM và chuẩn bị cho việc thao tác. Nếu tệp không tồn tại, một ngoại lệ sẽ được ném, vì vậy bạn có thể muốn bọc lời gọi này trong khối try‑catch cho mã sản xuất.

## Bước 3: Tạo và cấu hình HtmlSaveOptions

`HtmlSaveOptions` cho phép bạn tinh chỉnh quá trình lưu. Để bật các kiểu phông chữ web in đậm và nghiêng, kết hợp các cờ `WebFontStyle` tương ứng bằng toán tử OR bitwise (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### Tại sao cần cấu hình WebFontStyle?

Khi bạn xuất một tài liệu HTML, Aspose.HTML có thể nhúng các phông chữ web phù hợp với kiểu dáng gốc. Bằng cách thiết lập `WebFontStyle`, bạn cho trình xuất biết những biến thể phông chữ nào cần bao gồm. Điều này giảm kích thước tệp cuối cùng khi bạn chỉ cần các kiểu cụ thể và đảm bảo rằng kết quả hiển thị khớp với nguồn.

#### Các biến thể thường gặp

| Kiểu mong muốn | Cờ `WebFontStyle` tương ứng |
|----------------|-----------------------------|
| Bình thường (regular) | `WebFontStyle.Regular` |
| In đậm | `WebFontStyle.Bold` |
| Nghiêng | `WebFontStyle.Italic` |
| In đậm + Nghiêng | `WebFontStyle.Bold | WebFontStyle.Italic` |
| Tất cả các biến thể | `WebFontStyle.All` |

Bạn có thể kết hợp bất kỳ tổ hợp nào phù hợp với kịch bản của mình.

## Bước 4: Lưu tài liệu với các tùy chọn đã cấu hình

Bây giờ ghi tài liệu vào một tệp mới. Phương thức `Save` nhận đường dẫn đích và thể hiện `HtmlSaveOptions` mà bạn đã chuẩn bị.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

Nếu bạn cần ghi vào một memory stream (ví dụ, để gửi tệp qua HTTP), hãy sử dụng overload chấp nhận đối tượng `Stream`:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## Bước 5: Xác minh kết quả

Mở `output.html` trong trình duyệt hoặc kiểm tra tệp bằng trình soạn thảo văn bản. Bạn sẽ thấy khối `<style>` hiện chứa các quy tắc `@font-face` cho cả biến thể in đậm và nghiêng của bất kỳ phông chữ web nào được tham chiếu trong tài liệu gốc.

**Đoạn mã đầu ra mong đợi:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

Nếu HTML gốc tham chiếu một họ phông chữ chỉ có trọng lượng bình thường, Aspose.HTML sẽ chỉ bao gồm tệp đó, tuân theo cấu hình `WebFontStyle`.

## Nâng cao: Sử dụng HtmlSaveOptions với các tính năng bổ sung

### 5.1 Kiểm soát việc nhúng CSS

Bạn có thể quyết định nhúng CSS inline, giữ liên kết ngoài, hoặc nhúng tất cả:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 Lưu với mã hoá cụ thể

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 Xử lý tài liệu lớn

Đối với các tệp HTML rất lớn, hãy cân nhắc streaming đầu ra để tránh tiêu thụ bộ nhớ cao:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 Thực hành tốt trong xử lý lỗi

Bọc toàn bộ quy trình trong khối try‑catch và ghi lại chi tiết ngoại lệ. Điều này đảm bảo mọi lỗi I/O hoặc phân tích cú pháp đều được ghi nhận:

```csharp
try
{
    // Load, configure, and save as shown earlier
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error processing HTML: {ex.Message}");
}
```

## Mẹo chuyên nghiệp: Tái sử dụng HtmlSaveOptions cho nhiều lần lưu

Nếu bạn cần lưu nhiều tài liệu với cùng cấu hình kiểu phông chữ, hãy tạo một thể hiện `HtmlSaveOptions` duy nhất và tái sử dụng nó. Điều này giảm tải cấp phát đối tượng và đảm bảo đầu ra nhất quán.

```csharp
HtmlSaveOptions sharedOptions = new HtmlSaveOptions
{
    WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
    CssSavingMode = CssSavingMode.EmbedAllCss
};

foreach (var file in Directory.GetFiles("input_folder", "*.html"))
{
    HTMLDocument doc = new HTMLDocument(file);
    string outputPath = Path.Combine("output_folder", Path.GetFileName(file));
    doc.Save(outputPath, sharedOptions);
}
```

## Ví dụ đầy đủ có thể chạy

Dưới đây là chương trình đầy đủ tích hợp tất cả các bước đã thảo luận. Sao chép nó vào `Program.cs` và chạy sau khi điều chỉnh các đường dẫn tệp.

```csharp
using System;
using System.IO;
using System.Text;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath = "YOUR_DIRECTORY/input.html";
        string outputPath = "YOUR_DIRECTORY/output.html";

        try
        {
            // Step 1: Load the source HTML document
            HTMLDocument document = new HTMLDocument(inputPath);

            // Step 2: Create HtmlSaveOptions and enable bold + italic web‑font styles
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
                // Optional: embed all CSS and use UTF‑8 encoding
                CssSavingMode = CssSavingMode.EmbedAllCss,
                Encoding = Encoding.UTF8
            };

            // Step 3: Save the document with the configured options
            document.Save(outputPath, saveOptions);

            Console.WriteLine($"HTML saved successfully to '{outputPath}'.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Đầu ra console mong đợi

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

Mở `output.html` đã tạo để xác nhận rằng các kiểu phông chữ web in đậm và nghiêng đã có mặt.

## Kết luận

Bây giờ bạn đã biết **cách sử dụng HtmlSaveOptions** để kiểm soát việc nhúng phông chữ web, xử lý CSS và mã hoá khi lưu HTML bằng thư viện Aspose HTML trong C#. Bằng cách cấu hình các cờ `WebFontStyle`, bạn có thể tùy chỉnh đầu ra để chỉ bao gồm các biến thể phông chữ cần thiết, giúp cải thiện hiệu năng và giảm kích thước tệp.

Từ đây bạn có thể khám phá các thuộc tính khác của `HtmlSaveOptions` như `ImageSavingMode`, `JavaScriptSavingMode`, hoặc kết hợp nhiều tùy chọn cho các quy trình chuyển đổi phức tạp. Thử nghiệm lưu vào stream cho các API web, hoặc tích hợp quy trình vào hệ thống tạo tài liệu lớn hơn.

---

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh có hướng dẫn từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Save HTML with Aspose.Html – Complete C# Guide](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [How to Use Aspose to Render HTML to PNG in C#](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}