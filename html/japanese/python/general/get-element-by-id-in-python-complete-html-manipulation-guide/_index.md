---
category: general
date: 2026-05-31
description: Python を使って id で要素を取得し、HTML の背景色を変更し、HTML テキストを読み取り、HTML 属性を設定する方法を学びましょう。ステップバイステップのチュートリアルです。
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: ja
og_description: Python を使用して、ID で要素を取得し、HTML テキストを読み取り、HTML 属性を設定し、背景色を変更する方法を、シンプルで分かりやすいガイドで紹介します。
og_title: Pythonでidによる要素取得 – 完全HTML操作チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: PythonでIDによる要素取得 – 完全HTML操作ガイド
url: /ja/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでIDで要素を取得する – 完全なHTML操作ガイド

HTMLページから **get element by id** を取得しながら手早く Python スクリプトを書きたくなったことはありませんか？ あなたは一人ではありません。多くの開発者がサイトをクロールしたりローカルレポートを調整したりし始めたときに、同じ壁にぶつかります。朗報です。数行のコードで要素のテキストを読み取り、背景色を変更し、さらには新しい属性を設定することが、エディタを離れることなく可能です。

このチュートリアルでは、実際の例としてローカルの `sample.html` を読み込み、ID が `main‑content` の要素を取得し、その内部テキストを出力、最後に背景色を薄いグレーに差し替える手順を解説します。最後まで読むと **how to read HTML text**、**how to set HTML attribute**、そして **manipulate HTML with Python** が自動化ツールボックスでどれほど便利かが分かります。

## What You’ll Need

始める前に以下を用意してください。

- **Python 3.9+**（最近のバージョンであればどれでも可）
- **`lxml`** ライブラリ（好みで **BeautifulSoup** でも可） – ここでは `lxml.html` を使用します。`get_element_by_id` 風の API がクリーンです。
- `YOUR_DIRECTORY` フォルダー内に置く `sample.html` という小さな HTML ファイル。以下のスニペットをそのファイルにコピーして構いません。

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

以上です。特別なフレームワークは不要、純粋な Python と静的 HTML ファイルだけで始められます。

## Step 1: Install the Required Library

まだ `lxml` をインストールしていない場合は、ターミナルを開いて次のコマンドを実行してください。

```bash
pip install lxml
```

*Pro tip:* 仮想環境を使うと、複数プロジェクトを扱う際にグローバルな Python 環境をすっきり保てます。

## Step 2: Load the HTML Document

次に、ファイルを `lxml.html` のドキュメントオブジェクトに読み込みます。これは、生のテキストを操作可能なツリー構造に変換するイメージです。

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

実行すると “Document loaded successfully.” と表示されます。ファイルが見つからない場合は Python が `FileNotFoundError` を投げますので、要素を探す前に早めに捕捉しておきましょう。

## Step 3: Get element by id

ここが本題です。`lxml` は JavaScript の DOM API と同様の便利な `get_element_by_id` メソッドを提供します。

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

要素が存在すればコンソールに “Element found!” と表示されます。これが **get element by id** のステップで、以降の操作の基盤となります。

## Step 4: How to read HTML text

要素を取得したら、可視テキストの抽出はとても簡単です。`text_content()` メソッドはタグを除去したすべてのテキストを返します。

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

期待される出力:

```
Inner text: Hello, world! This is the original text.
```

*「要素に入れ子のタグが含まれていたらどうなるの？」* と疑問に思うかもしれませんが、`text_content()` は子孫テキストノードをすべて連結してくれるので、クリーンな文字列が得られ、ログに記録したり別のアルゴリズムに渡したりできます。

## Step 5: How to set HTML attribute

属性の変更や追加も同様にシンプルです。`set` メソッドを使えば、好きな属性名を割り当てられます。

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

出力:

```
New attribute value: true
```

この行は **how to set HTML attribute** をその場で実演しています。`"data-modified"` を `"class"`、`"title"` など、要素がサポートする任意の属性名に置き換えて構いません。

## Step 6: Change background colour HTML

次は見た目の調整です。背景色を変えるには、デフォルトを上書きする `style` 属性を注入します。

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

スクリプトを実行すると、`sample.html` の `div` はブラウザで開いたときに以下のように表示されます。

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

これが **change background colour html** のテクニックです。任意の要素に対して色コードを差し替えるだけで再利用できます。

## Step 7: Manipulate HTML with Python – Putting It All Together

以下はすべてのステップを組み合わせた完全な実行可能スクリプトです。`modify_html.py` として保存し、`YOUR_DIRECTORY` フォルダーと同じディレクトリで実行してください。

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### What the script does, line by line

1. **Imports** `lxml.html`（解析用）と `pathlib`（OS 非依存パス用）。  
2. **Loads** `sample.html`。ファイルが無ければ明確なエラーメッセージで中止。  
3. **Retrieves** the element using **get element by id**。  
4. **Prints** the element’s text—showing **how to read HTML text**。  
5. **Adds** a custom attribute, illustrating **how to set HTML attribute**。  
6. **Changes** the background colour, fulfilling the **change background colour html** requirement。  
7. **Writes** the updated markup to `sample_modified.html`。ブラウザで開くと変更が確認できます。

スクリプトを実行すると、コンソールに以下のような出力が表示されます。

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

`sample_modified.html` を開くと、テキストの背後にグレーの背景が現れます。これが **manipulate HTML with python** が実際に機能する証拠です。

## Common Pitfalls & How to Avoid Them

- **Missing ID** – 対象要素が存在しない場合、`get_element_by_id` は `None` を返します。属性にアクセスする前に必ず `None` チェックを行わないと `AttributeError` が発生します。  
- **Encoding issues** – 非 ASCII ページを読むときは `html.parse` に `encoding='utf-8'` を渡すか、ファイル自体を UTF‑8 で保存してください。  
- **Overwriting existing styles** – `style` 属性を設定すると既存のインラインスタイルは上書きされます。既存ルールを残したい場合は、現在の `style` 値を取得し、新しいルールを追記してから書き戻しましょう。  
- **File permissions** – 読み取り専用システムでは同フォルダーへの書き込みが失敗することがあります。書き込み可能な出力先（例: `sample_modified.html`）を選択してください。

## Extending the Example

基本をマスターしたら、次のステップを検討してください。

- **Loop over multiple IDs** – ID のリストを作成し、`for` ループでページ内の複数セクションを一括処理。  
- **Replace text content** – `elem.text = "New text"` を呼び出して表示文字列を変更。  
- **Add child elements** – Use `

## What Should You Learn Next?

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}