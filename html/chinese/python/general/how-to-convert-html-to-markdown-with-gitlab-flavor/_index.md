---
category: general
date: 2026-09-07
description: 使用 Python 和 GitLab 风格的 Markdown 快速将 HTML 转换为 Markdown。学习如何从 HTML 中提取链接并在一个脚本中保存为
  Markdown 文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- gitlab flavored markdown
- how to convert html
- html to markdown file
language: zh
lastmod: 2026-09-07
og_description: 将 HTML 转换为带有 GitLab 风格格式的 Markdown。本教程展示了如何从 HTML 中提取链接并使用 Python
  生成 Markdown 文件。
og_image_alt: Screenshot of Python code that converts HTML to markdown
og_title: 将 HTML 转换为 GitLab 风格的 Markdown – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: Convert HTML to markdown quickly using Python and GitLab‑flavoured
    markdown. Learn to extract links from HTML and save a markdown file in one script.
  headline: How to convert HTML to markdown with GitLab flavor
  type: TechArticle
- description: Convert HTML to markdown quickly using Python and GitLab‑flavoured
    markdown. Learn to extract links from HTML and save a markdown file in one script.
  name: How to convert HTML to markdown with GitLab flavor
  steps:
  - name: Load the HTML source document
    text: '```python from aspose.html import HTMLDocument'
  - name: Configure GitLab‑flavoured markdown options
    text: '```python from aspose.html import MarkdownSaveOptions'
  - name: Perform the conversion and save the markdown file
    text: '```python from aspose.html import Converter'
  - name: Full script for quick copy‑paste
    text: '```python # convert_html_to_markdown.py """ How to convert HTML to markdown
      (GitLab flavor) and extract links from HTML. """'
  - name: Conclusion
    text: You now know how to **convert HTML to markdown**, extract links from HTML,
      and generate a **GitLab‑flavoured markdown** file using a concise Python script.
      The approach is reliable, works with any valid HTML source, and gives you fine‑grained
      control over which elements are exported. Feel free to ad
  type: HowTo
tags:
- HTML conversion
- Markdown
- Python
- Aspose.HTML
title: 如何将 HTML 转换为 GitLab 风格的 Markdown
url: /zh/python/general/how-to-convert-html-to-markdown-with-gitlab-flavor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 GitLab 风格将 HTML 转换为 markdown

如果您需要**将 HTML 转换为 markdown**，本指南将带您使用 Aspose.HTML 库完成一个完整的 Python 解决方案。我们还将展示**如何从 HTML 中提取链接**并在一次处理过程中生成**GitLab 风格的 markdown**文件。

您将学习：

* 读取 HTML 文档、配置转换选项并写入 markdown 文件所需的完整代码。  
* 在 GitLab 仓库中存储文档时，GitLab markdown 格式化器为何重要。  
* 常见陷阱——例如处理相对 URL 或缺失的 `<p>` 标签——以及如何避免它们。

通过本教程的学习，您可以运行一行脚本，生成仅包含您关心的链接和段落的**html to markdown file**。

## 前置条件

| Requirement | Reason |
|-------------|--------|
| Python ≥ 3.8 | 需要 Aspose.HTML Python 包。 |
| `aspose.html` package | 提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter`。使用 `pip install aspose-html` 安装。 |
| An HTML source file (e.g., `article.html`) | 您想要转换的文件。 |
| Write permission to the output directory | 脚本将创建 `article.md`。 |

> **专业提示：** 使用虚拟环境（`python -m venv venv`）来保持依赖的隔离。

## 安装 Aspose.HTML Python 包

```bash
pip install aspose-html
```

该包已捆绑 Windows、macOS 和 Linux 的本机二进制文件，无需额外的系统库。

## 使用 Aspose.HTML 将 HTML 转换为 markdown

### Step 1: Load the HTML source document

```python
from aspose.html import HTMLDocument

# Replace YOUR_DIRECTORY with the path where article.html lives
html_path = "YOUR_DIRECTORY/article.html"
html_doc = HTMLDocument(html_path)

# Verify that the document loaded correctly
print(f"Loaded HTML title: {html_doc.title}")
```

*此步骤重要原因：* `HTMLDocument` 解析整个 DOM，允许您访问每个元素——包括我们稍后要提取的 `<a>` 标签。

### Step 2: Configure GitLab‑flavoured markdown options

```python
from aspose.html import MarkdownSaveOptions

md_options = MarkdownSaveOptions()
# Choose the GitLab‑flavoured markdown formatter
md_options.formatter = MarkdownSaveOptions.Formatter.GIT

# Export only the features we need:
#   • LINKS – converts <a href=""> into markdown links
#   • PARAGRAPH – keeps <p> content as separate paragraphs
md_options.features = (
    MarkdownSaveOptions.Feature.LINK |
    MarkdownSaveOptions.Feature.PARAGRAPH
)

# Optional: preserve original line breaks (helps with diff tools)
md_options.use_original_line_breaks = True
```

*此步骤重要原因：* **gitlab flavored markdown** 格式化器遵循 GitLab 的扩展语法（例如表格、任务列表）。通过将 `features` 限制为 `LINK` 和 `PARAGRAPH`，我们**extract links from HTML**，同时丢弃图像或脚本等其他元素。

### Step 3: Perform the conversion and save the markdown file

```python
from aspose.html import Converter

output_path = "YOUR_DIRECTORY/article.md"
Converter.convert(html_doc, output_path, md_options)

print(f"Markdown file created at: {output_path}")
```

当脚本执行完毕，`article.md` 只包含 markdown 格式的链接和段落，已准备好提交到 GitLab 仓库。

### Full script for quick copy‑paste

```python
# convert_html_to_markdown.py
"""
How to convert HTML to markdown (GitLab flavor) and extract links from HTML.
"""

from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def convert_html_to_md(html_path: str, md_path: str) -> None:
    """Convert an HTML file to a GitLab‑flavoured markdown file."""
    # Load the source HTML
    html_doc = HTMLDocument(html_path)

    # Set up conversion options
    md_options = MarkdownSaveOptions()
    md_options.formatter = MarkdownSaveOptions.Formatter.GIT
    md_options.features = (
        MarkdownSaveOptions.Feature.LINK |
        MarkdownSaveOptions.Feature.PARAGRAPH
    )
    md_options.use_original_line_breaks = True

    # Convert and save
    Converter.convert(html_doc, md_path, md_options)

if __name__ == "__main__":
    # Adjust these paths to your environment
    src_html = "YOUR_DIRECTORY/article.html"
    dst_md = "YOUR_DIRECTORY/article.md"

    convert_html_to_md(src_html, dst_md)
    print("Conversion complete.")
```

#### Expected output

假设 `article.html` 包含：

```html
<h1>Welcome</h1>
<p>This is a sample paragraph.</p>
<p>Visit <a href="https://example.com">our site</a> for more info.</p>
```

生成的 `article.md` 将是：

```markdown
Welcome

This is a sample paragraph.

Visit [our site](https://example.com) for more info.
```

仅保留段落文本和链接——正是 **extract links from HTML** 选项所承诺的效果。

## 处理常见边缘情况

| Scenario | What to watch for | Suggested fix |
|----------|-------------------|---------------|
| Relative URLs (`href="/path/page.html"`) | GitLab markdown 会将其相对于仓库根目录渲染，可能导致外部链接失效。 | 在转换前添加基准 URL：`md_options.base_uri = "https://mydomain.com"` |
| Empty `<a>` tags (`<a href=""></a>`) | 会产生 `[]()`，在 markdown 中显得异常。 | 转换后使用简单正则过滤空链接：`re.sub(r'\[.*?\]\(\s*\)', '', markdown_text)` |
| Non‑ASCII characters in URLs | 某些 markdown 解析器会错误转义。 | 在传递给转换器之前使用 `urllib.parse.quote` 对 URL 进行编码。 |
| Large HTML files (>10 MB) | `HTMLDocument` 加载整个 DOM 会导致内存激增。 | 如有可用，使用流式 API（`HTMLDocument.load_from_stream`），或将源文件拆分为多个部分。 |

## 验证转换结果

您可以快速验证 markdown 文件仅包含所需的特性：

```python
import pathlib

md_file = pathlib.Path(dst_md)
assert md_file.read_text().strip() != "", "Markdown file is empty!"
print("Markdown preview:")
print(md_file.read_text().splitlines()[:10])  # Show first 10 lines
```

如果断言失败，请再次确认 `md_options.features` 已包含 `LINK` 和 `PARAGRAPH`。

## 后续步骤与相关主题

* **导出额外特性** – 添加 `MarkdownSaveOptions.Feature.IMAGE` 以包含 `<img>` 标签。  
* **转换为其他 markdown 风格** – 将 `md_options.formatter` 切换为 `MarkdownSaveOptions.Formatter.COMMONMARK`，生成通用 markdown。  
* **批量处理** – 遍历 HTML 文件目录，生成一套 markdown 文档。  
* **集成到 CI/CD** – 在 GitLab 流水线中运行脚本，自动保持文档同步。

---

### 结论

您现在已经掌握了如何**convert HTML to markdown**、extract links from HTML，并使用简洁的 Python 脚本生成**GitLab‑flavoured markdown**文件。该方法可靠，适用于任何有效的 HTML 源，并让您对导出的元素拥有细粒度的控制。欢迎将脚本用于批量转换、自定义格式或集成到您的文档工作流中。

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步深化对 API 功能的掌握，并在项目中探索替代实现方案。每个资源均提供完整可运行的代码示例和逐步解释。

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert markdown to html – Java guide with PDF output](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}