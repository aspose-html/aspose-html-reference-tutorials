---
category: general
date: 2026-08-12
description: 使用 Python 将 HTML 转换为 Markdown。学习命令行工作流，将网页转换为 Markdown 并实现文档自动化。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- convert web page to markdown
- convert html to markdown command line
language: zh
lastmod: 2026-08-12
og_description: 使用 Python 将 HTML 转换为 Markdown。本教程展示了一种命令行解决方案，能够快速且可靠地将网页转换为 Markdown。
og_image_alt: Screenshot of Python script that converts HTML to Markdown
og_title: 使用 Python 将 HTML 转换为 Markdown – 步骤指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-12'
  description: Convert HTML to Markdown using Python. Learn a command‑line workflow
    to convert web page to Markdown and automate documentation.
  headline: Convert HTML to Markdown with Python – complete programming guide
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- CLI
title: 使用 Python 将 HTML 转换为 Markdown —— 完整编程指南
url: /zh/python/general/convert-html-to-markdown-with-python-complete-programming-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 将 HTML 转换为 Markdown – 完整编程指南

如果您需要 **convert HTML to Markdown**，本指南为您展示一个可直接运行的解决方案。您将看到一个简短的 Python 脚本如何将任意 HTML 文件转换为干净的、Git 风格的 Markdown，以及如何在命令行中调用相同的逻辑。

将网页转换为 Markdown 是构建静态文档站点或为版本控制仓库准备内容的常见步骤。完成本教程后，您将拥有一个可重复使用的命令行工具，能够处理 HTML 编码、保留链接，并遵循 Git 风格的 Markdown 约定。

## 前提条件

* 在系统上安装了 Python 3.9 或更高版本。
* `groupdocs-conversion` Python 包（或任何提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 的库）。使用以下方式安装：

```bash
pip install groupdocs-conversion
```

* 包含要处理的源 `input.html` 文件的文件夹。

以下章节将逐步演示每一步，解释其重要性，并提供您所需的完整代码。

## 步骤 1：设置环境

创建隔离的虚拟环境可以防止依赖冲突，并使命令行工具可移植。

```bash
# Create a virtual environment in the project folder
python -m venv .venv

# Activate the environment (Windows)
.\.venv\Scripts\activate

# Activate the environment (macOS / Linux)
source .venv/bin/activate

# Install the required library
pip install groupdocs-conversion
```

*此步骤的原因？*  
虚拟环境将 `groupdocs-conversion` 包与其他项目隔离，确保 `convert html to markdown command line` 实用程序使用您测试过的确切版本运行。

## 步骤 2：编写转换脚本

创建一个名为 `html_to_md.py` 的文件并粘贴以下代码。该脚本接受三个参数：输入 HTML 路径、输出 Markdown 路径，以及一个可选标志用于选择 Git 风格的格式化器。

```python
"""html_to_md.py – Convert HTML to Markdown from the command line.

Usage:
    python html_to_md.py INPUT_HTML OUTPUT_MD [--git]

Arguments:
    INPUT_HTML   Path to the source HTML file.
    OUTPUT_MD    Desired path for the generated Markdown file.
    --git        Optional flag to use Git‑flavored Markdown (default is plain).

The script uses GroupDocs.Conversion to read the HTML document,
configure Markdown save options, and write the result to disk.
"""

import argparse
import sys
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, Converter


def parse_arguments() -> argparse.Namespace:
    parser = argparse.ArgumentParser(description="Convert HTML to Markdown.")
    parser.add_argument("input_html", help="Path to the HTML file to convert.")
    parser.add_argument("output_md", help="Path where the Markdown file will be saved.")
    parser.add_argument(
        "--git",
        action="store_true",
        help="Use Git‑flavored Markdown (adds tables, task lists, etc.).",
    )
    return parser.parse_args()


def convert_html_to_markdown(input_path: str, output_path: str, use_git: bool) -> None:
    """Perform the conversion and write the Markdown file."""
    # Load the HTML document
    html_doc = HTMLDocument(input_path)

    # Configure save options
    md_opts = MarkdownSaveOptions()
    if use_git:
        md_opts.formatter = MarkdownSaveOptions.Formatter.GIT

    # Execute the conversion
    Converter.convert_html(html_doc, md_opts, output_path)


def main() -> None:
    args = parse_arguments()
    try:
        convert_html_to_markdown(args.input_html, args.output_md, args.git)
        print(f"✅ Conversion succeeded: '{args.output_md}'")
    except Exception as exc:
        print(f"❌ Conversion failed: {exc}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

### 脚本说明

| 部分 | 目的 |
|---------|---------|
| **Argument parsing** | 启用 **convert html to markdown command line** 的使用模式。 |
| **HTMLDocument** | 加载源文件；库抽象了字符编码和 DOM 解析。 |
| **MarkdownSaveOptions** | 允许在普通 Markdown 与 Git 风格的 Markdown（`--git` 标志）之间切换。 |
| **Converter.convert_html** | 执行核心工作——遍历 HTML 树，转换标签，并写入输出文件。 |
| **Error handling** | 提供明确的成功/失败信息，这对于 CI 流水线至关重要。 |

## 步骤 3：从命令行运行转换

保存脚本后，您可以使用单个命令转换任意 HTML 文件：

```bash
# Basic conversion (plain Markdown)
python html_to_md.py YOUR_DIRECTORY/input.html YOUR_DIRECTORY/output.md

