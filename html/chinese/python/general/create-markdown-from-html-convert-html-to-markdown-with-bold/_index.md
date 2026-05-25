---
category: general
date: 2026-05-25
description: 学习如何从 HTML 创建 Markdown，并在将 HTML 转换为 Markdown 时保留粗体文本、链接和列表。
draft: false
keywords:
- create markdown from html
- convert html to markdown
- how to keep bold
- how to generate markdown
- convert html list
language: zh
og_description: 轻松将 HTML 转换为 Markdown。本指南展示如何将 HTML 转换为 Markdown，保持粗体格式，并处理列表。
og_title: 从HTML生成Markdown – 将HTML转换为Markdown的快速指南
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to create markdown from html and convert html to markdown
    while preserving bold text, links, and lists.
  headline: Create Markdown from HTML – Convert HTML to Markdown with Bold and Links
  type: TechArticle
- description: Learn how to create markdown from html and convert html to markdown
    while preserving bold text, links, and lists.
  name: Create Markdown from HTML – Convert HTML to Markdown with Bold and Links
  steps:
  - name: 1. What if my HTML contains nested lists?
    text: 'The `LIST` feature automatically respects nesting levels, converting `<ul><li><ul>...</ul></li></ul>`
      into indented markdown:'
  - name: 2. How do I keep other formatting like italics or code blocks?
    text: 'Add the relevant flags:'
  - name: 3. My links have absolute URLs—will they stay intact?
    text: Absolutely. The converter copies the `href` attribute verbatim, so `[Google](https://google.com)`
      appears exactly as expected.
  - name: 4. I need the markdown file in a different encoding (UTF‑8 vs. UTF‑16)?
    text: '`MarkdownSaveOptions` exposes an `encoding` property:'
  - name: 5. Can I convert an entire HTML file instead of a string?
    text: 'Yes—just load the file into an `HTMLDocument`:'
  type: HowTo
tags:
- markdown
- html
- conversion
- python
- aspose-words
title: 从HTML创建Markdown – 将HTML转换为带粗体和链接的Markdown
url: /zh/python/general/create-markdown-from-html-convert-html-to-markdown-with-bold/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 HTML 创建 Markdown – 将 HTML 转换为 Markdown 的快速指南

需要快速**create markdown from html**吗？在本教程中，您将学习如何**convert html to markdown**，同时保留粗体文本、链接和列表结构。无论您是构建静态站点生成器，还是只需要一次性转换，下面的步骤都能轻松实现。

我们将使用 Aspose.Words for Python 库演示一个完整、可运行的示例，解释每个设置为何重要，并展示如何保留粗体格式——这是许多开发者常碰到的问题。完成后，您将能够在几秒钟内从任意简单的 HTML 片段生成 markdown。

## 您需要的环境

- Python 3.8+（任何近期版本均可）
- `aspose-words` 包（`pip install aspose-words`）
- 对 HTML 标签的基本了解（列表、`<strong>`、`<a>`）

就这些——无需额外服务，也不需要繁琐的命令行技巧。准备好了吗？让我们开始吧。

![Create markdown from html workflow](image-placeholder.png "Diagram showing create markdown from html workflow")

## 步骤 1：从字符串创建 HTML 文档

首先，需要将原始 HTML 输入到 `HTMLDocument` 对象中。可以把它看作是将字符串转换为 Aspose 能够理解的文档树。

```python
from aspose.words import Document as HTMLDocument

# Your HTML snippet – a simple unordered list with bold text and a link
html_content = """
<ul>
    <li>Item <strong>bold</strong> <a href='#'>link</a></li>
</ul>
"""

# Step 1: Load the HTML into a document object
doc = HTMLDocument(html_content)
```

**为什么这很重要：**  
`HTMLDocument` 解析标记，构建 DOM，并规范化空白。没有这一步，转换器就无法识别 HTML 中哪些部分是列表、链接或 strong 标签——因此您会失去想要保留的格式。

## 步骤 2：设置 Markdown 保存选项 – 保留粗体、链接和列表

现在进入解决“**how to keep bold**”问题的关键部分。Aspose 允许您通过 `MarkdownSaveOptions` 对象选择哪些 HTML 特性会被转换为 markdown。

```python
from aspose.words.saving import MarkdownSaveOptions, MarkdownFeature

# Step 2: Configure which HTML features to retain in markdown
options = MarkdownSaveOptions()
options.features = (
    MarkdownFeature.LIST   |   # Preserve <ul>/<ol> as markdown lists
    MarkdownFeature.STRONG |   # Keep <strong> or <b> as **bold**
    MarkdownFeature.LINK       # Turn <a href> into [text](url)
)
```

**为什么使用这些标志？**  
- `LIST` 确保转换遵循原始顺序——否则会得到纯文本。  
- `STRONG` 将粗体标签映射为 `**bold**`，解决了“how to keep bold”难题。  
- `LINK` 将锚点标签转换为熟悉的 `[link](#)` 语法，满足“**convert html list**”和“**how to generate markdown**”的需求。

