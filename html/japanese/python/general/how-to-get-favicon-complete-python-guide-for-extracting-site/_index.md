---
category: general
date: 2026-06-26
description: URLからHTMLを読み込み、linkタグのhrefを抽出してfaviconを取得する方法を学びましょう。ウェブサイトのアイコンを素早く取得するためのステップバイステップのPythonコード。
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: ja
og_description: ファビコンを素早く取得する方法：URLからHTMLを読み込み、`link rel='icon'` を探し、リンクタグから href
  を抽出する（Python 使用）。
og_title: Faviconの取得方法 – Pythonチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: Favicon の取得方法 – サイトアイコンを抽出する完全な Python ガイド
url: /ja/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Favicon の取得方法 – サイトアイコン抽出の完全 Python ガイド

任意のウェブサイトから **how to get favicon** を手動でページソースを調べずに取得したいと思ったことはありませんか？ 開発者、SEO の専門家、デザイナーなど、多くの人がサイトを表す小さなアイコンを必要としています。このチュートリアルでは、URL から HTML を取得し、`<link rel="icon">` タグを見つけ、アイコンの URL を抽出する、クリーンで Python 中心の方法をご紹介します。最後まで読めば、任意のドメインに対して **how to get favicon** を正確に行う方法が分かり、プロジェクトで再利用できるスクリプトが手に入ります。

HTML の取得から、相対 URL や複数のアイコン形式といったエッジケースの処理まで、すべてカバーします。外部サービスは不要—標準の `requests` ライブラリと軽量な HTML パーサーだけで完結します。準備はいいですか？さっそく始めましょう。

## 前提条件

- Python 3.8+ がインストール済み（コードは 3.10 でも動作します）  
- `requests` とリスト内包表記の基本的な知識  
- 対象ウェブサイトへアクセスできるインターネット接続  

これらがすでに揃っているなら、最初のステップへ進んでください。まだの場合は、唯一必要な依存関係をインストールします。

```bash
pip install requests beautifulsoup4
```

> **プロのコツ:** `beautifulsoup4` は実績のあるパーサーで、 “load html from url” を簡単にします。

## Step 1: Load HTML from URL with Python  

**how to get favicon** を学ぶ際に最初に行うべきことは、ページのソースを取得することです。これがプロセスの “load html from url” 部分です。

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

なぜ `requests` を使うのか？ リダイレクト、HTTPS の検証、タイムアウトを自動で処理してくれるため、後で **get website icons** を試みたときの予期せぬエラーが減ります。

## Step 2: Parse the Document and Find Icon Links  

HTML を取得したら、`rel` 属性がアイコンを示すすべての `<link>` 要素を探す必要があります。これが **how to get favicon** の核心です。

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

`icon` と `shortcut icon` の両方をチェックしているのは、古いサイトが後者をまだ使用していることがあるためです。この小さな違いが “how to extract favicons” を検索する人をしばしば混乱させます。

## Step 3: Extract href from Link Elements  

対象のタグが取得できたら、次の論理的なステップ—**extract href from link**—はシンプルです。

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

`urljoin` を使うことで、サイトが `/favicon.ico` のような相対パスを提供していても、正しい絶対 URL に変換されます。信頼性の高い **how to get favicon** スクリプトにとって重要です。

## Step 4: Optional – Validate and Filter Icon URLs  

ページによっては多数のアイコン（Apple タッチアイコン、さまざまなサイズの PNG など）が列挙されています。古典的な `.ico` ファイルだけが欲しい場合は、ここでフィルタリングします。このステップは **how to extract favicons** の特定タイプ抽出方法を示しています。

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

フィルタは自由に調整できます。`".ico"` を `".png"` に置き換えたり、`rel="apple-touch-icon"` をチェックして高解像度アイコンを取得したりしてください。

## Step 5: Download the Icon Files (If You Want the Actual Image)  

URL の抽出だけでも半分の成功です。実際の画像ファイルが必要な場合は、以下のヘルパーでダウンロードできます。

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

前のステップの後に実行すれば、発見したすべての favicon のローカルコピーが得られ、キャッシュやオフライン分析に最適です。

## Step 6: Putting It All Together – Full Working Example  

以下は、任意のサイトから **how to get favicon** を実演する、完全に実行可能なスクリプトです。`target_url` を変更してコピー＆ペーストすればすぐに結果が確認できます。

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**期待される出力（簡略化）:**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

サイトが PNG や Apple タッチアイコンのみを提供している場合は、代わりにそれらの URL が列挙され、あらゆるシナリオで **how to get favicon** がどのように機能するかが分かります。

## Common Questions & Edge Cases  

### サイトが `<link>` ではなく `<meta>` タグでアイコンを指定している場合は？  
古いページでは `<meta name="msapplication‑TileImage">` にアイコン URL が埋め込まれていることがあります。`find_icon_links` を拡張してこれらの meta タグも検索し、同様に処理できます。

### `//` で始まる相対 URL はどう扱うべき？  
`urljoin` はプロトコル相対 URL（`//example.com/favicon.ico`）をベース URL のスキームに基づいて自動的に解決するので、追加ロジックは不要です。

### 複数サイズ（例: 32×32、180×180）を自動取得したい場合は？  
`filter_ico_urls` ステップを省略すれば、スクリプトは見つけたすべてのアイコン URL を返します。PNG のサイズバリエーションも含まれるので、ファイル名パターンでソートや選択が可能です。

### ボットをブロックするサイトでも動作しますか？  
サイトが 403 を返したりカスタム User‑Agent が必要な場合は、`requests.get` 呼び出しを次のように調整します。

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

この小さな変更で、厳格なドメインでも “how to get favicon” が解決できることが多いです。

## Visual Overview  

![Diagram showing the flow of how to get favicon from a website – load HTML, parse link tags, extract href, optional download](how-to-get-favicon-diagram.png "how to get favicon flow diagram")

*画像の alt テキストには主要キーワードが含まれており、画像 SEO を満たしています。*

## Conclusion  

**how to get favicon** の手順を順を追って解説しました：URL から HTML をロードし、…

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}