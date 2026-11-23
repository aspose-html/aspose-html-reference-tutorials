---
category: general
date: 2026-09-16
description: PythonでHTMLファイルを解析し、ファイルからHTMLドキュメントを読み込み、文字列からHTMLドキュメントを作成する、シンプルで実行可能なコード。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- parse html file in python
- create html document from string
- load html document from file
- read local html file python
language: ja
lastmod: 2026-09-16
og_description: PythonでHTMLファイルを解析し、ローカルのHTMLファイルを読み込み、文字列からHTMLドキュメントを迅速かつ確実に作成します。
og_image_alt: Screenshot of Python code parsing an HTML file and creating a document
  from a string
og_title: PythonでHTMLファイルを解析 – 文字列からドキュメントを作成
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  headline: Parse HTML file in Python and create document from string
  type: TechArticle
- description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  name: Parse HTML file in Python and create document from string
  steps:
  - name: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
    text: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
  - name: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
    text: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
  - name: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
    text: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
  type: HowTo
tags:
- python html parsing
- html document creation
- file handling python
title: PythonでHTMLファイルを解析し、文字列からドキュメントを作成する
url: /ja/python/general/parse-html-file-in-python-and-create-document-from-string/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでHTMLファイルを解析し、文字列からドキュメントを作成する

**PythonでHTMLファイルを解析**したい場合、本ガイドではローカルのHTMLファイルを読み込む方法、ファイルからHTMLドキュメントをロードする方法、そして**文字列からHTMLドキュメントを作成**する方法を詳しく解説します。データのスクレイピング、テンプレートのテスト、動的コンテンツの生成など、以下の手順で完全に実行可能なソリューションを提供します。

このチュートリアルで学べること：

* Pythonの標準ライブラリを使ってローカルHTMLファイルを読み込む方法
* ファイルパスからHTMLドキュメントをロードする方法
* HTML文字列から直接HTMLドキュメントを作成する方法
* ファイルが存在しない場合やエンコーディング問題など、一般的なエッジケースの処理方法

前提条件は Python 3.8+ と `beautifulsoup4` ライブラリだけです。最初のステップでインストールします。

## 前提条件

| 要件 | 理由 |
|------|------|
| Python 3.8 以上 | 型ヒントや最新構文との互換性を保証します。 |
| `beautifulsoup4` と `lxml` パッケージ | 不正なHTMLでも処理できる堅牢なパーサを提供し、便利な `HTMLDocument` ライクなオブジェクトを取得できます。 |
| プロジェクトフォルダー内のサンプルHTMLファイル（`index.html`） | **ファイルからHTMLドキュメントをロード**する例の入力として使用します。 |

pipで依存関係をインストールします：

```bash
pip install beautifulsoup4 lxml
```

## PythonでHTMLファイルを解析

チュートリアルの中心は **parse html file in python** 操作です。`HTMLDocument` という小さなヘルパークラスで BeautifulSoup をラップし、先ほどの例と同じ API を実現します。

```python
from pathlib import Path
from bs4 import BeautifulSoup
from typing import Union

class HTMLDocument:
    """
    Simple wrapper that mimics a “document” object.
    Accepts either a file path or a raw HTML string.
    """
    def __init__(self, source: Union[str, Path]):
        if Path(source).exists():
            # Load html document from file
            self._load_from_file(Path(source))
        else:
            # Assume source is a raw HTML string
            self._load_from_string(source)

    def _load_from_file(self, file_path: Path):
        try:
            # read local html file python – explicit UTF‑8 handling
            html = file_path.read_text(encoding="utf-8")
        except FileNotFoundError:
            raise FileNotFoundError(f"File not found: {file_path}")
        self.soup = BeautifulSoup(html, "lxml")

    def _load_from_string(self, html_string: str):
        self.soup = BeautifulSoup(html_string, "lxml")

    def title(self) -> str:
        """Return the content of the <title> tag, or an empty string."""
        if self.soup.title:
            return self.soup.title.string.strip()
        return ""

    def pretty(self) -> str:
        """Return a nicely formatted HTML representation."""
        return self.soup.prettify()
```

### 仕組み

1. **ソースタイプの検出** – コンストラクタは渡された `source` がディスク上に存在するか確認します。存在すれば **ファイルからHTMLドキュメントをロード**し、存在しなければ生文字列として扱い、**文字列からHTMLドキュメントを作成**の要件を満たします。  
2. **ファイルの読み取り** – `Path.read_text(encoding="utf-8")` を使用し、**ローカルHTMLファイルを安全に読み取る**推奨方法です。  
3. **BeautifulSoupで解析** – `lxml` パーサは高速で、壊れたマークアップにも寛容です。

## ファイルからHTMLドキュメントをロード

`HTMLDocument` クラスが用意できたので、ファイルのロードはシンプルです：

```python
# Step 1: Load an HTML document from a local file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")

# Verify that the file was parsed correctly
print("Document title:", doc.title())
```

