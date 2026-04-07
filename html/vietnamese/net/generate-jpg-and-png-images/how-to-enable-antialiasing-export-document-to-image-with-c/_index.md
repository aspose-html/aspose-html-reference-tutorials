---
category: general
date: 2026-04-06
description: Tìm hiểu cách bật khử răng cưa, đặt chiều rộng và chiều cao ảnh, và lưu
  tài liệu dưới dạng PNG trong C# – hướng dẫn nhanh để xuất tài liệu thành hình ảnh.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: vi
og_description: Cách bật khử răng cưa khi xuất tài liệu sang hình ảnh. Hướng dẫn này
  chỉ cho bạn cách đặt chiều rộng ảnh, đặt chiều cao ảnh và lưu tài liệu dưới dạng
  PNG.
og_title: Cách bật khử răng cưa – Xuất tài liệu sang hình ảnh
tags:
- C#
- ImageRendering
- Antialiasing
title: Cách bật khử răng cưa – Xuất tài liệu thành hình ảnh bằng C#
url: /vi/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách bật khử răng cưa – Xuất tài liệu thành hình ảnh trong C#

Bạn đã bao giờ tự hỏi **cách bật khử răng cưa** khi chuyển một tài liệu thành hình ảnh chưa? Có thể bạn đã thử một lời gọi `Save` nhanh và kết quả trông răng cưa, đặc biệt trên các đường chéo. Tin tốt là bạn không cần một chuyên gia đồ họa—chỉ cần vài dòng C# và các tùy chọn phù hợp.

Trong hướng dẫn này, chúng ta sẽ đi qua việc thiết lập chiều rộng ảnh, thiết lập chiều cao ảnh, và cuối cùng **lưu tài liệu dưới dạng PNG** để bạn có thể **xuất tài liệu thành hình ảnh** với các cạnh mượt mà. Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng chạy tạo ra PNG 800 × 600 sắc nét với khử răng cưa được bật.

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động trên .NET Framework 4.7+)  
- Tham chiếu tới một thư viện render hỗ trợ `ImageRenderingOptions` (ví dụ: Aspose.Words, Syncfusion, hoặc bất kỳ API nào cung cấp các thuộc tính tương tự)  
- Kiến thức cơ bản về cú pháp C#  

Không cần cài đặt phức tạp—chỉ cần thêm gói NuGet và bạn đã sẵn sàng.

## Bước 1: Cài đặt Thư viện Render

Đầu tiên, kéo gói vào dự án của bạn. Nếu bạn đang dùng Aspose.Words, chạy:

```bash
dotnet add package Aspose.Words
```

> **Mẹo chuyên nghiệp:** Giữ phiên bản thư viện luôn cập nhật; bản phát hành mới nhất (tính đến tháng 4 2026) đã bổ sung các cải tiến hiệu năng cho khử răng cưa.

## Bước 2: Tạo Đối tượng Document

Tải hoặc tạo tài liệu bạn muốn render. Dưới đây là một ví dụ tối thiểu tạo một tài liệu một trang với một đoạn văn đơn giản:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

Lớp `Document` là điểm vào; mọi thứ bạn render đều xuất phát từ nó. Trong các dự án thực tế, bạn có thể sẽ tải một tệp .docx hiện có:

```csharp
// Document doc = new Document("input.docx");
```

## Bước 3: Định nghĩa Các tùy chọn Render (Chiều rộng, Chiều cao, Khử răng cưa)

Bây giờ chúng ta trả lời câu hỏi cốt lõi: **cách bật khử răng cưa**. Đối tượng `ImageRenderingOptions` cho phép bạn bật làm mịn và kiểm soát kích thước.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Chú ý các chú thích: chúng rõ ràng đề cập **đặt chiều rộng ảnh**, **đặt chiều cao ảnh**, và **UseAntialiasing**—ba công tắc quan trọng nhất khi bạn muốn một PNG được tinh chỉnh.

### Tại sao Khử răng cưa quan trọng

Nếu không có khử răng cưa, các đường chéo và đường cong sẽ xuất hiện dạng bậc thang vì bộ render coi mỗi pixel là bật hoặc tắt. Bật tính năng này sẽ pha trộn các pixel ở biên, tạo ra một sự làm mềm thị giác giống như trong các phần mềm chỉnh sửa ảnh. Nhược điểm là thời gian xử lý tăng lên một chút, nhưng đối với hầu hết các xuất khẩu hướng UI thì không đáng kể.

