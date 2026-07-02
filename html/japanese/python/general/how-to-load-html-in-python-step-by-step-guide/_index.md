---
category: general
date: 2026-07-02
description: PythonでHTMLを読み込み、idで要素を取得し、ファイルからテキストを抽出する方法を学びましょう。この実践的なチュートリアルでは、BeautifulSoupを使ってHTMLファイルを読む手順を示します。
draft: false
keywords:
- how to load html
- how to get element
- how to extract text
- get element by id
- read html file python
language: ja
og_description: PythonでHTMLを読み込み、BeautifulSoupを使用してテキストを抽出する方法。ガイドに従ってHTMLファイルを読み込み、idで要素を取得し、その内容を表示します。
og_title: PythonでHTMLを読み込む方法 – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  headline: How to Load HTML in Python – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  name: How to Load HTML in Python – Step‑by‑Step Guide
  steps:
  - name: What if the HTML is malformed?
    text: BeautifulSoup’s `lxml` parser is forgiving, but for severely broken markup
      you might want to fallback to the built‑in `html.parser`. Swap `"lxml"` with
      `"html.parser"` in the `BeautifulSoup` constructor.
  - name: How to handle multiple elements with the same ID?
    text: HTML spec says IDs should be unique, but reality sometimes disagrees. Use
      `soup.find_all(id="duplicate-id")` to retrieve a list, then iterate over it.
  - name: Need to read from a URL instead of a file?
    text: Replace the file‑reading logic with `requests.get(url).text`. Remember to
      install the `requests` package (`pip install requests`) and handle network errors
      gracefully.
  - name: Want to extract other attributes (e.g., `class` or `href`)?
    text: 'Simply access them like a dictionary: `header[''class'']` or `header[''href'']`.
      If the attribute might be missing, use `.get(''class'')` to avoid `KeyError`.'
  type: HowTo
tags:
- Python
- HTML parsing
- BeautifulSoup
title: PythonでHTMLを読み込む方法 – ステップバイステップガイド
url: /ja/python/general/how-to-load-html-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python で HTML を読み込む方法 – 完全チュートリアル

Python スクリプトで **HTML を読み込む** 方法で、髪の毛をむしりたくなることはありませんか？ あなただけではありません。ニュースサイトをスクレイピングしたり、ローカルレポートを処理したり、メールテンプレートから見出しを取得したりする場合、HTML の読み込み技術はすべての開発者にとって必須のスキルです。

このガイドでは **ID で要素を取得する方法**、**テキストを抽出する方法**、そして最終的に結果を出力する方法を、コードをクリーンで Pythonic に保ちながら解説します。また **Python で HTML ファイルを読む** コツもカバーするので、すぐに使える解決策をコピーペーストできます。

> **プロのコツ:** 例では軽量でドキュメントが充実しており、シンプルから複雑な HTML 構造まで対応できる *BeautifulSoup* ライブラリを使用しています。

## 必要なもの

始める前に以下を用意してください。

- Python 3.9 以上（コードは 3.10+ でも動作します）
- `beautifulsoup4` と `lxml` がインストール済み（`pip install beautifulsoup4 lxml`）
- サンプル HTML ファイル – ここでは `sample.html` と呼び、`YOUR_DIRECTORY` フォルダーに置きます

以上です。重いブラウザや Selenium は不要、純粋な Python だけです。

## ステップ 1: HTML を読み込む – ファイルをメモリに読み込む

最初にやるべきことは **HTML ファイルをディスクから読み込む** ことです。これは以降のすべてのステップの基礎になるので、正しく行いましょう。

```python
from pathlib import Path

# Define the path to the HTML file
html_path = Path("YOUR_DIRECTORY/sample.html")

# Read the file contents as a string
html_content = html_path.read_text(encoding="utf-8")
```

*なぜ重要か:* `Path.read_text` を使うと OS 固有の改行コードを抽象化し、UTF‑8（現代のウェブページの事実上のエンコーディング）を自動的に処理します。ファイルが存在しない場合は `FileNotFoundError` が明確に発生し、デバッグが楽になります。

## ステップ 2: HTML ドキュメントをパースする

生の文字列が手に入ったら、**HTML をパーサーオブジェクトにロード** します。BeautifulSoup は DOM を操作する便利な API を提供します。

```python
from bs4 import BeautifulSoup

# Create a BeautifulSoup object using the lxml parser (fast and reliable)
soup = BeautifulSoup(html_content, "lxml")
```

*なぜ lxml?* `lxml` パーサーは Python 標準のパーサーより大幅に高速で、壊れたマークアップもより寛容に処理します。実務でスクレイピングするような HTML に最適です。

## ステップ 3: ID で要素を取得 – ヘッダーを探す

ドキュメントがパースできたら、**特定の ID を持つ要素を取得する方法** を見ていきます。例では `id` 属性が `"main-header"` の `<h1>` タグを対象にします。

```python
# Retrieve the element with the specific ID
header = soup.find(id="main-header")
```

要素が見つからなければ `header` は `None` になります。以下のようにガードするのがベストプラクティスです。

