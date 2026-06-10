---
category: general
date: 2026-06-10
description: URLからHTMLを読み込み、ウェブサイトのアイコンを素早く取得します。favicon の抽出方法、ウェブサイトの favicon URL
  の取得方法、そして Python でのエッジケースの処理方法を学びましょう。
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: ja
og_description: URLからHTMLを読み込み、ファビコンを抽出してウェブサイトのファビコンURLを取得します。開発者向けのステップバイステップPythonチュートリアル。
og_title: URLからHTMLを読み込み、ウェブサイトのアイコンを取得する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML from URL to get website icons quickly. Learn how to extract
    favicons, fetch website favicon URLs, and handle edge cases in Python.
  headline: Load HTML from URL and Get Website Icons – Complete Guide
  type: TechArticle
tags:
- web scraping
- favicon extraction
- python
- html parsing
title: URLからHTMLをロードし、ウェブサイトのアイコンを取得する – 完全ガイド
url: /ja/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# URL から HTML を読み込み、ウェブサイトのアイコンを取得する – 完全ガイド

サイトの小さなロゴだけを取得したいときに **URL から HTML を読み込む** 必要があること、ありませんか？ブックマークマネージャーや SEO ダッシュボード、あるいは個人の趣味プロジェクトを作っているときでも、ウェブサイトのアイコンを取得することは小さくても重要なパズルのピースです。

このチュートリアルでは、重い Selenium やブラウザ操作を使わずに、純粋な Python だけで **favicon を抽出する方法** をご紹介します。最後まで読めば、**ウェブサイトの favicon URL を取得** し、相対パスを処理し、サイトが複数のアイコンを提供している場合でも取得できるようになります。準備はいいですか？さっそく始めましょう。

## なぜ最初に URL から HTML を読み込むのか？

ページの生の HTML を取得すると、ブラウザが favicon を探すために使用する `<link>` タグに直接アクセスできます。そのタグは通常次のようになります:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

このマークアップを取得できれば、`href` 属性をプログラムで読み取り、画像を自分でダウンロードできます。スクリーンショットをスクレイピングするよりも高速で、標準的な慣習に従っているサイトならどこでも機能します。

## Step 1 – URL から HTML ドキュメントを読み込む

まず最初に必要なのは、ページのソースを取得する手段です。Python で最も一般的に使われるのは **requests** ライブラリで、シンプルかつ信頼性が高く、リダイレクトも自動で処理してくれます。

```python
import requests

def fetch_html(url: str) -> str:
    """
    Retrieve the raw HTML from the given URL.
    Raises an exception if the request fails.
    """
    response = requests.get(url, timeout=10)
    response.raise_for_status()          # Fail fast on HTTP errors
    return response.text
```

> **プロのコツ:** 社内プロキシ環境下で作業している場合は、`requests.get` に `proxies=` を渡してください。また、短めのタイムアウトを設定すると、死んだサイトでスクリプトがハングするのを防げます。

これで `fetch_html("https://example.com")` を呼び出すと、ページのマークアップが文字列として返ってきます。これが **URL から HTML を読み込む** の核心で、以降のパイプラインはこの文字列を基に動作します。

## Step 2 – ウェブサイトのアイコンを取得する

HTML が手に入ったら、次は `rel` 属性に「icon」が含まれるすべての `<link>` 要素を探します。標準の `html.parser` モジュールでも可能ですが、**BeautifulSoup** を使うとコードが格段に読みやすくなります。

```python
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def extract_icon_links(html: str, base_url: str) -> list[str]:
    """
    Parse the HTML and return a list of absolute URLs pointing to icons.
    Handles relative hrefs by joining them with the page’s base URL.
    """
    soup = BeautifulSoup(html, "html.parser")
    icons = []

    # Look for any <link> tag where rel contains "icon"
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            # Convert relative URLs to absolute ones
            absolute_url = urljoin(base_url, href)
            icons.append(absolute_url)

    return icons
```

