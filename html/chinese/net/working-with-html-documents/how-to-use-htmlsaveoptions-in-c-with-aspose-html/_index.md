---
category: general
date: 2026-09-10
description: 学习如何在 C# 中使用 HtmlSaveOptions 控制网页字体样式并使用 Aspose.HTML 保存 HTML 文件。包括完整的代码示例和实用技巧。
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
language: zh
lastmod: 2026-09-10
og_description: 如何在 C# 中使用 HtmlSaveOptions 在使用 Aspose.HTML 保存 HTML 时启用粗体和斜体网络字体样式。请查看完整示例和最佳实践技巧。
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: 在 C# 中使用 Aspose.HTML 的 HtmlSaveOptions – 步骤指南
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
title: 如何在 C# 中使用 Aspose.HTML 的 HtmlSaveOptions
url: /zh/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.HTML 的 HtmlSaveOptions

如果您需要控制 Aspose.HTML 保存 HTML 文档的方式，**学习如何使用 HtmlSaveOptions 至关重要**。本教程将逐步演示如何使用 HtmlSaveOptions 在保存文档时启用粗体和斜体网络字体样式。

Aspose HTML 库提供了丰富的 API 用于加载、操作和导出 HTML 内容。阅读本指南后，您将能够：

* 将现有 HTML 文件加载到 `HTMLDocument` 中。
* 配置 `HtmlSaveOptions` 以应用特定的 `WebFontStyle` 标志。
* 将修改后的文档保存到新位置或流中。
* 将解决方案扩展到其他字体样式、 自定义 CSS 和错误处理。

## 前提条件

在开始之前，请确保您已拥有：

* 已安装 .NET 6.0 或更高版本。
* 有效的 **Aspose.HTML for .NET** 许可证（免费试用可用于本示例）。
* Visual Studio 2022（或任何 C# IDE）用于编译和运行代码。

除 `Aspose.HTML` 之外，无需其他 NuGet 包。

## 步骤 1：设置项目并导入命名空间

创建一个新的 **Console App** 项目并添加 Aspose.HTML NuGet 包：

```bash
dotnet add package Aspose.HTML
```

然后，在 `Program.cs` 顶部导入所需的命名空间：

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

这些命名空间公开了在本教程中将使用的 `HTMLDocument`、`HtmlSaveOptions` 和 `WebFontStyle` 类型。

## 步骤 2：加载源 HTML 文档

第一步是读取您想要处理的 HTML。将 `"YOUR_DIRECTORY/input.html"` 替换为实际文件路径。

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` 解析标记，构建 DOM 树，并准备好进行操作。如果文件不存在，将抛出异常，因此在生产代码中可能需要将此调用包装在 try‑catch 块中。

## 步骤 3：创建并配置 HtmlSaveOptions

`HtmlSaveOptions` 让您可以微调保存过程。要启用粗体和斜体网络字体样式，请使用位或运算符 (`|`) 组合相应的 `WebFontStyle` 标志。

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### 为什么要配置 WebFontStyle？

导出 HTML 文档时，Aspose.HTML 可以嵌入与原始样式匹配的网络字体。通过设置 `WebFontStyle`，您告诉导出器要包含哪些字体变体。当只需要特定样式时，这可以减小最终文件大小，并确保渲染输出与源文件一致。

#### 常见变体

| 所需样式 | 对应的 `WebFontStyle` 标志 |
|---------------|-----------------------------------|
| Normal (regular) | `WebFontStyle.Regular` |
| Bold | `WebFontStyle.Bold` |
| Italic | `WebFontStyle.Italic` |
| Bold + Italic | `WebFontStyle.Bold | WebFontStyle.Italic` |
| All variants | `WebFontStyle.All` |

您可以根据实际需求组合任意组合。

## 步骤 4：使用配置好的选项保存文档

现在将文档写入新文件。`Save` 方法接受目标路径和您准备好的 `HtmlSaveOptions` 实例。

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

如果需要写入内存流（例如通过 HTTP 发送文件），请使用接受 `Stream` 对象的重载：

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## 步骤 5：验证结果

在浏览器中打开 `output.html`，或使用文本编辑器检查文件。您应该看到 `<style>` 块现在包含了原始文档中引用的所有网络字体的粗体和斜体 `@font-face` 规则。

**预期输出片段：**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

如果原始 HTML 引用了仅包含常规粗细的字体族，Aspose.HTML 将仅包含该文件，遵循 `WebFontStyle` 配置。

## 高级：使用 HtmlSaveOptions 的其他功能

### 5.1 控制 CSS 嵌入

您可以决定是将 CSS 内联嵌入、保留外部链接，还是全部嵌入：

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 保存为特定编码

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 处理大型文档

对于非常大的 HTML 文件，考虑将输出流式写入，以避免高内存消耗：

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 错误处理最佳实践

将整个工作流包装在 try‑catch 块中并记录异常详情。这样可以捕获任何 I/O 或解析错误：

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

## 专业提示：在多个保存操作中复用 HtmlSaveOptions

如果需要使用相同的字体样式配置保存多个文档，请创建单个 `HtmlSaveOptions` 实例并复用它。这可以减少对象分配开销，并保证输出一致。

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

## 完整可运行示例

下面是整合所有步骤的完整程序。将其复制到 `Program.cs`，并在调整文件路径后运行。

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

### 预期控制台输出

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

打开生成的 `output.html`，确认其中包含粗体和斜体网络字体样式。

## 结论

您现在已经掌握了 **如何使用 HtmlSaveOptions** 来控制使用 Aspose HTML 库在 C# 中保存 HTML 时的网络字体嵌入、CSS 处理和编码。通过配置 `WebFontStyle` 标志，您可以仅包含所需的字体变体，从而提升性能并减小文件体积。

接下来，您可以探索其他 `HtmlSaveOptions` 属性，如 `ImageSavingMode`、`JavaScriptSavingMode`，或将多个选项组合用于复杂的转换流水线。尝试将保存到流的方式用于 Web API，或将此工作流集成到更大的文档生成系统中。

---

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步掌握 API 的其他功能，并在项目中探索替代实现方案。每个资源都包含完整的可运行代码示例和逐步说明。

- [如何使用 Aspose.Html 保存 HTML – 完整 C# 指南](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [如何在 C# 中使用 Aspose 将 HTML 渲染为 PNG](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [如何使用 Aspose 将 HTML 渲染为 PNG – 步骤指南](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}