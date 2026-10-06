---
category: general
date: 2026-10-05
description: 使用 Python 将 HTML 转换为 GitLab Markdown 风格的 Markdown。了解如何将 HTML 保存为 Markdown，并在三个清晰的步骤中将
  HTML 导出为 Markdown。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab markdown flavor
- save html as markdown
- export html to markdown
- how to convert html
language: zh
lastmod: 2026-10-05
og_description: 使用 Python 将 HTML 转换为 GitLab 风格的 Markdown。按照此分步指南，将 HTML 保存为 Markdown
  并高效导出为 Markdown。
og_image_alt: Diagram showing the flow from HTML document to Markdown file using GitLab
  flavor
og_title: 使用 GitLab 风格将 HTML 转换为 Markdown – Python 指南
schemas:
- author: Aspose
  dateModified: '2026-10-05'
  description: Convert HTML to Markdown with GitLab markdown flavor using Python.
    Learn how to save HTML as Markdown and export HTML to Markdown in three clear
    steps.
  headline: Convert HTML to Markdown using GitLab flavor in Python
  type: TechArticle
- description: Convert HTML to Markdown with GitLab markdown flavor using Python.
    Learn how to save HTML as Markdown and export HTML to Markdown in three clear
    steps.
  name: Convert HTML to Markdown using GitLab flavor in Python
  steps:
  - name: Why choose the GitLab flavor?
    text: '* **Consistency with GitLab repositories** – When the generated file lands
      in a GitLab repo, the markdown renders exactly as it would if you wrote it by
      hand. * **Extended syntax support** – Features like task lists (`- [ ]`) and
      tables (`|`) are interpreted correctly. * **Future‑proofing** – GitLab'
  - name: Expected output
    text: 'If `sample.html` contains:'
  - name: Common pitfalls
    text: '| Issue | Cause | Fix | |-------|-------|-----| | Empty output file | `HTMLDocument`
      path is wrong or file is unreadable | Double‑check the path and file permissions
      | | Missing links | `features` list does not include `LINK` | Add `MarkdownSaveOptions.Feature.LINK`
      to the list | | Unexpected HTML t'
  - name: Extending the script
    text: '* **Export HTML to Markdown with images** – Add `MarkdownSaveOptions.Feature.IMAGE`
      to the `features` list. * **Batch conversion** – Wrap the conversion call in
      a loop that iterates over all `.html` files in a directory. * **Custom post‑processing**
      – Read the generated `.md` file, apply regex repla'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Conversion
title: 在 Python 中使用 GitLab 风格将 HTML 转换为 Markdown
url: /zh/python/general/convert-html-to-markdown-using-gitlab-flavor-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 HTML 转换为 GitLab 风格的 Markdown（Python 实现）

如果你需要 **将 HTML 转换为 Markdown**，本教程提供了一个完整、可直接运行的解决方案。阅读完本指南后，你将能够 **将 HTML 保存为 Markdown** 并 **使用 GitLab Markdown 风格导出 HTML 为 Markdown**，全部通过一段简短的 Python 脚本实现。

你将了解为何 GitLab 风格重要、如何配置转换选项，以及最终生成的 Markdown 长什么样。无需外部工具——只需示例代码中使用的库以及几行 Python 代码。

## 将 HTML 转换为 Markdown – 概览

转换过程包括三个逻辑步骤：

1. 加载源 HTML 文件。  
2. 定义 Markdown 选项（GitLab 风格、选择的特性）。  
3. 执行转换并写入输出文件。

每一步都直接对应示例代码中的一行或一个代码块，便于阅读和修改。

## 环境准备

在编写代码之前，请确保已安装所需的包。示例使用的假想库 `html2md` 提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 类。

```bash
pip install html2md
```

> **小贴士：** 通过运行 `python -c "import html2md; print(html2md.__version__)"` 来验证安装。该库支持 Python 3.8 及以上版本。

## 配置 GitLab Markdown 风格

GitLab Markdown 风格（有时称为 *GFM*，即 GitHub Flavored Markdown）增加了任务列表、表格等普通 Markdown 所不具备的扩展。要启用它，只需将 `MarkdownSaveOptions` 的 `formatter` 属性设为 `GIT`。你还可以限制转换仅包含特定特性——本例中仅保留链接和段落。

