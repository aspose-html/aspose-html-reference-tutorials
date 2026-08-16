---
category: general
date: 2026-08-15
description: 快速在 C# 中创建粗斜体字体。了解如何使用内置的 Font 类在 C# 中创建带粗体和斜体样式的字体。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create bold italic font
- create font in c#
- C# FontStyle
- text styling C#
- System.Drawing.Font
language: zh
lastmod: 2026-08-15
og_description: 在 C# 中创建粗斜体字体并提供清晰示例。本教程展示如何使用 FontStyle 标志在 C# 中创建字体，并解释常见的陷阱。
og_image_alt: Screenshot of text rendered with a bold italic Arial font in a C# console
  window
og_title: 在 C# 中创建粗斜体字体 – 完整编码指南
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  headline: Create bold italic font in C# – step‑by‑step guide
  type: TechArticle
- description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  name: Create bold italic font in C# – step‑by‑step guide
  steps:
  - name: Save the code to a file named `Program.cs`.
    text: Save the code to a file named `Program.cs`.
  - name: Open a terminal in the file’s directory.
    text: Open a terminal in the file’s directory.
  - name: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
    text: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
  - name: Replace the generated `Program.cs` with the code above.
    text: Replace the generated `Program.cs` with the code above.
  - name: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
    text: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
  - name: Build and run with `dotnet run`.
    text: Build and run with `dotnet run`.
  type: HowTo
tags:
- C#
- fonts
- text styling
title: 在 C# 中创建粗斜体字体 – 步骤指南
url: /zh/net/advanced-features/create-bold-italic-font-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建粗斜体字体 – 步骤指南

如果你需要在 C# 中 **创建粗斜体字体**，本指南将手把手教你如何实现。你将看到一个完整、可运行的示例，同时演示如何使用标准 .NET `Font` 类 **在 C# 中创建字体**。

在 Windows 桌面应用、生成 PDF 或在服务器端渲染 HTML 时，使用自定义字体是常见需求。阅读完本教程后，你将能够实例化既粗体又斜体的字体，理解为何使用位运算符 `|`，并处理如字体族缺失等常见边界情况。

## 你将学到

* 如何导入处理字体所需的命名空间。  
* `FontStyle.Bold` 与 `FontStyle.Italic` 的组合语法。  
* 如何验证字体是否成功创建。  
* 当请求的字体族未安装时的回退处理技巧。  

无需外部库——全部使用 .NET Framework / .NET Core 基础类库。

## 前置条件

* .NET 6.0 SDK 或更高（代码同样适用于 .NET Framework 4.6+）。  
* 代码编辑器或 IDE（Visual Studio、VS Code、Rider 等）。  
* 基本的 C# 语法了解。  

满足以上条件后，即可按步骤操作，无需额外配置。

## 步骤 1：添加必要的 using 指令

`Font` 类位于 `System.Drawing` 命名空间，它是 `System.Drawing.Common` NuGet 包在 .NET Core/.NET 5+ 中的组成部分。请在文件顶部加入该命名空间：

```csharp
using System;
using System.Drawing;   // Provides Font and FontStyle
```

> **为什么这一步重要** – 若缺少 `using System.Drawing;`，编译器将找不到 `Font` 或 `FontStyle`，导致 “type or namespace name could not be found” 错误。

## 步骤 2：使用位或运算符组合粗体和斜体样式

在 .NET 中，`FontStyle` 是标记了 `[Flags]` 特性的枚举。这意味着可以使用 `|`（位或）运算符合并多个值：

```csharp
// Step 2: Create a Font that is both bold and italic
var font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
```

### 说明

* `"Arial"` – 字体族名称。如果系统未安装 Arial，构造函数会回退到默认字体。  
* `12` – 字号（磅）。  
* `FontStyle.Bold | FontStyle.Italic` – 将两个样式标志合并。`|` 运算符会把每个标志的二进制表示合并，生成表示 “粗体 + 斜体” 的单一值。

> **小技巧**：始终使用枚举名称（`FontStyle.Bold`）而非魔法数字；这样可提升可读性，并防止枚举值变动导致的 bug。

## 步骤 3：验证创建的字体（可选但推荐）

打印字体属性可以帮助确认样式组合是否成功，尤其在新机器上调试时非常有用。

```csharp
// Step 3: Output the font details to the console
Console.WriteLine($"Font family: {font.Name}");
Console.WriteLine($"Size (pt): {font.Size}");
Console.WriteLine($"Style: {font.Style}");
```

**预期输出**

```
Font family: Arial
Size (pt): 12
Style: Bold, Italic
```

如果输出同时列出 `Bold` 和 `Italic`，说明字体已正确创建。

## 步骤 4：渲染示例字符串（可视化确认）

在控制台应用中看不到实际字形样式，但可以生成图片来证明结果。下面的代码片段使用粗斜体字体绘制 “Hello, World!” 并保存为 *sample.png*：