`urljoin` を使って `"/favicon.ico"` を `"https://example.com/favicon.ico"` に変換しているのが分かりますか？これは **ウェブサイトのアイコンを取得** する際の典型的なエッジケースです。デバイス別に異なるアイコンを提供しているサイトもあるので、結果として複数の URL が得られることがあります。問題ありません、すべて収集すれば OK です。

## Step 3 – Favicon URL を抽出して表示する

全体の流れを組み合わせるのはシンプルです。HTML を取得し、抽出器を走らせ、結果のリストを出力します。最終スクリプトは次のようになります:

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def extract_icon_links(html: str, base_url: str) -> list[str]:
    soup = BeautifulSoup(html, "html.parser")
    icons = []
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            icons.append(urljoin(base_url, href))
    return icons

def main():
    target = "https://example.com"
    html = fetch_html(target)
    icon_urls = extract_icon_links(html, target)
    print("Found icon URLs:", icon_urls)

if __name__ == "__main__":
    main()
```

### 期待される出力

標準的な favicon を提供しているサイトに対してスクリプトを実行すると、次のような出力が得られるでしょう:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

サイトが複数のアイコン（Apple touch icon、shortcut icon など）を提供している場合は、より長いリストが表示されます:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

これが **favicon URL を抽出** するワークフロー全体です。コンパクトで依存性が少なく、どんなプロジェクトにもすぐに組み込めます。

## 共通の落とし穴への対処

| 問題 | 発生理由 | 簡単な解決策 |
|------|----------|--------------|
| **`<base>` タグがない相対 `href`** | `urljoin` はページ URL を基準に解決するため、ほとんどの場合は問題ありません。 | `<base href="...">` タグが存在すれば、まずそれを取得し `base_url` として渡します。 |
| **`rel="icon"` が欠落** | 一部のサイトは `rel="shortcut icon"` やカスタム値を使用します。 | ラムダ式を拡張: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())` |
| **別ドメインへのリダイレクト** | favicon が CDN 上に置かれていることがあります。 | `urljoin` は最終リクエスト URL（`response.url`）を基に正しく解決します。 |
| **リンク切れ（404）** | HTML が存在しないファイルを指している場合です。 | URL を抽出した後、HEAD リクエストで各リンクの有効性を確認できます。 |
| **同一アイコンの `<link>` が複数** | 重複エントリがリストを膨らませます。 | `set(icon_urls)` を使って返す前に重複を除去します。 |

## さらに踏み込む – 大量にウェブサイトの Favicon URL を取得する

複数ドメインの **ウェブサイト favicon URL を取得** したい場合は、`main` ロジックをループで包みます:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

このパターンはスケールしやすく、`functools.lru_cache` などでキャッシュを追加すれば同じサイトへの過剰なリクエストを防げます。

## ビジュアル概要

![URL から HTML を読み込む図](load-html-url.png)

*Alt text: URL から HTML を読み込む図 – fetch → parse → extract のステップを示す。*

上の画像は、**URL から HTML を読み込む**、**ウェブサイトのアイコンを取得**、**favicon URL を抽出** の 3 ステッププロセスを凝縮しています。チームメンバーにフローを説明する際に便利です。

## 結論

Python の `requests` と `BeautifulSoup` だけを使って、**URL から HTML を読み込み**、**ウェブサイトのアイコンを取得** する完全なプロダクションレベルのソリューションを解説しました。`<link rel="icon">` タグの `href` 属性を抽出することで、**favicon URL を抽出** し、相対パスを処理し、複数形式のアイコンも取得できます—コードは数十行ですむシンプルさです。

次は何をしますか？アイコンをローカルフォルダにダウンロードしたり、ドメイン‑to‑favicon のマッピングを CSV に出力したり、Flask API に組み込んでオンデマンドで favicon を提供したりしてみましょう。**ウェブサイト favicon URL を取得** する可能性は無限大で、基本テクニックは変わりません。

エッジケースに関する質問や、 clever な工夫があればぜひコメントで共有してください—アイコンハンティングを楽しんでください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基に、さらに関連するトピックを深く掘り下げています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能をマスターしたり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Load HTML Documents from Stream with Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Handle Document Load Events in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}