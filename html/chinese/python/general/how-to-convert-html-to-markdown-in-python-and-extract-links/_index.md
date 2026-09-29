---
category: general
date: 2026-09-29
description: 在 Python 中将 HTML 转换为 Markdown，同时提取 HTML 中的链接和段落。学习如何以细粒度控制将 HTML 保存为
  Markdown。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- extract paragraphs from html
- convert html to markdown python
language: zh
lastmod: 2026-09-29
og_description: 使用 Aspose.HTML 在 Python 中将 HTML 转换为 Markdown。本指南展示了如何从 HTML 中提取链接、提取段落以及将
  HTML 保存为 Markdown。
og_image_alt: Screenshot of Python code converting an HTML file to a partial Markdown
  file
og_title: 在 Python 中将 HTML 转换为 Markdown – 提取链接和段落
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: convert HTML to markdown in Python while extracting links from HTML
    and paragraphs. Learn to save HTML as markdown with fine‑grained control.
  headline: How to convert HTML to Markdown in Python and extract links and paragraphs
  type: TechArticle
tags:
- Python
- Aspose.HTML
- Markdown conversion
title: 如何在 Python 中将 HTML 转换为 Markdown 并提取链接和段落
url: /zh/python/general/how-to-convert-html-to-markdown-in-python-and-extract-links/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中将 HTML 转换为 Markdown 并提取链接和段落

如果您需要在 Python 中 **将 HTML 转换为 markdown**，本教程为您提供一个即开即用的解决方案。无论您是在构建静态站点生成器还是采集文档，您都将学习如何从 HTML 中提取链接、提取段落，并以精确控制的方式将 HTML 保存为 markdown。

您将在本指南的最后获得一个完整脚本，该脚本读取 HTML 文件，只选择您关心的元素，并写入仅包含这些元素的 Markdown 文件。无需外部 CLI 工具——所有操作均使用纯 Python 并借助 Aspose.HTML 库完成。

## 前置条件

* 已安装 Python 3.8 或更高版本。
* 有效的 Aspose.HTML for Python 许可证（免费试用可用于评估）。
* 使用 `pip install aspose-html` 安装 SDK。
* 一个位于可引用文件夹中的示例 HTML 文件（`sample.html`）。

如果您尚未安装 SDK，请运行：

```bash
pip install aspose-html
```

## 步骤 1：加载要转换的 HTML 文档

第一步是创建一个表示源文件的 `HTMLDocument` 对象。构造函数接受文件路径或流，因此您可以将其指向任何本地或远程的 HTML 源。

```python
from aspose.html import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

# Load the HTML file you want to convert
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

**为什么这很重要：** `HTMLDocument` 将标记解析为 DOM 树，提供对每个元素的编程访问。此步骤是必需的，因为转换器在文档对象上工作，而不是在原始文本上。

## 步骤 2：配置哪些 HTML 元素应转换为 Markdown

Aspose.HTML 通过 `MarkdownSaveOptions` 让您对转换进行精细调节。通过设置 `features` 标志，您可以决定源文件的哪些部分会以 Markdown 形式输出。在本教程中，我们仅启用 **links** 和 **paragraphs**，满足二级关键词 *extract links from html* 和 *extract paragraphs from html*。

```python
# Create Markdown save options
md_opts = MarkdownSaveOptions()

# Enable only links and paragraphs; all other elements are ignored
md_opts.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

**为什么这很重要：** 如果省略此配置，转换器将翻译整个页面，包括图像、表格和脚本。通过限制功能集，您可以保持输出小且聚焦，这对于内容抓取流水线非常理想。

## 步骤 3：执行转换并保存结果

在文档已加载且选项已设置后，调用 `Converter.convert_html`。该方法会直接将 Markdown 文件写入磁盘。

```python
# Destination path for the generated Markdown file
md_path = "YOUR_DIRECTORY/partial.md"

# Convert the HTML document to Markdown using the configured options
Converter.convert_html(html_doc, md_opts, md_path)

print(f"Markdown saved to {md_path}")
```

**您将看到：** 如果 `sample.html` 包含段落和链接，`partial.md` 将包含类似如下内容：

```markdown
This is a sample paragraph extracted from the HTML file.

[Visit Aspose](https://www.aspose.com)
```

