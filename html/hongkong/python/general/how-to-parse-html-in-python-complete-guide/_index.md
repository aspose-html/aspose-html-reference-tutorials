---
category: general
date: 2026-05-28
description: 如何在 Python 中快速解析 HTML——載入 HTML 檔案、使用 CSS 選擇器，並以 XPath contains 範例提取 href
  屬性。
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: zh-hant
og_description: 如何在 Python 中解析 HTML：學習載入 HTML 檔案、使用 CSS 選擇器，並透過 XPath contains 範例取得
  href 屬性。
og_title: 如何在 Python 中解析 HTML – 逐步教學
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: 如何在 Python 中解析 HTML – 完整指南
url: /zh-hant/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中解析 HTML – 完整指南

有沒有想過在 Python 腳本中 **如何解析 HTML**，卻不需要載入龐大的瀏覽器？你並不孤單。我們大多只需要 **載入 HTML 檔案**，抓取幾個標題，甚至可能取得一兩個下載連結。在本教學中，我會示範如何使用一個小型函式庫、CSS selector 以及 XPath contains 範例來 **取得 href 屬性** 的值。

我們將逐步說明完整流程，從讀取本機 HTML 文件到印出你關心的資料。沒有多餘的說明，只有實用、可直接執行的範例，讓你今天就能把它放入自己的專案中。

## 你將學會

- 如何使用輕量級解析器 **載入 HTML 檔案**。
- 如何 **使用 CSS selector** 語法取得如文章標題等元素。
- 如何編寫 **XPath contains 範例** 以篩選連結。
- 如何安全地從匹配的節點 **取得 href 屬性** 值。
- 處理錯誤標記與擴充腳本的技巧。

你只需要 Python 3.8+ 以及 `lxml` 與 `cssselect` 套件——兩者皆可透過單一 `pip` 指令安裝。

---

## 步驟 1：載入 HTML 檔案

在開始之前，你需要先將 HTML 內容載入記憶體。`lxml.html` 模組提供了便利的 `fromstring` 輔助函式，但若是有磁碟上的檔案，使用 `parse` 函式會更簡潔。

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **為什麼這很重要：** 只載入一次檔案可降低記憶體使用，並提供一個支援 CSS selector 與 XPath 查詢的 `root` 物件。如果檔案遺失或無法讀取，`html.parse` 會拋出明確的 `OSError`，之後你可以捕捉它。

### 小技巧
如果你處理的是字串而非檔案，請將 `html.parse` 換成 `html.fromstring(your_html_string)`。

---

## 步驟 2：使用 CSS Selector 取得標題

CSS selector 簡潔且對任何寫過樣式表的人都很熟悉。讓我們抓取每個位於 `<article>` 內的 `<h2>`——非常適合新聞標題。

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**預期輸出**（假設範例 HTML 包含兩篇文章）：

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **為什麼選擇 CSS？** 它易讀、快速，且可直接與 `lxml` 搭配使用。`cssselect` 方法在底層會把 selector 轉換成 XPath 表達式，讓你同時享有兩者的優點。

---

## 步驟 3：XPath Contains 範例 – 找出「download」連結

有時候你需要比 CSS 更細緻的控制。XPath 的 `contains()` 函式在想要匹配屬性內子字串時非常好用，例如所有指向下載的連結。

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**範例輸出**：

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **為什麼使用 XPath contains？** 它讓你直接在屬性值上過濾，無需額外的 Python 迴圈。這就是常見的 **xpath contains 範例**，但此處結合了實務案例。

---

## 步驟 4：封裝成可重複使用的函式

硬編碼路徑與印出對於快速測試還算可以，但正式程式碼較喜歡使用函式。以下是一個簡潔的輔助函式，會回傳標題與下載連結。

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

現在你可以呼叫此函式並以美化格式印出結果：

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

執行腳本會得到與之前相同的輸出，但現在已整齊封裝，方便重複使用。

---

## 步驟 5：處理邊緣情況與常見陷阱

1. **缺少 `href` 屬性** – 即使 `href` 不存在，XPath 仍會回傳 `<a>` 節點。需防止 `None`：

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **相對與絕對 URL** – 若你的連結是相對路徑，可能需要根據基礎 URL 進行解析：

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **HTML 結構錯誤** – `lxml` 雖然寬容，但極度損壞的標記仍可能導致 `html.parse` 拋出 `XMLSyntaxError`。請將解析呼叫包在 `try/except` 區塊中，以記錄並跳過有問題的檔案。

4. **大型檔案的效能** – 對於多兆位元組的頁面，考慮使用 `iterparse` 串流處理，而非一次載入整個 DOM 到記憶體。

---

## 視覺概覽（可選）

![HTML 解析流程圖示，顯示載入檔案 → CSS selector → XPath contains → 取得 href 屬性](how-to-parse-html-flow.png "HTML 解析流程圖示")

*Alt 文字包含主要關鍵字以符合 SEO 需求。*

---

## 結論

我們已完整說明在 Python 中 **如何解析 HTML**：載入 HTML 檔案、使用 CSS selector 抓取文章標題、編寫 XPath contains 範例以定位下載連結，最後安全地 **取得 href 屬性** 值。可重複使用的 `parse_news_html` 函式展示了一種乾淨、易於維護的做法，能套用於任何爬蟲任務。

準備好接受下一個挑戰了嗎？試著擴充腳本以：

- 使用 `//table//tr` XPath 查詢解析表格。
- 使用另一個 **xpath contains 範例** 取得圖片 `src` 屬性。
- 以 `aiohttp` 進行非同步抓取，處理即時網頁。

祝你解析愉快，記住——一旦掌握這些基礎，HTML 爬蟲就變得輕而易舉。如果遇到任何問題，請在下方留言——讓我們一起排除故障！

## 相關教學

- [在 Aspose.HTML for Java 中從檔案載入 HTML 文件](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [在 Aspose.HTML for Java 中編輯 HTML 文件樹](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [在 Aspose.HTML for Java 中為 HTML 文件新增 CSS – 行內 CSS](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}