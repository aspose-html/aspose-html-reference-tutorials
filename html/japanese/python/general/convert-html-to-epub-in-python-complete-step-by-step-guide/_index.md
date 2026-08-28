---
category: general
date: 2026-07-18
description: PythonでHTMLを迅速にEPUBに変換します。PythonでHTMLファイルを読み込む方法と、シンプルなライブラリを使ってHTMLをMHTMLに変換する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: ja
lastmod: 2026-07-18
og_description: PythonでHTMLをEPUBに変換する、分かりやすく実行可能なサンプル付き。さらに、PythonでHTMLファイルを読み込む方法や、数分でHTMLをMHTMLに変換する方法も学べます。
og_image_alt: Diagram showing convert html to epub workflow
og_title: PythonでHTMLをEPUBに変換する – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: PythonでHTMLをEPUBに変換する – 完全ステップバイステップガイド
url: /ja/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでHTMLをEPUBに変換する – 完全ステップバイステップガイド

HTMLを **convert HTML to EPUB** したいけど、頭を抱えるほど大変だと思ったことはありませんか？ あなただけではありません。開発者はオフラインで読むためにウェブページを電子書籍に変換する必要が頻繁にあり、Pythonで行うのは意外と簡単です。このチュートリアルでは、PythonでHTMLファイルを読み込み、HTMLをEPUBに変換し、さらに同じソースからMHTMLを作成してメールフレンドリーなアーカイブにする方法を順を追って解説します。

ガイドの最後までに、`sample.html` 1つを入力として `sample.epub` と `sample.mhtml` を出力する実行可能なスクリプトが手に入ります。謎はなく、コードと説明が明快です。

---

![Conversion pipeline diagram](https://example.com/images/convert-html-epub.png "Diagram showing convert html to epub workflow")

## 作成するもの

- **Python の組み込み `pathlib` と `io` モジュール** を使って HTML ファイルをロードする方法。  
- **`ebooklib` ライブラリ** を使って HTML を EPUB に変換する方法。EPUB のコンテナ形式を自動で処理してくれます。  
- **`email` パッケージ** を使って HTML を MHTML（別名 MHT）に変換し、ブラウザで直接開ける単一ファイルのウェブアーカイブを作成する方法。  

さらに以下もカバーします：

- 必要な依存関係とインストール手順。  
- スクリプトが適切に失敗するようにするエラーハンドリング。  
- EPUB ファイルのタイトルや作者などのメタデータをカスタマイズする方法。  

準備はいいですか？ さっそく始めましょう。

---

## 前提条件

コードを書き始める前に、以下を用意してください：

1. **Python 3.9+** – ここで使用している構文は最近のバージョンで動作します。  
2. **pip** – サードパーティパッケージをインストールするために必要です。  
3. 任意のフォルダーに置いたシンプルな HTML ファイル（例：`sample.html`）。  

すでに揃っているなら、次のセクションへ進んでください。  

> **プロのコツ:** HTML はきちんと構造化（`<head>` と `<body>` が正しく配置）されていることを確認しましょう。`ebooklib` は軽微な問題を自動修正しますが、クリーンなソースにしておく方が後々楽です。

---

## ステップ 1 – 必要なライブラリをインストール

外部パッケージが 2 つ必要です：

- **ebooklib** – EPUB 生成用。  
- **beautifulsoup4** – 任意ですが、変換前に HTML を整形するのに便利です。

ターミナルで次のコマンドを実行してください：

```bash
pip install ebooklib beautifulsoup4
```

> **なぜこれらのライブラリが必要か？** `ebooklib` は ZIP ベースの EPUB 構造（`META‑INF` フォルダー、`content.opf`、`toc.ncx` など）を自動で作成してくれます。`beautifulsoup4` は HTML を整形し、最終的な電子書籍がすべてのリーダーで正しく表示されるようにします。

---

## ステップ 2 – Python で HTML ファイルをロード

HTML ファイルの読み込みはシンプルですが、後で使える **BeautifulSoup** オブジェクトを返す小さなヘルパー関数でラップします。

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**解説:**  
- `Path` を使うことで OS に依存しないファイル操作が可能です。  
- `read_text` により手動で `open`/`close` を書く必要がなくなります。  
- `BeautifulSoup` オブジェクトを返すことで、スクリプト内でスクリプトタグの除去や壊れたタグの修正、スタイルシートの注入など、**convert HTML to EPUB** 前の前処理が容易になります。

---

## ステップ 3 – HTML を EPUB に変換

**load HTML file in Python** ができたので、これをクリーンな EPUB に変換しましょう。以下の関数は `BeautifulSoup` オブジェクト、出力先パス、任意のメタデータを受け取ります。

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**この実装が機能する理由:**  
- `ebooklib.epub.EpubBook` が ZIP コンテナと必須のマニフェストファイルを抽象化します。  
- 複数の書籍を作成した際に ID が重複しないよう、UUID を識別子として生成します。  
- `spine` は読者に章の順序を示します。シングルチャプターの書籍であればこれだけで十分です。  

**変換の実行例:**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

スクリプトを実行すると、緑のチェックマークとともに EPUB ファイルの保存場所が表示されます。

---

## ステップ 4 – HTML を MHTML に変換

MHTML（または MHT）は HTML とすべてのリソース（画像、CSS）を単一の MIME ファイルにまとめます。Python の `email` パッケージだけで外部依存なしにこの形式を作成できます。

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**重要ポイント:**  

- `multipart/related` MIME タイプは、HTML 部分とそのリソースが一体であることをブラウザに示します。  
- `<img>` タグを走査して画像を埋め込みます。画像が不要な場合はこのブロックを省略できます。  
- `Content-Location` には `file://` URI を使用し、ブラウザが内部でリソースを解決できるようにします。  

**関数呼び出し例:**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

これで `sample.epub` と `sample.mhtml` が隣り合わせに生成されました。

---

## 完全スクリプト – すべての手順を 1 ファイルにまとめる

以下はすべてを統合した、すぐに実行できるスクリプトです。`convert_html.py` として保存し、`YOUR_DIRECTORY` を `sample.html` があるディレクトリに置き換えてください。

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
convert_html.py

A tiny utility that demonstrates:
- How to load an HTML file in Python
- How to convert HTML to EPUB (convert html to epub)
- How to convert HTML to MHTML (convert html to mhtml)

Author: Your Name
Date: 2026‑07‑18
"""

from pathlib import Path
import uuid
import mimetypes


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Convert EPUB to PDF with Java – Using Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [How to Convert EPUB to Images with Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}