# Git‑flavored conversion (adds tables, task lists, etc.)
python html_to_md.py YOUR_DIRECTORY/input.html YOUR_DIRECTORY/output.md --git
```

**预期输出**

```
✅ Conversion succeeded: 'YOUR_DIRECTORY/output.md'
```

在文本编辑器中打开 `output.md`；您会看到标题、列表和链接以干净的 Markdown 语法呈现。由于我们使用了 Git 格式化器，表格使用管道符（`|`）分隔，任务列表使用 `- [ ]` 语法，GitHub 和 GitLab 能原生渲染这些内容。

## 步骤 4：将工具集成到自动化流水线

如果您在仓库中维护文档，可以将转换步骤添加到 CI 工作流中。下面是一个在每次 push 时运行的 GitHub Actions 作业示例：

```yaml
name: Convert HTML docs to Markdown

on:
  push:
    paths:
      - 'docs/**/*.html'

jobs:
  convert:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'
      - name: Install dependencies
        run: pip install groupdocs-conversion
      - name: Convert HTML to Markdown
        run: |
          python html_to_md.py docs/input.html docs/output.md --git
      - name: Commit converted files
        uses: stefanzweifel/git-auto-commit-action@v4
        with:
          commit_message: "Auto‑convert HTML to Markdown"
```

*此步骤的重要性* – 自动化 **convert web page to markdown** 步骤可确保文档与源 HTML 文件保持同步，无需人工操作。

## 边缘情况和最佳实践提示

* **编码问题** – 如果您的 HTML 包含非 UTF‑8 字符，请在创建 `HTMLDocument` 时传入显式编码（例如 `HTMLDocument(input_path, encoding='utf-8')`）。  
* **大文件** – 对于大于 50 MB 的 HTML 文件，考虑使用流式转换以避免内存峰值。库提供了 `convert_html_stream` 方法来处理此场景。  
* **自定义 CSS 处理** – 转换器默认会剥离 style 属性。如果需要保留特定格式，请启用 `md_opts.preserveFormatting = True`。  
* **命令行快捷方式** – 创建一个小的包装脚本 (`html2md`)，将参数转发给 `html_to_md.py`。将其放置在 `$HOME/.local/bin` 并添加到 `PATH`，即可获得更简短的 **convert html to markdown command line** 使用体验。

## 常见问题

**此脚本是否在 Windows、macOS 和 Linux 上均可运行？**  
是的。该脚本仅依赖跨平台的 `groupdocs-conversion` 包和标准的 Python 库，因此在这三种操作系统上均可不做修改地运行。

**我可以直接转换远程网页吗？**  
您可以使用 `requests` 获取页面，并将 HTML 字符串传递给 `HTMLDocument`：

```python
import requests
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, Converter

response = requests.get("https://example.com")
html_doc = HTMLDocument.from_string(response.text)
# Continue with the same md_opts and Converter.convert_html call
```

**如果我只需要将 HTML 转换为 GitHub 风格的 Markdown，该怎么办？**  
只需始终传入 `--git` 标志；格式化器会生成兼容 GitHub、GitLab 和 Bitbucket 的输出。

## 结论

您现在拥有一个强大的 **convert HTML to Markdown** 解决方案，可通过 Python 脚本和命令行使用。本教程涵盖了环境搭建、完整源码、命令行用法、CI 集成以及实用的边缘情况处理。

接下来，您可以探索 **convert markdown to HTML**，尝试使用 Pandoc 实现高级转换选项，或添加 front‑matter 生成器，将元数据直接嵌入 Markdown 文件中。这些扩展都基于您刚刚掌握的核心概念。

祝转换愉快！

## 接下来您可以学习什么？

以下教程涵盖与本指南技术密切相关的主题，构建在本教程展示的技巧之上。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [在 Aspose.HTML for Java 中将 HTML 转换为 Markdown](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [在 .NET 中使用 Aspose.HTML 将 HTML 转换为 Markdown](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}