---
category: general
date: 2026-04-23
description: Áp dụng kiểu phông chữ bằng lập trình và học cách xóa gạch chân, thay
  đổi kiểu chữ và đặt chữ in đậm bằng lập trình trong một hướng dẫn ngắn gọn.
draft: false
keywords:
- apply font style
- remove underline from text
- change text style
- text formatting tutorial
- set bold text programmatically
language: vi
og_description: Áp dụng kiểu phông chữ bằng lập trình và khám phá cách xóa gạch chân
  khỏi văn bản, thay đổi kiểu chữ và đặt chữ in đậm bằng lập trình trong một hướng
  dẫn ngắn gọn, thực tế.
og_title: Áp dụng kiểu phông chữ bằng lập trình – Hướng dẫn nhanh C#
tags:
- csharp
- ui
- text-formatting
- programming
title: Áp dụng kiểu phông chữ bằng lập trình – Hướng dẫn nhanh C#
url: /vi/net/html-document-manipulation/apply-font-style-programmatically-quick-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Áp dụng kiểu phông chữ bằng mã – Hướng dẫn nhanh C#

Bạn đã bao giờ cần **áp dụng kiểu phông chữ** cho một phần tử UI nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất—hầu hết các nhà phát triển đều gặp khó khăn này khi lần đầu làm việc với định dạng văn bản động. Tin tốt là gì? Chỉ trong vài phút, bạn sẽ biết chính xác cách thay đổi giao diện của một label, loại bỏ gạch chân khỏi văn bản, và đặt văn bản in đậm bằng mã mà không phải lục lọi tài liệu vô tận.

Trong **bài hướng dẫn định dạng văn bản** này, chúng tôi sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, giải thích “tại sao” mỗi dòng lại cần thiết, và cung cấp các mẹo thực tiễn mà bạn có thể sao chép‑dán vào bất kỳ dự án WinForms hoặc WPF nào. Không có phần thừa, chỉ có những gì giúp bạn hoàn thành công việc.

---

## Những gì bạn sẽ học

- Cách **áp dụng kiểu phông chữ** bằng một lớp trợ giúp nhỏ.  
- Các bước chính xác để **loại bỏ gạch chân khỏi văn bản** trong khi giữ các kiểu khác nguyên vẹn.  
- Các cách để **thay đổi kiểu văn bản** (đậm, nghiêng, gạch chân) một cách linh hoạt.  
- Một đoạn mã hoàn chỉnh, sẵn sàng sao chép, **đặt văn bản in đậm bằng mã**.  
- Những lỗi thường gặp và cách xử lý các trường hợp biên để bạn không bị bất ngờ sau này.

**Điều kiện tiên quyết:** .NET 6+ (hoặc bất kỳ .NET Framework hiện đại nào), kiến thức cơ bản về C#, và một IDE bạn thích (Visual Studio, Rider, hoặc VS Code). Đó là tất cả—không cần thêm gói NuGet nào.

---

## Bước 1 – Áp dụng kiểu phông chữ cho Control của bạn

Cốt lõi của bất kỳ thao tác **áp dụng kiểu phông chữ** nào là enum `FontStyle` kết hợp với đối tượng `Font`. Để giữ cho mã gọn gàng, chúng ta sẽ gói logic enum này trong một lớp nhỏ `WebFontStyle`. Lớp này phản ánh các thuộc tính bạn đã thấy trong đoạn mã gốc (`Bold`, `Italic`, `Underline`) và tạo ra giá trị `FontStyle` mà bạn có thể truyền cho `Font`.

