---
category: general
date: 2026-06-04
description: 快速從 EPUB 取得文字，學習如何閱讀 EPUB 檔案、將 EPUB 轉換為文字，並使用 Python 抽取章節。
draft: false
keywords:
- get text from epub
- convert epub to text
- how to read epub
language: zh-hant
og_description: 只需數分鐘，即可使用 Python 從 EPUB 取得文字。本教學示範如何讀取 EPUB 檔案、將 EPUB 轉換為文字，並處理常見的例外情況。
og_title: 使用 Python 從 EPUB 取得文字 – 完整指南
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
title: 在 Python 中從 EPUB 取得文字 – 完整指南
url: /zh-hant/python/general/get-text-from-epub-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 EPUB 取得文字 – 完整指南

有沒有想過 **如何在不開啟笨重閱讀器的情況下讀取 EPUB** 檔案？也許你需要抽取第一章做分析，或只是想 **將 EPUB 轉成文字** 以便快速搜尋。無論是哪種需求，你都來對地方了。在本教學中，我們會示範如何使用幾行 Python **從 EPUB 取得文字**，同時說明每一步的原因，讓你能將此解決方案套用到任何書本上。

我們會一步步說明安裝正確的函式庫、載入 EPUB、抽取第一個 `<section>` 元素，並印出純文字內容。完成後，你將擁有一個可重複使用的腳本，能處理放入資料夾的任何 EPUB。

## 前置條件

- Python 3.8+（程式碼使用 f‑string 與 pathlib）
- 現代化的 IDE 或僅使用終端機
- `ebooklib` 與 `beautifulsoup4` 套件（使用 `pip install ebooklib beautifulsoup4` 安裝）

不需要其他外部工具，腳本可在 Windows、macOS 與 Linux 上執行。

---

## 從 EPUB 取得文字 – 步驟說明

以下是核心程式碼，正如標題所示：**從 EPUB 取得文字** 並印出第一章。我們會逐行說明，讓你了解每一行的作用。

### 步驟 1：匯入函式庫並載入 EPUB

```python
from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

# Path to the .epub file – change this to your own location
EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")

# Load the EPUB container
book = epub.read_epub(EPUB_PATH)
```

*為什麼要這樣做？*  
`ebooklib` 能辨識 EPUB 以 ZIP 為基礎的結構，而 `BeautifulSoup` 則讓解析內嵌的 HTML 變得輕鬆。使用 `Path` 可讓程式碼保持跨平台。

### 步驟 2：抓取第一章（第一個 `<section>` 元素）

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

*為什麼要這樣做？*  
EPUB 會把每章存成一個 HTML 檔案。迴圈在第一個文件停下，通常是封面或簡介。透過定位第一個 `<section>`，我們直接指向真正的第一章；若書本未使用 `<section>`，則會回退至 `<body>` 元素。

### 步驟 3：去除標籤並輸出純文字

```python
# .get_text() removes all HTML tags and returns clean text
chapter_text = first_chapter.get_text(separator="\n", strip=True)

print(chapter_text)
```

*為什麼要這樣做？*  
`get_text()` 是 **將 EPUB 轉成文字** 最簡單的方式。`separator` 參數確保每個區塊元素換行，讓輸出更易讀。

### 完整腳本 – 可直接執行

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

將此檔案存為 `extract_epub.py`，然後執行 `python extract_epub.py`。若環境設定正確，第一章的文字會印在終端機上。

![顯示已抽取 EPUB 文字的終端機輸出畫面](get-text-from-epub.png "取得 EPUB 文字範例輸出")

---

## 將 EPUB 轉成文字 – 大規模處理

上面的程式碼只處理單一章節，但大多數專案需要整本書的文字。以下是快速擴充版，會遍歷 **所有** 文件項目，將清理過的文字串接起來，最後寫入 `.txt` 檔案。

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

**小技巧：** 有些 EPUB 內嵌腳本或樣式標籤會讓 `BeautifulSoup` 解析出錯。若出現雜訊字元，可改為 `soup = BeautifulSoup(item.get_content(), "lxml")`，並安裝 `lxml` 以使用更嚴格的解析器。

---

## 高效閱讀 EPUB 檔案 – 常見陷阱

1. **編碼問題** – EPUB 為 ZIP 包含 UTF‑8 HTML。若出現 `UnicodeDecodeError`，請在讀取時強制使用 UTF‑8：`item.get_content().decode("utf-8", errors="ignore")`。
2. **多語言書籍** – 含有多種語言的書可能為每種語言各自使用 `<section>` 標籤。可使用 `soup.find_all("section")`，並依 `lang` 屬性過濾。
3. **圖片與註腳** – 腳本會去除所有標籤，導致圖片的 alt 文字消失。若需要保留，請在清理前先抽取 `<img>` 的 `alt` 屬性或註腳 `<a>` 連結。
4. **大型書籍** – 若一次將所有章節載入記憶體，可能會耗盡 RAM。建議改為逐章寫入檔案（append 模式），以降低記憶體使用。

---

## FAQ – 常見問題快速解答

**Q: 可以直接用這個腳本處理 .mobi 檔嗎？**  
A: 不能直接。`.mobi` 使用不同的容器格式。請先將其轉成 EPUB（Calibre 轉換效果不錯），再使用本腳本。

**Q: 若 EPUB 沒有 `<section>` 標籤怎麼辦？**  
A: 程式碼中已提供回退至 `<body>` 的處理方式。若出版商使用自訂標記，也可以搜尋 `<div class="chapter">`。

**Q: `ebooklib` 是唯一的函式庫嗎？**  
A: 不是。還有 `zipfile` 搭配手動 HTML 解析，或 `pypub` 提供更高層次的 API。`ebooklib` 受歡迎是因為它已內建 ZIP 處理，且能直接取得項目類型。

---

## 結論

現在你已掌握如何使用 Python **從 EPUB 取得文字**，無論只要第一章或整本書。本教學說明了 **將 EPUB 轉成文字** 的關鍵步驟，解釋了每行程式碼背後的原因，並提醒了可能遇到的邊緣情況。

接下來，你可以嘗試擴充腳本，使用 `book.get_metadata('DC', 'title')` 抽取書名、作者等中繼資料，或將輸出格式改為 Markdown、JSON 等。原理相同，讓你能輕鬆應對任何類似的檔案解析挑戰。

祝編程愉快，若有任何問題，歡迎留言討論！

## 接下來該學什麼？

以下教學與本指南的技巧密切相關，能幫助你進一步掌握相關 API 功能，並探索在專案中使用的其他實作方式。

- [如何使用 Aspose.HTML 於 Java 將 EPUB 轉成 PDF](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [使用 Aspose HTML for Java 將 EPUB 轉成圖片](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [使用 Aspose.HTML for Java 同時將 EPUB 轉成 PDF 與圖片](/html/english/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}