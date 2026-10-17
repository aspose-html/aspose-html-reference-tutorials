---
category: general
date: 2026-06-10
description: PythonでHTMLを読み込み、ページからSVG画像を抽出する—ステップバイステップのコード、ヒント、エッジケースの対処方法。
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: ja
og_description: PythonでHTMLを読み込み、SVG画像を抽出する明確で実行可能な例。HTMLのSVG要素の検索方法とエッジケースの処理を学びましょう。
og_title: PythonでHTMLを読み込む – SVG画像を効率的に抽出
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: PythonでHTMLを読み込む – SVG画像抽出の完全ガイド
url: /ja/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでHTMLを読み込む – SVG画像抽出の完全ガイド

ページからすべてのSVGグラフィックを取得するために **PythonでHTMLを読み込む** 必要があったことはありませんか？ あなただけではありません。ウェブスクレイパーを作成する場合でも、アセットレポートを生成する場合でも、単にサイトが使用しているアイコンに興味があるだけでも、 **SVG画像を抽出する** 方法を知っていれば、手作業で探す手間が大幅に省けます。

このチュートリアルでは、 **PythonでHTMLを読み込む** 方法から始め、 **HTML SVG** 要素を検索し、 **インラインSVG** を見つけ、 `<img>` タグで参照されている外部SVGファイルまで取得する、実用的なエンドツーエンドのソリューションを順を追って解説します。最後まで読めば、再利用可能なスクリプトと、ちょっとしたコツ、そして出力イメージの全体像が手に入ります。

## 学べること

* ローカルHTMLファイル（または取得したページ）を解析し、見つけたすべてのSVGを一覧表示する、完全に実行可能なPythonスクリプト。  
* **インラインSVG** (`<svg>…</svg>`) と **外部SVG** (`<img src="… .svg">`) の違いの理解。  
* 不正なマークアップ、欠損ファイル、名前空間の問題への対処法。  
* コードの拡張アイデア――SVGを保存したり、PNGに変換したり、データベースに投入したりする方法。

### 前提条件

* Python 3.8+ がインストールされていること。  
* Python の `requests` と `BeautifulSoup` ライブラリに基本的に慣れていること（インポートは行いますが、深い解説は不要です）。  
* スキャンしたいローカルHTMLファイルまたはURLが用意されていること。  

それでは、始めましょう。

## PythonでHTMLを読み込む – パーサーの設定

最初のステップは **PythonでHTMLを読み込む** ことです。ディスク上のファイルを読むか、リモートページを取得するかは選べます。以下は、両方に対応した最小限ながら堅牢なヘルパーです。

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **重要ポイント:** `BeautifulSoup` を使うことで、生の文字列解析の癖を隠蔽できます。この関数はローカルファイルとリモートURLの両方を優雅に処理し、ネットワーク要求が失敗した場合は例外を投げます――エラーがすぐに分かります。

## SVG画像の抽出 – インラインSVG要素の取得

ドキュメントが読み込めたら、次は **インラインSVG** タグを **見つける** 作業です。インラインSVGはHTMLマークアップに直接埋め込まれているため、DOMからそのまま取得できます。

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*プロのコツ:* ページがSVG名前空間 (`<svg xmlns="http://www.w3.org/2000/svg">`) を使用していても、`BeautifulSoup` はデフォルトで名前空間を無視してタグを検出します。これは **HTML SVGを検索する** ときにとても便利です。

## HTML SVGの検索 – 外部 `<img>` 参照の処理

多くのサイトはSVGを直接埋め込まず、 `<img src="icon.svg">` のように外部ファイルを参照しています。これらを取得するには、すべての `<img>` タグを走査し、`src` が `.svg` で終わるかを確認します。

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **エッジケース注意:** 一部のページはクエリ文字列（`icon.svg?v=2`）やフラグメント（`icon.svg#layer`）を付加しています。`endswith(".svg")` のチェックは文字列の小文字化した末尾だけを見るので問題なく機能します。より厳密な検証が必要な場合は、`urllib.parse` を使ってパラメータを除去すると良いでしょう。

## インラインSVGの検索 – 結果のレポート

これで、インラインSVGマークアップのリストと外部ファイル参照のリストという二つが揃いました。両方を統合して総数を報告すれば完了です。これは最初に提示したスニペットを拡張した形ですが、少しだけコンテキストを付加しています。

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## すべてをまとめる – 完全スクリプト

以下が実行可能なフルプログラムです。`extract_svg.py` という名前で保存し、ローカルHTMLファイルまたはURLを指定して実行してください。

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### 期待される出力

サンプルの `sample.html` に対してスクリプトを実行すると、次のような出力が得られるでしょう。

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

ダウンロードブロックのコメントを外せば、外部SVGも取得できます。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法をベースに、さらに関連するトピックを深掘りしています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加のAPI機能を習得したり、独自プロジェクトで代替実装アプローチを試したりするのに役立ちます。

- [svg to png java – Aspose.HTML for JavaでSVGを画像に変換](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}