---
category: general
date: 2026-05-25
description: 使用輕量級的 HTML 轉 Markdown 函式庫將 HTML 轉換為 Markdown。了解如何只需幾行程式碼即可將 Markdown
  檔案的 HTML 輸出儲存。
draft: false
keywords:
- convert html to markdown
- html to markdown library
- save markdown file html
language: zh-hant
og_description: 快速將 HTML 轉換為 Markdown。本教學示範如何使用 HTML 轉 Markdown 的函式庫，並將 Markdown 檔案儲存為
  HTML 結果。
og_title: 使用 Python 將 HTML 轉換為 Markdown – 快速指南
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: convert html to markdown using a lightweight html to markdown library.
    Learn how to save markdown file html output in just a few lines.
  headline: convert html to markdown with Python – html to markdown lib
  type: TechArticle
- description: convert html to markdown using a lightweight html to markdown library.
    Learn how to save markdown file html output in just a few lines.
  name: convert html to markdown with Python – html to markdown lib
  steps:
  - name: Expected Output
    text: 'Running the script produces a file `links_and_paragraphs.md` containing:'
  - name: 1. What if I need to keep tables too?
    text: 'Just change the filter logic:'
  - name: 2. How does the library handle nested tags like `<strong>` or `<em>`?
    text: '`markdownify` automatically translates `<strong>` → `**bold**` and `<em>`
      → `*italic*`. If you only want links and paragraphs, those lines will be stripped
      by our filter, but you can relax the filter to keep them.'
  - name: 3. Is the conversion Unicode‑safe?
    text: ' ## Related Tutorials

      - [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
      - [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
      - [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Conversion
title: 使用 Python 將 HTML 轉換為 Markdown – html to markdown lib
url: /zh-hant/python/general/convert-html-to-markdown-with-python-html-to-markdown-lib/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 轉換 HTML 為 Markdown – 完整 Python 教學

有沒有曾經需要**convert html to markdown**卻不確定該使用哪個工具？你並不孤單。在許多專案——靜態網站產生器、文件流程或快速資料遷移——將原始 HTML 轉換為乾淨的 Markdown 是日常工作。好消息是？只要使用一個小型的**html to markdown library**，再加上幾行 Python 程式碼，你就能自動化整個流程，甚至**save markdown file html**結果直接寫入磁碟，輕鬆完成。

在本指南中，我們將從零開始，逐步說明如何安裝合適的函式庫、設定轉換選項，最後將輸出保存至檔案。完成後，你將擁有一段可重複使用的程式碼片段，能直接嵌入任何腳本，並提供處理連結、表格及其他複雜 HTML 元素的技巧。

## 你將學到什麼

- 為何選擇正確的**html to markdown library**對於保真度與效能很重要。  
- 如何設定轉換選項，只挑選你需要的功能（例如連結與段落）。  
- 一次完成**convert html to markdown**與**save markdown file html**所需的完整程式碼。  
- 針對表格、圖片與巢狀元素的邊緣案例處理。  

不需要先前使用 Markdown 轉換器的經驗；只要有基本的 Python 安裝即可。

---

## 步驟 1：挑選合適的 HTML 轉 Markdown 函式庫

市面上有多個 Python 套件聲稱能將 HTML 轉換為 Markdown，但並非所有套件都提供細緻的控制。於本教學，我們將使用**markdownify**，這是一個維護良好的函式庫，允許透過 `markdownify.MarkdownConverter` 物件切換各項功能。它輕量、純 Python，且可在 Windows 與類 Unix 系統上運行。

```bash
pip install markdownify
```

> **專業提示：** 若你在受限環境（例如 AWS Lambda）中執行，請鎖定版本（`markdownify==0.9.3`），以避免意外的破壞性變更。

使用**markdownify**符合我們的次要關鍵字需求——*html to markdown library*——同時保持程式碼易讀。

## 步驟 2：準備你的 HTML 來源

讓我們定義一段小型的 HTML 片段，包含標題、帶有連結的段落，以及簡易表格。這與你可能從部落格文章或電子郵件範本中抽取的內容相似。

```python
# Step 2: Define the source HTML content
html = """
<h1>Title</h1>
<p>Paragraph with a <a href="https://example.com">link</a>.</p>
<table><tr><td>Cell</td></tr></table>
"""
```

請注意，HTML 被存放在三重引號字串中以提升可讀性。你同樣可以從檔案或網路請求中讀取；轉換邏輯保持不變。

## 步驟 3：以所需功能設定轉換器

有時你只需要特定的 Markdown 結構。`markdownify` 函式庫允許傳入 `heading_style` 與 `bullets` 旗標，但為了模仿原始範例，我們將聚焦於連結與段落。雖然 `markdownify` 未提供位元遮罩 API，我們仍可透過後處理輸出達成相同效果。

```python
from markdownify import markdownify as md

def convert_html_to_markdown(html_content, keep_links=True, keep_paragraphs=True):
    """
    Convert HTML to Markdown, optionally stripping out unwanted elements.
    """
    # Convert everything first
    full_md = md(html_content, heading_style="ATX")

    # If we only want links and paragraphs, filter the lines
    lines = full_md.splitlines()
    filtered = []

    for line in lines:
        stripped = line.strip()
        if not stripped:
            continue  # skip empty lines

        if keep_links and "[" in stripped and "](" in stripped:
            filtered.append(stripped)
        elif keep_paragraphs and not stripped.startswith("#") and not stripped.startswith("-"):
            # Assume plain text lines are paragraphs
            filtered.append(stripped)

    return "\n\n".join(filtered)
```

輔助函式 `convert_html_to_markdown` 承擔主要工作：它先執行完整轉換，然後剔除非連結或段落的內容。這呼應了原始程式碼中**html to markdown library**的功能選擇模式。

## 步驟 4：將 Markdown 輸出保存至檔案

現在我們已取得乾淨的 Markdown 字串，將其持久化相當簡單。我們會將結果寫入你指定目錄下名為 `links_and_paragraphs.md` 的檔案。

```python
import os

def save_markdown(markdown_text, directory, filename="output.md"):
    """
    Ensure the target directory exists and write the markdown text to a file.
    """
    os.makedirs(directory, exist_ok=True)  # creates the folder if needed
    file_path = os.path.join(directory, filename)

    with open(file_path, "w", encoding="utf-8") as f:
        f.write(markdown_text)

    print(f"✅ Markdown saved to {file_path}")
```

此處滿足**save markdown file html**的需求：函式明確處理路徑，並使用 UTF‑8 編碼以保留可能出現的非 ASCII 字元。

## 步驟 5：整合全部 – 完整可執行腳本

以下是完整且可執行的腳本，將所有步驟整合。將其複製貼上至名為 `html_to_md.py` 的檔案，然後執行 `python html_to_md.py`。調整 `output_dir` 變數以指定 Markdown 檔案的儲存位置。

```python
# html_to_md.py
# ----------------------------------------------------
# Complete example: convert html to markdown and save
# ----------------------------------------------------
from markdownify import markdownify as md
import os

# --- Step 1: Define source HTML ------------------------------------------------
html = """
<h1>Title</h1>
<p>Paragraph with a <a href="https://example.com">link</a>.</p>
<table><tr><td>Cell</td></tr></table>
"""

# --- Step 2: Conversion helper -------------------------------------------------
def convert_html_to_markdown(html_content, keep_links=True, keep_paragraphs=True):
    """
    Convert HTML to Markdown, optionally keeping only links and paragraphs.
    """
    full_md = md(html_content, heading_style="ATX")
    lines = full_md.splitlines()
    filtered = []

    for line in lines:
        stripped = line.strip()
        if not stripped:
            continue

        if keep_links and "[" in stripped and "](" in stripped:
            filtered.append(stripped)
        elif keep_paragraphs and not stripped.startswith("#") and not stripped.startswith("-"):
            filtered.append(stripped)

    return "\n\n".join(filtered)

# --- Step 3: Save helper -------------------------------------------------------
def save_markdown(markdown_text, directory, filename="links_and_paragraphs.md"):
    """
    Save markdown_text to `directory/filename`. Creates the directory if missing.
    """
    os.makedirs(directory, exist_ok=True)
    file_path = os.path.join(directory, filename)

    with open(file_path, "w", encoding="utf-8") as f:
        f.write(markdown_text)

    print(f"✅ Markdown saved to {file_path}")

# --- Step 4: Execute conversion & saving ---------------------------------------
if __name__ == "__main__":
    # Choose which features you need – here we keep links & paragraphs only
    markdown_result = convert_html_to_markdown(html, keep_links=True, keep_paragraphs=True)

    # Define where you want the .md file to live
    output_dir = "YOUR_DIRECTORY"

    # Finally, write the file
    save_markdown(markdown_result, output_dir)
```

### 預期輸出

執行腳本後會產生一個 `links_and_paragraphs.md` 檔案，內容如下：

```markdown
Paragraph with a [link](https://example.com).

Cell
```

- 標題（`# Title`）被省略，因為我們只要求保留連結與段落。  
- 表格儲存格被呈現為純文字，示範了過濾器的運作方式。

---

## 常見問題與邊緣案例

### 1. 如果我也需要保留表格呢？

只要修改過濾邏輯即可：

```python
elif keep_tables and stripped.startswith("|"):
    filtered.append(stripped)
```

在函式簽名中加入 `keep_tables` 旗標，呼叫時將其設為 `True`。

### 2. 函式庫如何處理 `<strong>` 或 `<em>` 等巢狀標籤？

`markdownify` 會自動將 `<strong>` 轉換為 `**bold**`，將 `<em>` 轉換為 `*italic*`。如果你只想保留連結與段落，這些行會被過濾器剔除，但你可以放寬過濾條件以保留它們。

### 3. 轉換是否支援 Unicode？

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}