如果需要保留其他元素（如图片或表格），只需使用 OR‑操作添加相应的 `MarkdownFeature` 枚举值即可。

## 步骤 3：执行转换并保存文件

文档和选项准备好后，最后一步是一行代码完成繁重的转换工作。

```python
from aspose.words import Converter

# Step 3: Convert the HTML document to markdown and write to disk
output_path = "output/list_strong_link.md"
Converter.convert_html(doc, options, output_path)

print(f"Markdown saved to {output_path}")
```

运行脚本会生成文件 `list_strong_link.md`，其内容如下：

```markdown
- Item **bold** [link](#)
```

**刚才发生了什么？**  
`Converter.convert_html` 读取 DOM，应用特性掩码，并将结果以 markdown 形式输出。输出展示了 markdown 列表（`-`）、用双星号包裹的粗体文本，以及标准的 `[text](url)` 链接格式——正是您在想要**create markdown from html**时所要求的。

## 处理边缘情况和常见问题

### 1. 如果我的 HTML 包含嵌套列表怎么办？

`LIST` 功能会自动遵循嵌套层级，将 `<ul><li><ul>...</ul></li></ul>` 转换为缩进的 markdown：

```markdown
- Parent item
  - Child item
```

只要在需要层级结构时不要禁用 `LIST` 即可。

### 2. 如何保留其他格式，如斜体或代码块？

添加相应的标志：

```python
options.features |= MarkdownFeature.EMPHASIS   # for <em> or <i>
options.features |= MarkdownFeature.CODE      # for <code>
```

### 3. 我的链接是绝对 URL——会保持完整吗？

当然。转换器会原样复制 `href` 属性，因此 `[Google](https://google.com)` 会如预期那样完整显示。

### 4. 我需要 markdown 文件使用不同的编码（UTF‑8 与 UTF‑16）？

`MarkdownSaveOptions` 提供了 `encoding` 属性：

```python
import aspose.words as aw
options.encoding = aw.Encoding.UTF_8
```

### 5. 能否转换整个 HTML 文件而不是字符串？

可以——只需将文件加载到 `HTMLDocument` 中：

```python
doc = HTMLDocument(open("mypage.html", "r", encoding="utf-8").read())
```

## 专业技巧：顺畅的转换体验

- **先验证 HTML。** 损坏的标签可能导致意外的 markdown 输出。使用 `BeautifulSoup(html, "html.parser")` 快速检查会有帮助。  
- **使用绝对路径** 为 `output_path`，如果从不同的工作目录运行脚本，可避免 “file not found” 错误。  
- **批量处理** 多个文件：遍历目录并复用同一个 `options` 对象——这对静态站点生成器非常有用。  
- **开启 `options.pretty_print`**（如果可用），以获得良好缩进的 markdown，便于阅读和对比。

## 完整可运行示例（可直接复制粘贴）

下面是完整脚本，已准备好运行。没有缺失的导入，也没有隐藏的依赖。

```python
# ------------------------------------------------------------
# create_markdown_from_html.py
# ------------------------------------------------------------
# Purpose: Demonstrate how to create markdown from html,
#          keep bold, links, and list structures using Aspose.Words.
# ------------------------------------------------------------

import os
from aspose.words import Document as HTMLDocument, Converter
from aspose.words.saving import MarkdownSaveOptions, MarkdownFeature

# 1️⃣ Define the HTML snippet
html_content = """
<ul>
    <li>Item <strong>bold</strong> <a href='#'>link</a></li>
</ul>
"""

# 2️⃣ Load HTML into a document object
doc = HTMLDocument(html_content)

# 3️⃣ Configure markdown features (list, bold, link)
options = MarkdownSaveOptions()
options.features = (
    MarkdownFeature.LIST |
    MarkdownFeature.STRONG |
    MarkdownFeature.LINK
)

# Optional: set encoding to UTF‑8 (default is UTF‑8)
# options.encoding = aw.Encoding.UTF_8

# 4️⃣ Define output path
output_dir = "output"
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "list_strong_link.md")

# 5️⃣ Convert and save
Converter.convert_html(doc, options, output_path)

print(f"✅ Markdown successfully created at: {output_path}")
# ------------------------------------------------------------
```

使用 `python create_markdown_from_html.py` 运行它，然后打开 `output/list_strong_link.md` 查看结果。

## 小结

我们已经一步步阐述了**how to create markdown from html**的过程，解答了**how to keep bold**，并演示了一个简洁的**convert html to markdown**方法，适用于列表、粗体文本和链接。关键要点是：使用正确的特性标志配置 `MarkdownSaveOptions`，库会完成繁重的工作。

## 接下来怎么办？

- 探索更多 `MarkdownFeature` 标志，以保留图片、表格或引用块。  
- 将此转换与 Jekyll 或 Hugo 等静态站点生成器结合，实现内容自动化流水线。  
- 试验自定义后处理（例如添加 front‑matter），将原始 markdown 转换为可直接发布的博客文章。

对转换复杂 HTML 结构还有疑问吗？留下评论，我们一起解决。祝您玩转 markdown！

## 相关教程

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}