---
category: general
date: 2026-11-20
description: Cách bật khử răng cưa trong đồ họa C# và thiết lập kích thước phông chữ,
  kiểu phông chữ bằng mã, kèm ví dụ đầy đủ, có thể chạy được sử dụng ImageRenderingOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- set font size
- set font style programmatically
- C# graphics rendering
- ImageRenderingOptions example
language: vi
lastmod: 2026-11-20
og_description: Cách bật khử răng cưa trong đồ họa C#, thiết lập kích thước phông
  chữ và kiểu phông chữ bằng chương trình sử dụng ImageRenderingOptions – mã đầy đủ
  và giải thích.
og_image_alt: Screenshot of antialiased text with custom font size and style generated
  by C# code showing how to enable antialiasing
og_title: Cách bật khử răng cưa và thiết lập kích thước & kiểu phông chữ bằng mã trong
  C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to enable antialiasing in C# graphics and set font size, set font
    style programmatically with a complete, runnable example using ImageRenderingOptions.
  headline: How to enable antialiasing and set font size and style programmatically
    in C#
  type: TechArticle
tags:
- C#
- graphics
- antialiasing
- fonts
title: Cách bật khử răng cưa và thiết lập kích thước, kiểu chữ một cách lập trình
  trong C#
url: /vi/net/canvas-and-image-manipulation/how-to-enable-antialiasing-and-set-font-size-and-style-progr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách bật khử răng cưa và thiết lập kích thước, kiểu chữ bằng mã C#

Cách bật khử răng cưa trong đồ họa C# là một yêu cầu phổ biến khi bạn cần các cạnh mượt mà cho hình dạng hoặc văn bản. Hướng dẫn này sẽ chỉ cho bạn cách bật khử răng cưa, đặt kích thước phông chữ và thiết lập kiểu phông chữ bằng cách lập trình sử dụng lớp **ImageRenderingOptions**. Khi hoàn thành, bạn sẽ có một ứng dụng console tự chứa, render văn bản sắc nét, có kiểu vào một tệp ảnh.

Bạn sẽ học cách cấu hình pipeline render, chọn họ phông chữ phù hợp, điều chỉnh kích thước phông chữ và áp dụng kiểu đậm hoặc nghiêng mà không rời khỏi mã nguồn. Điều kiện tiên quyết duy nhất là .NET SDK mới và gói NuGet Aspose.Imaging, mà ví dụ sẽ cài đặt tự động.

## Các yêu cầu trước