```python
from html2md import HTMLDocument, MarkdownSaveOptions, Converter

# Step 1: Load the HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/sample.html")

# Step 2: Set up Markdown conversion options
md_options = MarkdownSaveOptions()
md_options.formatter = MarkdownSaveOptions.Formatter.GIT   # GitLab markdown flavor
md_options.features = [
    MarkdownSaveOptions.Feature.LINK,        # Preserve hyperlinks
    MarkdownSaveOptions.Feature.PARAGRAPH   # Keep paragraph breaks
]
```

### 为什么选择 GitLab 风格？

* **与 GitLab 仓库保持一致** – 当生成的文件提交到 GitLab 仓库时，Markdown 的渲染效果与手写完全相同。  
* **扩展语法支持** – 任务列表（`- [ ]`）和表格（`|`）等特性能够被正确解释。  
* **面向未来** – GitLab 的解析器持续维护，降低渲染错误的风险。

如果你想使用其他风格（例如 CommonMark），只需将 `Formatter.GIT` 替换为相应的枚举值。

## 执行转换

准备好文档对象和选项后，调用静态的 `convert` 方法。此调用会读取 HTML、应用选定的特性，并将结果写入 `.md` 文件。

```python
# Step 3: Convert the HTML to a Markdown file
Converter.convert(html_doc, "YOUR_DIRECTORY/sample.md", md_options)
```

脚本执行完毕后，`sample.md` 即为转换后的内容。文件遵循 GitLab Markdown 风格，任何 GitLab UI 都会正确渲染。

## 验证输出并处理边缘情况

### 预期输出

如果 `sample.html` 的内容为：

```html
<h1>Welcome</h1>
<p>This is a <a href="https://example.com">sample link</a> inside a paragraph.</p>
```

生成的 `sample.md` 将会是：

```markdown
# Welcome

This is a [sample link](https://example.com) inside a paragraph.
```

请注意：

* 标题被转换为 Markdown 的 `#` 级标题。  
* 链接使用了标准的 GitLab 语法。  
* 由于我们将 `features` 限制为 `LINK` 和 `PARAGRAPH`，只有段落和链接被保留下来。

### 常见陷阱

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 输出文件为空 | `HTMLDocument` 路径错误或文件不可读 | 检查路径及文件权限 |
| 链接缺失 | `features` 列表未包含 `LINK` | 将 `MarkdownSaveOptions.Feature.LINK` 加入列表 |
| 出现意外的 HTML 标签 | 特性列表包含 `ALL` 或更宽泛的集合 | 将 `features` 限制为仅需要的（如 `PARAGRAPH`、`LINK`） |
| GitLab 特有语法未渲染 | `formatter` 设置为非 GitLab 值 | 将 `md_options.formatter = MarkdownSaveOptions.Formatter.GIT` |

### 脚本扩展

* **导出带图片的 HTML 为 Markdown** – 在 `features` 列表中加入 `MarkdownSaveOptions.Feature.IMAGE`。  
* **批量转换** – 将转换调用放入循环，遍历目录下所有 `.html` 文件。  
* **自定义后处理** – 读取生成的 `.md` 文件，使用正则替换后再写回最终版本。

## 保存 HTML 为 Markdown – 快速回顾

1. 使用 `HTMLDocument` **加载** HTML 文件。  
2. **配置** `MarkdownSaveOptions`，使用 GitLab Markdown 风格并仅选择所需特性。  
3. 通过 `Converter.convert` **转换**，并指定输出路径。

这三步即构成了本库的完整 **HTML 转 Markdown** 工作流。

## 结论

现在，你已经掌握了如何在 Python 中使用 GitLab Markdown 风格 **将 HTML 转换为 Markdown**。本指南从环境搭建到输出验证全方位覆盖，并展示了如何 **保存 HTML 为 Markdown** 以及 **导出 HTML 为 Markdown**，同时对特性进行细粒度控制。

接下来，你可以进一步探索：

* **添加表格和代码块** – 使用 `MarkdownSaveOptions.Feature.TABLE` 与 `FEATURE.CODE`。  
* **将脚本集成到 CI/CD 流水线** – 在每次合并时自动生成文档。  
* **比较其他风格** – 尝试 `Formatter.COMMONMARK` 以观察差异。

欢迎随意实验各种选项，将脚本改造成批量处理，或与静态站点生成器结合使用。祝转换愉快！

## 接下来你可以学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并在项目中尝试不同实现方式。每篇资源均提供完整可运行的代码示例和逐步解释。

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}