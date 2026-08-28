---
category: general
date: 2025-12-29
description: Tạo tài liệu HTML trong C# và học cách đặt phông chữ, đặt kích thước
  phông chữ, sau đó lưu HTML thành PDF hoặc chuyển đổi HTML sang PDF bằng Aspose.HTML.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: vi
og_description: Tạo tài liệu HTML trong C# và ngay lập tức xem cách thiết lập phông
  chữ, thiết lập kích thước phông chữ, sau đó lưu HTML thành PDF hoặc chuyển đổi HTML
  sang PDF với Aspose.HTML.
og_title: Tạo tài liệu HTML – Văn bản định dạng & Xuất PDF
tags:
- aspnet
- csharp
- pdf-generation
title: Tạo tài liệu HTML với văn bản được định dạng và xuất ra PDF – Hướng dẫn đầy
  đủ
url: /vi/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo tài liệu HTML có định dạng văn bản và xuất ra PDF

Bạn đã bao giờ cần **tạo tài liệu HTML** ngay lập tức và chuyển nó thành PDF mà không rời khỏi code C#? Có thể bạn đang xây dựng một engine báo cáo, một trình tạo hoá đơn, hoặc chỉ đơn giản là một bản xem trước nhanh cho người dùng. Tin tốt là bạn có thể làm điều này trong vài dòng code bằng Aspose.HTML, và sẽ có toàn quyền kiểm soát font family, kích thước font, và thậm chí cả định dạng in đậm‑nghiêng.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình — từ tạo một tài liệu HTML trong bộ nhớ đến lưu nó dưới dạng file PDF. Khi hoàn thành, bạn sẽ biết chính xác cách **đặt font family**, **đặt kích thước font**, và **lưu HTML dưới dạng PDF** (hay còn gọi là **chuyển đổi HTML sang PDF**) với một mẫu code sạch, sẵn sàng cho môi trường production.

## Những gì bạn cần

- .NET 6+ (API hoạt động với .NET Core và .NET Framework)  
- Gói NuGet Aspose.HTML for .NET (`Aspose.Html`) – cài đặt bằng `dotnet add package Aspose.Html`  
- Một thư mục trên đĩa để ghi file PDF được tạo  

Không cần template HTML phụ, không cần bộ chuyển đổi bên ngoài, chỉ cần C# thuần.

![create html document illustration](/images/create-html-document.png){alt="ví dụ tạo tài liệu html"}

## Bước 1: Tạo tài liệu HTML

Đầu tiên, chúng ta cần một đối tượng tài liệu HTML rỗng. Hãy tưởng tượng nó như một canvas trắng mà sau này bạn sẽ vẽ đoạn văn có định dạng.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Tại sao lại quan trọng:** `HTMLDocument` cung cấp cho bạn một cấu trúc giống DOM mà có thể thao tác bằng code. Không cần chạm vào chuỗi thô hay I/O file cho tới khi cuối cùng.

## Bước 2: Thêm đoạn văn và Đặt Font Family & Font Size

Bây giờ chúng ta sẽ tạo một phần tử `<p>`, chèn một đoạn văn bản, và xác định rõ font family và kích thước. Đây là nơi các từ khóa **set font family** và **set font size** xuất hiện.

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Mẹo chuyên nghiệp:** Nếu bạn cần một fallback an toàn cho web, có thể cung cấp danh sách ngăn cách bằng dấu phẩy như `"Arial, Helvetica, sans-serif"`; trình duyệt (hoặc Aspose) sẽ chọn font đầu tiên có sẵn.

## Bước 3: Áp dụng định dạng In Đậm và Nghiêng với cờ WebFontStyle

Aspose.HTML cung cấp enum tiện lợi `WebFontStyle` cho phép bạn kết hợp các kiểu bằng phép OR bitwise. Hãy làm cho văn bản vừa in đậm **và** nghiêng.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**Điều gì đang diễn ra phía sau?** Thuộc tính `FontStyle` được chuyển thành các khai báo CSS `font-weight` và `font-style`. Bằng cách OR các cờ, chúng ta tránh việc viết hai dòng CSS riêng biệt.

## Bước 4: Chuyển đổi HTML sang PDF (Lưu HTML dưới dạng PDF)

Bước cuối cùng là thực hiện chuyển đổi. Chỉ với một lời gọi `Save`, Aspose.HTML sẽ render DOM và ghi file PDF ra đĩa. Điều này đáp ứng cả yêu cầu **save html as pdf** và **convert html to pdf**.

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Kết quả mong đợi:** Mở `styled.pdf` và bạn sẽ thấy một đoạn văn duy nhất ghi “Bold & Italic text” với kích thước 18‑px Arial, được render in đậm và nghiêng. Kích thước PDF khớp với trang A4 tiêu chuẩn, và văn bản có thể chọn được — nhờ render vector.

## Ví dụ hoàn chỉnh

Kết hợp mọi thứ lại, đây là chương trình đầy đủ, sẵn sàng chạy:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### Chạy code

1. Cài đặt gói NuGet Aspose.HTML:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. Thay `C:\Temp\styled.pdf` bằng thư mục mà bạn có quyền ghi.  
3. Biên dịch và chạy: `dotnet run`.  

Bạn sẽ thấy thông báo trên console xác nhận vị trí file, và PDF sẽ chứa đoạn văn đã được định dạng.

## Các câu hỏi thường gặp & Trường hợp đặc biệt

- **Nếu tôi cần một web font tùy chỉnh thì sao?**  
  Tải font bằng `HTMLFontFaceRule` hoặc tham chiếu một file CSS `@font-face` từ xa trước khi tạo đoạn văn.

- **Có thể thêm hình ảnh trước khi chuyển đổi không?**  
  Chắc chắn. Dùng `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` và đặt `img.Source` thành đường dẫn cục bộ hoặc data URI.

- **Còn PDF đa trang thì sao?**  
  Thêm nhiều phần tử (bảng, div, …) và Aspose.HTML sẽ tự động phân trang khi nội dung vượt quá chiều cao trang.

- **Có cách kiểm soát metadata của PDF không?**  
  Truyền một đối tượng `PdfSaveOptions` và thiết lập các thuộc tính như `Author`, `Title`, hoặc `PdfAConformanceLevel`.

## Tóm tắt

Chúng ta đã tìm hiểu cách **tạo tài liệu HTML** trong C#, **đặt font family**, **đặt kích thước font**, áp dụng kiểu in đậm‑nghiêng, và cuối cùng **lưu HTML dưới dạng PDF** — thực chất là **chuyển đổi HTML sang PDF** bằng Aspose.HTML. Đoạn code ngắn gọn đủ để chèn vào bất kỳ dự án .NET nào, đồng thời đủ đầy để làm nền tảng vững chắc cho các kịch bản báo cáo phức tạp hơn.

## Bước tiếp theo

- Thử nghiệm với các lớp CSS để tái sử dụng kiểu dáng.  
- Kết hợp nhiều đoạn văn, bảng và hình ảnh để tạo PDF phong phú hơn.  
- Khám phá tuân thủ PDF/A nếu bạn cần tài liệu lưu trữ cấp cao.  

Hãy thoải mái tùy chỉnh font, kích thước hoặc màu sắc — không có giới hạn gì cho những gì bạn có thể tạo ra bằng code. Chúc lập trình vui vẻ, và hy vọng các PDF của bạn luôn hiển thị đúng như mong muốn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}