**期待される出力**（`index.html` に `<title>My Page</title>` が含まれている場合）：

```
Document title: My Page
```

ファイルが存在しない場合、クラスは明確な `FileNotFoundError` を送出し、実運用コードで捕捉できます。

## 文字列からHTMLドキュメントを作成

文字列から直接ドキュメントを作成すると、テストやオンザフライでのHTML生成に便利です：

```python
# Step 2: Create an HTML document directly from an HTML string
html_content = "<html><head><title>Hello</title></head><body><h1>Hello</h1></body></html>"
doc_from_string = HTMLDocument(html_content)

print("String‑based title:", doc_from_string.title())
```

**期待される出力**：

```
String-based title: Hello
```

同じ `HTMLDocument` クラスが両シナリオを処理するため、**parse html file in python** の API が一貫して利用できます。

## ローカルHTMLファイル（Python） – エッジケースの扱い

実務でファイルを扱う際に頻繁に遭遇する課題：

* **ファイルが見つからない** – `FileNotFoundError` で既に対処済みです。  
* **エンコーディングの違い** – BeautifulSoup に自動判定させても良いですが、明示的に UTF‑8 を指定するのが安全です。  
* **大容量ファイル** – ファイル全体をメモリに読み込むのはコストが高くなる可能性があります。必要に応じて `BeautifulSoup(open(...), "lxml")` でストリーム処理が可能です。

以下はこれらの保護策を組み込んだ防御的ラッパーです：

```python
def safe_load_html(path: Union[str, Path]) -> HTMLDocument:
    """
    Load an HTML file safely, handling missing files and encoding issues.
    Returns an HTMLDocument instance or raises a descriptive exception.
    """
    try:
        return HTMLDocument(path)
    except FileNotFoundError as e:
        raise RuntimeError(f"Unable to read local HTML file Python: {e}")
    except UnicodeDecodeError:
        raise RuntimeError("File encoding is not UTF-8; consider specifying the correct encoding.")
```

これで `safe_load_html("index.html")` を呼び出すだけで、エラーが明確に報告される `HTMLDocument` オブジェクトが取得できます。

## プロのコツとよくある落とし穴

* **`open(...).read()` のみを使用しない** – `Path.read_text` はパス展開とエンコーディング処理を一行で行います。  
* **ファイルハンドルのクローズを忘れない** – `Path.read_text` は自動でクローズします。`open()` を使う場合は必ず `with` ブロックで囲みましょう。  
* **デフォルトパーサより `lxml` を推奨** – 速度が速く、壊れたマークアップにも寛容です。これはウェブから **parse html file in python** する際に重要です。  
* **文字列から作成する場合は完全なHTMLドキュメントであることを確認** – `<html>` や `<body>` タグが欠けていると、要素検索時に予期せぬ `None` が返ることがあります。

## コピー＆ペースト可能なフルスクリプト

以下は本稿で説明したすべての手順を網羅した自己完結型スクリプトです。`html_demo.py` として保存し、`python html_demo.py` で実行してください。

```python
#!/usr/bin/env python3
"""
Complete example: parse html file in python, load html document from file,
and create html document from string.
"""

from pathlib import Path
from bs4 import BeautifulSoup
from typing import Union

class HTMLDocument:
    """Wraps BeautifulSoup to provide a simple document interface."""
    def __init__(self, source: Union[str, Path]):
        if Path(source).exists():
            self._load_from_file(Path(source))
        else:
            self._load_from_string(source)

    def _load_from_file(self, file_path: Path):
        try:
            html = file_path.read_text(encoding="utf-8")
        except FileNotFoundError:
            raise FileNotFoundError(f"File not found: {file_path}")
        self.soup = BeautifulSoup(html, "lxml")

    def _load_from_string(self, html_string: str):
        self.soup = BeautifulSoup(html_string, "lxml")

    def title(self) -> str:
        return self.soup.title.string.strip() if self.soup.title else ""

    def pretty(self) -> str:
        return self.soup.prettify()


def safe_load_html(path: Union[str, Path]) -> HTMLDocument:
    """Safely load a local HTML file, handling common errors."""
    try:
        return HTMLDocument(path)
    except FileNotFoundError as e:
        raise RuntimeError(f"Unable to read local HTML file Python: {e}")
    except UnicodeDecodeError:
        raise RuntimeError("File encoding is not UTF-8; specify the correct encoding.")


def main():
    # Load from a real file (replace with your actual path)
    file_doc = safe_load_html("YOUR_DIRECTORY/index.html")
    print("File‑based title :", file_doc.title())
    print("\nPretty‑printed HTML from file:\n", file_doc.pretty()[:200], "...")

    # Create from a raw string
    html_str = "<html><head><title>Hello</title></head><body><h1>Hello</h1></body></html>"
    string_doc = HTMLDocument(html


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全に動作するコード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Create HTML Document with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}