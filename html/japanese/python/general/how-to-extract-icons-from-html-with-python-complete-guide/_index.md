---
category: general
date: 2026-07-02
description: Python を使用して HTML ファイルからアイコンを抽出する方法。Python で HTML ファイルを読み込み、HTML ドキュメントを解析し、href
  属性を抽出して favicon の URL を取得する方法を学びます。
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: ja
og_description: Python を使用して HTML ページからアイコンを抽出する方法。このチュートリアルでは、Python で HTML ファイルを読み込み、ドキュメントを解析し、favicon
  の URL を取得する手順を示します。
og_title: HTMLからアイコンを抽出する方法 – Pythonガイド
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: PythonでHTMLからアイコンを抽出する方法 – 完全ガイド
url: /ja/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでHTMLからアイコンを抽出する方法 – 完全ガイド

ブラウザを開かずにウェブページから **アイコンを抽出する方法** を考えたことはありませんか？サイトカタログやSEO監査ツールを作っているか、タブに表示される小さなファビコンが気になるだけかもしれません。良いニュースは、Python数行で実現できることです—SeleniumもヘッドレスChromeも不要で、プレーンテキストのHTMLファイルだけで済みます。

このチュートリアルでは、HTMLファイルをPythonで読み込み、HTMLドキュメントをパースし、最終的に `<link rel="icon">` タグから **href属性を抽出** してファビコンのURLを取得する手順を解説します。最後まで読むと、任意の静的HTMLに対して使える再利用可能なスニペットが手に入り、相対パスや複数のアイコン宣言といったエッジケースの処理方法も学べます。

## 学べること

- PythonでローカルHTMLファイルを読み込む (read html file python)  
- 軽量パーサーを使用して **HTMLドキュメントを安全にパース** する  
- `<link>` 要素でアイコンが宣言されている箇所を特定する  
- **href属性** の値を抽出し、絶対URLに変換する  
- 取得したすべての **favicon URL** を収集して出力する  

外部サービスは不要です—標準ライブラリと人気の **BeautifulSoup** パッケージだけで完結します。

![Pythonスクリプトでアイコンを抽出する様子のスクリーンショット – アイコン抽出方法](https://example.com/images/extract-icons-python.png "アイコン抽出方法")

*画像の代替テキスト: "Pythonスクリプトを使用したアイコン抽出方法"*

## 前提条件

- Python 3.8+ がインストールされていること  
- `beautifulsoup4` ライブラリ (`pip install beautifulsoup4`)  
- スキャンしたいローカルHTMLファイル（例: `sample.html`）  

これらが揃っているなら、さっそく始めましょう。

## ステップ1: HTMLファイルをPythonで読み込む – ドキュメントのロード

まず最初に、ファイルを開いてその内容をパーサーに渡す必要があります。`with open(..., "r", encoding="utf‑8")` を使用すれば、ファイルは自動的に閉じられ、UTF‑8 エンコーディングはほとんどの最新ページに対応します。

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**なぜ重要か:** 正しいエンコーディングでファイルを開くことで、後でパーサーを壊す可能性のある謎の `�` 文字を防げます。標準ライブラリの `Path` を使用すれば、コードはクロスプラットフォームにもなります。

## ステップ2: HTMLドキュメントをパース – すべてのアイコンリンクを取得

ここで生のHTMLを **BeautifulSoup** に渡すと、ナビゲート可能なツリーが構築されます。`rel` 属性に `icon` という単語が含まれるすべての `<link>` タグを探します。`rel` はスペース区切りのリスト（例: `rel="shortcut icon"`）になることがあるので、柔軟なチェックが必要です。

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**このステップが重要な理由:** 単純な `soup.find_all("link", rel="icon")` では `rel="shortcut icon"` や `rel="apple-touch-icon"` といったバリエーションを見逃します。私たちのヘルパー関数 `is_icon_link` がこれらのケースを網羅し、抽出を堅牢にします。

## ステップ3: href属性を抽出 – URLを取得

対象のタグを収集したら、各タグから `href` 属性を取得します。ページによっては `href` が省略されていることもあります（稀ですが可能性はあります）ので、`None` に対するガードを入れます。さらに、ファビコンは相対URLで指定されることが多いため、ベースURLが分かっていればそれに対して解決します。ローカルファイルの場合はパスをそのまま保持します。

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**空白を除去する理由:** HTML作者がURLの前後にスペースを入れてしまうことがあり、後続のリクエストが失敗します。トリミングすることでクリーンな文字列が得られます。

## ステップ4: Favicon URLを抽出 – 結果を出力

最後に、取得したURLのリストを出力（または返却）します。実際のスクリプトではCSVに書き出したり、アイコンをダウンロードしたり、別のサービスに渡したりすることが考えられます。以下はコンソールに結果を表示するシンプルなループです。

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### エッジケースの処理

- **複数の rel 値:** `is_icon_link` のチェックはすでに `rel="shortcut icon"` や `rel="apple-touch-icon"` を捕捉します。  
- **相対パス:** 後で絶対URLが必要な場合は `urllib.parse.urljoin(base_url, href)` を使用します。  
- **href が欠如:** ガード `if href:` により不正なタグをスキップし、`NoneType` エラーを防ぎます。  
- **重複エントリ:** `icon_urls = list(dict.fromkeys(icon_urls))` とすれば重複を除去できます。

## 完全スクリプト – ワンストップソリューション

すべてを統合した、実行可能な完全プログラムを示します。`extract_icons.py` として保存し、`html_path` を任意のファイルに設定してください。

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**期待される出力**（`sample.html` にアイコンが2つあると仮定）:

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

`python extract_icons.py` で実行すると、コンソールにURLが表示されます。

## よくある質問

**Q: HTMLが `<meta>` タグでアイコンを指定している場合は？**  
A: 一部のサイトは `<meta itemprop="image">` でアイコンを埋め込んでいます。`is_icon_link` を拡張して `itemprop="image"` を持つ `meta` をチェックし、その `content` 属性を取得するようにします。

**Q: アイコンを自動で取得できますか？**  
A: はい。各URLを `requests.get(url, stream=True)` に渡してコンテンツをファイルに書き出すだけです。相対URLは `urljoin` で処理することを忘れないでください。

**Q: リモートページでも動作しますか？**  
A: もちろんです。ファイル読み込みのステップを `requests.get(page_url).text` に置き換えて、HTML文字列を BeautifulSoup に渡せば動作します。ただし、robots.txt とレートリミットには注意してください。

## まとめ

Pythonを使って任意の静的HTMLから **アイコンを抽出する方法** を、ファイルの読み込みから各favicon URLの出力までカバーしました。ファイルを読む、ドキュメントをパースする、適切なタグを見つける、`href` 属性を取得するという基本的な考え方は、さまざまなウェブスクレイピングタスクで再利用できるパターンです。

次のステップは？スクリプトを拡張してみましょう：

- ページのベースURLに対して相対URLを解決する  
- 各アイコンをダウンロードしてローカルに保存する  
- 追加のアイコン形式（Safari 用の `rel="mask-icon"` など）に対応する  

自由に試してみて、問題があれば下にコメントを残してください。楽しいパースを！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加のAPI機能を習得したり、プロジェクトで代替実装アプローチを検討したりするのに役立ちます。

- [JavaでHTMLをクエリする方法 – 完全チュートリアル](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Aspose.HTML for JavaでHTMLドキュメントツリーを編集する方法](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Aspose.HTML for JavaでHTMLドキュメントをファイルに保存する方法](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}