所有其他元素（图像、表格、脚本）都会被省略，因为我们仅启用了 `LINKS` 和 `PARAGRAPHS`。

## 完整脚本 – 可直接复制运行

下面是完整的可运行程序，整合了上述三个步骤。将 `YOUR_DIRECTORY` 替换为包含 `sample.html` 的绝对或相对路径。

```python
# convert_html_to_markdown.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(
    source_html: str,
    target_md: str,
    include_links: bool = True,
    include_paragraphs: bool = True,
) -> None:
    """
    Convert an HTML file to a Markdown file, optionally extracting only links
    and/or paragraphs.

    Args:
        source_html: Path to the input HTML file.
        target_md:   Path where the Markdown output should be written.
        include_links:      When True, <a> elements become Markdown links.
        include_paragraphs: When True, <p> elements become plain text paragraphs.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_html)

    # Prepare save options
    md_opts = MarkdownSaveOptions()
    features = 0
    if include_links:
        features |= MarkdownFeatures.LINKS
    if include_paragraphs:
        features |= MarkdownFeatures.PARAGRAPHS
    md_opts.features = features

    # Convert and save
    Converter.convert_html(html_doc, md_opts, target_md)
    print(f"Conversion complete: {target_md}")

if __name__ == "__main__":
    # Example usage
    convert_html_to_markdown(
        source_html="YOUR_DIRECTORY/sample.html",
        target_md="YOUR_DIRECTORY/partial.md",
        include_links=True,
        include_paragraphs=True,
    )
```

### 运行脚本

```bash
python convert_html_to_markdown.py
```

您应该会看到确认信息，并在同一文件夹中找到 `partial.md`。

## 处理边缘情况和常见变体

| Situation | Recommended tweak | Reason |
|-----------|-------------------|--------|
| **您还需要标题** | 在 `features` 标志中添加 `MarkdownFeatures.HEADINGS`。 | 标题有助于生成目录。 |
| **需要保留图像** | 包含 `MarkdownFeatures.IMAGES`。 | 转换器将使用 `![]()` 语法嵌入图像链接。 |
| **大型 HTML 文件导致内存压力** | 使用带缓冲的流调用 `HTMLDocument.from_stream`，然后分块转换。 | 流式处理可降低峰值内存使用。 |
| **您想保留内联样式** | 设置 `md_opts.inline_styles = True`。 | 这会将 CSS 样式保留为 Markdown 中的内联 HTML，适用于电子邮件模板。 |
| **Unicode 字符被破坏** | 确保源文件保存为 UTF‑8，并在创建 `HTMLDocument` 时传入 `encoding='utf-8'`。 | 正确的编码可避免字符乱码。 |

## 可靠转换的专业技巧

* **先验证 HTML** – 错误的标记可能导致元素缺失。如果怀疑有问题，请使用 `html_doc.validate()`。
* **记录已启用的功能** – 在转换前打印 `md_opts.features` 有助于调试为何某个元素缺失。
* **使用最小 HTML 片段进行测试** – 仅包含 `<p>` 和 `<a>` 的文件可快速验证标志逻辑。
* **版本锁定** – Aspose.HTML 的发布向后兼容，但请在 `requirements.txt` 中固定 SDK 版本，以避免意外的破坏性更改。

## 结论

现在您已经了解如何在 Python 中 **将 HTML 转换为 markdown**，并精确 **从 HTML 中提取链接** 和 **提取段落**。通过配置 `MarkdownSaveOptions`，您还可以 **将 HTML 保存为 markdown**，并根据需要选择任意元素组合，使该过程在网页抓取、文档流水线或静态站点生成中具备灵活性。

接下来您可以探索的步骤包括：

* 添加 `MarkdownFeatures.HEADINGS` 和 `MarkdownFeatures.IMAGES` 以生成更丰富的 Markdown。
* 将脚本集成到 CI/CD 工作流中，自动从 HTML 源生成文档。
* 将输出与 MkDocs 或 Hugo 等静态站点生成器结合，实现全自动发布流水线。

欢迎尝试不同的 `MarkdownFeatures` 标志并分享您的成果。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，构建在本指南演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [在 Aspose.HTML for Java 中将 HTML 转换为 Markdown](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [在 .NET 中使用 Aspose.HTML 将 HTML 转换为 Markdown](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [将 markdown 转换为 html – Java 指南并输出 PDF](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}