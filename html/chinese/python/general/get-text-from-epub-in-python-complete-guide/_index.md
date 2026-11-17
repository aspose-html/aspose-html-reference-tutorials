---
category: general
date: 2026-06-04
description: 快速获取 EPUB 文本，并学习如何读取 EPUB 文件、将 EPUB 转换为文本以及使用 Python 提取章节。
draft: false
keywords:
- get text from epub
- convert epub to text
- how to read epub
language: zh
og_description: 在几分钟内使用 Python 从 EPUB 获取文本。本教程展示如何读取 EPUB 文件、将 EPUB 转换为文本，并处理常见的边缘情况。
og_title: 在 Python 中获取 EPUB 文本 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-04'
  description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  headline: Get Text from EPUB in Python – Complete Guide
  type: TechArticle
- description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  name: Get Text from EPUB in Python – Complete Guide
  steps:
  - name: Import Libraries and Load the EPUB
    text: '```python from pathlib import Path from ebooklib import epub from bs4 import
      BeautifulSoup'
  - name: Grab the First Chapter (First <section> Element)
    text: '```python # Find the first HTML document inside the EPUB first_item = None
      for item in book.get_items(): if item.get_type() == epub.ITEM_DOCUMENT: first_item
      = item break'
  - name: Strip Tags and Output Plain Text
    text: '```python # .get_text() removes all HTML tags and returns clean text chapter_text
      = first_chapter.get_text(separator="

      ", strip=True)'
  - name: Full Script – Ready to Run
    text: '```python #!/usr/bin/env python3 """ Get text from EPUB – extract the first
      chapter and print it as plain text. """'
  type: HowTo
- questions:
  - answer: Not directly. `.mobi` uses a different container format. Convert it to
      EPUB first (Calibre does a solid job), then apply the same script.
    question: Can I use this with a .mobi file?
  - answer: The fallback to `<body>` (shown in the code) covers that case. You can
      also look for `<div class="chapter">` if the publisher uses custom markup.
    question: What if the EPUB has no `<section>` tags?
  - answer: 'No. Alternatives include `zipfile` + manual HTML parsing, or `pypub`
      for a higher‑level API. `ebooklib` is popular because it abstracts the ZIP handling
      and gives you item types out of the box. --- ## Conclusion You now know how
      to **get text from EPUB** files using Python, whether you need just the'
    question: Is `ebooklib` the only library?
  type: FAQPage
tags:
- python
- epub
- text‑extraction
title: 使用 Python 从 EPUB 获取文本 – 完整指南
url: /zh/python/general/get-text-from-epub-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 从 EPUB 获取文本 – 完整指南

是否曾想过 **如何在不打开笨重阅读器的情况下读取 EPUB** 文件？也许你需要提取第一章进行分析，或者只是想 **将 EPUB 转换为文本** 以便快速搜索。无论何种需求，这里都有答案。在本教程中，我们将展示如何使用几行 Python **从 EPUB 获取文本**，并解释每一步背后的原因，以便你能够将该方案适配到任何书籍。

我们将一步步演示如何安装合适的库、加载 EPUB、提取首个 `<section>` 元素，并打印其纯文本内容。完成后，你将拥有一个可复用的脚本，能够处理放入文件夹的任意 EPUB。

## 前置条件

- Python 3.8+（代码使用 f‑strings 和 pathlib）
- 现代 IDE 或者直接使用终端
- `ebooklib` 与 `beautifulsoup4` 包（使用 `pip install ebooklib beautifulsoup4` 安装）

无需其他外部工具，脚本可在 Windows、macOS 和 Linux 上运行。

---

## 从 EPUB 获取文本 – 步骤详解

下面的核心逻辑正是标题所承诺的：**从 EPUB 获取文本** 并打印第一章。我们会逐行拆解，帮助你理解每一行代码的作用。

### 步骤 1：导入库并加载 EPUB

```python
from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

# Path to the .epub file – change this to your own location
EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")

# Load the EPUB container
book = epub.read_epub(EPUB_PATH)
```

*为什么要这样做？*  
`ebooklib` 能识别 EPUB 基于 ZIP 的结构，而 `BeautifulSoup` 则让解析嵌入的 HTML 变得轻松。使用 `Path` 可以保持代码跨平台。

### 步骤 2：获取第一章（首个 <section> 元素）

```python
# Find the first HTML document inside the EPUB
first_item = None
for item in book.get_items():
    if item.get_type() == epub.ITEM_DOCUMENT:
        first_item = item
        break

if not first_item:
    raise ValueError("No HTML content found in the EPUB.")

# Parse the HTML with BeautifulSoup
soup = BeautifulSoup(first_item.get_content(), "html.parser")

# Retrieve the first <section> element – this usually holds a chapter
first_chapter = soup.find("section")
if not first_chapter:
    # Fallback: use the first <body> if no <section> exists
    first_chapter = soup.body
```

*为什么要这样做？*  
EPUB 将每章存为一个 HTML 文件。循环在第一个文档处停止，该文档通常是封面或简介。通过定位首个 `<section>`，我们直接指向真正的第一章；如果书中未使用 `<section>`，则回退到 `<body>` 元素。

### 步骤 3：去除标签并输出纯文本

```python
# .get_text() removes all HTML tags and returns clean text
chapter_text = first_chapter.get_text(separator="\n", strip=True)

print(chapter_text)
```

*为什么要这样做？*  
`get_text()` 是 **将 EPUB 转换为文本** 的最简方式。`separator` 参数确保每个块级元素换行，从而使输出更易阅读。

### 完整脚本 – 可直接运行

```python
#!/usr/bin/env python3
"""
Get text from EPUB – extract the first chapter and print it as plain text.
"""

from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

def extract_first_chapter(epub_path: Path) -> str:
    """Return the plain‑text of the first chapter in an EPUB file."""
    book = epub.read_epub(epub_path)

    # Locate the first HTML document
    first_item = next(
        (i for i in book.get_items() if i.get_type() == epub.ITEM_DOCUMENT),
        None,
    )
    if not first_item:
        raise ValueError("The EPUB does not contain any HTML documents.")

    soup = BeautifulSoup(first_item.get_content(), "html.parser")

    # Try to find a <section>; otherwise fall back to <body>
    chapter_tag = soup.find("section") or soup.body
    if not chapter_tag:
        raise ValueError("No readable content found in the first HTML document.")

    # Clean the text
    return chapter_tag.get_text(separator="\n", strip=True)


if __name__ == "__main__":
    # Replace with the actual path to your EPUB file
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    try:
        text = extract_first_chapter(EPUB_PATH)
        print(text)
    except Exception as e:
        print(f"Error: {e}")
```

将其保存为 `extract_epub.py` 并运行 `python extract_epub.py`。如果环境配置正确，你将在控制台看到第一章的文本输出。

![显示提取的 EPUB 文本的终端输出截图](get-text-from-epub.png "获取 EPUB 文本示例输出")

---

## 将 EPUB 转换为文本 – 扩展到全书

上面的代码片段只处理单章，但大多数项目需要将整本书合并为一个大字符串。下面的扩展示例遍历 **所有** 文档项，拼接清理后的文本，并写入 `.txt` 文件。

```python
def convert_epub_to_text(epub_path: Path, output_path: Path) -> None:
    """Convert an entire EPUB into a plain‑text file."""
    book = epub.read_epub(epub_path)
    all_text = []

    for item in book.get_items():
        if item.get_type() == epub.ITEM_DOCUMENT:
            soup = BeautifulSoup(item.get_content(), "html.parser")
            # Grab everything inside <body> – safe for most EPUBs
            body = soup.body
            if body:
                all_text.append(body.get_text(separator="\n", strip=True))

    output_path.write_text("\n\n".join(all_text), encoding="utf-8")
    print(f"✅ EPUB converted – saved to {output_path}")

# Example usage
if __name__ == "__main__":
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    TXT_PATH = Path("YOUR_DIRECTORY/book.txt")
    convert_epub_to_text(EPUB_PATH, TXT_PATH)
```

**小技巧：** 某些 EPUB 会嵌入脚本或样式标签，可能会让 `BeautifulSoup` 产生杂乱字符。若出现此类情况，可改为 `soup = BeautifulSoup(item.get_content(), "lxml")` 并安装 `lxml` 以使用更严格的解析器。

---

## 高效读取 EPUB 文件的常见陷阱

1. **编码意外** – EPUB 是包含 UTF‑8 HTML 的 ZIP 文件。如果出现 `UnicodeDecodeError`，读取时强制使用 UTF‑8：`item.get_content().decode("utf-8", errors="ignore")`。
2. **多语言混杂** – 包含多语言的书籍可能为每种语言使用单独的 `<section>` 标签。可使用 `soup.find_all("section")` 并根据 `lang` 属性进行过滤。
3. **图片与脚注** – 脚本会去除所有标签，导致图片的 alt 文本丢失。如需保留，可在清理前提取 `<img>` 的 `alt` 属性或脚注 `<a>` 链接。
4. **大部头** – 将每章全部加载到内存会导致 RAM 爆炸。可改为以追加模式直接写入文件，从而保持低内存占用。

---

## FAQ – 常见问题快速解答

**问：可以用这个脚本处理 .mobi 文件吗？**  
答：不能直接处理。`.mobi` 使用不同的容器格式。请先使用 Calibre 等工具将其转换为 EPUB，然后再运行本脚本。

**问：如果 EPUB 没有 `<section>` 标签怎么办？**  
答：代码中对 `<body>` 的回退已经覆盖了这种情况。若出版商使用自定义标记，也可以搜索 `<div class="chapter">`。

**问：`ebooklib` 是唯一可用的库吗？**  
答：不是。还有 `zipfile` + 手动 HTML 解析的方案，或提供更高级 API 的 `pypub`。`ebooklib` 之所以流行，是因为它封装了 ZIP 处理并直接提供项目类型。

---

## 结论

现在，你已经掌握了使用 Python **从 EPUB 获取文本** 的方法，无论是只取第一章还是整本书。教程涵盖了 **将 EPUB 转换为文本** 的关键步骤，解释了每行代码的原理，并指出了可能遇到的边缘情况。

接下来，可以尝试扩展脚本以提取元数据（如 `book.get_metadata('DC', 'title')`），或将输出格式改为 Markdown、JSON 等。原理相同，帮助你轻松应对任何类似的文件解析挑战。

祝编码愉快，若遇到问题欢迎留言交流！

## 接下来你可以学习什么？

以下教程与本指南紧密相关，基于相同技术进一步扩展功能。每篇资源都提供完整可运行的代码示例和逐步解释，帮助你掌握更多 API 特性并探索替代实现方式。

- [如何使用 Aspose.HTML 将 EPUB 转换为 PDF – Java 版](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [使用 Aspose HTML for Java 将 EPUB 转换为图片](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [使用 Aspose.HTML for Java 将 EPUB 转换为 PDF 与图片](/html/english/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}