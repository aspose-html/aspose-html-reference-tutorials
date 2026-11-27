---
category: general
date: 2026-11-27
description: 使用 Python 将 HTML 转换为 Markdown，并在支持 GitLab 风格的 Markdown 的情况下从 HTML 生成
  Markdown。了解如何设置 Markdown 格式化器以及将 HTML 导出为 Markdown。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab flavored markdown
- export html as markdown
- generate markdown from html
- set markdown formatter
language: zh
lastmod: 2026-11-27
og_description: 使用 Python 和 GitLab 风格的 Markdown 将 HTML 转换为 Markdown。本指南展示了如何设置 Markdown
  格式化器并在几步内将 HTML 导出为 Markdown。
og_image_alt: Diagram illustrating how to convert html to markdown using a Python
  script
og_title: 在 Python 中使用 GitLab 风格的 Markdown 将 HTML 转换为 Markdown
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Convert html to markdown using Python and generate markdown from html
    with GitLab‑flavored markdown support. Learn how to set markdown formatter and
    export html as markdown.
  headline: Convert html to markdown with GitLab‑flavored Markdown using Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
title: 使用 Python 将 HTML 转换为 GitLab 风格的 Markdown
url: /zh/python/general/convert-html-to-markdown-with-gitlab-flavored-markdown-using/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 将 html 转换为 GitLab‑flavored Markdown

如果您需要 **convert html to markdown**，本指南提供了一个完整、可直接运行的解决方案。您将看到如何 **export html as markdown**，选择 **GitLab‑flavored markdown** 格式，并 **set markdown formatter** 选项，以使输出符合您仓库的渲染规则。

在接下来的章节中，我们将逐行讲解代码，说明每个设置为何重要，并涵盖常见的变体，例如仅保留链接和段落或切换到默认风格。完成后，您将能够在一次函数调用中 **generate markdown from html**。

## 前置条件

* 已安装 Python 3.8+  
* 已通过 `pip install aspose-words` 安装 `aspose.words`（或提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 的类似库）  
* 一个您想要转换的小 HTML 文件，例如位于已知目录下的 `sample.html`  

不需要额外的工具；本教程仅使用库内置的转换引擎。

## 步骤 1：加载要转换的 HTML 文档

转换流水线首先将源文件加载到 `HTMLDocument` 对象中。该对象解析 HTML 标记并为后续转换做好准备。

```python
from aspose.words import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

# Load the HTML file you wish to convert
html_doc = HTMLDocument("YOUR_DIRECTORY/sample.html")
```

*此步骤的重要性*：`HTMLDocument` 会规范化 HTML 结构，解析相对 URL，并创建 markdown 引擎可遍历的 DOM。跳过此步骤会导致转换器读取原始文本，从而出现标签缺失或链接损坏。

## 步骤 2：创建 Markdown 保存选项并配置所需的风格和功能

这里我们 **set markdown formatter** 选项。`format` 属性选择 markdown 风格——`"GIT"` 生成 **GitLab‑flavored markdown**，而 `"DEFAULT"` 则产生标准的 CommonMark。

```python
# Create a MarkdownSaveOptions instance
md_options = MarkdownSaveOptions()

# Set the formatter to GitLab‑flavored markdown
md_options.formatter = "GIT"  # alternatives: "DEFAULT", "MARKDOWN"

# Choose which markdown features to keep.
# In this example we keep only links and paragraphs.
md_options.features = (
    MarkdownFeatures.LINK |
    MarkdownFeatures.PARAGRAPH
)
```

*此步骤的重要性*：不同平台（GitHub、GitLab、Bitbucket）对 markdown 的解释略有差异。通过 **set markdown formatter** 为 `"GIT"`，可确保表格、任务列表及其他 GitLab‑specific 语法正确渲染。`features` 标志允许您 **export html as markdown**，同时剔除不需要的元素，使输出在文档或 README 文件中保持整洁。

## 步骤 3：使用配置好的选项将 HTML 文档转换为 Markdown

在加载源文件并准备好选项后，调用静态的 `convert` 方法。此一次调用完成所有繁重的转换工作。

```python
# Perform the conversion and write the result to a .md file
Converter.convert(html_doc, md_options, "YOUR_DIRECTORY/sample.md")
```

