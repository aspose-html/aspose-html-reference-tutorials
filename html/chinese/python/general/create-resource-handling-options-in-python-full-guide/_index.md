---
category: general
date: 2026-07-21
description: 在 Python 中创建资源处理选项，并学习如何设置 HTML 解析的最大处理深度。按照本分步教程实现可靠的资源管理。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: zh
lastmod: 2026-07-21
og_description: 在 Python 中创建资源处理选项，并立即了解如何设置最大处理深度以安全加载 HTML 文档。几分钟内掌握此技巧。
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: 在 Python 中创建资源处理选项 – 完整的逐步指南
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: 在 Python 中创建资源处理选项 – 完整指南
url: /zh/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中创建资源处理选项 – 完整指南

有没有想过如何在不耗尽内存的情况下为巨大的 HTML 页面**创建资源处理选项**？你并不是唯一有此困惑的人。当你将一个庞大的文档喂给解析器时，像 frames、iframe 或链接的 CSS 等嵌套资源会迅速失控。  

好消息是？你可以让解析器在达到一定的嵌套层数后停止。在本教程中我们将展示**如何设置最大处理深度**并保持应用的响应性。准备好了吗？让我们开始吧。

## 你将学到的内容

- 为什么限制嵌套深度对性能和安全至关重要。  
- 使用 `ResourceHandlingOptions` 类**创建资源处理选项**所需的完整代码。  
- 如何配置 `max_handling_depth` 使解析器在三层后停止。  
- 处理边缘情况的技巧，例如包含循环引用或缺失资源的文档。  

无需任何库的使用经验——只需一套可运行的 Python 3 环境以及对文件 I/O 的基本了解。

## 前置条件

- Python 3.8+（该库兼容所有近期版本）。  
- `htmlparser` 包，提供 `HTMLDocument` 和 `ResourceHandlingOptions`。  
- 一个示例 HTML 文件（`big_page.html`），放置在可引用的文件夹中。  

如果尚未安装该包，请运行：

```bash
pip install htmlparser
```

既然前期准备工作已经完成，让我们进入正题。

## 创建资源处理选项 – 步骤 1

首先，你需要一个 `ResourceHandlingOptions` 实例。可以把它看作一个工具箱，用来设置解析器应遵循的限制和策略。

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**为什么这很重要：**  
当解析器在一个 `<iframe>` 中再次遇到 `<iframe>` 时，通常会无限递归。将深度限制为 `3`，可以防止递归失控，从而避免耗尽内存或导致栈溢出。  

> **专业提示：** 如果你在解析不可信的内容（例如用户上传的 HTML），考虑将深度降低到 `1` 或 `2`，以降低潜在攻击的风险。

## 加载 HTML 文档 – 步骤 2

准备好选项对象后，将其传递给 `HTMLDocument`。构造函数会遵循你刚才设置的 `max_handling_depth`。

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**内部发生了什么？**  
`HTMLDocument` 读取文件，构建 DOM 树，然后遍历每个外部资源（样式表、脚本、图片）。每当遇到嵌套资源时，它会检查 `resource_options.max_handling_depth`。如果达到限制，解析器会记录警告并跳过进一步的嵌套。  

这意味着前三级的 DOM 可以完整使用，而其余层级会被安全地忽略。

## 验证配置 – 步骤 3

确认设置已生效总是个好主意。`resource_options` 对象会公开其当前状态，你可以将其打印出来或在测试中进行断言。

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

如果断言通过，你就可以确信解析器在整个运行期间都会遵守该限制。

## 处理边缘情况

### 循环引用

某些旧站点会嵌入指向原页面的 iframe，形成循环。设置 `max_handling_depth` 后，循环会在第三次迭代后自动中断。不过，你仍可能在日志中看到警告。要消除噪声日志，请调整日志记录器级别：

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### 缺失资源

如果嵌套资源加载失败（404 或网络超时），解析器默认会抛出异常。将加载调用包装在 `try/except` 块中，以保持应用存活：

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### 动态调整深度

有时你需要为流水线的不同部分设置不同的深度。由于 `resource_options` 是可变对象，你可以在运行时修改 `max_handling_depth`：

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

只需记得在另一个线程中再次使用同一选项实例前将该值重置。

## 完整可运行示例

下面是一段完整脚本，你可以复制粘贴、修改文件路径后立即运行。

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**预期输出（文件存在且格式正确时）：**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

如果文件无法读取，你会看到错误信息，而不是程序崩溃。

![在 Python 中创建资源处理选项](/images/resource-options.png){alt="在 Python 中创建资源处理选项"}

## 小结 – 为什么这种方法很棒

- **安全第一：** 限制嵌套深度可防止递归失控和内存膨胀。  
- **灵活性：** 你可以在运行时更改 `max_handling_depth` 以适应不同场景。  
- **简洁性：** 只需几行代码即可**创建资源处理选项**并立即应用。  

简而言之，你现在拥有一种稳健的模式来控制解析器跟随外部资源的深度。

## 接下来怎么做？

- 进一步探索 `ResourceHandlingOptions` 类——它包含缓存、超时处理和 MIME 类型过滤等标志。  
- 将深度限制与自定义 `UserAgent` 字符串结合，以避免被激进的服务器阻止。  
- 如果使用异步 I/O，了解 `aiohtmlparser` 变体，它遵循相同的选项并与 `asyncio` 配合使用。  

随意尝试：将深度设为 `0`，观察解析器忽略所有外部引用。当你只需要原始 HTML 标记时，这是一种方便的快捷方式。

有疑问或遇到仍然让你头疼的页面？在下方留言，我会乐意帮助你微调设置。祝你解析愉快！

## 接下来该学习什么？

以下教程涵盖与本指南技术密切相关的主题，构建在本指南演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [在 C# 中从字符串创建 HTML – 自定义资源处理器指南](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [如何在 C# 中保存 HTML – 使用自定义资源处理器的完整指南](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [在 Java 中为 HTML 创建沙箱 – 步骤指南](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}