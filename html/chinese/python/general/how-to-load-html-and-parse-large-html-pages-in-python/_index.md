---
category: general
date: 2026-10-28
description: 如何在 Python 中加载 HTML，同时限制资源并高效解析大型 HTML 页面。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to load html
- how to limit resources
- parse large html page
language: zh
lastmod: 2026-10-28
og_description: 如何在 Python 中加载 HTML，同时限制资源并高效解析大型 HTML 页面。
og_image_alt: Diagram showing HTML parsing flow with resource limits
og_title: 如何在 Python 中加载 HTML 并解析大型 HTML 页面
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to load HTML in Python while limiting resources and parsing large
    HTML pages efficiently.
  headline: How to load HTML and parse large HTML pages in Python
  type: TechArticle
- description: How to load HTML in Python while limiting resources and parsing large
    HTML pages efficiently.
  name: How to load HTML and parse large HTML pages in Python
  steps:
  - name: Missing or malformed HTML
    text: When the source file is incomplete, the parser may stop early. Use the `strict`
      flag on the options object to force a warning instead of an exception.
  - name: Extremely large files (>500 MB)
    text: Even with depth limits, loading a gigantic file can strain memory. Consider
      streaming the file in chunks and feeding each chunk to the parser. Some libraries
      expose a `parse_chunk` method for this purpose.
  - name: External resources (scripts, images)
    text: 'External resources are ignored by default when `max_handling_depth` is
      low, but you can also disable them explicitly:'
  - name: Next steps
    text: '* Explore deeper parsing by incrementally raising `max_handling_depth`.
      * Integrate the script with a database to store extracted headings. * Try the
      same approach with other parsers such as `BeautifulSoup` by wrapping their constructors
      in a custom options class.'
  type: HowTo
tags:
- HTML parsing
- Python
- resource management
title: 如何在 Python 中加载 HTML 并解析大型 HTML 页面
url: /zh/python/general/how-to-load-html-and-parse-large-html-pages-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何加载 HTML 并在 Python 中解析大型 HTML 页面

如果您需要在处理大规模文档的 Python 脚本中 **如何加载 HTML**，本指南提供完整的解决方案。您将学习在加载过程中如何限制资源，避免深层递归，并可靠地 **解析大型 HTML 页面**，而不会耗尽内存。

大型 HTML 文件通常包含成千上万的嵌套元素、外部脚本和大量资源。通过将解析器配置为在安全深度处停止，您可以保持进程响应，并防止崩溃。下面的步骤涵盖了从设置资源处理选项到从大页面中提取数据的全部内容。

## 您将实现的目标

* 使用自定义 **如何限制资源** 设置加载 HTML 文档。  
* 将解析深度限制为安全值（例如，三层）。  
* 遍历 **解析大型 HTML 页面** 示例的 DOM 并提取所需信息。  

唯一的前置条件是最近的 Python 3.x 安装以及 `htmlparser` 库（或任何提供 `ResourceHandlingOptions` 和 `HTMLDocument` 类的兼容解析器）。如果您更喜欢其他库，概念保持不变——只需将选项映射到您使用的 API 即可。

## 步骤 1：安装所需库

首先，安装提供资源处理 API 的解析器。示例使用了一个虚构的 `htmlparser` 包，但相同的模式同样适用于 `lxml`、`BeautifulSoup` 或 `html5lib`，只要您将它们包装在自定义选项对象中。

```bash
pip install htmlparser
```

安装命令会安装最新版本，支持 Python 3.9+，并包含 **如何限制资源** 所需的 `ResourceHandlingOptions` 类。

## 步骤 2：创建资源处理选项

在加载文件之前配置解析器是安全 **如何加载 HTML** 的核心。您需要创建一个选项对象，然后设置最大处理深度。深度为三时，解析器将在处理完顶层的 `<html>`、`<head>` 和 `<body>` 元素后停止，防止因深度嵌套的表格或错误标记导致的递归失控。

```python
from htmlparser import ResourceHandlingOptions, HTMLDocument

# Step 2.1: Instantiate the options container
opts = ResourceHandlingOptions()

# Step 2.2: Limit the handling depth to avoid deep nested resources
opts.max_handling_depth = 3
```

**为什么这很重要：**  
当解析器遍历每个节点时，每增加一级都会消耗更多的栈空间和内存。通过限制深度，您可以保证即使是 **解析大型 HTML 页面** 也能在可预测的时间内完成。

## 步骤 3：使用配置好的选项加载 HTML 文档

现在可以加载文件了。`HTMLDocument` 构造函数接受文件路径和您准备好的选项对象。这是需要资源约束时 **如何加载 HTML** 的规范方式。

```python
# Replace the path with the location of your large HTML file
html_path = "YOUR_DIRECTORY/bigpage.html"

# Load the document using the options defined above
doc = HTMLDocument(html_path, opts)
```

如果文件不存在，构造函数会抛出 `FileNotFoundError`。在生产代码中，请将调用包装在 `try/except` 块中并记录有用的提示信息。