*此步骤的重要性*：`Converter` 类抽象了整个转换流水线。它读取 `HTMLDocument` 中的 DOM，应用您 **set markdown formatter** 的格式化器，遵循所选的 `features`，并写入最终的 markdown 文件。结果是一个干净、兼容 GitLab 的 `.md` 文件，已准备好进行版本控制。

## 预期输出

假设 `sample.html` 包含一个带链接的简单段落：

```html
<p>Check out the <a href="https://example.com">example site</a> for more info.</p>
```

生成的 `sample.md` 将如下所示：

```markdown
Check out the [example site](https://example.com) for more info.
```

由于我们将功能限制为 `LINK` 和 `PARAGRAPH`，原始 HTML 中的任何图片、表格或脚本都会被省略。如果需要更丰富的转换，请相应地调整 `md_options.features`（例如，添加 `MarkdownFeatures.IMAGE`）。

## 步骤 4：验证转换并处理边缘情况

在批量处理大量文件时，最好将输出文件重新读取到 Python 中，以验证转换是否成功。

```python
# Verify the markdown file exists and print its first lines
import pathlib

output_path = pathlib.Path("YOUR_DIRECTORY/sample.md")
if output_path.is_file():
    print("Conversion succeeded. First 3 lines:")
    print("\n".join(output_path.read_text().splitlines()[:3]))
else:
    raise FileNotFoundError("The markdown file was not created.")
```

**常见边缘情况**

| Situation | How to address it |
|-----------|-------------------|
| **相对图片 URL** – 在 markdown 中会变成失效链接 | 使用 `md_options.features |= MarkdownFeatures.IMAGE`，然后在 markdown 中后处理以重写图片路径。 |
| **复杂表格** – GitLab 对表格的支持有限 | 保留默认格式化器（`"DEFAULT"`），或在转换后手动调整表格语法。 |
| **Unicode 字符** – 可能显示为转义序列 | 确保您的 Python 脚本以 `encoding="utf-8"` 打开文件，并在库提供时设置 `md_options.encoding = "UTF-8"`。 |

## 专业提示：批量转换整个文件夹

如果您需要为数十个文件 **generate markdown from html**，可以将上述三步放入循环中：

```python
import os

source_dir = "YOUR_DIRECTORY"
target_dir = "YOUR_DIRECTORY/markdown"

os.makedirs(target_dir, exist_ok=True)

for filename in os.listdir(source_dir):
    if filename.lower().endswith(".html"):
        html_path = os.path.join(source_dir, filename)
        md_path = os.path.join(target_dir, os.path.splitext(filename)[0] + ".md")

        html_doc = HTMLDocument(html_path)
        md_options = MarkdownSaveOptions()
        md_options.formatter = "GIT"
        md_options.features = MarkdownFeatures.LINK | MarkdownFeatures.PARAGRAPH

        Converter.convert(html_doc, md_options, md_path)
        print(f"Converted {filename} → {os.path.basename(md_path)}")
```

此脚本会对每个 `.html` 文件 **export html as markdown**，在整个批处理过程中保持 GitLab 风格。

## 结论

您现在拥有完整的、可投入生产的方式来 **convert html to markdown**，选择 **GitLab‑flavored markdown** 输出，并 **set markdown formatter** 选项以匹配项目需求。按照上述步骤，您可以可靠地 **export html as markdown**、**generate markdown from html**，并根据需要对批量处理或自定义功能集进行调整。

接下来，您可以考虑探索：

* 在 **export html as markdown** 时添加 `MarkdownFeatures.IMAGE`，以保留内联图片，实现更丰富的文档。
* 如果需要更通用的 markdown 文件，可将格式化器切换为 `"DEFAULT"`。
* 将此转换集成到 CI/CD 流水线中，使每个 HTML 报告自动转换为 Markdown 产物。

祝编码愉快，尽情享受从 HTML 到干净、GitLab‑ready markdown 的无缝转换！

## 接下来该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都提供完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能，并在项目中探索替代实现方案。

- [如何使用自定义格式化器在 Python 中将 HTML 转换为 Markdown](/html/english/python/general/how-to-convert-html-to-markdown-with-a-custom-formatter-in-p/)
- [如何使用 Python 将 HTML 转换为带图片的 Markdown](/html/english/python/general/how-to-convert-html-to-markdown-with-images-using-python/)
- [使用 Python 将 HTML 转换为 Markdown – 完整指南](/html/english/python/general/how-to-convert-html-to-markdown-with-python-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}