```csharp
using System;
using System.Drawing;

/// <summary>
/// Simple helper that mimics the original WebFontStyle API.
/// It lets you toggle Bold, Italic, and Underline flags and
/// converts the result into a System.Drawing.FontStyle value.
/// </summary>
public class WebFontStyle
{
    public bool Bold { get; set; } = false;
    public bool Italic { get; set; } = false;
    public bool Underline { get; set; } = false;

    /// <summary>
    /// Returns a FontStyle that combines the selected flags.
    /// </summary>
    public FontStyle ToFontStyle()
    {
        FontStyle style = FontStyle.Regular;
        if (Bold)      style |= FontStyle.Bold;
        if (Italic)    style |= FontStyle.Italic;
        if (Underline) style |= FontStyle.Underline;
        return style;
    }

    /// <summary>
    /// Creates a new Font based on an existing one but with the
    /// updated style. Handy for UI controls that already have a font.
    /// </summary>
    public Font ToFont(Font baseFont)
    {
        return new Font(baseFont, ToFontStyle());
    }
}
```

**Tại sao điều này quan trọng:**  
Bằng cách tách riêng logic xây dựng cờ, bạn tránh việc rải rác các phép toán bitwise `|` khắp mã UI. Mã sẽ dễ đọc hơn, dễ kiểm thử hơn, và—quan trọng nhất—giúp ý định **áp dụng kiểu phông chữ** trở nên rõ ràng.

---

## Bước 2 – Loại bỏ gạch chân khỏi văn bản (và giữ các kiểu khác)

Giả sử bạn kế thừa một label đã được gạch chân, nhưng thiết kế yêu cầu chỉ có văn bản in đậm. Bạn không muốn mất độ đậm khi loại bỏ gạch chân. Đây là lúc lớp `WebFontStyle` tỏa sáng.

```csharp
// Assume we already have a Label named lblSample.
var fontStyle = new WebFontStyle
{
    Bold = true,          // Keep bold on.
    Italic = false,      // No italic needed.
    Underline = false    // This line **removes underline**.
};

// Apply the new Font to the label.
lblSample.Font = fontStyle.ToFont(lblSample.Font);
```

**Điểm then chốt:** Đặt `Underline = false` một cách rõ ràng sẽ khiến trợ giúp loại bỏ cờ gạch chân. Nếu bạn bỏ qua dòng này, gạch chân cũ sẽ vẫn tồn tại, đây là nguồn gây lỗi phổ biến khi các nhà phát triển chỉ bật tắt thuộc tính `Bold`.

---

## Bước 3 – Thay đổi kiểu văn bản: Đậm, Nghiêng và hơn thế nữa

Bạn có thể tự hỏi, “Nếu tôi cần bật/tắt nghiêng thì sao?” Cùng một đối tượng vẫn hoạt động cho bất kỳ tổ hợp nào. Dưới đây là một ma trận nhanh bạn có thể tham khảo khi lập trình.

| Kiểu mong muốn | `Bold` | `Italic` | `Underline` |
|----------------|--------|----------|-------------|
| **Bold only** | true   | false    | false       |
| *Italic only* | false  | true     | false       |
| **Bold + Italic** | true   | true     | false       |
| **Bold + Underline** | true   | false    | true        |

Chỉ cần đặt các thuộc tính bạn cần và gọi `ToFont`. Trợ giúp sẽ thực hiện phần nặng cho bạn, để bạn tập trung vào logic UI.

---

## Ví dụ đầy đủ – Đặt văn bản in đậm bằng mã

Dưới đây là một ví dụ **đầy đủ, có thể chạy** trên WinForms, minh họa mọi thứ chúng ta đã thảo luận. Sao chép nó vào một dự án WinForms kiểu console và nhấn **F5**.

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

namespace FontStyleDemo
{
    static class Program
    {
        [STAThread]
        static void Main()
        {
            ApplicationConfiguration.Initialize(); // .NET 6+ boilerplate
            Application.Run(new DemoForm());
        }
    }

    public class DemoForm : Form
    {
        private readonly Label _sampleLabel;

        public DemoForm()
        {
            Text = "Apply Font Style Demo";
            Size = new Size(400, 200);
            StartPosition = FormStartPosition.CenterScreen;

            _sampleLabel = new Label
            {
                Text = "Hello, world!",
                AutoSize = true,
                Location = new Point(20, 30)
            };
            Controls.Add(_sampleLabel);

            // STEP: instantiate WebFontStyle and configure it
            var fontStyle = new WebFontStyle
            {
                Bold = true,          // set bold text programmatically
                Italic = false,      // no italic
                Underline = false    // remove underline from text
            };

            // Apply the new style to the label
            _sampleLabel.Font = fontStyle.ToFont(_sampleLabel.Font);
        }
    }