- .NET 6.0 SDK hoặc mới hơn (tải từ https://dotnet.microsoft.com/)
- Visual Studio 2022 hoặc bất kỳ trình soạn thảo nào hỗ trợ dự án .NET
- **Aspose.Imaging** NuGet package (thư viện cung cấp `ImageRenderingOptions`)

Bạn có thể thêm gói bằng lệnh sau:

```bash
dotnet add package Aspose.Imaging
```

## Cách bật khử răng cưa với ImageRenderingOptions

`ImageRenderingOptions` là đối tượng trung tâm điều khiển cách Aspose.Imaging vẽ đồ họa. Đặt thuộc tính `UseAntialiasing` cho nó sẽ yêu cầu rasterizer làm mượt các cạnh, loại bỏ hiệu ứng “bậc thang” khi khử răng cưa bị tắt.

```csharp
// Step 1: Create a new ImageRenderingOptions instance
ImageRenderingOptions renderingOptions = new ImageRenderingOptions();

// Step 2: Enable antialiasing for smoother graphics
renderingOptions.UseAntialiasing = true;
```

Bật khử răng cưa là yếu tố thiết yếu cho các thành phần UI chất lượng cao, render biểu đồ và bất kỳ tình huống nào mà độ trung thực hình ảnh quan trọng.

## Đặt kích thước phông chữ bằng mã

Kích thước phông chữ quyết định độ lớn của các glyph trong bitmap cuối cùng. Bạn có thể thay đổi nó bằng cách tạo một đối tượng `Font` với kích thước điểm mong muốn. Ví dụ dưới đây đặt kích thước thành **24 pt**, một kích thước phổ biến cho tiêu đề dễ đọc.

```csharp
// Step 3: Choose a font family and size
Font font = new Font("Arial", 24); // 24‑point Arial
```

Bạn có thể thay `24` bằng bất kỳ giá trị nguyên hoặc số thực nào để đáp ứng yêu cầu bố cục. Lớp `Font` cũng chấp nhận tham số `GraphicsUnit` nếu bạn cần kích thước dựa trên pixel.

## Đặt kiểu phông chữ bằng mã

Áp dụng các kiểu đậm, nghiêng hoặc gạch chân chỉ cần truyền cờ `WebFontStyle` khi tạo `Font`. Enum `WebFontStyle` kết hợp nhiều kiểu bằng phép OR bitwise.

```csharp
// Step 4: Apply bold and italic styles
font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);
```

Nếu bạn chỉ cần một kiểu duy nhất, hãy dùng `WebFontStyle.Bold`, `WebFontStyle.Italic` hoặc `WebFontStyle.Underline`. Cách này cho phép bạn **đặt kiểu phông chữ bằng mã** mà không cần mã hóa cứng các tệp phông chữ riêng.

## Ví dụ đầy đủ có thể chạy được

Dưới đây là một ứng dụng console hoàn chỉnh, kết hợp tất cả các yếu tố:

```csharp
using System;
using Aspose.Imaging;
using Aspose.Imaging.Brushes;
using Aspose.Imaging.ImageOptions;
using Aspose.Imaging.Sources;
using Aspose.Imaging.FileFormats.Png;
using Aspose.Imaging.Graphics;
using Aspose.Imaging.Fonts;
using Aspose.Imaging.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Create rendering options and enable antialiasing
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            // Enable hinting for sharper text on low‑resolution images
            TextOptions = new TextOptions { UseHinting = true }
        };

        // 2️⃣ Define the font (size + style)
        Font font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);

        // 3️⃣ Prepare a bitmap with a white background
        int width = 800;
        int height = 200;
        using (var bitmap = new RasterImage(width, height, PixelFormat.Format24bppRgb))
        {
            bitmap.SaveOptions = new PngOptions { ColorType = PngColorType.Truecolor };
            bitmap.Fill(new SolidBrush(Color.White));

            // 4️⃣ Create a graphics object that respects our rendering options
            using (Graphics graphics = new Graphics(bitmap, renderingOptions))
            {
                // Position the text in the center of the image
                PointF location = new PointF(50, 80);
                graphics.DrawString("Antialiased Bold Italic Text", font, new SolidBrush(Color.Black), location);
            }

            // 5️⃣ Save the result
            string outputPath = "antialiased_text.png";
            bitmap.Save(outputPath);
            Console.WriteLine($"Image saved to {outputPath}");
        }
    }
}
```

### Giải thích từng phần

| Phần | Lý do quan trọng |
|------|-------------------|
| **Rendering options** | Bật `UseAntialiasing` đảm bảo các cạnh mượt cho cả hình vector và văn bản. |
| **TextOptions.UseHinting** | Hinting cải thiện khả năng đọc trên đầu ra độ phân giải thấp bằng cách điều chỉnh đường viền glyph. |
| **Font construction** | Hàm khởi tạo `Font` kết hợp **đặt kích thước phông chữ** và **đặt kiểu phông chữ bằng mã** trong một lời gọi duy nhất. |
| **Graphics object** | Truyền `renderingOptions` vào `Graphics` đảm bảo mọi thao tác vẽ đều tuân theo khử răng cưa và hinting. |
| **DrawString** | Phương thức này render văn bản với phông chữ đã cấu hình, tạo ra kết quả cuối cùng đã được khử răng cưa. |
| **Saving** | Định dạng PNG giữ nguyên dữ liệu pixel mà không có các artefact nén thêm. |

#### Kết quả mong đợi

Chạy chương trình sẽ tạo ra **antialiased_text.png** trông như sau:

![Ví dụ văn bản đã khử răng cưa](https://example.com/antialiased_text.png "Văn bản đã khử răng cưa với kích thước và kiểu phông chữ tùy chỉnh – cách bật khử răng cưa")

Hình ảnh hiển thị văn bản Arial đậm‑nghiêng sắc nét, kích thước 24 pt với các cạnh mượt, xác nhận rằng **cách bật khử răng cưa** đã hoạt động như mong muốn.

## Các biến thể phổ biến và trường hợp đặc biệt

- **Các họ phông chữ khác** – Thay `"Arial"` bằng bất kỳ tên phông chữ nào đã được cài đặt (ví dụ: `"Times New Roman"`). Nếu phông chữ không tồn tại, Aspose.Imaging sẽ ném `FontNotFoundException`.
- **Thay đổi kích thước phông chữ** – Điều chỉnh đối số thứ hai của hàm khởi tạo `Font` thành bất kỳ giá trị số thực nào. Giá trị lớn hơn tăng khả năng đọc nhưng có thể yêu cầu bitmap lớn hơn.
- **Nhiều kiểu** – Kết hợp `WebFontStyle.Underline` với `Bold` và `Italic` bằng toán tử `|`: `WebFontStyle.Bold | WebFontStyle.Underline`.
- **Render ở DPI cao** – Đối với đầu ra kiểu retina, tăng kích thước bitmap (ví dụ: 1600 × 400) trong khi giữ nguyên kích thước phông chữ; khử răng cưa vẫn sẽ cho kết quả mượt.
- **Tắt khử răng cưa** – Đặt `renderingOptions.UseAntialiasing = false;` để so sánh sự khác biệt về hình ảnh. Văn bản sẽ xuất hiện răng cưa, hữu ích cho việc gỡ lỗi hoặc kiểm tra hiệu năng.

## Mẹo chuyên nghiệp

- **Cache đối tượng `Font`** nếu bạn vẽ nhiều chuỗi trong một vòng lặp; tạo `Font` mới mỗi lần lặp sẽ gây tốn tài nguyên.
- **Sử dụng `TextOptions.UseHinting` cùng với khử răng cưa** để đạt được cân bằng tốt nhất giữa độ sắc nét và độ mượt trên ảnh độ phân giải thấp.
- **Xác thực tệp đầu ra** bằng cách mở trong trình xem ảnh hiển thị chi tiết pixel (ví dụ: Photoshop hoặc GIMP). Điều này giúp bạn chắc chắn rằng khử răng cưa thực sự đã được áp dụng.

## Kết luận

Bây giờ bạn đã biết **cách bật khử răng cưa** trong đồ họa C#, cách **đặt kích thước phông chữ**, và cách **đặt kiểu phông chữ bằng mã** sử dụng `ImageRenderingOptions`. Ví dụ hoàn chỉnh minh họa quy trình thực tiễn mà bạn có thể sao chép vào dự án của mình, dù bạn đang tạo biểu đồ, tạo thumbnail UI, hay sản xuất đồ họa động cho dịch vụ web.

Tiếp theo, bạn có thể khám phá **đặt màu phông chữ bằng mã**, thêm **đổ màu gradient**, hoặc render **các hình vector** với cùng cài đặt khử răng cưa. Tất cả các chủ đề này dựa trên nền tảng đã được trình bày ở đây, vì vậy bạn đã sẵn sàng tạo ra đồ họa chất lượng cao hoàn toàn bằng mã. Chúc bạn render vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Enable Antialiasing When Rendering HTML to PNG in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-when-rendering-html-to-png-in-c/)
- [How to enable antialiasing for HTML image rendering in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-for-html-image-rendering-in-c/)
- [How to Enable Antialiasing in Aspose HTML to PDF Conversion (C#)](/html/english/net/html-extensions-and-conversions/how-to-enable-antialiasing-in-aspose-html-to-pdf-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}