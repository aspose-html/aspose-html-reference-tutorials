---
category: general
date: 2026-10-21
description: 快速学习如何将 HTML 转换为 PNG。本教程还涵盖将网页导出为 PNG，以及使用 Python 将 HTML 文件转换为 PNG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: zh
lastmod: 2026-10-21
og_description: 使用 Python 将 HTML 转换为 PNG。遵循本清晰指南，将网页导出为 PNG，处理边缘情况，并实现图像生成自动化。
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: 在 Python 中将 HTML 转换为 PNG – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: 如何在 Python 中将 HTML 转换为 PNG——一步步指南
url: /zh/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 HTML 转换为 PNG（Python） – 完整编程指南

如果您需要 **convert HTML to PNG**，本指南将向您展示一种使用纯 Python 的可靠方法。无论是导出静态报告、为画廊生成缩略图，还是自动化测试截图，您都可以在几分钟内获得完整、可运行的解决方案。

您还将了解如何 **export webpage to PNG**，理解将 HTML 文件转换为 PNG 与将实时 URL 转换为 PNG 的区别，并学习处理大页面或动态内容的最佳实践。无需外部服务——只需几个 Python 包和一个简短脚本。

## 前置条件

- 已安装 Python 3.9+（代码在 Windows、macOS 和 Linux 上均可运行）
- 可使用终端或命令提示符
- 对 Python 包管理器 (`pip`) 有基本了解

您需要 `imgkit` 包（`wkhtmltoimage` 的轻量包装器）以及 `wkhtmltoimage` 二进制文件本身。两者均为免费开源软件。

## 步骤 1：安装所需工具

第一步是安装 `wkhtmltoimage` 以及与之交互的 Python 包装器。

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **此步骤的重要性** – `wkhtmltoimage` 使用 WebKit 引擎渲染 HTML，生成像素完美的 PNG。`imgkit` 只会将您的选项转发给二进制文件，因此您获得的质量与浏览器相同。

## 步骤 2：验证安装

运行快速检查，以确认 Python 能够访问该二进制文件。

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

如果脚本打印出 `wkhtmltoimage` 的路径，说明您已准备好将 HTML 转换为 PNG。如果出现 `OSError`，请再次确认该二进制文件已在系统 `PATH` 中。

## 步骤 3：编写可复用的转换函数

将逻辑封装在函数中，可轻松在项目的任何位置 **convert HTML file to PNG** 或 **export webpage to PNG**。

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **为何同时封装 `from_file` 和 `from_url`** – 同一个函数现在既支持本地文件的 **how to convert HTML to image**，也支持实时网页，保持代码 DRY（不要重复自己）。

## 步骤 4：将本地 HTML 文件转换为 PNG

在名为 `assets` 的文件夹中放置一个名为 `sample.html` 的 HTML 文件。然后调用我们刚定义的辅助函数：

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### 预期输出

运行脚本后会打印：

```
✅ Successfully saved PNG to: output/sample.png
```

新文件 `output/sample.png` 现在包含 `sample.html` 的像素完美快照。使用任何图像查看器打开它，都会看到页面渲染效果与浏览器中完全一致。

## 步骤 5：将实时网页导出为 PNG

如果需要为经常变化的 URL（例如仪表盘） **export webpage to PNG**，只需传入 URL 字符串，而不是文件路径。

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### 为什么要调整视口大小？

针对桌面屏幕设计的网页在小宽度渲染时常显得拥挤。通过增大 `width` 和 `height` 参数，您可以捕获完整布局，这对 **export webpage to PNG** 任务尤为有用。

## 步骤 6：处理常见边缘情况

### 6.1 大页面或无限滚动

对于懒加载内容的页面（例如无限滚动），请增加 JavaScript 延迟，并可选择设置更大的视口：

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 需要身份验证的页面

如果页面需要会话 Cookie，您可以在请求中嵌入 Cookie 头部：

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 缺失的图片或字体

`wkhtmltoimage` 为安全起见会遵循 `--disable-local-file-access` 标志。如果您的 HTML 引用了本地资源，需要显式启用它们：

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## 步骤 7：以编程方式验证结果（可选）

有时您需要确认 PNG 已正确生成（例如在 CI 流水线中）。以下代码片段检查文件大小和尺寸：

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

如果 PNG 通过这些检查，您即可安全地在后续流程中使用它，例如 PDF 生成、邮件附件或机器学习流水线。

## 结论

现在，您已经拥有使用 Python **convert HTML to PNG** 的完整、可投入生产的方法。本指南涵盖了：

- 安装 `wkhtmltoimage` 和 `imgkit`
- 验证环境
- 可复用的 `convert_html_to_png` 函数，支持本地文件和 URL
- 针对 **export webpage to PNG**、**how to convert HTML to image** 和 **convert HTML file to PNG** 的真实案例
- 大页面、身份验证和本地资源的边缘情况处理
- CI/CD 流水线的可选验证步骤

欢迎尝试更多 `imgkit` 选项——例如 `zoom`、`crop-h` 或 `crop-w`——以微调输出以满足您的特定需求。接下来，您可以探索：

- 将 PNG 转换为 PDF 报告（使用 `img2pdf` 库）
- 自动批量转换整个文件夹的 HTML 文件
- 对需要完整浏览器渲染的页面（例如大型 JavaScript 框架），使用 Selenium

祝编码愉快，尽享像素完美的截图！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能，并在项目中探索替代实现方案。

- [Convert HTML to PNG – Complete Python Guide](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Convert HTML to PNG in Python – Complete Streaming Save Guide](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Convert SVG to PNG in Python using Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}