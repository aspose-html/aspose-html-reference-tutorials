---
category: general
date: 2026-08-25
description: シンプルなPythonスクリプトを使って、HTMLドキュメントの作成、要素のCSS選択、HTMLテキストの編集、HTMLファイルの保存方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: ja
lastmod: 2026-08-25
og_description: 数行のPythonでHTMLドキュメントを作成し、要素のCSSを選択、HTMLテキストを変更してHTMLファイルを保存します。完全なチュートリアルをご覧ください。
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: PythonでHTMLドキュメントを作成し、内容を編集する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: PythonでHTMLドキュメントを作成し、内容を編集する方法
url: /ja/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonでhtmlドキュメントを作成し、内容を編集する方法

最初から **create html document** を作成し、要素をプログラムで変更する必要がある場合、このガイドが具体的な手順を示します。短く実行可能なスクリプトを通じて、ファイルを作成し、CSSセレクタで段落を選択し、テキストを更新し、結果をディスクに書き戻す方法が分かります。

PythonでHTMLを扱うことは、レポートやメールテンプレート、静的サイトのコンテンツを生成する際に一般的です。このチュートリアルの最後までに、IDEを離れることなく **select element css**、**modify html text**、**save html file** ができるようになります。

## 前提条件

* Python 3.9 以上がインストールされていること。
* `beautifulsoup4` と `lxml` パッケージ（`pip install beautifulsoup4 lxml` でインストール）。
* 出力ファイルを保存するディレクトリへの書き込み権限があること。

追加のツールは不要です。標準ライブラリがファイルI/Oを処理します。

## ステップ 1: 必要なライブラリをインストールする

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` はHTMLの解析と操作のための便利な API を提供し、`lxml` はCSSセレクタを理解できる高速パーサを提供します。

## ステップ 2: 初期HTMLドキュメントを作成する

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

`BeautifulSoup` コンストラクタはメモリ上に **create html document** オブジェクトを構築します。`"lxml"` パーサを使用することで、完全な CSS セレクタサポートが保証されます。

## ステップ 3: CSSセレクタを使用して段落要素を選択する

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

`select_one` メソッドは **select element css** ロジックを実装し、最初に一致したタグを返します。セレクタが何も一致しない場合、`para` は `None` になるため、本番コードでは防御的チェックを行うことが推奨されます。

## ステップ 4: 段落のテキストコンテンツを変更する

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

`para.string` に代入することで **modify html text** 操作が実行されます。BeautifulSoup は基底の DOM ツリーを更新するため、シリアライズ時に変更が反映されます。

## ステップ 5: 更新されたHTMLをファイルに保存する

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

`open` と `write` の組み合わせで **save html file** 機能が実装されます。`prettify()` を使用するとインデントが整った出力が得られ、デバッグ時に便利です。

### 簡単にコピーできるフルスクリプト

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

`python edit_html.py` を実行すると、`updated.html` が作成され、以下が含まれます：

```html
<p>
 New
</p>
```

## 一般的なバリエーションとエッジケース

### 複数要素の選択

複数のタグに一致する **select element css** セレクタ（例: `"div.note"`）が必要な場合は、リストを返す `doc.select("div.note")` を使用します。リストを反復処理して各要素に変更を適用します。

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### 既存属性の保持

テキストを置換しても、BeautifulSoup はタグの属性を保持します。例：

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### 欠損要素の優雅な処理

本番スクリプトでは、しばしば不正なHTMLに遭遇します。Step 4 の例のように、条件分岐または try‑except ブロックで選択をラップし、クラッシュを防ぎます。

### 特定ディレクトリへの書き込み

`output_path` を絶対パスまたは相対パスに置き換えます：

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

ディレクトリが存在することを確認してください。存在しない場合、Python は `FileNotFoundError` を送出します。

## プロのコツ

* **Performance** – 大きなHTMLファイルでは、直接 `lxml.etree` を使用することを推奨します。BeautifulSoup は便利な薄い抽象層を提供しますが、若干遅くなります。
* **Encoding** – 非ASCII文字を保持するため、常に `encoding="utf-8"` でファイルを開いてください。
* **Testing** – 変更後、ユニットテストで `assert "New" in open(output_path).read()` を使って出力を検証できます。

## 結論

これで **create html document** の方法、**select element css** クエリでノードを特定し、**modify html text** を行い、最終的に Python で **save html file** する方法が分かりました。このパターンは、バルク更新、属性変更、テンプレート生成など、より複雑な変換にも拡張できます。

次に、XPath式を使用した **how to edit html**、Jinja2でのフルHTMLページ生成、複数ファイルのバッチ処理の自動化などの関連トピックを探求してください。これらはすべて、本稿で示した基本手順を基にしており、プログラムによるHTML操作のツールキットを拡張します。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれており、追加のAPI機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.HTMLでHTMLドキュメントを作成する – ステップバイステップガイド](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [Aspose.HTML for JavaでHTMLドキュメントツリーを編集する方法](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Aspose.HTML for JavaでHTMLドキュメントを保存する](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}