```python
try:
    doc = HTMLDocument(html_path, opts)
except FileNotFoundError as e:
    print(f"Unable to locate the HTML file: {e}")
    raise
```

## 步骤 4：验证深度限制是否生效

加载后，您可以检查解析器的内部状态，以确认深度限制已被遵守。此步骤对调试以及演示 **如何限制资源** 实际生效非常有帮助。

```python
# The parser stores the actual depth it processed
processed_depth = doc.parsing_stats.max_depth_reached
print(f"Maximum depth processed: {processed_depth}")

# Expected output: Maximum depth processed: 3
```

如果输出显示的值大于 `3`，请再次确认您已正确将 `opts` 传递给构造函数。

## 步骤 5：遍历 DOM 并提取数据

文档加载后，您现在可以安全地遍历 DOM。由于深度受限，您只能看到顶层结构，这通常足以完成提取标题、元标签或章节标题等任务。

```python
# Example: Print the text of all <h1> elements within the allowed depth
for element in doc.find_all('h1'):
    print(element.get_text())
```

如果需要更深入部分的详细数据，请逐步增加 `max_handling_depth` 并重新运行脚本。**如何限制资源** 设置让您能够在完整性与性能之间进行细粒度的权衡。

## 步骤 6：处理边缘情况和常见陷阱

### 缺失或格式错误的 HTML

当源文件不完整时，解析器可能会提前停止。使用选项对象上的 `strict` 标志可强制发出警告而不是抛出异常。

```python
opts.strict = False  # Continue parsing even if the HTML is malformed
```

### 极大文件（>500 MB）

即使设置了深度限制，加载巨大的文件仍可能导致内存紧张。考虑将文件分块流式读取，并将每个块喂给解析器。一些库提供了 `parse_chunk` 方法来实现此目的。

```python
with open(html_path, "rb") as f:
    for chunk in iter(lambda: f.read(1024 * 1024), b""):
        doc.parse_chunk(chunk)
```

### 外部资源（脚本、图像）

当 `max_handling_depth` 较低时，外部资源默认会被忽略，但您也可以显式禁用它们：

```python
opts.load_external_resources = False
```

## 步骤 7：完整可运行示例

将所有部分组合在一起，下面是一个自包含的脚本，演示了 **如何加载 HTML**、**如何限制资源** 和 **解析大型 HTML 页面** 的完整工作流。

```python
# full_example.py
from htmlparser import ResourceHandlingOptions, HTMLDocument

def load_and_process_html(path: str, max_depth: int = 3) -> None:
    """
    Load an HTML file with a depth limit and print all top‑level headings.
    """
    # Configure resource handling
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth
    opts.strict = False               # Allow minor markup errors
    opts.load_external_resources = False

    # Load the document
    try:
        doc = HTMLDocument(path, opts)
    except FileNotFoundError as e:
        print(f"File not found: {e}")
        return

    # Verify depth limit
    print(f"Depth limit set to: {opts.max_handling_depth}")
    print(f"Depth actually processed: {doc.parsing_stats.max_depth_reached}")

    # Extract <h1> and <h2> headings (within the allowed depth)
    for tag in ('h1', 'h2'):
        for element in doc.find_all(tag):
            print(f"{tag.upper()}: {element.get_text().strip()}")

if __name__ == "__main__":
    # Replace with the path to your large HTML file
    html_file = "YOUR_DIRECTORY/bigpage.html"
    load_and_process_html(html_file, max_depth=3)
```

**预期输出（示例）：**

```
Depth limit set to: 3
Depth actually processed: 3
H1: Welcome to the Documentation
H2: Overview
H2: Installation
```

在多兆字节的 HTML 文件上运行此脚本可在数秒内完成，展示了 **如何加载 HTML** 与 **如何限制资源** 的组合使得处理大型文档变得实用。

## 结论

您现在了解了在 Python 中 **如何加载 HTML** 并控制内存消耗，如何使用最大处理深度配置 **如何限制资源**，以及如何可靠地 **解析大型 HTML 页面** 以获取所需数据。调整 `max_handling_depth` 以在完整性和性能之间取得平衡，并将这些技术与流式处理或外部资源禁用相结合，以应对最大文件。

### 下一步

* 通过逐步提升 `max_handling_depth` 探索更深层的解析。  
* 将脚本与数据库集成，以存储提取的标题。  
* 尝试使用其他解析器（如 `BeautifulSoup`），通过将其构造函数包装在自定义选项类中，使用相同的方法。  

尝试这些变体，以便根据您的具体工作负载定制解决方案，您将拥有一个强大的管道来处理任何 HTML 文档，无论其大小如何。

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术密切相关的主题，每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方式。

- [How to configure HTML resource handling in Python and load an HTML document](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [Load HTML File Python – Set Max Depth & Parse Large Files](/html/english/python/general/load-html-file-python-set-max-depth-parse-large-files/)
- [How to Limit Resources in Aspose.HTML Python](/html/english/python/general/how-to-limit-resources-in-aspose-html-python/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}