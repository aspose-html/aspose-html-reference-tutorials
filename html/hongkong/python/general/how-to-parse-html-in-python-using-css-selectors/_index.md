---
category: general
date: 2026-10-21
description: 學習如何在 Python 中解析 HTML、載入 HTML 文件、使用 CSS 選擇器，並快速提取 HTML 中的超連結。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: zh-hant
lastmod: 2026-10-21
og_description: 如何在 Python 中使用 CSS 選擇器解析 HTML。載入 HTML 文件，選取連結，並以簡潔的程式碼從 HTML 中提取超連結。
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: 如何在 Python 中解析 HTML – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: 如何在 Python 中使用 CSS 選擇器解析 HTML
url: /zh-hant/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 CSS 選擇器解析 HTML

如果你需要在 Python 腳本中 **how to parse html**，本指南將會完整示範。你將學習如何載入 HTML 文件、如何使用 selector 語法找出元素，以及如何在不自行編寫解析器的情況下從 html 中擷取超連結。

解析 HTML 是網路爬蟲、資料分析管線或自動化測試的常見任務。完成本教學後，你將擁有一個可重複使用的函式，能載入 HTML 文件、使用 CSS selector 選取所有 `<a>` 標籤，並回傳一個乾淨的 URL 清單。

## 你需要的環境

- Python 3.8+（此程式碼在任何近期版本皆可執行）  
- **lxml** 套件 (`pip install lxml`) – 提供快速的 HTML 解析與 CSS selector 支援  
- 你想要分析的 HTML 檔案（例如 `sample.html`）  

不需要其他工具；所有功能皆可在標準函式庫加上一個第三方套件下執行。

## 步驟 1：How to parse HTML – 載入文件

任何 HTML 工作流程的第一步都是將檔案讀入記憶體。使用 **lxml.html** 可取得支援 CSS selector 的樹狀物件。

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**為什麼這很重要：**  
`load_html` 抽象化了讀檔的樣板程式，並確保文件以容錯的 HTML 解析器進行解析。這是 **load html document python** 最安全的做法，無需擔心標記不完整。

## 步驟 2：How to use selector – 找出所有連結元素

文件載入後，你可以使用 CSS selector 來定位每個 `<a>` 標籤。選擇器 `"a"` 會匹配所有錨點元素，但你也可以進一步細化（例如 `"a.external"` 或 `"nav a"`）。

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**為什麼這很重要：**  
**how to use selector** 方法讓你能以單一、易讀的字串表達複雜查詢，免除手動樹狀遍歷。它支援 `lxml.cssselect` 所提供的所有 CSS 模式。

## 步驟 3：Extract hyperlinks from HTML and process them

現在你已取得 `<a>` 元素的清單，可以從每個元素取出 `href` 屬性。以下輔助函式同時會將相對 URL 正規化為基礎 URL（若你提供的話）。

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**預期輸出**（假設 `sample.html` 包含三個連結）：

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**為什麼這很重要：**  
`extract_hyperlinks` 是 **extract hyperlinks from html** 的核心。它能優雅地處理缺失的 `href` 屬性、解析相對連結，並回傳一個純粹的 Python 清單，供後續處理（例如 requests、pandas 或資料庫）使用。

## 完整端對端範例

將這三個函式結合，即可得到一個單一腳本，能載入檔案、選取所有錨點，並印出每個超連結。

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

執行 `python parse_links.py` 會在終端機列印出每個已完整解析的超連結。此腳本示範了 **how to parse html**、**how to use selector** 與 **extract hyperlinks from html** 的單一可重複使用流程。

## 常見變化與邊緣案例處理

| Situation | What to change | Reason |
|-----------|----------------|--------|
| **只需要絕對 URL** | 在 `extract_hyperlinks` 中省略 `base_url` 參數 | 保留相對 URL 不變 |
| **同時需要連結文字** | 在 `extract_hyperlinks` 中回傳元組 `(href, link.text_content())` | 允許同時儲存 URL 與錨點文字 |
| **大型 HTML 檔案** | 使用帶有 CSS selector 篩選的 `lxml.etree.iterparse` | 透過串流減少記憶體使用 |
| **不同的 selector** | 將 `"a"` 替換為 `"nav a[href]"` 或 `"div.content a.external"` | 針對特定子集合的連結，在複雜頁面中對 **how to use selector** 很有幫助 |

**專業提示：** 在發送網路請求前，務必驗證擷取到的 URL。快速使用 `urlparse` 檢查即可過濾掉格式錯誤的字串，防止爬蟲當機。

## 結論

現在你已掌握在 Python 中 **how to parse html**、**load html document python**、**how to use selector** 以定位元素，以及 **extract hyperlinks from html** 的高效方法。上述完整範例已可直接複製貼上至你的專案，且你可以依需求調整各函式，以因應分頁、JavaScript 產生的內容或多頁爬取等進階情境。

接下來你可能想探索的步驟包括：

- 使用 **requests‑html** 或 **Playwright** 取得需要 JavaScript 執行的頁面。  
- 將擷取的 URL 儲存於 CSV 或 SQLite 資料庫，以供日後分析。  
- 為網路逾時與 HTTP 狀態碼加入錯誤處理。

祝解析順利，歡迎隨意嘗試不同的 selector，發掘 Python 中基於 CSS 的 HTML 查詢的完整威力！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在所示技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索替代實作方式。

- [如何在 Python 中設定 HTML 資源處理並載入 HTML 文件](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [如何在 Python 中解析 HTML – 完整指南](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [如何在 Python 中載入 HTML – 步驟說明指南](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}