```csharp
// Step 4: Draw text to an image file for visual confirmation
using (var bitmap = new Bitmap(300, 100))
using (var graphics = Graphics.FromImage(bitmap))
{
    graphics.Clear(Color.White);
    var brush = Brushes.Black;
    graphics.DrawString("Hello, World!", font, brush, new PointF(10, 30));
    bitmap.Save("sample.png");
    Console.WriteLine("Image saved as sample.png");
}
```

程序运行后，打开 *sample.png* 即可看到带有粗斜体样式的文本。

![Sample text rendered with bold italic font](sample.png)

*图片替代文字：在 C# 控制台窗口中使用粗斜体 Arial 字体渲染的文本截图* – 该 alt 文本满足 SEO 要求。

## 步骤 5：当字体族不可用时的优雅回退

如果请求的字体族（例如 “Arial”）未安装，`Font` 构造函数会抛出 `ArgumentException`。请将创建代码放入 `try/catch` 块，并回退到已知安全的字体，如 “Segoe UI”。

```csharp
Font font;
try
{
    font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
}
catch (ArgumentException)
{
    Console.WriteLine("Arial not found – falling back to Segoe UI.");
    font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
}
```

**为何需要处理？** 在容器化或无头环境中，默认字体集合可能与普通桌面不同。提供回退可以防止运行时崩溃，确保样式一致。

## 完整可运行示例

将所有内容整合后，下面是一段可以直接复制、粘贴并运行的完整程序：

```csharp
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create the font (bold + italic)
        Font font;
        try
        {
            font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
        }
        catch (ArgumentException)
        {
            Console.WriteLine("Arial not found – using Segoe UI as fallback.");
            font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
        }

        // Display font information
        Console.WriteLine($"Font family: {font.Name}");
        Console.WriteLine($"Size (pt): {font.Size}");
        Console.WriteLine($"Style: {font.Style}");

        // Render a sample image
        using (var bitmap = new Bitmap(300, 100))
        using (var graphics = Graphics.FromImage(bitmap))
        {
            graphics.Clear(Color.White);
            graphics.DrawString("Hello, World!", font, Brushes.Black, new PointF(10, 30));
            bitmap.Save("sample.png");
        }

        Console.WriteLine("Sample image saved as sample.png");
    }
}
```

### 运行方式

1. 将代码保存为 `Program.cs`。  
2. 在文件所在目录打开终端。  
3. 执行 `dotnet new console -n FontDemo`（如需创建项目骨架）。  
4. 用上述代码替换生成的 `Program.cs`。  
5. 运行 `dotnet add package System.Drawing.Common`（.NET Core/5+ 必需）。  
6. 使用 `dotnet run` 构建并运行。  

你将看到控制台输出的字体属性，并在项目文件夹中生成 `sample.png`。

## 常见陷阱及规避方法

| 陷阱 | 产生原因 | 解决方案 |
|------|----------|----------|
| **缺少 `System.Drawing.Common` 包** | .NET Core 默认不包含 `System.Drawing`。 | 运行 `dotnet add package System.Drawing.Common`。 |
| **字体族未安装** | 无头 Docker 镜像通常缺少 Windows 字体。 | 使用回退字体或在容器中安装所需字体。 |
| **错误使用 `|`** | 使用 `+` 而非 `|` 会导致无效组合。 | 始终使用位或运算符 (`|`) 合并 `FontStyle` 值。 |
| **未释放 `Font` 对象** | 不调用 `Dispose` 会泄漏 GDI 资源。 | 将 `Font` 包装在 `using` 块中，或在使用完后调用 `font.Dispose()`。 |

## 结论

现在你已经掌握了在 C# 中 **创建粗斜体字体** 的方法，并能够安全、高效地 **在 C# 中创建字体**。本教程涵盖了导入正确命名空间、组合 `FontStyle` 标志、验证结果、渲染可视化示例以及处理缺失字体族的技巧。

接下来，你可以进一步探索：

* **创建下划线或删除线字体** – 添加 `FontStyle.Underline` 或 `FontStyle.Strikeout`。  
* **使用自定义 TrueType 字体** – 通过 `PrivateFontCollection` 加载 `.ttf` 文件。  
* **在 WinForms、WPF 或 PDF 生成中使用字体** – 同一个 `Font` 对象即可传递给 UI 控件或第三方库。

尽情尝试不同的字体族、大小和样式组合吧。如遇问题，请回顾 “常见陷阱” 表格或查阅官方 [.NET 文档 for System.Drawing.Font](https://learn.microsoft.com/dotnet/api/system.drawing.font)。祝编码愉快！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，提供完整的代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [Cara Menggabungkan Font Secara Programatis di C# – Panduan Langkah demi Langkah](/html/indonesian/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/)
- [Create HTML Document with Styled Text and Export to PDF – Full Guide](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [convert docx to png – create zip archive c# tutorial](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}