    // ---- WebFontStyle class from Step 1 (included for completeness) ----
    public class WebFontStyle
    {
        public bool Bold { get; set; } = false;
        public bool Italic { get; set; } = false;
        public bool Underline { get; set; } = false;

        public FontStyle ToFontStyle()
        {
            FontStyle style = FontStyle.Regular;
            if (Bold)      style |= FontStyle.Bold;
            if (Italic)    style |= FontStyle.Italic;
            if (Underline) style |= FontStyle.Underline;
            return style;
        }

        public Font ToFont(Font baseFont)
        {
            return new Font(baseFont, ToFontStyle());
        }
    }
}
```

### Kết quả mong đợi

Khi bạn chạy chương trình, một cửa sổ sẽ xuất hiện với văn bản **“Hello, world!”** được hiển thị **đậm**, **không nghiêng**, và **không có gạch chân**. Điều này xác nhận rằng logic **áp dụng kiểu phông chữ** đã hoạt động hoàn hảo.

---

## Mẹo chuyên nghiệp & Các trường hợp biên

- **Cập nhật động:** Nếu bạn cần thay đổi kiểu sau khi form đã hiển thị (ví dụ, phản hồi một checkbox), chỉ cần tạo lại đối tượng `WebFontStyle` hoặc sửa đổi các thuộc tính và gán lại `lbl.Font`. UI sẽ cập nhật ngay lập tức.  
- **Xem xét DPI cao:** Khi bạn thay thế một đối tượng `Font`, Windows sẽ tự động điều chỉnh kích thước dựa trên DPI hiện tại. Không cần mã bổ sung trừ khi bạn tự xử lý scaling.  
- **Tương đương WPF:** Trong WPF bạn sẽ bind `FontWeight`, `FontStyle`, và `TextDecorations` thay vì thay đổi đối tượng `Font`. Nguyên tắc tách logic vẫn áp dụng—giữ logic kiểu cách ra khỏi lớp view.  
- **Tránh rò rỉ bộ nhớ:** Gán lại `Label.Font` tạo ra một đối tượng `Font` mới. Hãy giải phóng đối tượng cũ nếu bạn thường xuyên thay đổi kiểu: `var oldFont = lbl.Font; lbl.Font = newFont; oldFont.Dispose();`

---

## Kết luận

Bây giờ bạn đã biết cách **áp dụng kiểu phông chữ** cho bất kỳ control .NET nào, **loại bỏ gạch chân khỏi văn bản**, và **thay đổi kiểu văn bản** một cách linh hoạt—tất cả trong khi giữ mã sạch sẽ và tái sử dụng được. Trợ giúp nhỏ `WebFontStyle` biến một vài cờ boolean thành một thành phần vững chắc, có thể kiểm thử, và ví dụ đầy đủ chứng minh rằng bạn có thể **đặt văn bản in đậm bằng mã** chỉ trong vài dòng.

Tiếp theo bạn muốn làm gì? Hãy thử kết hợp cách tiếp cận này với các cài đặt do người dùng điều khiển, hoặc khám phá các cờ `FontStyle` khác như `Strikeout`. Bạn thậm chí có thể tạo một panel UI nhỏ cho phép người dùng không chuyên chọn in đậm, nghiêng, hoặc gạch chân tại thời gian chạy—không cần biên dịch lại.

Nếu bạn thấy **bài hướng dẫn định dạng văn bản** này hữu ích, hãy để lại bình luận hoặc chia sẻ các biến thể của bạn. Chúc lập trình vui vẻ, và mong UI của bạn luôn hiển thị đúng như mong muốn!

---

![Screenshot showing how to apply font style to a label in C#](https://example.com/images/apply-font-style.png

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}