## Bước 4: Lưu tài liệu dưới dạng PNG (Xuất tài liệu thành hình ảnh)

Với các tùy chọn đã sẵn sàng, cuối cùng chúng ta **lưu tài liệu dưới dạng PNG**. Phương thức `Save` nhận đường dẫn tệp và các tùy chọn chúng ta vừa cấu hình.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

Xong rồi—tài liệu của bạn bây giờ là một PNG 800 × 600 với khử răng cưa đã được áp dụng. Nếu bạn mở `output.png` sẽ thấy văn bản sạch sẽ, các đường nét mượt mà và không có hiện tượng răng cưa.

### Kiểm tra Kết quả

Bạn có thể nhanh chóng kiểm tra tệp trong bất kỳ trình xem ảnh nào. Tìm kiếm:

- Kích thước đúng (800 × 600)  
- Không có cạnh bậc thang trên văn bản hoặc bất kỳ hình dạng nào  
- Nền trong suốt nếu tài liệu của bạn không chứa màu nền (hầu hết các thư viện mặc định là màu trắng)

Nếu hình ảnh vẫn có răng cưa, hãy kiểm tra lại rằng `UseAntialiasing = true` không bị ghi đè ở nơi khác.

## Bước 5: Các trường hợp đặc biệt & Biến thể

### Thay đổi Định dạng Đầu ra

Muốn JPEG thay vì PNG? Chỉ cần thay đổi phần mở rộng tệp và tùy chọn nén nếu cần:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Xuất nhiều trang

Khi tài liệu nguồn có nhiều trang, bộ render sẽ tạo các tệp ảnh riêng cho mỗi trang theo mặc định. Bạn có thể lặp qua các trang:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Lưu vào Stream (ví dụ: phản hồi HTTP)

Nếu bạn đang xây dựng một API web, có thể muốn trả về PNG trực tiếp:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Ví dụ Hoàn chỉnh

Dưới đây là chương trình đầy đủ, sẵn sàng sao chép‑dán, bao gồm mọi bước đã thảo luận:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

Chạy chương trình này sẽ tạo `output.png` trong thư mục chứa file thực thi. Mở nó lên, và bạn sẽ thấy một PNG mượt mà, 800 × 600—đúng như mục tiêu chúng ta đặt ra.

## Câu hỏi Thường gặp & Khắc phục sự cố

- **Nếu hình ảnh bị mờ thì sao?**  
  Hình mờ có thể xảy ra khi bạn phóng to một trang nguồn nhỏ. Giữ kích thước trang nguồn gần với kích thước mục tiêu, hoặc tăng DPI qua `imageOptions.Resolution` (ví dụ: `Resolution = 300`).

- **Điều này có hoạt động trên .NET Framework không?**  
  Có. API tương tự tồn tại trong framework cổ điển; chỉ cần tham chiếu đúng DLL.

- **Tôi có thể điều chỉnh màu nền không?**  
  Chắc chắn. Đặt `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` trước khi lưu.

- **Khử răng cưa có được tăng tốc bằng phần cứng không?**  
  Hầu hết các thư viện thực hiện khử răng cưa bằng phần mềm. Nếu bạn cần tăng tốc GPU, hãy tìm một engine render có hỗ trợ rõ ràng.

## Kết luận

Chúng ta đã tìm hiểu **cách bật khử răng cưa** khi **xuất tài liệu thành hình ảnh**, đi qua **đặt chiều rộng ảnh** và **đặt chiều cao ảnh**, và chỉ ra các bước chính để **lưu tài liệu dưới dạng PNG**. Đoạn mã trên đã sẵn sàng cho môi trường sản xuất, và bạn có thể dễ dàng chuyển đổi sang JPEG, PDF đa trang, hoặc thậm chí stream ảnh trực tiếp tới client.

Tiếp theo, bạn có thể khám phá việc thêm watermark, điều chỉnh DPI cho đầu ra chất lượng in, hoặc tích hợp logic này vào một endpoint ASP.NET Core. Nguyên tắc vẫn giống nhau—chỉ cần thay đổi đường dẫn tệp thành stream phản hồi.

Chúc lập trình vui vẻ, và tận hưởng những hình ảnh sắc nét, đã được khử răng cưa!

![Rendered PNG with antialiasing enabled](output.png "Rendered PNG with antialiasing enabled")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}