```python
if header is None:
    raise ValueError("Element with id='main-header' not found in the HTML file.")
```

## ステップ 4: テキストを抽出する – 中身を取得

要素が取得できたら、テキストコンテンツを抽出するのはとても簡単です。これが **タグからテキストを抽出する方法** です。

```python
# Extract the visible text inside the element
header_text = header.get_text(strip=True)  # strip removes surrounding whitespace
```

`get_text` はネストしたテキストノードを自動で連結してくれるので、子要素を手動でループする必要はありません。`strip=True` フラグで改行や余分なスペースが除去され、クリーンな文字列が得られます。

## ステップ 5: 結果を出力 – 正しく動くか確認

最後に、コンソールへ結果を出力します。これは元のスニペットの `print(header.text_content)` 行に相当します。

```python
print(header_text)  # prints: The text inside <h1 id="main-header">
```

スクリプトを実行して期待通りの見出しが表示されたら、**Python で HTML ファイルを読み込み、ID で要素を取得し、テキストを抽出** できたことになります。おめでとうございます！

## 完全動作サンプル

以下がそのまま実行できる完全版スクリプトです。`extract_header.py` という名前で保存し、`python extract_header.py` を実行してください。

```python
# extract_header.py
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(file_path: str) -> str:
    """Read an HTML file and return its contents as a string."""
    path = Path(file_path)
    if not path.is_file():
        raise FileNotFoundError(f"Unable to locate the file: {file_path}")
    return path.read_text(encoding="utf-8")

def get_element_by_id(soup: BeautifulSoup, element_id: str):
    """Return the first tag with the given id, or raise an informative error."""
    element = soup.find(id=element_id)
    if element is None:
        raise ValueError(f"Element with id='{element_id}' not found.")
    return element

def main():
    # Step 1: Load the HTML document
    html = load_html("YOUR_DIRECTORY/sample.html")
    
    # Step 2: Parse the HTML with BeautifulSoup
    soup = BeautifulSoup(html, "lxml")
    
    # Step 3: Retrieve the element by its ID
    header = get_element_by_id(soup, "main-header")
    
    # Step 4: Extract and print the text content
    print(header.get_text(strip=True))

if __name__ == "__main__":
    main()
```

**期待される出力**（`sample.html` に `<h1 id="main-header">Welcome to My Site</h1>` が含まれている場合）:

```
Welcome to My Site
```

これだけです—BeautifulSoup と lxml 以外の余計な依存関係は不要です。

## よくある質問とエッジケース

### HTML が壊れている場合は？

BeautifulSoup の `lxml` パーサーは寛容ですが、極端に壊れたマークアップの場合は組み込みの `html.parser` にフォールバックすると良いでしょう。`BeautifulSoup` コンストラクタの `"lxml"` を `"html.parser"` に置き換えるだけです。

### 同じ ID が複数ある場合は？

HTML 仕様では ID は一意であるべきですが、実務では例外もあります。`soup.find_all(id="duplicate-id")` でリストを取得し、必要に応じてイテレートしてください。

### ファイルではなく URL から読み込む場合は？

ファイル読み込みロジックを `requests.get(url).text` に置き換えます。`requests` パッケージ（`pip install requests`）をインストールし、ネットワークエラーを適切にハンドリングすることを忘れずに。

### 他の属性（例: `class` や `href`）を取得したい場合は？

辞書のようにアクセスできます: `header['class']` や `header['href']`。属性が存在しない可能性がある場合は `.get('class')` を使って `KeyError` を回避しましょう。

## ビジュアルサマリー

![how to load html example](https://example.com/placeholder-image.png "how to load html example")

*Alt text:* how to load html example – ファイル読み込みからテキスト抽出までの流れを示す図

## まとめ

**Python で HTML を読み込む方法**、**ID で要素を取得する方法**、そして **要素からテキストを抽出する方法** をカバーしました。上記の手順に従えば、確実に **Python で HTML ファイルを読み込み、DOM を操作し、必要な情報を取得** できるようになります。

## 次にやること

- **CSS セレクタを試す:** `soup.select_one('.my-class')` で柔軟なクエリが可能です。
- **複数ページをスクレイプ:** このパターンに `requests` とループ処理を組み合わせて、サイトを一括処理しましょう。
- **HTML に書き戻す:** BeautifulSoup はツリーを変更して保存できるので、テンプレート生成にも便利です。
- **パフォーマンスチューニング:** 大容量ファイルの場合は `lxml.etree.iterparse` のようなストリーミングパーサーを検討してください。

ぜひ実験してみてください—ID を変えてみたり、別のタグを対象にしたり、XHTML を扱うなら `xml.etree.ElementTree` に切り替えても構いません。概念は同じで、これで HTML パースの基礎がしっかり身につきました。

Happy coding! 問題があったり、面白いユースケースを共有したいときは、ぜひコメントで教えてください。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した、密接に関連するトピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能をマスターしたり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [ファイルから HTML ドキュメントを読み込む – Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Java で HTML をクエリする方法 – 完全チュートリアル](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Java 用 Aspose.HTML で HTML を編集する方法](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}